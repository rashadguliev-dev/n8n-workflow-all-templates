# 🔐 Credentials Setup Guide

To run the **Antigravity UAE Project**, you must configure the following credentials in your n8n instance.

## 1. ScrapeGraphAI (Sourcing)
- **Used in:** `01_Sourcing_Amazon_Noon.json`
- **Type:** Header Auth
- **Header Name:** `Authorization`
- **Value:** `Bearer sg-xxxxxxxxx` (Get from [scrapegraphai.com](https://scrapegraphai.com))

## 2. OpenAI (Intelligence)
- **Used in:** `03_Communications_Router.json`
- **Type:** OpenAI API
- **API Key:** `sk-proj-xxxxxx`
- **Model:** `gpt-4o-mini` (Cost-effective for classification)

## 3. Telegram (Notifications & Chat)
- **Used in:** `03_Communications_Router.json`, `99_Error_Handler.json`
- **Type:** Telegram API
- **Token:** `123456:ABC-xxxxxxx` (From @BotFather)
- **Manager Chat ID:** Create a group, add bot, get ID (starts with `-100`).

## 4. Google Sheets (Database)
- **Used in:** `02_Inventory_Sync.json`
- **Type:** Google OAuth2
- **Scopes:** `drive`, `spreadsheets`
- **Setup:** Follow [n8n Google Docs guide](https://docs.n8n.io/integrations/builtin/credentials/google/).

## 5. WhatsApp (Provider)
- **Used in:** `03_Communications_Router.json` (Trigger)
- **Note:** This project uses a Generic Webhook. You need to configure your provider (360dialog/Meta) to POST to:
  `https://your-n8n-instance.com/webhook/chat-webhook`
