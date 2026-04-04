# 📚 RAG System — Learning Repository

A hands-on learning project covering the full pipeline of **Retrieval-Augmented Generation (RAG)** systems, built progressively from data ingestion to hybrid search strategies.

> **Purpose:** Personal reference and learning resource for building production-ready RAG pipelines in Python.

---

## 📁 Project Structure

```
RAG_System/
│
├── DataingestParsing/               # Stage 1 — Load & parse raw documents
├── vectorembedding_and_data_base/   # Stage 2 — Embed text & store in vector DB
├── vector_store/                    # Stage 3 — Vector store operations & retrieval
├── vectorDB/                        # Stage 4 — Advanced vector database configs
├── advanced_chankes_and_preprocessing/  # Stage 5 — Chunking strategies & text preprocessing
├── Hypird_search_stratigy/          # Stage 6 — Hybrid search (semantic + keyword)
│
├── requirements.txt                 # All dependencies
├── .gitignore                       # Files excluded from Git
└── README.md                        # You are here
```

---

## 🗺️ Learning Roadmap

| # | Stage | Folder | Status |
|---|-------|--------|--------|
| 1 | Data Ingestion & Parsing | `DataingestParsing/` | ✅ Done |
| 2 | Vector Embeddings & Database | `vectorembedding_and_data_base/` | ✅ Done |
| 3 | Vector Store & Retrieval | `vector_store/` | ✅ Done |
| 4 | Advanced Vector DB Configs | `vectorDB/` | ✅ Done |
| 5 | Advanced Chunking & Preprocessing | `advanced_chankes_and_preprocessing/` | ✅ Done |
| 6 | Hybrid Search Strategy | `Hypird_search_stratigy/` | ✅ Done |
| 7 | Query Enhancement | *(coming soon)* | 🔜 Next |
| 8 | Agentic AI | *(separate folder)* | 🔜 Planned |

---

## 📦 Dependencies

All packages are listed in `requirements.txt`. Below is a breakdown by category.

---

### 🔗 LangChain Core

| Package | Purpose |
|---|---|
| `langchain` | Core framework — chains, prompts, retrievers, memory |
| `langchain-community` | Community integrations — loaders, vector stores, tools |
| `langchain-experimental` | Experimental features — agents, PAL chains, etc. |

> **What is LangChain?** A framework for building LLM-powered applications. It connects your data sources, embedding models, vector stores, and LLMs into a unified pipeline (called a "chain").

---

### 🤖 LLM Providers

| Package | Purpose |
|---|---|
| `langchain-groq` | Connect to Groq API — fast inference with LLaMA, Mixtral |
| `langchain-openai` | Connect to OpenAI API — GPT-4, GPT-3.5, Ada embeddings |
| `langchain-openrouter` | Connect to OpenRouter — access many models via one API |

> **What is Groq?** A hardware + API provider that runs open-source LLMs (like LLaMA 3) extremely fast. Great for free-tier experimentation.

---

### 🧠 Embeddings

| Package | Purpose |
|---|---|
| `sentence-transformers` | Local embedding models — runs on your machine, no API key needed |
| `langchain-huggingface` | LangChain wrapper for HuggingFace embedding models |
| `tiktoken` | OpenAI's tokenizer — counts tokens before sending to API |

> **What are embeddings?** A way to convert text into a list of numbers (a vector) that captures its meaning. Similar texts produce similar vectors. This is the core of semantic search.

> **`sentence-transformers` models to know:**
> - `all-MiniLM-L6-v2` — fast, small, good quality
> - `all-mpnet-base-v2` — slower, better quality
> - `BAAI/bge-small-en` — state-of-the-art, compact

---

### 🗄️ Vector Databases

| Package | Purpose |
|---|---|
| `faiss-cpu` | Facebook's local vector store — fast similarity search, no server needed |
| `chromadb` | Local vector database — persistent storage, easy to use |
| `langchain-astradb` | Connect to AstraDB (DataStax) — cloud vector DB |
| `langchain-pinecone` | Connect to Pinecone — managed cloud vector DB |

> **Which to use when?**
> - **FAISS** → quick experiments, no persistence needed
> - **ChromaDB** → local development with persistence
> - **Pinecone / AstraDB** → production / cloud deployments

---

### 📄 Document Loaders & Parsers

| Package | Purpose |
|---|---|
| `pypdf` | Parse PDF files — extract text page by page |
| `pymupdf` | Advanced PDF parsing — handles complex layouts, images |
| `python-docx` | Read and write `.docx` Word files |
| `docx2txt` | Simple `.docx` → plain text converter |
| `unstructured[DOCX]` | Intelligent document parsing — handles mixed layouts |

> **`pypdf` vs `pymupdf`:**
> `pypdf` is simpler and pure Python. `pymupdf` (also called `fitz`) is faster and handles scanned PDFs and complex formatting better.

---

### 🔍 Hybrid Search

| Package | Purpose |
|---|---|
| `rank_bm25` | BM25 keyword search algorithm — the classic TF-IDF-based retriever |

> **What is Hybrid Search?** Combining **semantic search** (vector similarity) with **keyword search** (BM25) and merging their results. This catches both meaning-based and exact-match cases, improving retrieval quality.

> **How it works:**
> 1. Run BM25 search → get top-k keyword matches
> 2. Run FAISS/Chroma search → get top-k semantic matches
> 3. Merge + re-rank results (e.g. with Reciprocal Rank Fusion)

---

### 📊 Data & Utilities

| Package | Purpose |
|---|---|
| `pandas` | Data manipulation — load CSVs, DataFrames, structured data |
| `openpyxl` | Read/write Excel `.xlsx` files |
| `matplotlib` | Plot charts — visualize embeddings, retrieval scores |
| `numpy` | Numerical operations — array math, vector operations |
| `python-dotenv` | Load API keys from a `.env` file securely |

---

## ⚙️ Setup & Installation

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/RAG_System.git
cd RAG_System
```

### 2. Create a virtual environment

```bash
python -m venv .venv

# On Windows
.venv\Scripts\activate

# On Mac/Linux
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Set up API keys

Create a `.env` file in the root directory:

```env
OPENAI_API_KEY=your_openai_key_here
GROQ_API_KEY=your_groq_key_here
PINECONE_API_KEY=your_pinecone_key_here
```

Load it in your Python scripts with:

```python
from dotenv import load_dotenv
load_dotenv()
```

---

## 🧱 RAG Pipeline Overview

```
Raw Documents (PDF, DOCX, TXT)
        ↓
  [1] Data Ingestion & Parsing
        ↓
  [2] Text Chunking & Preprocessing
        ↓
  [3] Embedding Generation
        ↓
  [4] Vector Store (FAISS / ChromaDB)
        ↓
  [5] Retrieval (Semantic + BM25 Hybrid)
        ↓
  [6] Query Enhancement  ← coming next
        ↓
  [7] LLM Generation (Groq / OpenAI)
        ↓
      Answer
```

---

## 🔜 Coming Next

### Query Enhancement
Techniques to improve the user's query before retrieval:
- **Query rewriting** — rephrase the question for better matches
- **HyDE (Hypothetical Document Embeddings)** — generate a fake answer, embed it, search with that
- **Multi-query retrieval** — generate multiple versions of the question, retrieve for each, merge results
- **Step-back prompting** — ask a more general question first to find broader context

### Agentic AI *(planned — separate folder)*
Moving from static RAG chains to dynamic agents that can:
- Decide *when* to retrieve
- Use multiple tools (search, calculator, code executor)
- Plan and reflect on multi-step tasks
- Frameworks: LangGraph, AutoGen, CrewAI

---


## 📚 Learning Resources

- [LangChain Docs](https://python.langchain.com/)
- [HuggingFace Sentence Transformers](https://www.sbert.net/)
- [ChromaDB Docs](https://docs.trychroma.com/)
- [FAISS GitHub](https://github.com/facebookresearch/faiss)
- [Groq Console](https://console.groq.com/)
- [BM25 Explained](https://en.wikipedia.org/wiki/Okapi_BM25)

---

*Built while learning RAG — step by step 🚀*