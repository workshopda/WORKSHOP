# Workshop: Building a RAG System with PDF/Text Input for Accurate AI Responses

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
* pip
* Git
* At least 8GB RAM recommended

---

## Installation Guide

```bash
# Step 1: Clone the repo
git clone https://github.com/yourname/rag-chatbot.git
cd rag-chatbot

# Step 2: Create a virtual environment
python3 -m venv venv
source venv/bin/activate

# Step 3: Install dependencies
pip install -r requirements.txt

# Step 4: Download a supported LLM (via Ollama)
ollama pull llama3

# Step 5: Start Ollama (in background or terminal)
ollama run llama3

# Step 6: Launch your FastAPI server
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

---

## PDF/Text File Ingestion

We use `llama-index` or `langchain` to load and chunk your files:

```python
from llama_index import SimpleDirectoryReader
from llama_index import VectorStoreIndex

# Load PDFs or .txt files from the "docs" folder
documents = SimpleDirectoryReader("docs").load_data()
index = VectorStoreIndex.from_documents(documents)

# Persist the index for querying later
index.storage_context.persist()
```

Store your documents inside a `/docs` folder.

---

## Running the Chatbot

Once your index is built:

```python
from llama_index import load_index_from_storage

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

| Problem                 | Solution                                  |
| ----------------------- | ----------------------------------------- |
| Import Errors           | Check `requirements.txt` and install      |
| Slow Responses          | Use smaller models or better hardware     |
| "Index Not Found" Error | Make sure `storage_context.persist()` ran |

---

## Resources & Links

* [LlamaIndex Docs](https://docs.llamaindex.ai/)
* [LangChain](https://docs.langchain.com/)
* [Ollama](https://ollama.com)
* [FastAPI](https://fastapi.tiangolo.com/)

---

## License

This RAG setup is MIT licensed. Feel free to fork, customize, and build!

---

## Contact

Mail: contact@darion.in for support or inquiries.
