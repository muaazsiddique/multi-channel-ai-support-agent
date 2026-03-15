# Workflow 2: AI Brain - RAG Support Engine

## Purpose
Core AI engine that receives customer questions, searches the knowledge base, and generates accurate responses in the customer's language.

## How It Works
1. Webhook receives customer message (email, channel, message text)
2. OpenAI GPT-4o-mini classifies: language, English translation, intent category, urgency
3. OpenAI Embeddings API converts question to 1,536-dimension vector
4. HTTP module queries Pinecone for top 3 most similar FAQ chunks
5. OpenAI GPT-4o-mini generates a response using the retrieved FAQ context, in the customer's language

## Architecture
[Webhook] → [OpenAI Classify] → [OpenAI Embedding] → [Pinecone Query] → [OpenAI Generate Response]

## Tech Stack
- Make.com (workflow orchestration)
- OpenAI GPT-4o-mini (classification + response generation)
- OpenAI text-embedding-ada-002 (vector embeddings)
- Pinecone (vector similarity search)
- HTTP module (direct API integration)

## Key Features
- Multi-language support (auto-detects and responds in customer's language)
- Intent classification (FAQ, billing, technical, complaint, escalation)
- Urgency scoring (low, medium, high)
- RAG-powered responses (answers come from real company data, not AI imagination)
- Top 3 knowledge base matches for comprehensive context

## Trigger
POST request to webhook URL with JSON body:
{
  "customer_email": "customer@example.com",
  "message": "Customer question here",
  "channel": "web-chat"
}

## Tested Scenarios
- English shipping question → correct English response
- English returns question → correct English response
- Spanish shipping question → correct Spanish response