# DeenFlow Credentials & Setup Guide

## 1. OpenAI API (Assistant)
- **Required**: `apiKey`
- **Scope**: Access to GPT-4o model.
- **Node**: Used in `02_DeenFlow_AI_Assistant`.

## 2. Telegram Bot
- **Required**: `accessToken`, `chatId`
- **Setup**: Create a bot via [@BotFather](https://t.me/botfather).
- **Node**: Used in `03_DeenFlow_Tracker_Plan` and optionally in Dashboard notifications.

## 3. Google Sheets
- **Required**: OAuth2 or Service Account.
- **Setup**: Create a sheet with columns: `Date`, `Prayer_Count`, `Quran_Reading`, `Dhikr_Consistency`.
- **Node**: Used in `03_DeenFlow_Tracker_Plan`.

## 4. n8n Configuration
- **Webhook Path**: `/deenflow/dashboard` must be set in your n8n environment to serve the UI.
- **Memory**: Ensure `memoryBufferWindow` nodes are correctly connected to the AI Agent.

## ⚠️ Security Note
- Never share your n8n `.env` file or export workflows containing hardcoded credentials. Always use n8n's Credential system.
