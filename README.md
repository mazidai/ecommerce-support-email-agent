# E-commerce Customer Support Email Agent

An AI-powered email support agent built with **n8n** and **OpenAI**. It watches a Gmail inbox, reads each incoming customer email, understands the request, and replies automatically in the customer's language, so a small online store can answer customers faster with less manual work.

> **Note:** This is a **demo / sample project** built for a fictional clothing store ("Suyi"). It is not running for a real client.

![n8n workflow](Email%20workflow.png)

## Overview

Small online stores spend a lot of time answering the same emails: product questions, prices, delivery details, order requests and discount negotiation. This workflow automates that first line of support.

The agent greets the customer, answers from the store's product and policy information, collects the details needed for an order, and sends a polished reply.

## How It Works

```
Gmail Trigger  →  AI Agent (OpenAI Chat Model)  →  Reply to a message (Gmail)
```

1. **Gmail Trigger:** checks the inbox every minute for new emails.
2. **AI Agent:** reads the email and decides how to respond, following the instructions in its system prompt.
3. **Reply to a message:** sends the generated answer back to the customer in the same email thread.

## Features

- **Multilingual replies:** answers in the customer's language (Bangla or English; any other language gets an English reply)
- **Product enquiries:** shares price, delivery charge and payment method
- **Order collection:** gathers name, mobile number, full address, product, size, colour and quantity, and gives an order summary before confirming
- **Delivery rules:** Inside Dhaka ৳120 (1 day), Outside Dhaka ৳150 (3 days)
- **Payment:** Cash on Delivery only
- **Discount negotiation:** no discount at first; after 3 bargaining attempts, up to 5% off
- **Escalation:** refunds, returns, exchanges and complaints are directed to the store's support email
- **Professional tone:** every reply has a greeting and a closing signature

## Tech Stack

| Component | Tool |
|---|---|
| Automation platform | [n8n](https://n8n.io) |
| Language model | OpenAI (`gpt-5-mini`) |
| Email | Gmail (Trigger + Reply nodes) |

## Setup

1. Install and start n8n (`npm install n8n -g`, then `n8n start`) and open `http://localhost:5678`.
2. In n8n, choose **Import from File** and select `Email workflow.json` from this repository.
3. Add your own credentials:
   - **Gmail OAuth2** for the Gmail Trigger and Reply nodes
   - **OpenAI API key** for the Chat Model node
4. Open the **AI Agent** node and edit the system prompt: product list, prices, delivery charges, payment method, discount rules and support email.
5. Send a test email to the connected inbox, then **activate** the workflow.

> Credentials are not included in the workflow file. Never commit API keys to GitHub.

## Testing

Tested with 4 sample customer emails (product enquiry, price question, order request and discount request). All 4 received appropriate replies. This is a small test and not a production evaluation.

## Limitations

- **No live store data:** product, price, delivery and policy details come only from the system prompt. The agent has no connection to an inventory or order database, so it **cannot look up real stock levels or real order status.**
- **Automatic sending:** replies are sent directly without human review. For a real store, consider adding an approval step or saving replies as drafts first.
- **Processes all emails:** the trigger has no filter, so unrelated emails (newsletters, spam) would also get a reply. Add a label or sender filter before using it on a real inbox.
- **Complex cases:** refunds, returns and complaints are redirected to a human, not resolved by the agent.

## Possible Improvements

- Connect Google Sheets or a database for real inventory and order lookup
- Add a memory node so the agent remembers earlier messages in a conversation
- Add an approval step (draft first, send after review)
- Filter by Gmail label or sender
- Log every conversation to a spreadsheet for review

## Author

**Mamun Mazid**, AI Automation & AI Agent Developer

- Portfolio: [mazidai.github.io](https://mazidai.github.io)
- GitHub: [@Mazidai](https://github.com/Mazidai)
