# Workshop: RAG Chatbot Setup using Ollama + LangChain + VS Code

Learn how to create a Retrieval-Augmented Generation (RAG) chatbot using **LangChain**, **Ollama** (with LLaMA models), and **VS Code**. This setup runs locally, uses your own files (PDFs or .txt), and returns accurate, grounded answers.

---

## Table of Contents

1. [What is RAG?](#what-is-rag)
2. [Why Ollama + LangChain?](#why-ollama--langchain)
3. [System Requirements](#system-requirements)
4. [Step-by-Step Setup](#step-by-step-setup)
5. [Ingesting PDFs or Text Files](#ingesting-pdfs-or-text-files)
6. [Asking Questions](#asking-questions)
7. [Common Errors](#common-errors)
8. [License](#license)
9. [Contact](#contact)

---

## What is RAG?

**Retrieval-Augmented Generation (RAG)** enhances language models by combining them with an information retriever. This allows the model to look up relevant info from documents before generating a response.

---

## Why Ollama + LangChain?

* **Ollama**: Run powerful LLaMA models locally — no need for APIs or cloud access.
* **LangChain**: Chains tools like retrievers, memory, prompts, and agents.
* **VS Code**: Simple, developer-friendly IDE to run everything smoothly.

---

## System Requirements

* macOS, Linux, or Windows with WSL2
* Python 3.9+
* Ollama installed and LLaMA model pulled
* VS Code
* 8GB+ RAM recommended

---

## Step-by-Step Setup

### 🔹 Step 1: Install Ollama

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

### 🔹 Step 2: Pull LLaMA3 Model

```bash
ollama pull llama3
```

### 🔹 Step 3: Set Up Project in VS Code

```bash
git clone https://github.com/langchain-ai/langchain.git
cd langchain/examples
mkdir rag_ollama_demo && cd rag_ollama_demo
```

### 🔹 Step 4: Create Virtual Environment

```bash
python3 -m venv venv
source venv/bin/activate
pip install langchain llama-index pypdf ollama fastapi uvicorn
```

---

## Ingesting PDFs or Text Files

### Place files in a `docs/` folder

### Use LangChain to index content

```python
from langchain.document_loaders import PyPDFLoader
from langchain.vectorstores import FAISS
from langchain.embeddings import OllamaEmbeddings
from langchain.text_splitter import RecursiveCharacterTextSplitter

loader = PyPDFLoader("docs/sample.pdf")
documents = loader.load()

splitter = RecursiveCharacterTextSplitter(chunk_size=500, chunk_overlap=50)
chunks = splitter.split_documents(documents)

embeddings = OllamaEmbeddings(model="llama3")
db = FAISS.from_documents(chunks, embeddings)
```

---

## Asking Questions

```python
from langchain.chains import RetrievalQA
from langchain.llms import Ollama

llm = Ollama(model="llama3")
qa = RetrievalQA.from_chain_type(llm=llm, retriever=db.as_retriever())

query = "Summarize the second chapter"
response = qa.run(query)
print(response)
```

---

## Common Errors

| Problem             | Fix                                        |
| ------------------- | ------------------------------------------ |
| LLM not responding  | Ensure Ollama is running with `ollama run` |
| PDF not loading     | Check file path and file permissions       |
| Module import error | Run `pip install` inside your virtual env  |

---

## License

This setup and code are under the **MIT License**.

---

## Contact

Email: [contact@darion.in](mail to:contact@darion.in)
