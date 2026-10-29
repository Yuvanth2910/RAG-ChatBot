# RAG-Based Intelligent Chatbot for PDF Question Answering

A Retrieval-Augmented Generation (RAG) application that enables users to ask questions about PDF documents and receive context-based answers using **Google Gemini, LangChain, and ChromaDB**.

This project demonstrates a practical implementation of a document question-answering pipeline, combining semantic search with large language models (LLMs) to retrieve relevant document content before generating a response.

Developed as part of my journey towards becoming an **AI Engineer**, with a focus on building practical LLM applications and understanding how retrieval-based AI systems work.

## Overview

Traditional LLM applications can generate answers that are not grounded in a specific document. RAG addresses this limitation by retrieving relevant information from an external knowledge source and providing it as context to the language model.

This project implements a PDF-based RAG pipeline that:

- Extracts text from PDF documents.
- Splits extracted text into manageable chunks.
- Generates vector embeddings using a Google Gemini embedding model.
- Stores document embeddings in ChromaDB.
- Retrieves relevant chunks through semantic similarity search.
- Uses Gemini 2.5 Flash to generate answers based on the retrieved context.

## Architecture

```text
                DOCUMENT INGESTION
                        |
                        v
                   PDF Document
                        |
                        v
                 PyPDF Text Extraction
                        |
                        v
                   Text Chunking
                        |
                        v
                Gemini Embeddings
                        |
                        v
                 ChromaDB Vector Store
                        |
                ---------------------
                        |
                  QUESTION ANSWERING
                        |
                        v
                   User Question
                        |
                        v
                Question Embedding
                        |
                        v
                Semantic Retrieval
                        |
                        v
                Relevant Document Chunks
                        |
                        v
                 Contextual Prompt
                        |
                        v
                  Gemini 2.5 Flash
                        |
                        v
                   Generated Answer
```

## Tech Stack

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| Google Gemini API | Embeddings and LLM-based answer generation |
| Gemini 2.5 Flash | Response generation |
| LangChain | Document processing and RAG pipeline integration |
| ChromaDB | Vector storage and semantic retrieval |
| PyPDF | PDF text extraction |
| Google Colab | Development and experimentation environment |

## How It Works

### 1. PDF ingestion

PDF documents are loaded and their text is extracted using PyPDF. The extracted content becomes the source material for the question-answering system.

### 2. Text chunking

The extracted text is divided into smaller chunks to make retrieval more focused and provide relevant context to the language model.

### 3. Embedding generation

The text chunks are converted into numerical vector representations using a Google Gemini embedding model. These embeddings represent the semantic meaning of the document content.

### 4. Vector storage

The generated embeddings and their associated document content are stored in ChromaDB, enabling similarity-based retrieval.

### 5. Semantic retrieval

When a user submits a question, the system generates a corresponding query embedding and searches the vector store for relevant document chunks.

### 6. Context-based generation

The retrieved content is included in a prompt alongside the user's question. Gemini 2.5 Flash uses this context to generate a response.

### 7. Answer generation

The system returns the generated answer to the user. Its usefulness depends on the quality of the source document, chunking strategy, retrieval results, and prompt design.

## Example Use Case

**Document:** Employee handbook

**Question:**

> How many casual leaves are given?

**Retrieved context:**

```text
Employees are entitled to 18 casual leaves,
12 sick leaves, and 15 earned leaves.
```

**Expected answer:**

```text
Employees are entitled to 18 casual leaves per year.
```

This illustrates how the system can answer a question using information retrieved from a document rather than requiring the entire PDF to be included in every prompt.

*The example illustrates the intended behaviour. Actual answers depend on the document and retrieval results.*

## Getting Started

### Prerequisites

- Python 3.10 or a compatible Python version supported by the selected dependencies.
- A Google account for Google Colab.
- Access to the Google Gemini API.
- A PDF document containing extractable text.

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/rag-pdf-chatbot.git
cd rag-pdf-chatbot
```

Replace `YOUR_USERNAME` with your GitHub username and adjust the repository name if necessary.

### 2. Install dependencies

```bash
pip install pypdf langchain langchain-text-splitters
pip install langchain-google-genai langchain-chroma chromadb
```

For a reproducible setup, install the dependency versions recorded in the project's `requirements.txt`, if provided.

### 3. Configure the Gemini API key

Create a Gemini API key through Google AI Studio.

When using Google Colab, store the key in Colab Secrets under:

```text
GOOGLE_API_KEY
```

Retrieve it in the notebook:

```python
from google.colab import userdata

GOOGLE_API_KEY = userdata.get("GOOGLE_API_KEY")
```

Keep API keys private. Do not commit secrets, credentials, or environment files containing real keys to GitHub.

### 4. Run the notebook

Open `RAG_Based_Intelligent_Chatbot.ipynb` in Google Colab, upload your PDF document, configure the API key, and execute the notebook cells in order.

Follow the notebook's configuration for the embedding and generation models.

## Project Structure

```text
rag-pdf-chatbot/
│
├── RAG_Based_Intelligent_Chatbot.ipynb
├── Employee_Handbook_Sample.pdf
├── requirements.txt
├── .gitignore
└── README.md
```

The structure above describes the intended repository layout. Include only files that actually exist in your repository.

## Key Concepts Demonstrated

- Retrieval-Augmented Generation (RAG)
- PDF document ingestion and text extraction
- Text chunking and document preprocessing
- Vector embeddings and semantic similarity
- Vector database integration with ChromaDB
- LLM integration using the Google Gemini API
- Context construction and prompt engineering
- Building a document question-answering workflow

## Current Scope and Limitations

The current project focuses on the core PDF-based RAG workflow.

- Answer quality depends on the relevance and quality of retrieved chunks.
- PDFs with scanned pages may require OCR before their contents can be retrieved.
- Semantic similarity does not guarantee that the retrieved text contains the correct answer.
- Generated answers can still be inaccurate or unsupported by the source document.
- API usage may incur costs and is subject to provider limits.
- Features such as multi-document management, persistent production storage, source citations, automated evaluation, and deployment are not claimed as implemented unless they are added and verified.

## Future Improvements

The following are potential extensions, not features of the current implementation.

- [ ] Support uploading and querying multiple PDF documents.
- [ ] Add source citations with page numbers for generated answers.
- [ ] Improve retrieval with hybrid search using BM25 and vector similarity.
- [ ] Add cross-encoder reranking to improve the relevance of retrieved chunks.
- [ ] Evaluate retrieval quality and answer faithfulness using a test dataset.
- [ ] Add automated tests and continuous integration checks.
- [ ] Build a FastAPI backend.
- [ ] Develop a Streamlit or React user interface.
- [ ] Add persistent vector storage and document management.
- [ ] Containerise the application with Docker.
- [ ] Deploy the application to a cloud platform.

## Learning Objectives

Through this project, I aim to strengthen my practical understanding of:

1. How document-based RAG systems are designed.
2. How embeddings and vector databases support semantic retrieval.
3. How retrieved context influences LLM-generated responses.
4. How to integrate LLMs and retrieval components into a Python application.
5. How to evolve a prototype into a tested, reliable AI application.

## About Me

I am pursuing an **MSc in Artificial Intelligence with Industrial Practice at the University of Surrey, UK**, with a goal of becoming an AI Engineer.

I am building practical projects to strengthen my skills in Python, machine learning, LLM applications, and AI system development, with a focus on understanding the underlying concepts rather than relying only on pre-built solutions.

**GitHub:** [Add your GitHub profile URL](https://github.com/)

**LinkedIn:** [Add your LinkedIn profile URL](https://www.linkedin.com/)

## Acknowledgements

This project uses the Google Gemini API, LangChain, ChromaDB, and PyPDF. Refer to their official documentation for setup instructions, API usage, and supported versions.

## License

Choose and add an appropriate open-source license before publishing the repository for reuse. No license is implied by this README.
