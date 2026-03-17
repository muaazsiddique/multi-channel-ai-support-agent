# 🤖 Multi-Channel AI Customer Support Agent

[![Make.com](https://img.shields.io/badge/Make.com-Automation-6D3EEF.svg)](https://make.com)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4o--mini-412991.svg)](https://openai.com)
[![Pinecone](https://img.shields.io/badge/Pinecone-Vector_DB-000000.svg)](https://pinecone.io)
[![Google Sheets](https://img.shields.io/badge/Google_Sheets-CRM-34A853.svg)](https://sheets.google.com)
[![Slack](https://img.shields.io/badge/Slack-Notifications-4A154B.svg)](https://slack.com)
[![Gmail](https://img.shields.io/badge/Gmail-Email_Channel-EA4335.svg)](https://gmail.com)

> **An AI-powered customer support system that handles email, web chat, and WhatsApp inquiries using RAG (Retrieval-Augmented Generation). Answers customer questions from your company's knowledge base — in any language — with automatic ticket logging and smart escalation.**

---

## 🎯 What This Does

Most businesses spend $2,000–$4,000/month on support staff answering the same questions over and over. This system automates 80%+ of those responses using AI that pulls answers from your real company data — not generic ChatGPT guesses.

**A customer sends a message → AI detects their language → searches your knowledge base → generates an accurate response → replies automatically → logs the ticket → notifies your team if escalation is needed. All in under 5 seconds.**

### Key Features

- 🌐 **Multi-Channel Support** — Email (Gmail), website chat (webhook), with WhatsApp-ready architecture
- 🧠 **RAG-Powered Responses** — AI answers from YOUR company data, not imagination. No hallucination.
- 🌍 **Multi-Language** — Auto-detects customer language and responds in the same language (tested: English, Spanish)
- 🏷️ **Smart Classification** — Every message classified by intent (FAQ, billing, technical, complaint) and urgency (low, medium, high)
- 📊 **Ticket Tracking** — Every interaction logged in Google Sheets with full details
- 🔔 **Team Notifications** — Slack alerts for all tickets with customer details and AI response
- 📈 **Daily Reports** — Automated daily summary of support activity sent to Slack
- ⚡ **Instant Responses** — Web chat responses delivered in 3-5 seconds

---

## 🏗️ Architecture

```
                                    ┌─────────────────────┐
                                    │   Knowledge Base     │
                                    │   (Pinecone DB)      │
                                    └─────────┬───────────┘
                                              │
┌──────────────┐                    ┌─────────▼───────────┐
│  Email        │───────────────────▶│                     │
│  (Gmail)      │                    │    AI RAG Engine     │
├──────────────┤                    │                     │
│  Web Chat     │───────────────────▶│  1. Classify intent  │
│  (Webhook)    │                    │  2. Create embedding │──────▶ Google Sheets
├──────────────┤                    │  3. Search Pinecone  │       (Ticket Log)
│  WhatsApp     │───────────────────▶│  4. Generate reply   │
│  (Future)     │                    │                     │──────▶ Slack
└──────────────┘                    └─────────────────────┘       (Notifications)
```

---

## 📁 Workflows

| # | Workflow | Description | Status |
|---|---------|-------------|--------|
| 1 | **KB Ingestion** | Feeds FAQ/docs into Pinecone vector database via OpenAI embeddings | ✅ Complete |
| 2 | **AI Brain (RAG Engine)** | Standalone RAG engine — classify, embed, search, generate response | ✅ Complete |
| 3 | **Email Support Channel** | Gmail trigger → AI processing → auto-reply → ticket log → Slack | ✅ Complete |
| 4 | **Web Chat Channel** | Webhook → AI processing → instant response → ticket log → Slack | ✅ Complete |
| 5 | **Smart Escalation** | Conditional routing based on urgency/intent (customizable per client) | 🔧 Configurable |
| 6 | **Daily Summary Report** | Scheduled daily report of ticket metrics to Slack | ✅ Complete |

---

## 🛠️ Tech Stack

### Workflow Automation
- **Make.com** — Primary automation platform with 5 production scenarios

### AI & Machine Learning
- **OpenAI GPT-4o-mini** — Intent classification, language detection, response generation
- **OpenAI text-embedding-ada-002** — Vector embeddings for semantic search (1,536 dimensions)

### Vector Database
- **Pinecone** — Vector similarity search with cosine metric, namespace isolation

### Communication & Data
- **Gmail API** — Email support channel with auto-reply
- **Slack API** — Team notifications and daily reports
- **Google Sheets** — Ticket tracking CRM with 13-column schema
- **Webhooks** — Real-time web chat integration

---

## 📊 How RAG Works in This System

Traditional chatbots guess answers. Our system **retrieves** real information first, then **generates** a response based on facts.

```
Customer: "How long does shipping take?"
                    │
                    ▼
        ┌───────────────────┐
        │ Convert question   │
        │ to 1,536 numbers   │  ← OpenAI Embeddings
        │ (vector embedding) │
        └─────────┬─────────┘
                  │
                  ▼
        ┌───────────────────┐
        │ Search Pinecone    │
        │ for most similar   │  ← Cosine similarity
        │ FAQ chunk          │
        └─────────┬─────────┘
                  │
                  ▼
        ┌───────────────────┐
        │ Found: "Standard   │
        │ shipping 5-7 days, │  ← Real company data
        │ express 2-3 days"  │
        └─────────┬─────────┘
                  │
                  ▼
        ┌───────────────────┐
        │ Generate natural   │
        │ response using     │  ← OpenAI GPT-4o-mini
        │ retrieved context  │
        └─────────┬─────────┘
                  │
                  ▼
AI Response: "Standard shipping takes 5-7 business days.
If you need it sooner, we offer express shipping
(2-3 days) for $12.99."
```

**Result:** Accurate, grounded responses. No hallucination. No made-up information.

---

## 🌍 Multi-Language Support

The system auto-detects the customer's language and responds accordingly.

| Customer Message | Language | AI Response |
|---|---|---|
| "How long does shipping take?" | English | "Standard shipping takes 5-7 business days..." |
| "Cuanto tiempo tarda el envio?" | Spanish | "El envío estándar tarda de 5 a 7 días hábiles..." |
| "Quelle est votre politique de retour?" | French | "Notre politique permet les retours dans les 30 jours..." |

---

## 📋 Ticket Tracking Schema

Every customer interaction is logged in Google Sheets with these fields:

| Field | Description |
|---|---|
| Ticket ID | Unique identifier (TKT-20260316143022) |
| Timestamp | When the message was received |
| Channel | email, web-chat, or whatsapp |
| Customer Email | Customer's email address |
| Original Language | Detected language of the message |
| Customer Message | The original question |
| English Translation | Translated version (if not English) |
| Intent Category | FAQ, billing, technical, complaint, escalation |
| Urgency | low, medium, high |
| AI Response Sent | The auto-generated response |
| Status | Auto-Resolved, Escalated, Closed |
| Escalated to Human | Yes/No |
| Resolution Notes | How the ticket was handled |

---

## 🚀 Quick Start

### Prerequisites
- Make.com account (Core plan or higher)
- OpenAI API key
- Pinecone account (free tier works)
- Google account (for Sheets + Gmail)
- Slack workspace

### Setup

1. **Clone this repository**
```bash
git clone https://github.com/muaazsiddique/multi-channel-ai-support-agent.git
```

2. **Create Pinecone Index**
   - Index name: `support-knowledge-base`
   - Dimensions: `1536`
   - Metric: `cosine`

3. **Set up Google Sheet**
   - Create a spreadsheet named "AI Support Agent - Ticket Tracker"
   - Add the 13 columns listed in the Ticket Tracking Schema above

4. **Create Slack Channels**
   - `#support-escalations` — for ticket notifications
   - `#support-daily-report` — for daily summaries

5. **Import Make.com Scenarios**
   - Download the JSON files from the `workflows/` folder
   - In Make.com: Scenarios → Import Blueprint → upload each file
   - Configure credentials (OpenAI, Pinecone, Google, Slack) in each scenario

6. **Ingest Your Knowledge Base**
   - Trigger the KB Ingestion webhook with your FAQ data
   - See `docs/workflow-1-kb-ingestion.md` for the exact JSON format

7. **Test**
   - Send a test email to your Gmail
   - Send a POST request to the web chat webhook
   - Verify responses, Google Sheets logging, and Slack notifications

---

## 📁 Project Structure

```
multi-channel-ai-support-agent/
├── workflows/                          # Make.com scenario blueprints
│   ├── kb-ingestion-faq-to-pinecone.json
│   ├── ai-brain-rag-support-engine.json
│   ├── email-support-channel.json
│   ├── web-chat-support-channel.json
│   └── daily-support-summary.json
├── docs/                               # Setup and architecture docs
│   ├── workflow-1-kb-ingestion.md
│   ├── workflow-2-ai-brain.md
│   ├── workflow-3-email-channel.md
│   ├── workflow-4-web-chat.md
│   ├── workflow-6-daily-summary.md
│   ├── google-sheets-setup.md
│   ├── slack-setup.md
│   ├── pinecone-setup.md
│   └── platform-setup.md
├── knowledge-base/                     # Sample FAQ for testing
│   └── sample-faq.md
├── assets/                             # Screenshots and demos
├── .env.example                        # Required environment variables
├── .gitignore
├── LICENSE
└── README.md
```

---

## 💰 Business Impact

| Metric | Traditional Support | This AI System |
|---|---|---|
| **Monthly Cost** | $2,000–$4,000 (employee) | $5–$20 (API costs) |
| **Response Time** | Minutes to hours | 3–5 seconds |
| **Availability** | Business hours only | 24/7/365 |
| **Languages** | Limited by staff | 50+ languages |
| **Scalability** | Hire more people | Handles unlimited volume |
| **Setup Cost** | Ongoing salary | One-time build ($500–$2,000) |

---

## 🔧 Customization

This system is designed to be easily customized for any business:

- **Knowledge Base:** Replace `sample-faq.md` with your own FAQ, policies, or documentation
- **Channels:** Add WhatsApp, Telegram, or any webhook-compatible platform
- **Escalation Rules:** Configure urgency thresholds and routing rules per client needs
- **Branding:** Customize AI response tone and style via the system prompt
- **Languages:** Works with any language supported by OpenAI (50+)

---

## 🙋‍♂️ About the Developer

**Muaaz Siddique** — AI Automation Specialist

- 🤖 **Expertise:** AI workflow automation, RAG systems, business process automation
- 🔧 **Tools:** Make.com, n8n, OpenAI, Pinecone, LangChain
- 💼 **Upwork:** Available for custom automation projects
- 📧 **Email:** muaazsiddique97@gmail.com
- 🔗 **GitHub:** [@muaazsiddique](https://github.com/muaazsiddique)

---

**⭐ If this project is useful, please give it a star!**

*Need a custom AI support system for your business? Let's connect and discuss your needs.*
