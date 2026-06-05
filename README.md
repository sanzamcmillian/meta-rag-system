#  Meta-Powered RAG Document Assistant

A PDF question-answering system powered by **Meta's Llama 3.3 70B** model.
Upload any PDF, ask questions in plain English, and get accurate answers grounded strictly in the document — no hallucinations, no guessing.

---

##  What Is This?

This project implements a **Retrieval-Augmented Generation (RAG)** pipeline that turns any PDF into an interactive AI assistant.

Instead of relying on the AI's general knowledge, the system reads *your* document, finds the most relevant sections, and generates answers based only on what is written in the PDF.

**Example use cases:**
- Query a company report: *"What were the key risks identified this quarter?"*
- Understand a policy document: *"What does this policy say about remote work?"*
- Summarise research: *"What are the main findings in chapter two?"*

---

##  Features

- **Semantic Chunking** — splits the PDF into meaning-based sections rather than arbitrary text blocks, improving retrieval accuracy
- **Query Fusion Retrieval** — rewrites each user question 6 different ways, performs parallel searches, and merges the best results (based on Meta's Llama Cookbook)
- **Anti-Hallucination Guardrails** — the AI is instructed to answer only from the document and explicitly say so when information is not found
- **Google Drive Integration** — paste a Drive link and the system downloads your PDF automatically
- **Retry Logic** — handles network timeouts gracefully with automatic retries
- **Interactive Q&A Loop** — keep asking questions until you type `end`

---

##  Tech Stack

| Component | Technology |
|---|---|
| RAG Framework | LlamaIndex |
| LLM | Meta Llama 3.3 70B (via OpenRouter) |
| Embeddings | HuggingFace `BAAI/bge-small-en-v1.5` |
| Chunking | SemanticSplitterNodeParser |
| Retrieval | QueryRewritingRetrieverPack (Query Fusion) |
| Runtime | Google Colab |
| Language | Python |

---

##  Architecture

```
PDF (Google Drive)
       │
       ▼
 Document Loader
 (SimpleDirectoryReader)
       │
       ▼
 Semantic Chunker
 (HuggingFace Embeddings)
       │
       ▼
 Vector Index
       │
       ▼
 User Question
       │
       ▼
 Query Fusion Retriever
 (6x query rewrites → parallel search → merge)
       │
       ▼
 Meta Llama 3.3 70B
 (context-grounded answer generation)
       │
       ▼
 Answer (with anti-hallucination rules)
```

---

##  Getting Started

### Prerequisites

- Google Colab account
- OpenRouter API key → [Get one here](https://openrouter.ai)
- A PDF stored in Google Drive (with sharing enabled)

### Steps

1. Open `meta_rag_sys.ipynb` in Google Colab
2. Run **Step 1** to install all dependencies
3. Run **Step 2** and enter your OpenRouter API key when prompted
4. Run **Step 3** and paste your Google Drive PDF link
5. Run **Step 4** — the system will semantically chunk your document
6. Run **Step 5** — the Query Fusion search engine is built
7. Run **Step 6** — start asking questions!

---

## 💬 Example Session

```
🟦 Enter your question: What was the document about?

🔍 Retrieving answer...

Generated queries:
  What is the main topic of the document?
  What are the key points discussed?
  Can you summarise the content?
  ...

──────────────────────────────────────────────
❓ QUESTION:
What was the document about?

🧠 ANSWER:
The document appears to be about identifying and scaling AI use cases.
* It discusses prioritising high-impact use cases using an Impact/Effort Framework.
* It provides examples of AI applications in content creation and marketing workflows.
* It appears to be an enterprise guide for AI adoption.
──────────────────────────────────────────────

🟦 Enter your question: How much is bread?

🧠 ANSWER:
There is no information about the price of bread.
* The context discusses AI use cases and does not mention bread or any related prices.
──────────────────────────────────────────────
```

---

##  Project Structure

```
meta-rag-system/
│
├── meta_rag_sys.ipynb        # Main notebook (all 6 steps)
└── README.md                 # You are here
```

---

##  Key Concepts

**RAG (Retrieval-Augmented Generation)**
A technique that combines a search/retrieval system with a generative AI model. Instead of answering from memory, the model retrieves relevant context from a document first, then generates a grounded answer.

**Semantic Chunking**
Rather than splitting a document every N characters, semantic chunking uses embedding similarity to find natural breakpoints — keeping related ideas together and improving retrieval quality.

**Query Fusion**
An advanced retrieval technique where the user's question is rewritten into multiple variations, each variation is searched independently, and the results are fused together using Reciprocal Rank Fusion (RRF) before being passed to the LLM.

---

##  Author

**Sanele Skhosana**
[GitHub](https://github.com/sanzamcmillian) · [Email](mailto:sanzamcmillian@gmail.com)

---

## 📄 License

This project is licensed under the MIT License.
