# 🧠 Enterprise RAG System (LangServe + Gradio)

> A modular, decoupled Retrieval-Augmented Generation (RAG) application built with LangChain, LangServe, FastAPI, and Gradio.

This project implements a "Smart Backend / Orchestrating Frontend" architecture. It allows users to upload PDF documents, live-update a FAISS vector database, and ask context-aware questions powered by Google's Gemini models.



## 🏗️ Architecture Overview

This application is split into two distinct microservices communicating over HTTP:

1. **The Backend (`server.py` & `llm.py`)**: A FastAPI server wrapped with LangServe. It hosts the LLM, the embedding model, and the FAISS vector database. It exposes specific components of the RAG pipeline as isolated REST API endpoints.
2. **The Frontend (`frontend.py`)**: A Gradio web interface. It acts as the orchestrator, using LangServe's `RemoteRunnable` to fetch documents from the backend, reorder them for optimal LLM context retention, and pass them to the generator.

## ✨ Key Features

* **Live Document Ingestion:** Upload PDFs directly through the chat UI to instantly update the AI's knowledge base without restarting the server.
* **LangServe Integration:** Exposes LangChain components (Retriever, Generator, Basic Chat) as standard API routes.
* **Long Context Reordering:** Automatically reorders retrieved documents (putting the most relevant at the top and bottom) to prevent the LLM from "forgetting" information in the middle of the context window.
* **Multimodal UI:** A clean, modern chat interface built with Gradio 6.0.

## ⚙️ Prerequisites

* Python 3.9+
* A Google Gemini API Key

## 🚀 Installation

1. **Clone or create the project folder** containing `server.py`, `llm.py`, and `frontend.py`.
2. **Install the required dependencies:**
   ```bash
   pip install langchain langchain-google-genai langchain-community langserve fastapi uvicorn gradio pypdf faiss-cpu python-multipart requests python-dotenv
