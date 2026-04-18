# NEWS-MLOPS: Retrieval-Augmented News Query System

## Overview
NEWS-MLOPS is an end-to-end MLOps pipeline that implements a Retrieval-Augmented Generation (RAG) system for financial news intelligence.

The system generates news data, preprocesses it, stores it in a database, creates embeddings, and retrieves relevant information to generate contextual answers using a FastAPI backend and an optional Gradio interface.

The project demonstrates a production-oriented pipeline including data ingestion, feature engineering, vector storage, retrieval, deployment, monitoring, and automation.

## Key Features
- Programmatic data generation
- Data ingestion and preprocessing
- Embedding-based feature engineering (Sentence Transformers)
- Vector database using ChromaDB
- Retrieval-Augmented Generation (RAG)
- FastAPI backend (`/ask` endpoint)
- Gradio UI for interaction
- Logging and artifact tracking
- GitHub Actions automation
- Docker-ready setup


## Repository Structure
NEWS-MLOPS/
│
├── app_fastapi.py # FastAPI backend
├── rag.py # Gradio UI
├── create_data.py # Data generation
├── ingest_data.py # Data ingestion (JSON → SQLite)
├── vector_db.py # Embedding + ChromaDB creation
├── vectordb_query.py # Query + LLM response
├── search.py # Vector search utility
│
├── requirements.txt
├── Dockerfile
│
├── .devcontainer/
│
├── artifacts/
│ └── logs.txt
│
└── chroma_db/

## Pipeline Architecture

Data Generation (create_data.py)
↓
Data Ingestion (ingest_data.py)
↓
Embedding Generation (vector_db.py)
↓
ChromaDB (Vector Store)
↓
User Query (API / UI)
↓
Retriever
↓
RAG + LLM (Groq API)
↓
Response via FastAPI
↓
Optional Gradio UI

## How to Run (Local)

### 1. Install dependencies
pip install -r requirements.txt
2. Generate data
python create_data.py
3. Ingest data
python ingest_data.py
4. Build vector database
python vector_db.py
5. Start backend
uvicorn app_fastapi:app --host 0.0.0.0 --port 8000

API Docs:

http://localhost:8000/docs
Gradio UI (Frontend)

Run:

python rag.py

Access:

http://localhost:7860
API Usage
Endpoint
POST /ask
Example Request
{
  "query": "What is happening in global markets?"
}
Automation (GitHub Actions)

The pipeline is automated using GitHub Actions:

Runs every 2 hours
Can be triggered manually
Executes full pipeline:
Data generation
Data ingestion
Vector database update

Workflow:

.github/workflows/schedule.yml

Artifacts

Stored in:

artifacts/logs.txt
chroma_db/

Includes:

Logs for ingestion, API, retrieval
Persisted vector database
Monitoring

The system logs:

Data ingestion
Embedding creation
API requests
Retrieval results
Deployment
Docker (Optional)

Build:

docker build -t news-mlops .

Run:

docker run -p 8000:8000 news-mlops

Reproducibility

The project ensures reproducibility through:

Fixed dependencies (requirements.txt)
Devcontainer environment
Automated workflows (GitHub Actions)
Persisted vector database
Structured pipeline design
Important Note

The API and UI run as services and must be started manually.

GitHub Actions automates the pipeline but does not host a live API.

Author

Riya Pokharel
Sristi Kulung Rai

MSc BDS – Data Engineering and Machine Learning Operations in Business
