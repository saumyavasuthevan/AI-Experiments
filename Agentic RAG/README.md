# Agentic RAG Workflow

To extract and analyse risks in contracts for lawyers, created an Agentic RAG workflow, using **Orchestration Agent** and **Agentic Retrieval** to improve retrieval of key terms and ensure analysis of risks is grounded in contract data.



---

## 🔄 Workflow Summary

The system processes queries through a structured multi-step pipeline:

1.  **User Query:** The entry point for any natural language question.
2.  **Orchestration Agent:** Classifies the query as **Factual** or **Analytical**.
3.  **Thought Agent (Enhancement):** Refines, expands, or reformulates the query for better search accuracy.
4.  **Vector Store Tool:** Performs semantic retrieval based on the enhanced query.
5.  **Final Response:** Synthesizes the retrieved context into a grounded final answer.

---

## 🛠 Component Breakdown

### 1. Orchestration Agent
The "Brain" of the system. It performs intent classification to determine the required depth of reasoning.
* **Factual:** Directed toward simple data retrieval.
* **Analytical:** Directed toward complex reasoning and synthesis.

### 2. Thought Agent (Query Enhancement)
Before searching, the selected agent optimizes the raw user input.
* **Clarification:** Resolving ambiguities.
* **Expansion:** Adding technical terms or synonyms.
* **Reformulation:** Converting questions into "search-optimized" prompts.

### 3. Simple Vector Store Tool
A retrieval utility that manages the knowledge base.
* **Embeddings:** Text is converted into vectors for mathematical comparison.
* **Top-K Retrieval:** Extracts the most relevant "chunks" of data from the database.

### 4. Final Reasoning & Synthesis
The active agent receives the data chunks and combines them with the enhanced query logic to produce a response that is accurate, relevant, and free of hallucinations.

---
