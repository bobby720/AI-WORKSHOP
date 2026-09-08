# 🤖 AI WORKSHOP

> A hands-on collection of practical AI projects covering **Retrieval-Augmented Generation (RAG), semantic search, vector databases, LLM-powered applications, and AI-based resume analysis.**

---

## 🚀 Overview

**AI-WORKSHOP** is a collection of practical Artificial Intelligence projects built to explore how modern AI systems work beyond simple prompting.

The repository focuses on three core applications:

* 🧠 **Mini RAG** — Build a basic Retrieval-Augmented Generation pipeline from scratch.
* 📄 **PDF Chatbot RAG** — Ask questions about PDF documents using semantic retrieval and an LLM.
* 📊 **AI Resume Analyzer** — Analyze resumes against a target job role using an LLM-powered API.

Each project demonstrates a different stage of building real-world AI applications, from **document processing and embeddings** to **vector search and LLM-based analysis**.

---

## 📂 Projects

| Project                                      | Description                                             | Main Concepts                                        |
| -------------------------------------------- | ------------------------------------------------------- | ---------------------------------------------------- |
| 🧠 [Mini RAG](./mini-rag-main)               | A lightweight RAG implementation for searching AI notes | Embeddings, Semantic Search, ChromaDB                |
| 📄 [PDF Chatbot RAG](./pdf-chatbot-rag-main) | Chat with a PDF using a manual RAG pipeline             | PDF Processing, Chunking, Embeddings, Vector DB, LLM |
| 📊 [Resume Analyzer](./resume-analzier-main) | AI-powered resume evaluation for a specific job role    | Flask, OpenRouter, ATS Analysis, LLM                 |

---

# 🧠 1. Mini RAG

### What is it?

The **Mini RAG** project demonstrates the fundamental workflow behind Retrieval-Augmented Generation.

Instead of directly asking an AI model to answer a question, the system first searches a knowledge base for relevant information.

### 🔄 Workflow

```text
PDF Document
     ↓
Text Extraction
     ↓
Text Chunking
     ↓
Sentence Embeddings
     ↓
ChromaDB Vector Store
     ↓
User Query
     ↓
Query Embedding
     ↓
Semantic Search
     ↓
Top Relevant Results
```

The implementation extracts text from `documents/ai_notes.pdf`, splits it into chunks, generates embeddings using `all-MiniLM-L6-v2`, and stores those vectors in ChromaDB. User queries are embedded and compared against the stored vectors to retrieve the top three results.

### 🛠️ Technologies

* Python
* PyPDF
* LangChain Text Splitters
* Sentence Transformers
* `all-MiniLM-L6-v2`
* ChromaDB

### ▶️ Run

```bash
cd mini-rag-main

pip install -r requirements.txt

python app.py
```

After the vector database has been created, you can query it using:

```bash
python query.py
```

---

# 📄 2. PDF Chatbot RAG

### What is it?

The **PDF Chatbot RAG** project takes the RAG concept further by creating a complete question-answering pipeline around a PDF document.

Users can ask questions about the contents of the document, and the system retrieves relevant sections before sending the context to an LLM to generate an answer.

### 🔄 RAG Pipeline

```text
                 PDF
                  ↓
            Read Document
                  ↓
            Create Chunks
                  ↓
          Generate Embeddings
                  ↓
             ChromaDB
                  ↓
            User Question
                  ↓
           Semantic Search
                  ↓
        Retrieve Relevant Chunks
                  ↓
            Build Prompt
                  ↓
              LLM
                  ↓
             Final Answer
```

The current implementation explicitly separates the pipeline into PDF reading, chunk creation, embedding generation, ChromaDB storage, semantic search, prompt construction, and answer generation through an OpenRouter-backed LLM.

### 🛠️ Technologies

* Python
* Sentence Transformers
* ChromaDB
* PyPDF2
* PyTorch
* OpenAI-compatible API
* OpenRouter
* python-dotenv

The project's dependency list includes Sentence Transformers, ChromaDB, PyPDF2, PyTorch, python-dotenv and OpenAI.

### ⚙️ Setup

```bash
cd pdf-chatbot-rag-main

python -m venv venv
```

### Windows

```bash
venv\Scripts\activate
```

### Install dependencies

```bash
pip install -r requirements.txt
```

### 🔑 Environment Variables

Create a `.env` file:

```env
OPENROUTER_API_KEY=your_api_key_here
```

### ▶️ Run

Make sure your PDF is available at:

```text
data/sample.pdf
```

Then run:

```bash
python app.py
```

The chatbot will allow you to enter questions interactively.

Type:

```text
exit
```

to stop the application.

---

# 📊 3. AI Resume Analyzer

### What is it?

The **AI Resume Analyzer** is an LLM-powered application that evaluates a resume against a specific target job role.

Instead of simply checking keywords, it generates a structured analysis containing:

* Resume summary quality
* Job-role match score
* Key strengths
* Weak areas
* Improvement suggestions
* Suggested projects
* Improved resume version
* Interview questions

The backend is implemented using Flask and communicates with OpenRouter through an OpenAI-compatible client.

### 🔄 Workflow

```text
             User
               ↓
        Resume + Job Role
               ↓
          Flask API
               ↓
       Resume Analysis Prompt
               ↓
           OpenRouter
               ↓
            LLM
               ↓
      Structured Evaluation
               ↓
             User
```

### 🛠️ Technologies

* Python
* Flask
* Flask-CORS
* OpenRouter
* OpenAI Python SDK
* HTML / CSS / JavaScript

### 🔑 Environment Setup

Create a `.env` file inside:

```text
resume-analzier-main/
```

Add:

```env
OPENROUTER_API_KEY=your_api_key_here
```

### ▶️ Run Backend

```bash
cd resume-analzier-main

pip install -r requirements.txt

python resume_api.py
```

The API runs on:

```text
http://localhost:8000
```

### API Endpoint

```http
POST /analyze
```

Example request:

```json
{
  "resume": "Your resume text here",
  "role": "Software Engineer"
}
```

Example response:

```json
{
  "result": "Resume analysis generated by the AI model..."
}
```

The backend validates both the resume text and target role before sending the request to the LLM.

---

# 🏗️ Repository Structure

```text
AI-WORKSHOP/
│
├── mini-rag-main/
│   ├── documents/
│   │   └── ai_notes.pdf
│   ├── app.py
│   ├── query.py
│   ├── requirements.txt
│   └── .gitignore
│
├── pdf-chatbot-rag-main/
│   ├── data/
│   │   └── sample.pdf
│   ├── utils/
│   │   ├── pdf_reader.py
│   │   ├── chunking.py
│   │   ├── embeddings.py
│   │   ├── vector_db.py
│   │   ├── retriever.py
│   │   ├── prompt_builder.py
│   │   └── openrouter_llm.py
│   ├── app.py
│   ├── config.py
│   ├── requirements.txt
│   └── README.md
│
└── resume-analzier-main/
    ├── index.html
    ├── resume_api.py
    ├── requirements.txt
    └── .gitignore
```

---

# 🧩 Key AI Concepts Demonstrated

### 1. Embeddings

Convert text into numerical vector representations so that semantically similar content can be compared.

### 2. Semantic Search

Instead of matching exact keywords, the system searches for content based on semantic similarity.

### 3. Vector Database

ChromaDB stores and retrieves vector representations of documents.

### 4. Retrieval-Augmented Generation

RAG combines:

```text
Retrieval + Context + Generation
```

This allows an LLM to generate responses using information retrieved from an external knowledge base.

### 5. Prompt Engineering

The projects demonstrate how retrieved information and user inputs can be structured into prompts for an LLM.

### 6. LLM APIs

The Resume Analyzer and PDF Chatbot demonstrate integrating applications with an external LLM service through OpenRouter.

---

# 🔐 Security

**Never commit API keys to GitHub.**

Use environment variables:

```env
OPENROUTER_API_KEY=your_api_key_here
```

Make sure `.env` is included in `.gitignore`:

```gitignore
.env
```

If an API key is accidentally pushed to GitHub, revoke it immediately and generate a new one.

---

# 🎯 Learning Objectives

By working through these projects, you can understand:

* How RAG works internally
* How documents are processed
* How text chunking works
* How embeddings represent meaning
* How vector databases work
* How semantic retrieval works
* How retrieved context is passed to an LLM
* How to build LLM-powered APIs
* How AI can be applied to real-world applications

---

# 🔮 Future Enhancements

Possible improvements include:

* [ ] Support multiple PDF uploads
* [ ] Add a web-based interface to the RAG projects
* [ ] Add conversation history
* [ ] Add streaming LLM responses
* [ ] Add document metadata filtering
* [ ] Add configurable chunk sizes
* [ ] Add multiple embedding models
* [ ] Add citation/source references to RAG answers
* [ ] Add resume PDF upload
* [ ] Add ATS keyword analysis
* [ ] Add resume-to-job-description comparison
* [ ] Add downloadable improved resumes
* [ ] Deploy applications using cloud platforms

---

# 📚 What This Repository Covers

```text
                 AI WORKSHOP
                      │
          ┌───────────┴───────────┐
          │                       │
        RAG                    LLM Apps
          │                       │
     ┌────┴────┐             ┌────┴────┐
     │         │             │         │
  Mini RAG  PDF Chatbot   Resume    Analysis
     │         │           Analyzer
     │         │             │
 Embeddings  Retrieval     Flask API
 ChromaDB    ChromaDB      OpenRouter
```

---

# 👨‍💻 Author

**Bobby**

GitHub: [@bobby720](https://github.com/bobby720)

---

# ⭐ Support

If you found these projects useful, consider giving the repository a ⭐ on GitHub.

---

## 📜 License

This repository is intended for educational and experimental purposes.
