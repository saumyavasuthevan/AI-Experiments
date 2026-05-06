# Interview Analysis

---

## Purpose

Analyses user research interviews for pain points, bright spots, and project-specific dimensions — one file per participant, with verbatim quotes. No synthesis.

---

## Workflow

Takes raw interview transcripts and company context files as input, produces one analysis file per transcript, and feeds into research-synthesis.

```mermaid
flowchart LR
    A["Input raw transcripts<br/>company context files"] --> B["interview-analysis"]
    B --> C["Generate 1 analysis file per transcript<br/><small>interview-analysis-[unit].md</small>"]
```

---

## Challenges and Iterations

| Challenge | Fix | Result |
|---|---|---|
| Agent **re-typed** quotes from memory after locating them — producing word substitutions (e.g. "redeeming" for "redemption"). | Output quotes are **copied directly from registry**: grep opening anchor → `Read` to bound utterance → grep closing anchor → copy verbatim into `quote-registry-[unit].json`; hard gate blocks `.md` until registry is saved. | This deteministic approach ensures word substitution errors are impossible. |
| Agent created new analysis dimensions at the start of every session - resulting in inconsistent analysis dimensions across units | **Added** `analysis-dimensions.md` as a locked file: written once and reloaded on all subsequent sessions for that study. | Analysis dimensions are consistent across all units ensuring the downstream synthesis agent can make 1:1 comparisons across units |
| Agent duplicated findings across standard and project-specific dimensions when topics overlapped. | **Added** de-duplication rule: findings covered by a project-specific dimension are captured there only| Findings counts are not inflated due to duplication. |

---

## Evals

**Method:** [`int-research-eval`](.claude/agents/int-research-eval.md) **Machine-led evaluation**: Conducts **objective** checks (e.g., quote verbatim accuracy, quote relevance, speaker attribution, structural compliance, inference violations, minimum quote count).

### Machine-led Evaluation

Based on latest interview analysis eval (version 2):

| Metric | v1 (U1 · Apr 18) | v2 (U2 · May 06) | Δ (v1→v2) |
|---|---|---|---|
| Auto-fix | 7 | 5 | -2 |
| Flagged | 1 | 2 | +1 |
| Passed | 9 | 9 | — |
| Precision | 100% | 100% | — |
| Recall | 93.8% | 100% | +6.2pp |
| F1 | 96.8% | 100% | +3.2pp |

- **Eval Reports:**
  - [2026-05-06 — HPB interview U2](projects/HPB/06-%20evals/2026-05-06-interview-u2-verification.md)

---

## Sample Output

- [HPB Interview Analysis — U1](projects/HPB/04-%20analysis/HPB-interview-analysis-U1.md)
- [HPB Interview Analysis — U2](projects/HPB/04-%20analysis/HPB-interview-analysis-U2.md)

---

## Outcome

✅ **Accuracy / Quality:** Zero inaccurate findings or missed insights on lastest version, ensuring we don't miss any context in our downstream synthesis. 

✅ **Cost savings:** ~€3,000/year — task reduced from 1 hr to 10 mins (incl. verification)<br/>
*Assumptions: run ~90 transcripts/year · 15 transcripts × 6 projects · pegged to PM salary*

---

## Next step

- Test interview analysis agent on another set of interview transcripts

---

## Link to Agent

- [interview-analysis](.claude/agents/interview-analysis.md) — prompt Claude uses at runtime
