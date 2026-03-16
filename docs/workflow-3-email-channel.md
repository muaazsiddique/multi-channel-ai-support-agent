# Workflow 3: Email Support Channel

## Purpose
Watches Gmail for incoming customer support emails, processes them through the AI RAG engine, auto-replies to customers, logs tickets in Google Sheets, and sends notifications to Slack.

## How It Works
1. Gmail trigger detects new incoming email
2. Set Variable cleans the email text (removes formatting characters)
3. OpenAI classifies: language, intent, urgency
4. OpenAI creates embedding of the question
5. Pinecone searches knowledge base for best matching FAQ
6. OpenAI generates a response using the FAQ context in the customers language
7. Gmail sends auto-reply to the customer
8. Google Sheets logs the full ticket
9. Slack receives notification with ticket details

## Architecture
[Gmail Watch] → [Clean Text] → [Classify] → [Embed] → [Pinecone Search] → [Generate Reply] → [Gmail Reply] → [Google Sheets Log] → [Slack Notify]

## Tech Stack
- Make.com (workflow orchestration)
- Gmail (email trigger + auto-reply)
- OpenAI GPT-4o-mini (classification + response generation)
- OpenAI text-embedding-ada-002 (embeddings)
- Pinecone (vector search)
- Google Sheets (ticket tracking)
- Slack (team notifications)

## Key Features
- Automatic email detection and processing
- Multi-language support
- RAG-powered accurate responses
- Complete ticket logging
- Team notifications via Slack
- Text cleaning with trim() and stripHTML() for reliable JSON parsing

## Tested
- English shipping question: correct response + auto-reply sent
- Return policy question: correct response + auto-reply sent
- Confirmed: Gmail reply, Google Sheets logging, and Slack notification all working