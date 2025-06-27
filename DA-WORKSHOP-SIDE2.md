# Workshop: Building a RAG System with PDF/Text Input using LangChain

This guide walks you through creating a Retrieval-Augmented Generation (RAG) system where you can feed PDFs or text files into a chatbot, and it responds accurately using your custom data.

---

## Table of Contents

1. What is RAG?
2. Why Use RAG?
3. System Requirements
4. Installation Guide
5. PDF/Text File Ingestion
6. Running the Chatbot
7. Customization Tips
8. Troubleshooting
9. Resources & Links
10. License
11. Contact

---

## What is RAG?

Retrieval-Augmented Generation (RAG) combines:

* A retriever: Finds relevant chunks from documents (like PDFs, .txt files)
* A generator: Language model (LLM) that forms an answer using those chunks

This boosts accuracy, reduces hallucination, and provides context-aware responses.

---

## Why Use RAG?

| Feature       | Benefit                                     |
| ------------- | ------------------------------------------- |
| Accurate      | Answers are backed by your custom documents |
| Customizable  | Add your own text, docs, or knowledge base  |
| Local Control | Works without cloud queries                 |
| Scalable      | Works for students, developers, enterprises |

---

## System Requirements

* Python 3.9+
* pip or Poetry
* Git
* VS Code (or any IDE)
* 8GB RAM or more recommended

---

## Installation Guide (VS Code)

### Step 1: Clone the Repository

```bash
git clone https://github.com/workshopda/rag.py.git
cd rag.py
```

### Step 2: Set Up Environment and Install Dependencies

```bash
python3 -m venv venv
source venv/bin/activate

pip install langchain-community chromadb sentence-transformers pypdf unstructured python-docx
```

### Step 3: Prepare Data Directory

```bash
mkdir data
# Add your files into data/ (e.g., data.txt, notes.pdf, etc.)
```

---

## PDF/Text File Ingestion

Using `rag.py`, the script supports `.txt`, `.pdf`, and `.docx` files using `llama_index` and LangChain loaders:

```python
from langchain_community.document_loaders import TextLoader, PyPDFLoader, UnstructuredWordDocumentLoader
```

All files should be placed in the `/data` folder. The script will automatically load and chunk them using:

```python
from langchain.text_splitter import RecursiveCharacterTextSplitter
```

---

## Running the Chatbot

To run the chatbot:

```bash
python rag.py
```

You can now ask questions in the terminal like:

* "What does this document talk about?"
* "Summarize the second paragraph."
* Type `exit` to stop.

---

## Customization Tips

* Replace `tinyllama` with any available Ollama model (e.g., `llama2`, `mistral`)
* Edit `chunk_size` and `chunk_overlap` in `RecursiveCharacterTextSplitter`
* Expand sources to web pages, CSVs, or APIs
* Customize prompt templates via LangChain chains

---

## Troubleshooting

| Problem            | Solution                                      |
| ------------------ | --------------------------------------------- |
| Import Errors      | Reinstall missing package using `pip install` |
| No documents found | Ensure files are in `data/` folder            |
| LLM not responding | Make sure `ollama run tinyllama` is active    |

---

## Resources & Links

* [https://github.com/jerryjliu/llama\_index](https://github.com/jerryjliu/llama_index)
* [https://github.com/langchain-ai/langchain](https://github.com/langchain-ai/langchain)
* [https://github.com/tiangolo/fastapi](https://github.com/tiangolo/fastapi)
* [https://github.com/ollama/ollama](https://github.com/ollama/ollama)
* [https://github.com/workshopda/rag.py](https://github.com/workshopda/rag.py)

---

## License

This RAG setup is open source under the MIT License. Fork, modify, and build your own AI tools!

---

## Contact

Mail: [contact@darion.in](mailto:contact@darion.in)

