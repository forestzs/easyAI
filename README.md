# EasyAI – Document Q&A Web App

EasyAI is a full-stack web application that lets users upload large PDF documents and ask natural-language questions about them. The app uses retrieval-augmented generation (RAG): it indexes document content into embeddings, performs vector search to find relevant passages, and then calls an LLM to generate concise, context-aware answers.

---

## Features

- Upload large PDF documents through a simple web interface  
- Automatic text extraction and chunking from PDFs  
- Embedding-based vector search over document chunks  
- Retrieval-augmented question answering using an LLM API  
- Chat-style interface that displays both questions and answers  
- Persistent default document so users can try the app without uploading anything  
- Simple Node.js backend API for chat and document handling  

---

## Tech Stack

**Frontend**

- React (Create React App structure)  
- Functional components with hooks  
- Custom components for chat, file upload, and answer rendering  

**Backend**

- Node.js  
- Express.js  
- PDF processing (e.g., pdf-parse or similar library)  
- Embedding + vector search (in-memory or simple store)  
- OpenAI (or compatible) LLM API for answer generation  

---

## Architecture Overview

- **Frontend (React App)**  
  - `App` component manages global layout and routing.  
  - `PdfUploader` handles file selection and upload to the backend.  
  - `ChatComponent` manages user questions, sends them to the server, and renders responses.  
  - `RenderQA` displays question–answer pairs in a clean, readable format.

- **Backend (Express Server)**  
  - `server/server.js`  
    - Main entry point for the Node.js backend.  
    - Exposes REST endpoints for file upload and chat requests.  
  - `server/chat.js`  
    - Core logic for document Q&A.  
    - Handles:
      - Loading the current document (PDF)  
      - Splitting text into chunks  
      - Generating embeddings and building a vector index  
      - Running similarity search to retrieve top-k relevant chunks  
      - Calling the LLM API with retrieved context + user question  
      - Returning the final answer to the frontend  

- **Uploads & Defaults**  
  - `server/uploads/`  
    - Stores uploaded PDFs and sample files (e.g. `your-default-file.pdf`)  
    - May contain additional notes or test documents (kept out of version control in production via `.gitignore`)  

---

## Project Structure

```text
easyAI/
├── README.md
├── package.json          # React frontend package
├── package-lock.json
├── public/
│   ├── index.html
│   └── ...
├── src/
│   ├── App.js
│   ├── App.css
│   ├── index.js
│   ├── components/
│   │   ├── ChatComponent.js
│   │   ├── PdfUploader.js
│   │   └── RenderQA.js
│   └── ...
└── server/
    ├── server.js         # Express server entry
    ├── chat.js           # RAG + LLM logic
    ├── package.json      # Backend dependencies
    ├── package-lock.json
    └── uploads/          # PDF files and default docs
