# RAG Pipeline for EHR Documents

A complete Retrieval-Augmented Generation (RAG) pipeline for processing Electronic Health Record (EHR) documents using multiple vector databases and embedding strategies.

## Features

- **Document Ingestion**: Upload and process Markdown EHR files (patient demographics, medical history, vitals, labs)
- **Three Chunking Strategies**: Fixed-size, sliding window, semantic chunking
- **Multi-Embedding Support**: gte-Qwen2-1.5B, e5-large-v2, bge-m3 models
- **Vector Database Integration**: Chroma Cloud, Pinecone, Weaviate Cloud
- **LLM Generation**: Groq API with context-bound prompting

## Pipeline Overview

## Quick Start

1. **Set Environment Variables**
```bash
export CHROMA_API_KEY="your_key"
export PINECONE_API_KEY="your_key"
export WEAVIATE_URL="your_url"
export WEAVIATE_API_KEY="your_key"
export GROQ_API_KEY="your_key"
```

2. **Process Documents**
## Run data pipeline first
jupyter notebook datapipeline.ipynb
Upload ehr1.md or similar patient records

3. **Generate Insights**
## Query patient records
jupyter notebook genaration.ipynb

## File Structure

├── datapipeline.ipynb # Document processing + vector storage  
├── genaration.ipynb   # Retrieval + LLM generation  
├── ehr1.md           # Sample: Jane Doe patient record  
└── README.md          # This file  

## Technical Stack
| Component  | Technology                                      |
| ---------- | ----------------------------------------------- |
| Framework  | LangChain + LangChain Community                 |
| Chunking   | RecursiveCharacterTextSplitter, SemanticChunker |
| Embeddings | HuggingFace (gte-Qwen2, e5-large, bge-m3)       |
| Vector DBs | Chroma Cloud, Pinecone, Weaviate                |
| LLM        | Groq API (gpt-oss-120b)                         |

## Example Patient Data
Jane A. Doe (processed sample):

Age: 43, Hypertension, Hyperlipidemia

Current: Acute migraine (Jan 21, 2026)

Meds: Lisinopril 10mg, Atorvastatin 20mg, Sumatriptan PRN

Vitals: BP 122/74, HR 72, BMI 25.0

## Chunking Comparison
| Method   | Chunks | Strategy                               |
| -------- | ------ | -------------------------------------- |
| Fixed    | 38     | chunk_size=100, overlap=0              |
| Sliding  | 40     | chunk_size=100, overlap=20             |
| Semantic | 3      | sentence-transformers/all-MiniLM-L6-v2 |

## Usage Example

### After running notebooks, query like:
### "What medications is Jane Doe taking?"
### "Show Jane Doe's latest vitals from Jan 2026"

### Response uses ONLY retrieved context (no hallucinations)
"Lisinopril 10mg daily, Atorvastatin 20mg daily, Sumatriptan 50mg PRN"

## Prerequisites
Python 3.12+
Jupyter/Colab environment
Vector DB accounts (Chroma/Pinecone/Weaviate)
Groq API key

## Installation
pip install -r requirements.txt  # Auto-generated from notebooks
### Includes: langchain, chromadb, pinecone-client, weaviate-client, sentence-transformers

## Contributing
Fork the repo
Add new embedding models or vector stores
Update both notebooks
Submit PR with notebook outputs

##License
MIT License - see **LICENSE** file.
