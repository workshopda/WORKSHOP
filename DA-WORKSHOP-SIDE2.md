# Workshop: Building a RAG System with PDF/Text Input using langchain

This guide walks you through creating a **Retrieval-Augmented Generation (RAG)** system where you can feed PDFs or text files into a chatbot, and it responds accurately using your custom data.

---

## Table of Contents

1. [What is RAG?](#what-is-rag)
2. [Why Use RAG?](#why-use-rag)
3. [System Requirements](#system-requirements)
4. [Installation Guide](#installation-guide)
5. [PDF/Text File Ingestion](#pdftext-file-ingestion)
6. [Running the Chatbot](#running-the-chatbot)
7. [Customization Tips](#customization-tips)
8. [Troubleshooting](#troubleshooting)
9. [Resources & Links](#resources--links)
10. [License](#license)
11. [Contact](#contact)

---

## What is RAG?

**Retrieval-Augmented Generation (RAG)** combines:

* A **retriever**: Finds relevant chunks from documents (like PDFs, .txt)
* A **generator**: Language model (LLM) that forms an answer using those chunks

This boosts accuracy, reduces hallucination, and provides context-aware responses.

---

## Why Use RAG?

| Feature       | Benefit                                    |
| ------------- | ------------------------------------------ |
| Accurate      | Answers are backed by your data            |
| Customizable  | Add your own text, docs, or knowledge base |
| Local Control | Works without sending queries to cloud     |
| Scalable      | Useful for enterprise, education, and devs |

---

## System Requirements

* Python 3.9+
* pip or Poetry
* Git
* At least 8GB RAM recommended

---

## Installation Guide

```bash
# Step 1: Clone the official RAG-FastAPI-LlamaIndex repo
git clone https://github.com/cespeleta/rag-fastapi-llamaindex.git
cd rag-fastapi-llamaindex

# Step 2: Copy and configure environment variables
cp .env.example .env
# Edit `.env` and add your HuggingFace token (if needed)

# Step 3: Install dependencies
# Using Poetry:
poetry install
poetry shell

# Or using pip (if using venv):
# python3 -m venv venv
# source venv/bin/activate
# pip install -r requirements.txt

# Step 4: Add your PDFs
# Place any PDF files you want to query into the ./pdfs directory

# Step 5: Run the service
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload

# Step 6: (Optional) Using Docker
make build.docker
make run.docker

# Step 7: Access the UI and API
# - FastAPI Swagger UI: http://localhost:8000/docs
# - Query endpoint: POST http://localhost:8000/api/v1/query/query
```

---

## PDF/Text File Ingestion

Using `llama-index` to load and chunk your files:

```python
from llama_index import SimpleDirectoryReader, VectorStoreIndex

# Load PDFs or .txt files from the "pdfs" folder
documents = SimpleDirectoryReader("pdfs").load_data()
index = VectorStoreIndex.from_documents(documents)

# Persist the index for querying later
index.storage_context.persist()
```

---

## Running the Chatbot

Once your index is built:

```python
from llama_index import load_index_from_storage, StorageContext

storage_context = StorageContext.from_defaults(persist_dir="./storage")
index = load_index_from_storage(storage_context)
query_engine = index.as_query_engine()

response = query_engine.query("What is the purpose of this document?")
print(response)
```

---

## Customization Tips

* Replace `llama3` with another model if needed
* Modify `chunk_size` and `chunk_overlap` for better recall
* Integrate with Gradio or Streamlit for UI
* Add `.env` support for configurations

---

## Troubleshooting

| Problem                 | Solution                                     |
| ----------------------- | -------------------------------------------- |
| Import Errors           | Check `requirements.txt` or `pyproject.toml` |
| Slow Responses          | Use smaller models or better hardware        |
| "Index Not Found" Error | Make sure `storage_context.persist()` ran    |

---

## Resources & Links

* [LlamaIndex](https://github.com/run-llama/llama_index) – Document ingestion and indexing framework.
* [LangChain](https://github.com/langchain-ai/langchain) – Chain components for RAG, agents, prompts.
* [FastAPI](https://github.com/fastapi/fastapi) – Web server to expose query endpoints.
* [Ollama](https://github.com/ollama/ollama) – Local LLM runtime via CLI or Python/JS SDK.
* [RAG-FastAPI-LlamaIndex (cespeleta)](https://github.com/cespeleta/rag-fastapi-llamaindex) – Full working RAG chatbot repo.

---

## License

This RAG setup is MIT licensed. Feel free to fork, customize, and build!

---

## Contact

MAIL: contact@darion.in for support or inquiries.
