# Workshop: Easy RAG Chatbot Setup with PDF/Text Input

This guide simplifies the **Retrieval-Augmented Generation (RAG)** setup for beginners using a light and fast project. You’ll install everything, upload your PDFs or notes, and query them — all in minutes.

---

## Table of Contents

1. [What is RAG?](#what-is-rag)
2. [Why Use It?](#why-use-it)
3. [Requirements](#requirements)
4. [Quick Setup Using Simple Repo](#quick-setup-using-simple-repo)
5. [How to Ask Questions from PDF](#how-to-ask-questions-from-pdf)
6. [Helpful Tools](#helpful-tools)
7. [Optional: Using LangChain](#optional-using-langchain)
8. [Common Issues](#common-issues)
9. [License](#license)
10. [Contact](#contact)

---

## What is RAG?

**RAG** stands for Retrieval-Augmented Generation. It makes your chatbot smarter by reading your own documents before answering.

---

## Why Use It?

| ✅ Feature       | 📌 Benefit                           |
| --------------- | ------------------------------------ |
| Uses your files | Answers only from your PDFs or notes |
| Offline-ready   | No cloud or external APIs needed     |
| Works locally   | Runs fully on your computer          |

---

## Requirements

* Python 3.9 or higher
* Git
* Internet (for setup only)
* At least 8GB RAM recommended

---

## Quick Setup Using Simple Repo

```bash
# Step 1: Clone the beginner-friendly repo
git clone https://github.com/ChocoPancakes1219/RAG-application-using-LlamaIndex.git
cd RAG-application-using-LlamaIndex

# Step 2: Install dependencies
python3 -m venv venv
source venv/bin/activate
pip install -r Requirements.txt

# Step 3: Add your documents
mkdir data
# Place your PDFs or .txt files in the 'data' folder

# Step 4: Start the chatbot
python main.py
```

🖥 Go to your browser: `http://localhost:8000`

Ask anything from your document like:

* "What is explained in section 2?"
* "Summarize chapter 5."

---

## How to Ask Questions from PDF

```python
from llama_index import SimpleDirectoryReader, VectorStoreIndex

documents = SimpleDirectoryReader("data").load_data()
index = VectorStoreIndex.from_documents(documents)
index.storage_context.persist()
```

Then:

```python
query_engine = index.as_query_engine()
response = query_engine.query("Give an overview of the second topic")
print(response)
```

---

## Helpful Tools

* [LlamaIndex](https://github.com/run-llama/llama_index)
* [FastAPI](https://github.com/fastapi/fastapi)
* [Ollama](https://github.com/ollama/ollama) – Local model runtime
* [ChocoPancakes1219 Repo](https://github.com/ChocoPancakes1219/RAG-application-using-LlamaIndex)

---

## Optional: Using LangChain

If you'd like more control over chains, memory, or custom workflows, you can also integrate [LangChain](https://github.com/langchain-ai/langchain).

LangChain lets you:

* Build advanced prompt chains
* Use memory and context-aware conversations
* Combine multiple tools with RAG (e.g., search + summarization)

Install with:

```bash
pip install langchain
```

---

## Common Issues

| Problem            | Fix                                      |
| ------------------ | ---------------------------------------- |
| Can't install deps | Run: `pip install -r Requirements.txt`   |
| Docs not loading   | Make sure PDFs are inside `/data` folder |
| Page not opening   | Visit: `http://localhost:8000`           |

---

## License

This project uses the **MIT License** — free to use, modify, and share.

---

## Contact

Email: [contact@darion.in](mailto:contact@darion.in)

