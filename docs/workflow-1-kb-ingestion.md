# Workflow 1: Knowledge Base Ingestion

## Purpose
Ingests FAQ/knowledge base documents into Pinecone vector database for RAG-powered customer support.

## How It Works
1. Webhook receives FAQ chunks (id + text) as JSON array
2. Iterator processes each chunk one by one
3. OpenAI API creates vector embedding (1,536 dimensions) for each chunk
4. HTTP module upserts each vector + metadata into Pinecone

## Architecture
[Webhook Trigger] → [Iterator] → [OpenAI Embeddings API] → [Pinecone Upsert API]

## Tech Stack
- Make.com (workflow orchestration)
- OpenAI text-embedding-ada-002 (vector embeddings)
- Pinecone (vector database, cosine similarity, 1536 dimensions)
- HTTP module for direct API integration

## Configuration
- Pinecone Index: support-knowledge-base
- Pinecone Namespace: faq
- Embedding Model: text-embedding-ada-002
- Dimensions: 1536
- Metric: cosine

## Trigger
POST request to webhook URL with JSON body:
{
  "chunks": [
    {"id": "unique-id", "text": "FAQ content here"},
    {"id": "unique-id-2", "text": "More FAQ content"}
  ]
}

## Notes
- Pinecone upsert uses HTTP module for full embedding array support
- Each chunk stores original text as metadata for retrieval during queries
- Re-running with same IDs overwrites existing vectors (safe to re-ingest)