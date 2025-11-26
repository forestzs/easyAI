
---

## EasyAI Web App（NextAI / easyAI）– README

```markdown
# EasyAI – AI-Powered Document Assistant

EasyAI is a web-based AI document assistant that supports retrieval-augmented question answering over large PDF documents (up to ~50MB). It focuses on fast, relevant responses using vector search, semantic chunking, and optimized backend routing.

## Features

- Upload PDF documents and query them in natural language
- Retrieval-augmented generation (RAG) powered by embeddings and vector search
- Supports large PDFs (up to around 50MB)
- Semantic chunking for improved context retrieval
- >90% of queries respond under 2 seconds under typical load :contentReference[oaicite:8]{index=8}
- Optimized routing and caching to reduce latency and stabilize performance under bursty workloads
- Clean REST endpoints and error handling contracts to support multiple frontends (voice input, conversation history, etc.) :contentReference[oaicite:9]{index=9}

## Tech Stack

**Backend**

- Java (or Node.js/Python depending on your implementation; resume says Java) :contentReference[oaicite:10]{index=10}
- LangChain (for orchestration / RAG pipeline)
- Vector store (e.g., FAISS / Pinecone / other)
- REST API framework (Spring Boot / Express)

**Frontend**

- React (from current repo structure)
- Components:
  - PDF uploader
  - Chat / Q&A interface
  - Rendered Q&A history

**Infrastructure**

- Cloud deployment (e.g., AWS / GCP)
- Caching layer (e.g., in-memory / Redis)
- Logging and monitoring for latency and error tracking

## Architecture Overview

- **Ingestion Pipeline**
  - Accepts PDF uploads via REST API.
  - Splits documents into semantic chunks.
  - Creates embeddings and writes them to a vector store.

- **Query Pipeline**
  - Accepts natural language questions.
  - Retrieves top-N relevant chunks from vector store.
  - Constructs prompts for the LLM and returns the final answer.
  - Tracks latency and hit rates.

- **Caching & Routing**
  - Caching frequently accessed query patterns and retrieval results.
  - Reduced average API latency by ~40% during peak usage and stabilized performance. :contentReference[oaicite:11]{index=11}

- **API Design**
  - Clear endpoints for:
    - `/api/upload` – upload and index PDFs
    - `/api/query` – ask questions about a specific document
    - `/api/history` – (optional) retrieve conversation history

## Getting Started

### Prerequisites

- JDK 17+ (if backend is Java)
- Node.js & npm (for React frontend)
- Access to an LLM provider (e.g., OpenAI)
- Vector store (local or managed)

### Backend Setup

1. Clone the repository:

   ```bash
   git clone https://github.com/<your-username>/easyAI.git
   cd easyAI
