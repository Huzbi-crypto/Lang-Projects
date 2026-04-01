# 📖 RAG with LangChain

A Retrieval Augmented Generation (RAG) system using LangChain, OpenAI, and Pinecone.

## Overview

This RAG pipeline includes:
1. **Document Ingestion** - Load, chunk, embed, and storing documents in a vector database
2. **Naive RAG** - A basic retrieval chain using manual function calls
3. **LCEL RAG** - LangChain Expression Language for a cleaner, more powerful approach

## Key Components

### Ingestion (`ingestion.py`)
- **TextLoader**: Load documents from text files
- **CharacterTextSplitter**: Split documents into manageable chunks (1000 chars)
- **OpenAIEmbeddings**: Convert text chunks to vector embeddings
- **PineconeVectorStore**: Store and index vectors for similarity search

### Retrieval (`main.py`)
- **Raw LLM**: Direct query to LLM (no context) - baseline comparison
- **Naive RAG**: Manual retrieval → format → prompt → LLM pipeline
- **LCEL RAG**: Declarative chain using `|` operator with built-in streaming/async

## Setup

1. Install dependencies:
```bash
uv sync
```

2. Set environment variables:
```bash
OPENAI_API_KEY=your_openai_key
PINECONE_API_KEY=your_pinecone_key
INDEX_NAME=your_index_name
```

3. Run ingestion to populate the vector store:
```bash
python ingestion.py
```

4. Run the RAG pipeline:
```bash
python main.py
```

## LCEL Features

| Feature | Naive Approach | LCEL Approach |
|---------|----------------|---------------|
| Code style | Imperative | Declarative |
| Streaming | Manual implementation | Built-in `.stream()` |
| Async | Manual implementation | Built-in `.ainvoke()` |
| Composability | Limited | Pipe operator `\|` |
| Batch processing | Manual loops | Built-in `.batch()` |

## Technologies

- **LangChain** - Framework for building LLM applications
- **OpenAI** - Embeddings and chat completions
- **Pinecone** - Vector database for similarity search
- **Python** - 3.12+
