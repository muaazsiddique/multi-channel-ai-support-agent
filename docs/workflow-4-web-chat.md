# Workflow 4: Web Chat Support Channel

## Purpose
Handles customer questions from a website chat widget via webhook, processes through AI RAG engine, returns instant response, logs ticket, and notifies team.

## How It Works
1. Webhook receives customer message from chat widget
2. OpenAI classifies language, intent, urgency
3. OpenAI creates embedding of the question
4. Pinecone searches knowledge base for best matching FAQ
5. OpenAI generates response using FAQ context in customers language
6. Google Sheets logs the ticket
7. Slack notifies the team
8. Webhook response sends AI answer back to chat widget instantly

## Architecture
[Webhook] → [Classify] → [Embed] → [Pinecone Search] → [Generate Reply] → [Google Sheets] → [Slack] → [Webhook Response]

## Tech Stack
- Make.com (workflow orchestration)
- OpenAI GPT-4o-mini (classification + response generation)
- OpenAI text-embedding-ada-002 (embeddings)
- Pinecone (vector search)
- Google Sheets (ticket tracking)
- Slack (team notifications)
- Webhook response (instant reply to chat widget)

## Tested
- Bulk discount question: correct response from knowledge base
- Payment methods question: correct response
- Password reset question: correct response
- Google Sheets logging confirmed
- Slack notifications confirmed
- Webhook response returns AI answer to caller