NEWS‑MLOPS: Retrieval‑Augmented News Query System
Overview
NEWS‑MLOPS is an end‑to‑end MLOps pipeline implementing a Retrieval‑Augmented Generation (RAG) system for news intelligence.
The system programmatically generates news data, preprocesses it, embeds it using Sentence Transformers, stores embeddings in ChromaDB, retrieves relevant documents, and produces contextual answers through a FastAPI backend and an optional Gradio UI.

The project demonstrates a production‑oriented workflow including ingestion, feature engineering, vector storage, retrieval, deployment, monitoring, reproducibility, and automation.

Key Features
Programmatic news data generation

Data ingestion and preprocessing

Embedding‑based feature engineering

Vector database using ChromaDB

Retrieval‑Augmented Generation (RAG) pipeline

FastAPI backend with /ask endpoint

Optional Gradio UI for user interaction

Logging and artifact tracking

Dockerized deployment

Automated pipeline execution via GitHub Actions

Repository Structure

NEWS-MLOPS/
│
├── app_fastapi.py          # FastAPI backend (RAG API)
├── rag.py                  # Gradio UI (frontend)
├── create_data.py          # Synthetic news data generator
├── ingest_data.py          # Preprocessing and ingestion
├── vector_db.py            # Embedding generation + ChromaDB creation
├── vectordb_query.py       # Retriever logic
├── search.py               # Utility search functions
│
├── requirements.txt        # Dependencies
├── Dockerfile              # Backend Docker image
│
├── .devcontainer/          # Devcontainer setup for Codespaces
│   ├── devcontainer.json
│   └── Dockerfile
│
├── artifacts/
│   └── logs.txt            # System logs
│
└── chroma_db/              # Persisted vector database

Devcontainer Environment (Codespaces Support)
This project includes a .devcontainer setup to ensure a fully reproducible development environment.

What the devcontainer provides
Automatic installation of Python and dependencies

Preconfigured environment for FastAPI, ChromaDB, and Gradio

Consistent environment across machines

One‑click startup in GitHub Codespaces

Eliminates “works on my machine” issues

How to use it
Open the repository in GitHub

Click Code → Codespaces → Create Codespace

The devcontainer automatically builds the environment

You can immediately run:
Code
uvicorn app_fastapi:app --reload
python rag.py

Pipeline Architecture
Data Generation (create_data.py)
        ↓
Data Ingestion & Preprocessing (ingest_data.py)
        ↓
Embedding Generation (vector_db.py)
        ↓
ChromaDB Vector Store (chroma_db/)
        ↓
User Query (API or UI)
        ↓
Retriever (vectordb_query.py)
        ↓
Context Builder + RAG Logic (app_fastapi.py)
        ↓
LLM Response
        ↓
FastAPI Endpoint (/ask)
        ↓
 Gradio UI (rag.py)

 How to Run Locally
1. Install dependencies
bash
pip install -r requirements.txt
2. Generate synthetic news data
bash
python create_data.py
3. Build the vector database
bash
python vector_db.py
4. Start the FastAPI backend
bash
uvicorn app_fastapi:app --host 0.0.0.0 --port 8000
API documentation is available at:

Code
http://localhost:8000/docs
Gradio User Interface (Frontend)
The project includes a simple Gradio UI for interacting with the RAG system without using API tools.

Run the UI
Ensure the backend is running, then:

bash
python rag.py
The UI will be available at:

Code
http://localhost:7860
UI → Backend Interaction
Code
Gradio UI (rag.py)
        ↓ POST /ask
FastAPI Backend (app_fastapi.py)
        ↓
Retriever + RAG Pipeline
        ↓
Generated Answer
Running with Docker
Build the image
bash
docker build -t news-mlops .
Run the container
bash
docker run -p 8000:8000 news-mlops
API docs:

Code
http://localhost:8000/docs
API Usage
Endpoint
Code
POST /ask
Example Request
json
{
  "query": "What is happening in global markets?"
}
Response
Returns a generated answer based on retrieved news context.

Pipeline Automation (GitHub Actions)
The pipeline is automated using GitHub Actions to ensure continuous updates:

Scheduled runs

Automatic data regeneration

Automatic embedding + vector DB refresh

Optional manual triggers

This ensures reproducibility and reduces manual workload.

Artifacts
Artifacts are stored in the artifacts/ directory:

logs.txt — ingestion, retrieval, and API logs

chroma_db/ — persisted vector database

These support debugging, monitoring, and reproducibility.

Monitoring
The system logs:

Data ingestion events

Vector DB creation

API requests

Retrieval results

UI interactions

Logs are stored in:

Code
artifacts/logs.txt
Reproducibility
Reproducibility is ensured through:

Deterministic data generation

Fixed dependencies (requirements.txt)

Docker containerization

Devcontainer environment for consistent development

Automated GitHub Actions workflows

Persisted vector database

Author
Riya Pokharel
Sristi Kulung Rai
MSc BDS – Data Engineering and Machine Learning Operations in Business

License
This project is submitted as part of the MLOps exam assignment.
