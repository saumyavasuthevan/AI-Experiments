# 🔬 n8n RAG Workflow Lab
Traditional RAG that allows users to chat with large documents that exceed standard AI context windows.

---

## 🧪 Completed Experiment: n8n RAG Workflow
**Description:** Solves the "Context Window" problem where large documents (like complex contracts) fail due to token limits. It uses an **n8n** workflow to split documents into chunks, convert them into vector embeddings, and store them for semantic retrieval.

### 🛠️ How it Works
1.  **Augmentation:** Raw files are segmented and vectorized into a Simple Vector Store.
2.  **Retrieval:** User queries are converted into embeddings to find semantically similar document chunks.
3.  **Generation:** Relevant context is passed to the LLM to provide accurate, grounded answers without processing the entire document at once.

### ✅ Key Capabilities
* **Handle Large Docs:** Effectively analyzes documents of any length.
* **Reduced Hallucinations:** Grounds AI responses in specific, retrieved facts.
* **Semantic Search:** Finds information based on meaning rather than just keywords.
