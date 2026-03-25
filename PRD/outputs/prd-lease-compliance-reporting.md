# Product Requirements Document: Lease Compliance Reporting

**Status**: Draft
**Author**: Senior PM, LegalGraph
**Date**: 2026-03-25
**Last Updated**: 2026-03-25

---

## 1. Introduction & Context

### Problem / Opportunity Statement

**Objective:** Automate lease term extraction and compliance report generation for legal teams managing IFRS 16 and ASC 842 obligations — eliminating the manual 2-week process that currently leaves GCs unable to answer board-level questions about lease exposure in real time.

**User pain points:**

- **GCs cannot answer "what is our total lease liability?" on demand.** When auditors or the CFO ask, legal teams manually pull data across dozens of lease PDFs — a process that takes 2 weeks. By the time the answer exists, it is stale. This is Jennifer's (GC persona) explicit Pain Point #3: *"CEO asks, 'What's our liability exposure?' Takes 2 weeks to manually review 200 contracts."*
- **Senior counsel performs manual, error-prone lease data entry.** David (Senior Counsel) extracts rent schedules, escalation clauses, and renewal options by hand into spreadsheets — repetitive work that comprises 80% of his lease review workload while contributing zero legal judgment.
- **Legal ops spends 2 days monthly assembling compliance reports.** Rachel (Legal Ops Manager) pulls data from six spreadsheets, emails attorneys for status, reformats everything for finance, and delivers a report that lands stale. This is her explicit Pain Point #4: "Monthly metrics report takes 2 days to compile. Error-prone. By the time it's done, data is out of date."
- **Legal and finance operate in near-total silos on lease data.** Visual Lease Data Institute (2024–2025) documented a 55-percentage-point perception gap: **81% of finance executives describe their collaboration with legal/real estate as "completely collaborative" — only 26% of legal/real estate teams agree.** LegalGraph sits at the source-document layer; no tool currently bridges legal extraction to finance-ready outputs.

**Background context:**
- IFRS 16 (effective January 1, 2019) and ASC 842 (effective Q1 2019, US FASB) mandate that all leases over 12 months appear on balance sheets as right-of-use (ROU) assets and lease liabilities. Despite years of adoption, compliance challenges remain acute: **$3.3 trillion in lease commitments held by listed companies**, with more than 85% historically unrecognized on balance sheets (PwC Viewpoint, 2025).
- **Over 30% of finance teams** that implemented new or modified lease accounting systems are now seeking enhancements or replacements (PwC survey of 900+ finance professionals).
- FRS 102 (UK) became effective January 1, 2026 — bringing UK SMEs under IFRS 16-style lease recognition and creating a new compliance wave that coincides with LegalGraph's planned UK expansion.
- **Evisort** — the only CLM competitor with documented ASC 842 features — was acquired by Workday in September 2024 and repositioned as an ERP-bundled enterprise tool, effectively exiting the mid-market. No remaining legal AI/CLM competitor has documented lease compliance reporting features for LegalGraph's target segment (source: market research, March 2026).

---

### Key Observations, Data & Insights

**Market demand is quantified and urgent:**

- The global lease management software market is valued at **$4.58B (2024), projected to reach $6.86B by 2031** (5.7% CAGR, Business Research Insights, 2024). Lease abstraction services specifically are growing at **7.5% CAGR** ($1.2B → $2.5B by 2032, DataIntelo, 2024).
- **87% of GCs report AI use within their teams (2026), up from 44% in 2025** (FTI Consulting, The General Counsel Report, March 2026), and **70% of legal departments plan to invest in new technologies in the next 12 months** — the market is actively buying.
- **64% of real estate/legal teams still use spreadsheets** to manage lease obligations (RE BackOffice, 2025), confirming the manual workflow is widespread, not edge-case.

**Accuracy is the adoption gate, not a feature detail:**

- **74.7% of lawyers cite accuracy as their primary barrier to AI adoption** (ABA 2024 AI TechReport). **69.7% of AI outputs currently require targeted edits or extensive rework.**
- David's profile is explicitly accuracy-skeptical: *"If your tool flags a risk that isn't actually risky, I'll lose trust. Accuracy matters more than speed."* For compliance-grade outputs — where an extraction error (e.g., wrong commencement date, missed escalation clause) can cause a material financial misstatement or audit finding — the bar is 95%+. LegalGraph's current overall extraction accuracy is 94%; lease-specific fine-tuning is required before launch.
- LegalGraph's existing confidence scoring system and "AI uncertain" flags are the trust mechanism that differentiates from competitors and addresses this adoption barrier.

**Audit risk is board-reportable — and the real value proposition:**

- **59% of accountants make several errors every month; 18% make daily errors** using spreadsheet-based workflows (Gartner, cited in Crunchafi, 2025). One public company reported **audit fees increased 25%** due to lease accounting spreadsheet errors (RSM Guide to Lease Accounting, November 2025).
- Immutable audit logs — already shipping in LegalGraph as SOC 2 Type II infrastructure — directly close this gap. The feature should be positioned as audit risk reduction, not just efficiency.

**Competitor white space is real and time-bounded:**

- Kira Systems has confirmed lease abstraction (Deloitte case study) but stops at extraction — no downstream compliance reporting, no accounting integrations.
- Evisort's Workday acquisition removes it from the mid-market: it now requires Workday ERP bundling at $100k+ pricing. LegalGraph's $45k pricing and 2-week setup creates a durable mid-market advantage while this gap exists.
- Trullion, Visual Lease, and FinQuery are dedicated lease accounting tools — their users cite persistent reporting limitations: *"The reports section isn't robust"* (Trullion, Capterra 2024–2025) and *"inability to put in custom calculations; must export to Excel"* (LeaseQuery, G2 2025–2026). LegalGraph enters as the legal-layer complement, not a direct competitor.

**Success looks like:**
- A GC can answer "what is our total lease liability?" in under 5 minutes — not 2 weeks
- A lease compliance report is generated with one click, formatted for direct use by the finance team and external auditors
- All three personas are actively using the feature within 90 days of launch (Jennifer: portfolio dashboard; David: per-lease extraction; Rachel: scheduled report delivery)

---

### Impact Sizing

**Qualitative Impact:**

- **Jennifer (GC):** Transforms from reactive (scrambles before every audit) to proactive (real-time portfolio visibility for board meetings, audit committee, and CFO questions). Elevates legal from a service function to a risk intelligence partner.
- **David (Senior Counsel):** Eliminates the "glorified data entry" portion of lease review — extracting 8+ fields per lease from scratch — freeing him to focus on legal risk judgment rather than mechanical extraction.
- **Rachel (Legal Ops Manager):** Reclaims 2 days monthly from manual report assembly. Positions legal ops as the bridge between legal and finance, rather than the bottleneck.
- **Finance teams:** Receive structured, finance-ready outputs (ROU schedules, maturity analyses) directly usable in their accounting tools — no reformatting required.
- **LegalGraph (strategic):** Establishes the "real estate/lease compliance" vertical and builds the use case for the planned 2026 UK/EU expansion (FRS 102 effective January 2026). Opens a new $8k–$15k/year add-on revenue stream on existing enterprise accounts.

**Quantitative Impact:**

| Value Driver | Calculation | Annual Value |
|---|---|---|
| Attorney time saved per lease (extraction) | 1.75 hrs × $300/hr × 200 leases/year | **$105,000/customer** |
| Rachel's report assembly time reclaimed | 16 hrs/month × $150/hr × 12 months | **$28,800/customer** |
| Audit fee risk avoided | 25% fee increase on avg $200k audit | **$50,000/incident avoided** |
| ARR from add-on (30 of 85 customers × $10k) | 30 × $10k | **$300k incremental ARR** |
| New vertical deal size uplift | $45k → $85k avg deal (real estate segment) | **$40k/deal upside** |

- **Total addressable add-on ARR (existing base, conservative):** $300k
- **New vertical opportunity:** Real estate/retail/healthcare companies with large lease portfolios represent a new buyer profile at higher deal size — aligning with 2025 OKR (average deal size $45k → $85k)

---

## 2. Goals & Metrics

### Success Metrics

**Primary (feature adoption and usage):**

| Metric | Baseline | Target (90-day post-launch) | Why It Matters |
|---|---|---|---|
| Lease compliance reports generated/month | 0 | 250+ reports across customer base | Direct indicator of feature adoption |
| % of enterprise customers using feature | 0% | 35% of 45 enterprise accounts | Add-on revenue prerequisite; validates ICP fit |
| Lease extraction accuracy (key fields) | 94% overall | 95%+ on 8 core IFRS 16/ASC 842 fields | Non-negotiable for trust; David's adoption gate |
| Time to generate compliance report | 2 weeks (manual) | <10 minutes | Primary value proposition validation |
| Feature add-on ARR | $0 | $150k by Q4 2026 | Revenue contribution from new capability |

**Secondary (persona-specific):**

| Metric | Persona | Target |
|---|---|---|
| % of customers with scheduled report delivery configured | Rachel | 50% of feature users |
| Lease portfolio dashboard weekly active views | Jennifer | 1+ view/week per GC user |
| Average leases processed per customer/month | David | 20+ leases/customer |
| NetSuite/SAP integration activations (Phase 2) | Rachel | 15 integrations by Q1 2027 |

---

### Guardrail Metrics

These must not degrade during the Lease Compliance Reporting rollout:

| Guardrail Metric | Current Value | Acceptable Threshold |
|---|---|---|
| Overall platform clause extraction accuracy | 94% | Must not drop below 93% |
| Support ticket volume (AI errors) | Baseline TBD | Must not increase >15% |
| Core contract review NPS | 42 | Must not drop below 40 |
| Enterprise net retention rate | 92% | Must not drop below 90% |
| Security incident count | 0 | Must remain 0 |

**Rationale:** Adding a new ML-fine-tuned extraction capability risks accuracy regression on existing clause types. CI/CD for model updates must include regression testing on existing extraction benchmarks before each lease-model update is deployed.

---

### Leading vs. Lagging Indicators

**Leading Indicators (within first 60 days):**
- Pilot customer NPS on lease extraction accuracy (target: 7+/10)
- % of pilot leases where David persona accepts AI extraction without full rereview (target: 80%+)
- Report export activations per customer during pilot (target: 3+ exports in first 30 days)
- Rachel persona feedback: "I would use this to replace my monthly manual report" (qualitative signal)

**Lagging Indicators (90–180 days):**
- Feature add-on ARR ($150k target by Q4 2026)
- Enterprise net retention improvement (92% → 95% target)
- Average contract value uplift in new real estate/retail deals
- Average deal size increase (toward $85k 2025 OKR)
- Customer reference count for lease compliance use case (target: 5 referenceable customers by Q4 2026)

---

## 3. Risks & Assumptions

### Known Risks

**Technical Risks:**

| Risk | Likelihood | Severity | Mitigation |
|---|---|---|---|
| Lease-specific accuracy does not reach 95%+ pre-launch | Medium | **Critical** — David will not adopt; Rachel cannot trust the output; compliance errors create liability | Require 95%+ accuracy on 8 core fields on a 500-lease holdout set before GA. Delay launch if threshold not met. |
| Complex lease structures reduce extraction reliability | High | High — non-standard escalation formulas, cross-referenced exhibits, multi-component contracts are the most common error cases (V7Labs, 2025) | Confidence scores + "requires review" flags are mandatory on every field. Human-in-the-loop validation remains the standard. |
| Model regression on existing clause types during fine-tuning | Medium | High | Automated regression testing gate in CI/CD before any lease model update goes to production |

**Product Risks:**

| Risk | Likelihood | Severity | Mitigation |
|---|---|---|---|
| Feature scope expands to full accounting engine (ROU asset calcs, journal entries) | High | **Critical** — consumes roadmap capacity; creates direct competition with Trullion/Visual Lease on their home ground | MVP scope is extraction + structured report only. ROU calculations, journal entries, and discount rate assumptions are out of scope. Partnership with Trullion/FinQuery for Phase 2 accounting layer. |
| Positioning confusion — users expect a full ASC 842 system | Medium | High — sets wrong expectations, creates support load | All marketing and in-product copy must be explicit: "LegalGraph generates audit-ready inputs for accountants — not a replacement for lease accounting software." Require an "accountant confirmation" step before any report is marked as compliance-ready. |
| Legal team does not share outputs with finance team | Medium | Medium — Rachel must champion the cross-functional handoff | Report formats must match what accountants expect (ROU schedule columns, maturity analysis layout) — designed with accountant consumption in mind, not legal-internal formatting |

**Market Risks:**

| Risk | Likelihood | Severity | Mitigation |
|---|---|---|---|
| Workday expands Evisort down-market | Medium | Medium — LegalGraph's 2-week setup, $45k pricing, and legal-team focus are durable advantages | Monitor Workday's SMB product announcements quarterly; accelerate real estate vertical GTM before gap closes |
| Dedicated lease accounting tools add legal team features | Low | Medium | LegalGraph's playbook integration, risk scoring, and clause-level precision are 3–5 years of ML investment that is difficult to replicate quickly |
| Output error causes material misstatement in customer financial filing | Low | **Critical** — legal exposure, reputational damage, enterprise churn | Mandatory disclaimers on all reports. Terms of service review by LegalGraph's Head of Legal & Compliance before launch. Never label output "compliance-ready" without accountant validation step. |

**Stated Assumptions:**
1. LegalGraph's existing GPT-4 + Claude 3 foundation models (fine-tuned on 500k+ contracts) can reach 95%+ on core lease fields with targeted lease-specific training — requires CTO and ML Lead validation before committing to Q3 2026 launch.
2. Mid-market enterprise customers (the 45 enterprise accounts) carry material lease portfolios subject to IFRS 16/ASC 842 — [ASSUMPTION]; validation required via customer discovery with 5–8 existing accounts before GA.
3. Partnership with Trullion or FinQuery for Phase 2 accounting computation layer is feasible — no partnership discussions have commenced; this is a Phase 2 dependency, not a Phase 1 blocker.
4. LegalGraph's existing NetSuite and SAP integrations can be extended to push structured lease data to ERP lease modules — technical feasibility requires CTO input before Phase 2 scoping.

---

## 4. Scope

### What Is In Scope

**Phase 1 MVP (target: Q3 2026):**

1. **Lease-specific AI extraction engine** — fine-tuned on IFRS 16/ASC 842 key fields:
   - Commencement date and lease term
   - Base rent (initial, escalated)
   - Annual escalation mechanism (fixed %, CPI-linked, stepped)
   - Renewal options (number, term, notice requirement)
   - Early termination rights and conditions
   - CAM (Common Area Maintenance) obligations and caps
   - Landlord/tenant obligations
   - Lease classification indicators (finance vs. operating under ASC 842)

2. **Per-field confidence scores** with mandatory "requires review" flag on fields below 90% confidence

3. **Structured compliance summary report** exportable as PDF, Excel, and CSV — formatted to match accountant/auditor expectations (ROU schedule columns, maturity analysis layout, lease-by-lease detail)

4. **Real-time lease portfolio dashboard** — total lease count, aggregate commitments by year, renewal decision windows, and rent escalation exposure curve

5. **Immutable audit trail** on all extractions: who triggered extraction, when, which model version, confidence scores at time of extraction

6. **IFRS 16 and ASC 842 dual-standard report templates** — separate column mappings and classification logic for each standard

7. **Retroactive analysis** on previously uploaded leases (customers should not need to re-upload existing contracts)

8. **Accountant confirmation disclaimer and workflow** — all reports include explicit disclaimer language; reports can be marked "ready for accountant review" (not "compliance-ready") by legal team

**Phase 2 (target: Q4 2026–Q1 2027):**

1. NetSuite/SAP data push — structured lease data pushed to ERP lease modules via existing API integrations
2. Scheduled automated report delivery with stakeholder routing (monthly, quarterly)
3. FRS 102 (UK) report template
4. Custom report templates (configurable by Rachel/Legal Ops)
5. Integration partnership with Trullion or FinQuery for ROU asset calculations (if commercial terms are reached)

---

### Out-of-Scope

The following are **explicitly excluded** from this feature — raising them in scope discussions should be treated as scope creep:

- **Right-of-use (ROU) asset calculations** — requires discount rate assumptions and accounting judgment; this is the accounting team's responsibility
- **Lease liability amortization schedules** — journal entry generation is an accounting function, not a legal extraction function
- **Present value computations or incremental borrowing rate inputs**
- **ASC 842 / IFRS 16 journal entry generation**
- **Disclosure footnote language generation** (legally adjacent to accounting opinion — liability risk)
- **Integration with lease accounting software** as a replacement (Trullion, Visual Lease, FinQuery remain the customer's accounting system of record)
- **E-signature or DocuSign initiation workflows** from within the compliance report
- **Lease drafting or negotiation assistance** (covered by Contract Negotiation Assistant on current roadmap)
- **Equipment lease classification rules** beyond the fields above (Phase 2 expansion opportunity, not MVP)
- **Multi-party or subleasing waterfall analysis**

---

## 5. User Stories

### Persona 1: Jennifer Martinez (General Counsel) — Audit Readiness & Board Reporting

**User Story 1: On-demand lease exposure reporting**

> As a General Counsel, I want to view a real-time summary of our total lease obligations, renewal exposure, and IFRS 16/ASC 842 compliance status, so that I can answer the CFO's or auditor's questions in under 5 minutes without triggering a 2-week manual pull from my team.

**Acceptance Criteria:**
- Portfolio dashboard loads within 3 seconds, showing: total active leases, aggregate lease commitments by year (minimum 10-year forward view), renewal decision windows (next 12 months highlighted), rent escalation exposure curve
- Dashboard data reflects all leases uploaded to LegalGraph with no manual data entry required
- GC can filter by: business unit, geography, lease type (real estate vs. equipment), compliance standard (IFRS 16 / ASC 842)
- Dashboard is accessible from the main navigation without navigating through individual lease records

**User Story 2: Audit-ready report generation**

> As a General Counsel, I want to generate a formatted compliance report for our external auditors with one click, so that I can respond to audit requests instantly rather than spending 2 weeks assembling documentation.

**Acceptance Criteria:**
- "Generate Report" action produces a PDF and Excel file within 60 seconds for portfolios up to 200 leases
- Report includes: lease-by-lease summary, aggregate ROU schedule (structured for accountant use), renewal and termination option schedule, data extraction audit trail (who extracted, when, model confidence at time of extraction)
- Report header includes explicit disclaimer: "This report is generated by LegalGraph for legal team review and is intended as input for accountant validation — it is not a certified financial statement or audit opinion."
- Report is exportable directly from the dashboard with no configuration required for the first run

---

### Persona 2: David Kim (Senior Corporate Counsel) — Lease Term Extraction Workflow

**User Story 3: Auto-extraction of lease terms with confidence transparency**

> As a Senior Corporate Counsel, I want AI to automatically extract all IFRS 16/ASC 842 relevant fields from a lease upon upload, with a confidence score on every field, so that I can focus my review time on the uncertain fields rather than re-reading the entire lease from scratch.

**Acceptance Criteria:**
- All 8 core IFRS 16/ASC 842 fields are extracted automatically within 30 seconds of lease upload
- Every extracted field displays a confidence score (0–100%) and source citation (page number, section reference)
- Fields below 90% confidence display a prominent "Requires attorney review" flag in red — not just a tooltip
- Overall extraction accuracy on core fields is 95%+ on a 500-lease validation set before launch (non-negotiable gate; feature does not ship if not met)
- Attorney can accept, edit, or reject individual field extractions — all edits are logged to the audit trail
- Editing one field does not trigger re-extraction of other fields (preserves attorney edits)

**User Story 4: Lease portfolio review queue**

> As a Senior Corporate Counsel, I want to see all leases pending my review in a prioritized queue, so that I can triage which leases need my attention and batch-approve standard leases efficiently.

**Acceptance Criteria:**
- Review queue shows: lease name, counterparty, commencement date, term, base rent, overall extraction confidence, days since upload
- Queue can be sorted by: confidence score (ascending — lowest confidence first), upload date, lease term end date, base rent value
- Leases with all fields at 90%+ confidence can be "batch approved" with a single action (without opening individual records)
- Attorney approval is required before any lease data flows into a compliance report — auto-approval is not permitted

---

### Persona 3: Rachel Thompson (Legal Ops Manager) — Reporting Automation & Finance-Ready Output

**User Story 5: Elimination of manual monthly report assembly**

> As a Legal Operations Manager, I want to generate a formatted compliance report in the format finance expects — with no manual reformatting — so that I can reclaim the 2 days per month I currently spend assembling lease data from six spreadsheets.

**Acceptance Criteria:**
- Compliance report exports in three formats: PDF (for audit committee), Excel (for finance team), CSV (for ERP import)
- Excel output uses column headers matching accountant standard inputs: commencement date, lease term (months), base rent (monthly), annual escalation mechanism, total minimum lease payments, renewal option terms
- Report can be generated for: all leases, filtered by standard (IFRS 16 / ASC 842), filtered by business unit or geography
- Report generation does not require attorney involvement once leases are reviewed and approved by legal team

**User Story 6: Scheduled report delivery**

> As a Legal Operations Manager, I want to configure automated monthly and quarterly compliance report delivery to specified stakeholders (CFO, audit committee, finance team), so that compliance reporting becomes a zero-effort recurring workflow.

*(Phase 2 — included for alignment; not in MVP scope)*

**Acceptance Criteria:**
- Scheduled delivery can be configured by Rachel without engineering support
- Recipients can be specified by email; reports attach in PDF + Excel
- Report delivery log is accessible by Rachel with timestamps

**User Story 7: ROI dashboard for GC budget approval**

> As a Legal Operations Manager, I want to see a time-savings dashboard showing attorney hours saved on lease extraction per month, so that I can build a concrete ROI case to justify the add-on budget to the GC.

**Acceptance Criteria:**
- Dashboard shows: leases processed this month, average extraction time (AI) vs. estimated manual time per lease, total hours saved, total dollar value saved (configurable attorney hourly rate, defaulting to $300/hour)
- Dashboard is exportable as a PDF for use in internal business case presentations
- Calculation methodology is visible to Rachel (not a black box)

---

## 6. Milestones & GTM

### Project Plan

| Phase | Milestone | Target Date | Owners |
|---|---|---|---|
| **Discovery** | Customer discovery interviews with 5–8 enterprise accounts to validate lease portfolio density and compliance pain | April 2026 | Senior PM + CS |
| **Discovery** | CTO feasibility assessment: lease-specific ML fine-tuning timeline, NetSuite/SAP Phase 2 API extension | April 2026 | CTO + ML Lead |
| **Discovery** | Legal & Compliance review of liability framework and report disclaimer language | April 2026 | Head of Legal & Compliance |
| **Design** | UX wireframes: extraction review UI, portfolio dashboard, report export flow | May 2026 | Emma Thompson (Head of Design) |
| **Design** | PRD approved by Priya Sharma (Head of Product) | May 2026 | Senior PM |
| **Engineering** | ML: Lease-specific fine-tuning on IFRS 16/ASC 842 fields; accuracy validation against 500-lease holdout set | May–June 2026 | ML Engineering Lead |
| **Engineering** | Backend: Extraction pipeline, confidence scoring, audit trail, report generation engine | May–July 2026 | Backend Lead |
| **Engineering** | Frontend: Portfolio dashboard, review queue, export UI | June–July 2026 | Frontend Lead |
| **QA** | End-to-end QA on 200-lease test portfolio; accuracy gate: 95%+ on core fields | July 2026 | QA + ML Lead |
| **Beta** | Closed beta with 5 enterprise customers (real estate and retail verticals preferred) | August 2026 | Senior PM + CS |
| **Beta** | Beta feedback synthesis; accuracy and UX issues resolved | August 2026 | Senior PM + Engineering |
| **GA** | General Availability launch | September 2026 | All |
| **Phase 2** | NetSuite/SAP data push, scheduled delivery, FRS 102 template | Q4 2026–Q1 2027 | Engineering |

**Critical path:** ML accuracy gate (95%+) must pass before beta launch. If accuracy gate is not met by July 2026, GA shifts to October 2026 — launch date is accuracy-dependent, not calendar-dependent.

---

### Release / Rollout Strategy

**Release Plan:**

| Stage | Scope | Duration | Criteria to Advance |
|---|---|---|---|
| **Internal alpha** | LegalGraph team dogfooding on internal contracts | 2 weeks (July 2026) | No critical extraction bugs; report export works end-to-end |
| **Closed beta** | 5 enterprise customers (selected by CS; real estate/retail vertical preferred) | 4 weeks (August 2026) | Beta NPS ≥ 7/10; accuracy confirmed at 95%+ on customer's actual leases; no P0/P1 bugs |
| **GA (feature-flag)** | All enterprise customers (45 accounts); add-on pricing active | September 2026 | Beta criteria met |
| **SMB rollout** | Professional plan customers (by request) | Q4 2026 | Enterprise GA stable; no new accuracy issues |

**Pricing at GA:**
- Lease Compliance Reporting is an **add-on module** priced at **$8k–$15k/year** for Enterprise customers, based on lease portfolio size (up to 50 leases: $8k; 51–200 leases: $12k; 200+: $15k)
- CS team will run upsell conversations with the 45 existing enterprise accounts in August–September 2026
- New enterprise deals including lease compliance feature are priced toward the $85k average deal target (2025 OKR)

**Rollout Communications:**

| Audience | Channel | Message | Timing |
|---|---|---|---|
| Existing enterprise customers | Dedicated email from CS + in-app banner | "New: Lease Compliance Reporting — generate IFRS 16/ASC 842 reports in one click" | Launch day |
| Pilot beta customers | CS-led call + Loom walkthrough | Preview access + feedback request | 4 weeks pre-launch |
| LegalGraph sales team | Internal sales deck + competitive battle card | Positioning vs. Evisort/Workday; real estate vertical pitch | 2 weeks pre-launch |
| External (prospects) | Blog post, LinkedIn announcement, G2 category update | "LegalGraph adds lease compliance reporting for mid-market legal teams" | Launch day |
| Real estate law firms (new vertical) | Outbound sequence from sales (5-person sales team) | Use Case 3 ROI story: 200 leases, 81% time savings | 2 weeks post-launch |

**Beta Users & Feedback Loops:**

- 5 beta customers selected by CS: prioritize accounts with 20+ active leases and known audit compliance pressure
- Weekly 30-minute feedback calls with beta contacts (David and Rachel personas) — structured feedback on: accuracy trust, report format usability, time savings vs. manual workflow
- Weekly accuracy report from ML team: % of beta lease extractions where attorney overrode AI extraction, with categorization by field type (used to prioritize fine-tuning)
- Beta NPS survey at week 3: "Would you replace your current manual lease reporting process with this feature?" Target: 7+/10; launch gate at 6+/10
- All beta feedback synthesized into a post-beta report within 1 week of beta close; GA ship/no-ship decision requires Senior PM, CTO, and Priya Sharma sign-off

---

## Appendix: Persona-Feature Fit Summary

| Feature | Jennifer (GC) | David (Sr. Counsel) | Rachel (Legal Ops) | Phase |
|---|---|---|---|---|
| Real-time lease portfolio dashboard | **Critical** — board/audit visibility | Low | High — ops metric | MVP |
| Auto-extraction (8 IFRS 16 fields) with confidence scores | High — audit readiness | **Critical** — trust gate | Medium | MVP |
| Formatted report export (PDF/Excel/CSV) | High — audit output | Medium | **Critical** — eliminates 2-day manual | MVP |
| Immutable audit trail | **Critical** — audit defense | High | High | MVP |
| IFRS 16 + ASC 842 dual templates | Medium — international ops | Medium | Medium | MVP |
| NetSuite/SAP data push | Medium | Low | **High** | Phase 2 |
| Scheduled automated report delivery | High | Low | **Critical** | Phase 2 |
| Renewal/escalation portfolio exposure view | **Critical** — board deck | Low | High | Phase 2 |
| FRS 102 (UK) template | High — UK expansion | Medium | Medium | Phase 2 |

---

*Word count: ~4,900*
