# DIY Expert Assistant: Retrieval-Augmented Generation (RAG) Chatbot

## Overview

The **DIY Expert Assistant** is a conversational AI tool designed to provide expert guidance on do-it-yourself (DIY) projects, repairs, and home improvements. Built using a Retrieval-Augmented Generation (RAG) architecture, it leverages a custom knowledge base extracted from a DIY book PDF to deliver accurate, step-by-step advice. The system processes user queries (e.g., "How to fix a leaking pipe?" or "What are big weekend DIY projects?") by retrieving relevant content, reranking for precision, and generating clear, helpful responses.

### Key Features
- **PDF Ingestion**: Extracts and organizes content from a PDF using PyMuPDF.
- **Semantic Search**: Uses IBM Granite embeddings for efficient retrieval.
- **Reranking**: Enhances relevance with a Granite cross-encoder.
- **Natural Responses**: Streams answers via Gemma-3 (quantized) using Llama.cpp.
- **Interactive UI**: Gradio-based web interface for real-time chat.
- **Offline Capability**: Runs locally with GPU support for fast inference.

This project is ideal for DIY enthusiasts, developers, or anyone building domain-specific AI assistants. It's optimized for Kaggle but can run locally.

## Architecture

The RAG pipeline consists of:
1. **PDF Processing**: Parse PDF with PyMuPDF; chunk text with LangChain.
2. **Embedding**: Generate vectors using IBM Granite (768-dim).
3. **Vector Store**: Index embeddings in Qdrant for fast retrieval.
4. **Retrieval**: Fetch top-k relevant chunks based on query embeddings.
5. **Reranking**: Reorder chunks using Granite cross-encoder.
6. **Generation**: Prompt Gemma-3 for natural, context-based responses.
7. **UI**: Stream responses via Gradio.

## Tech Stack

| Component | Technology | Purpose |
|-----------|------------|---------|
| PDF Parsing | PyMuPDF (fitz) | Extract text from PDFs |
| Text Chunking | LangChain | Split text into semantic chunks |
| Embeddings | SentenceTransformers (IBM Granite) | Generate dense text embeddings |
| Reranking | CrossEncoder (IBM Granite) | Reorder results by relevance |
| Vector DB | Qdrant | Store and query embeddings |
| LLM | Llama.cpp + Gemma-3 | Generate natural responses |
| UI | Gradio | Interactive web interface |
| Runtime | Python 3.12 + PyTorch | Core environment (CUDA support) |


## Process Flowchart


