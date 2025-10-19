Here is a README file and a Graphviz diagram for your project.

KnowDIY: A RAG Chatbot for DIY Projects
This project implements a complete Retrieval-Augmented Generation (RAG) pipeline to create a chatbot that answers questions based on a DIY (Do-It-Yourself) book. The system uses a sophisticated stack including a local vector database (Qdrant), a powerful embedding model (IBM Granite), a cross-encoder for reranking, and a quantized LLM (Gemma 3) for generation.

The entire pipeline is wrapped in a simple Gradio web interface for easy interaction.

🚀 Features
End-to-End RAG: Implements the full RAG workflow: Ingestion, Indexing, Retrieval, Reranking, and Generation.

High-Quality Embeddings: Uses ibm-granite/granite-embedding-english-r2 for accurately converting text chunks into vector representations.

Relevance-First Reranking: Employs ibm-granite/granite-embedding-reranker-english-r2 to re-sort the retrieved chunks, ensuring the most relevant information is passed to the LLM.

Efficient Local LLM: Runs the google/gemma-3-4b-it-qat-q4_0-gguf quantized model locally using llama-cpp-python for fast, private inference.

Persistent Vector Store: Uses Qdrant to create and store the vector index locally in the /kaggle/working/vectordb directory.

Smart PDF Parsing: Intelligently splits the source PDF by "topic" using regex before chunking, preserving semantic context.


🛠 Tech Stack
Component,Technology,Purpose,Version/Notes
PDF Parsing,PyMuPDF (fitz),Extract text and structure from PDF,Latest stable
Text Chunking,LangChain,Split documents into semantic chunks,langchain + langchain_huggingface
Embeddings,SentenceTransformers (IBM Granite),Generate dense vectors for text,granite-embedding-english-r2 (dim: 768)
Reranking,CrossEncoder (IBM Granite),Reorder results by relevance,granite-embedding-reranker-english-r2
Vector DB,Qdrant,Store and query embeddings,Local file-based instance
LLM Inference,Llama.cpp + Gemma-3,Generate responses,gemma-3-4b-it-q4_0.gguf (quantized)

📁 Code Structure
The project is organized into several key classes and functions:

EmbeddingManager: A wrapper class to load and manage the SentenceTransformer embedding model.

PreprocessPdf: Handles loading the PDF, splitting it into topics using regex, and then chunking the text using RecursiveCharacterTextSplitter.

VectorStore: Manages the Qdrant client. It handles creating the collection, generating embeddings (using EmbeddingManager), and upserting the documents (chunks) into the vector store.

Retriever: A simple class to perform semantic search. It takes a query, embeds it, and queries the Qdrant database to find the top_k most similar chunks.

ReRanker: A wrapper class to load the CrossEncoder model. It takes the user's query and the list of retrieved passages and re-sorts them based on a more accurate relevance score.

chatbot(user_query): The main orchestration function. It executes the RAG pipeline:

Calls retriever.retrieve() to get initial chunks.

Calls reranker.rerank() to get the most relevant chunks.

Formats the PROMPT_TEMPLATE with the reranked context.

Calls the llm.create_chat_completion() with the prompt and user query.

Streams the generated response.

📊 Project Workflow

