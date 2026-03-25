# PRD Generator (Experiment only)

I built this to test Claude’s ability to synthesize and structure a Product Requirements Document (PRD) by connecting internal company context with external market signals. 

### What it does
Generates a structured draft based on provided internal research and external market data.

### The Thinking Behind the Experiment
I am a firm believer that you cannot generate a meaningful PRD with the click of a button. A great PRD requires a deep understanding of internal goals, alignment with broader company strategies, and iteration.

* **What this is:** A way to test where AI can speed things up (summarization, structure, and initial ideation).
* **What this isn't:** A replacement for strategic thinking. 

**The Goal:** To explore how AI can handle the heavy lifting of documentation while maintaining the PM's role in defining the direction and then evaluating the final output. 

### Company Context Files (`company-context/`)

These files contain company information as context for PRD:

- `company-overview.md` - Company background, team, metrics, strategy, OKRs
- `user-personas.md` - Three user personas: Jennifer (GC), David (Senior Counsel), Rachel (Legal Ops)
- `product-description.md` - Current product features, roadmap, tech stack
- `competitive-landscape.md` - Competitors and market positioning

### Templates (`templates/`)

Pre-defined output format templates that ensure consistency in your deliverables:

- `market-research-format.md` - Structure for market research deliverables
- `prd-template.md` - Structure for Product Requirements Documents

### Sample Prompts (`sampleprompts/`)

Ready-to-use example prompts for common PM tasks:

- `market-research-prompt.md` - Example prompt for conducting market research
- `prd-prompt.md` - Example prompt for writing PRDs

### Configuration Files

- `CLAUDE.md` - Project-level instructions for Claude Code (defines context and workflows)


