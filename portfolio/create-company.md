# Company Context Agent

---

## Purpose

Conducts automated deep-dives into a company, its competitors, market landscape, and products. Serves as context for other agents (e.g. Interview Analysis Agent, Survey Analysis Agent).

---

## Workflow

Input a company name → agent researches and generates three context files used by downstream agents.

```mermaid
flowchart LR
    A["Input company name"] --> B["create-company-agent"]
    T["Ingest templates<br/><small>company-overview-template.md<br/>competitive-intelligence-template.md<br/>product-description-template.md</small>"] --> B
    B --> C["Generate 3 context files<br/><small>company-overview.md<br/>competitive-intelligence.md<br/>product-description.md</small>"]
```

---

## Challenges and Iterations

| Challenge | Fix | Result |
|---|---|---|
| Agent attempted a SWOT analysis, but search snippets **unable to substantiate qual claims** — producing hallucinations like "ASOS has weaker EU logistics than Zalando." | Shifted approach to **restrict the model to verifiable data extraction**, while allowing qualitative claims only when explicitly attributed to external sources. | Every claim is traceable to a specific source. |
| Citations relied on the model generating URLs from memory — a **stochastic** process that produced broken or hallucinated links. | **Introduced two deterministic registries.** `fact_registry.json` logs every source at retrieval (URL, title, date, key quote) — cited downstream as `SRC:id`. `quotes_registry.json` logs every verbatim user quote before analysis (exact text, platform, date) — cited as `Q-id`. | Every sourced claim and verbatim quote is auditable by source, date, and exact text. |
| Agent wrote **overconfident competitive claims** — e.g. "no other competitor offers X" — sourced only from the subject company's own press releases. | **Banned the subject company's domain from all competitor searches.** Every competitor now requires an independent third-party source. | Reduced error rate on competitive claims. |
| Parallel Brave Search calls hit **rate limits** mid-run, causing the agent to skip queries and hallucinate data to fill the gaps. | **Forced sequential searches with `sleep 2` latency between every call.** | 100% data retrieval; 14-second added latency is a negligible trade-off. |
| Figures without provenance — stale statistics, aggregator estimates, inferences from adjacent sources, and search failures — were written into outputs without caveats, silently promoting **unverified data** into confident claims in downstream synthesis. | **Introduced inline labelling** with six markers: `[UNVERIFIED]` (no primary source), `[SEARCH FAILED]` (no results), `[>2YR]` (stale), `[ASSUMPTION: reasoning]` (inferred), `[URL NOT RETRIEVED]` (link missing), `[VALIDATION_FAILED]` (blocked source not replaced). | Provenance caveats travel with each figure into downstream synthesis by agents and humans, without needing re-verification. |
| Labelling was **instruction-based** — the LLM was told to classify sources correctly, but instructions can't prevent it from declaring an aggregator as a primary source. Evaluations caught aggregator figures cited as Tier 1 (e.g. electroiq 6.5M customers vs. primary filing 17M). | **Added a structural validation layer** (`scripts/validate.py`): fact registries require a `source_type` field; only `tier1_official` and `tier2_news` are valid values. A hard-coded `KNOWN_BAD` domain blocklist (Crunchbase, PitchBook, electroiq, etc.) overrides any declared type. The agent runs the validator after writing — violations must be fixed before the report is finalised. `scripts/render.py` appends a Source Registry appendix (type badge per source), keeping the report body clean. | Aggregator citations are **structurally impossible** to pass validation — not just discouraged by instruction. |
| Native web search had **high token consumption** (~95K tokens per run). | **Switched to Brave Search API**, which returns compact structured JSON snippets. | **~50% reduction** in search-related token consumption, reducing cost and overcoming context window limits. |
| Customer sentiment analysis relied on Brave Search snippets — which surface page-level summaries, not individual user reviews, resulting in findings that were too **surface-level** to be useful. | **Integrated Bright Data API** to access behind-the-wall social data across B2C platforms (e.g., App Store, Play Store, Reddit) and B2B platforms (e.g,. G2, Trustpilot, LinkedIn). Thematic analysis uses pre-defined codes for common product feedback categories (deductive reasoning), combined with emergent codes emergent (inductive reasoning). | Sentiments analysis **grounded in rich social data**; Hybrid deductive and inductive coding framework **minimised token consumption** while ensuring we **captured novel patterns.** |
| Agent ignored rule about sequential searches, scraping all social media platforms **simultaneously**, leading to unnecessary API usage. | Replaced with a **sequential loop (search → scrape → count → gate)**, ensuring only one platform is processed at a time before proceeding to the next. | **Reduced redundant API calls** |
| Agent wrote quant figures from search snippets — which reflect **cached** earlier editions, not the live page. | **Forced a live fetch** using `mcp__Bright_Data__extract` for all frequently updated analyst report figures. | Cited figures now reflect the current live page. |
| Broken URLs were added to fact registries resulting 20% broken links in Zalando competitive intel v3| HTTP-validation for every URL and agent re-sources broken links before publication. | Broken URLs patched deterministically at the source — not during evals. |
| Quant numbers were attributed to wrong periods (e.g. 6.5M cited under HY26, which actually reports 16.5M), resulting in Quant Claims Accuracy rate of 66% in Zalando competitive intel v3. | New script extracts unitised numbers** (%, M, billion) adjacent to each `[SRC:id]` citation and verifies each appears in the registry `quote` field. Agent must correct claims or update `quote` fields before proceeding. | Number-source mismatches flagged deterministically; agent is forced to reconcile claim before the report is written. |

---

## Evals
**Method:** [`ext-research-eval`](../.claude/agents/ext-research-eval.md) — Uses a **two-pronged** evaluation approach: 
1. **Machine-led evaluation**: Conducts **objective** checks (e.g., quant computations, link and citation coverage, template adherence). 
2. **Human-led evaluation**: Conducts **subjective** checks based on HHH (Honesty, Helpfulness, Harmlessness) to assess its true usefulness to PMs. 

### Machine-led Evaluation 
Based on latest competitive intel eval (version 4):

| Metric | v1 (2026-04-18) | v2 (2026-04-22) | v3 (2026-04-26) | v4 (2026-05-05) | Δ (v3→v4) |
|---|---|---|---|---|---|
| Quant Claims Accuracy | 83% | 80% | 66.7% | 100% | +33.3pp |
| Link Validity | 100% | 93% | 80.0% | 100% | +20pp |
| Citation Coverage | 57.6% | 84.8% | 100.0% | 100% | — |
| Field Recall | 100% | 100% | 100.0% | 100% | — |
| Placeholder violations | 0 | 0 | 0 | 0 | — |
| Blocked source violations | 0 | 0 | 0 | 0 | — |
| Banned patterns | 0 | 0 | 0 | 0 | — |
| Stale untagged | 0 | 0 | 0 | 0 | — |
| Uncited quotes | N/A | N/A | N/A | N/A | — |

### Human-led Evaluation (HHH)
Based on latest competitive intel eval (version 4):

**Honesty** — Accuracy and truthfulness

| Criteria | Yes / No |
|---|---|
| H1: Are any citations inaccurate or incomplete? | No |
| H2: Are any links inaccessible or unverifiable? | No — human confirmed all 5 links are bot-blocked but accessible in browser |
| H3: Are any current-state qualitative claims poorly substantiated? | No |
| H4: Are any future-state claims presented with over-confidence? | No |

**Helpfulness** — Effectiveness in solving the PM's problem

| Criteria | Yes / No |
|---|---|
| He1: Does the report fail to provide novel information? | No |
| He2: Is the report not useful for framing insights or PM decisions? | No |

**Harmlessness** — Safe and appropriately framed

| Criteria | Yes / No |
|---|---|
| Ha1: Negative claims about the company lack sufficient evidence? | No |
| Ha2: Negative claims about competitors lack sufficient evidence? | No |


- **Eval Reports:**
  - [2026-05-05 — Zalando competitive intelligence](../projects/Zalando/06-%20evals/2026-05-05-ext-research-eval-competitive-intelligence-v4.md)
  - [2026-04-21 — Zalando company overview](../projects/Zalando/06-%20evals/2026-04-21-ext-research-eval-company-overview.md)

---

## Sample Output

- [Zalando — company-overview.md](../projects/Zalando/01-%20company%20context/company-overview.md)
- [Zalando — competitive-intelligence.md](../projects/Zalando/01-%20company%20context/competitive-intelligence-v4.md)

---

## Outcome

✅ **Accuracy / Quality:** While still requiring spot checks in this early stage of dev, now every claim is grounded with citations. 

✅ **Cost savings:** **~€1,150/year** — process time reduced from 6 hrs to 75 mins (incl. verification)<br/>
*Assumptions: run ~6 times/year · ~6 new companies/year · pegged to PM salary*

---

## Next step

- Assess if successsful eval results can be replicated with other companies

---

## Link to Agent

- [Company Context Agent](../.claude/agents/create-company.md) — prompt Claude uses at runtime

