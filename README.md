# 🔬 PM Operating System (WIP)

🔒 *Some links are intentionally restricted to protect IP.* 

### tl;dr
The PM OS is a unified system to inform **faster product bets**, made with the **confidence** to defend them. 

A growing collection of **WIP** workflows I'm building on **Claude Code**, after earlier iterations in n8n and OpenClaw. 

### Challenge
PMs are under heavy pressure to **quickly determine ["what to build"](https://www.ycombinator.com/rfs)** so that we can continue to deliver business outcomes at the new speed of execution

* But **fragmented tooling** and **ad hoc processes** result in:
  * Handing off human judgement to agents in the wrong use case
  * Outputs of unreliable quality which humans then need to spend a lot of time verifying or risk errors (which in turn, loses trust)
  * Incremental speed gains
* Ultimately, these disappointing outcomes result in an inability to compete with competitors due to:
  * Higher **OPEX** 
  * **Fewer successful business outcomes** 

### User Personas
 * Short-term target: **Solo PMs**
 * Long-term targets: **Squad PMs** and **"People who do product work"** (Rationale: This requires a scaled solution to collaborate effectively and alignment on shared processes, beyond MVP scope) 

### Product Principles  
1. **Never compromise on quality**

   Accuracy thresholds are defined first. If AI meets the threshold, within strict cost constraints, automate. If not, it's a human job for now.

   *Good looks like: a PM can say what work gets done by AI and what doesn't, and defend the line.*

2. **Guilty until proven innocent**

   High-risk outputs are assumed to be untrustworthy until proven otherwise through evals. No output feeds the next step without verification.

   *Good looks like: Stakeholder discussions are about strategy, not about whether a claim is substantiated.*

3. **Don't make me work harder**

   If the output requires verifying every step, the work has just been moved downstream.

   *Good looks like: HITL is used strategically, not as a catch-all for hallucination.*

4. **Outcomes over outputs**

   Start by defining what each task needs to achieve. Design the experience, process, and tool around that — not around what AI is capable of doing.

   *Good looks like: a lo-fi prototype for a concept test — even when AI could do a lot more.*

5. **Get smarter each round**

   Every human and machine eval feeds back into the system.

   *Good looks like: Precision/recall improves version to version and we learn why.*

### Measurements
**Lagging metrics:**

* **Efficiency:** 20% reduction in average time spent per validated feature (discovery to ready-for-dev, segmented by story points)
* **Quality:** 90% of agents in production meet eval thresholds, 1Q post-launch (measured quarterly)
* **Stakeholder trust:** % of OS-assisted outputs shared with stakeholders that were accepted without further requests for evidence or verification (manually tracked 14-days post-share)

**Leading metrics:**

* 20% reduction in time within each task type
* % fully autonomous tasks increasing MoM (agent completed, output used as-is)
* % semi-autonomous tasks increasing MoM (agent completed, PM refined or validated)
* % manual tasks decreasing MoM (agent not used or output not used entirely)

### Roadmap
MVP prioritises the critical user journey to minimise lead time from a business goal to a validated feature that's ready for development:
* Discovery: User research
* Solution definition
* Prototyping
* Meetings

R1 expands on the critical user journey to further increase efficiency:
* Discovery: Market Research
* Development 
* Testing
* GTM
* Comms

See detailed [roadmap and prioritisation criteria](https://docs.google.com/spreadsheets/d/14EWsWYquwbsFQ8w3uOwpFP5Fme2mU-jBUyPLY8_u5ts/edit?gid=0#gid=0)

## Index

### 🔍 Discovery

| Tool | Agent / Skill | Purpose |
| :--- | :--- | :--- |
| **Claude Code** | [Interview Analysis Agent](portfolio/interview-analysis.md) | Analyses user research interviews for pain points, bright spots, and project-specific dimensions — one file per participant, with verbatim quotes. No synthesis. |
| **Claude Code** | [Survey Analysis Agent](portfolio/survey-analysis.md) | Highlights key themes by user segment; deterministically computes all statistics via Python/pandas so the model only interprets, improving accuracy. |
| **Claude Code** | [Customer Feedback Analysis Agent](.claude/agents/customer-feedback-analysis.md) | Analyses customer support feedback verbatims for themes by user segment. |
| **Claude Code** | [Research Synthesis Agent](.claude/agents/research-synthesis.md) | Synthesises findings from analysis files (interview, survey, feedback) into a structured, visual-first research report for stakeholders. |
| **Claude Code** | [Company Context Agent](portfolio/create-company.md) | Conducts automated deep-dives into a company, its competitors, market landscape, and products. Serves as context for other agents (e.g. Interview Analysis Agent, PRD Generator). |
| **OpenClaw** | [Competitive Intel](.claude/agents/competitive-intel.md) | Sends a weekly competitive intelligence report to PMs. |

### 📄 Solution Definition 

| Tool | Agent / Skill | Purpose |
| :--- | :--- | :--- |
| **Claude Code** | [PRD Generator](others/01-prd-generator) | **Experiment only:** Creates PRD draft by synthesizing market research and internal company context files.<br>**Caveat:** Aimed to speed up summarization and initial ideation but cannot replace the deep understanding of problem context and strategic direction that a PM must first start with. |

### ✅ Eval / Verification

| Tool | Agent / Skill | Purpose |
| :--- | :--- | :--- |
| **Claude Code** | [Int Research Eval Agent](.claude/agents/int-research-eval.md) | Evaluates internal user research outputs. Combines human and machine evaluations to verify qual claims and quant calculations. Benchmarks Precision and Recall. |
| **Claude Code** | [Ext Research Eval Agent](.claude/agents/ext-research-eval.md) | Evaluates external web-based research outputs. Aggregates human's subjective assessment of Helpfulness, Honesty, and Harmlessness scores across reports to benchmark HHH scores over time. Machine evaluates objective criteria in each report (e.g., link validity, template adherence). |
| **Claude Code** | [Eval Feedback Command](.claude/commands/eval-feedback.md) | Updates the relevant agent or skill based on user's evaluation feedback. |
| **Claude Code** | [Check Agent Command](.claude/commands/check-agent.md) | Reviews and updates agent, skill, and command files to resolve conflicts, avoid template drift, and ensure consistency across files. |

### 👁️ Observability

| Tool | Agent / Skill | Purpose |
| :--- | :--- | :--- |
| **Claude Code** | [Observability Hooks](.claude/hooks/) | Captures tool inputs/outputs via deterministic shell hooks, preventing token consumption and Claude from forgetting instructions. Used by Debug Agent to trace errors and recommend improvements to agents and skills. |

### 🔧 Tooling

| Tool | Agent / Skill | Purpose |
| :--- | :--- | :--- |
| **Claude Code** | [Update Portfolio Command](.claude/commands/update-portfolio.md) | Generates or updates a portfolio README for any agent or skill. Reads the agent file and git history to draft an Iterations list, asks four questions, then writes a complete portfolio file with Mermaid workflow diagram and annual value-saved calculation. |
| **Claude Code** | [Meta Sync Command](.claude/commands/meta-sync.md) | Keeps CLAUDE.md, README.md, MEMORY.md, and .claudeignore up-to-date based on recent changes. |
| **Claude Code** | [Agent Template](.claude/_agent-template.md) | Template for building new Claude Code agents — forces agents to inherit conventions from CLAUDE.md to reuse instructions and prevent drift. |

### 🗂️ Misc. Experiments

| Tool | Agent / Skill | Purpose |
| :--- | :--- | :--- |
| **n8n** | [Agentic RAG Contract Auditor](others/04-agentic-rag) | Enhances retrieval when analyzing legal risks in contracts for lawyers. |
| **n8n** | [Traditional RAG Chatbot](others/05-traditional-rag) | Enables users to overcome context window limits. |
