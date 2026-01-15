📄 PDF Assistant (RAG-based CLI App)

A command-line PDF Assistant that ingests a PDF from a URL, stores its embeddings in a PostgreSQL + pgvector database, and allows interactive question answering using a Retrieval-Augmented Generation (RAG) pipeline.

The assistant:

Uses OpenAI embeddings for document indexing

Uses Groq LLM for fast inference

Persists conversation state in PostgreSQL

Runs as an interactive CLI application

🧠 Architecture Overview

PDF Ingestion: Downloads and chunks a PDF from a URL

Embeddings: OpenAI text-embedding-3-small

Vector Store: PostgreSQL with pgvector

LLM: Groq (llama-3.1-70b-versatile)

State Storage: PostgreSQL (assistant runs & history)

Interface: Typer-based CLI

📁 Project Structure
pdf_assistant/
│
├── pdf_assistant.py
├── .env
├── .venv/
└── README.md

⚙️ Prerequisites

Python 3.10+

PostgreSQL with pgvector extension enabled

OpenAI API key (for embeddings)

Groq API key (for LLM)

🧪 Database Setup

Create a PostgreSQL database and enable pgvector:

CREATE DATABASE ai;
\c ai
CREATE EXTENSION IF NOT EXISTS vector;


Update the connection string in the code if needed:

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"

🔐 Environment Variables

Create a .env file in the project root:

OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxxxxxxxxxx
GROQ_API_KEY=gsk_xxxxxxxxxxxxxxxxxxxxxxxx


Make sure .env is in the same directory as pdf_assistant.py.

📦 Installation

Activate your virtual environment and install dependencies:

pip install typer python-dotenv
pip install phi sentence-transformers psycopg[binary]
pip install openai

▶️ Running the Assistant

Start the CLI assistant:

python pdf_assistant.py


On first run:

The PDF is downloaded

It is chunked and embedded

Embeddings are stored in pgvector

You will then enter an interactive chat session.

💬 Example Questions
How do I make green curry?
What ingredients are used in Thai red curry?
Explain the steps for Pad Thai.


The assistant answers strictly based on the PDF content.

🔁 Run Persistence

Conversations are stored in PostgreSQL

Re-running the script continues the last session

Start a fresh run with:

python pdf_assistant.py --new

🚨 Common Issues
OpenAI quota error

If you see:

insufficient_quota


Your OpenAI account has no remaining embedding quota.
Either:

Enable billing on OpenAI

Or switch to local embeddings (HuggingFace)

🚀 Future Improvements

Support multiple PDFs

Add page-level citations

Switch to FastAPI / Web UI

Add local embeddings by default

Add evaluation & logging
