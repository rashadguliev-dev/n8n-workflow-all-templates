# 🚀 UAE Electronics Dropshipping Automation (Antigravity Edition)

This project contains the **production-ready n8n workflows** for the UAE Electronics Dropshipping business.
All workflows have been refactored to adhere to **Antigravity** best practices: robust error handling, rate limiting, and atomic data operations.

## 📂 Project Structure

### 1. Sourcing (Parsers)
- `01_Sourcing_Amazon_Noon.json`
  - **Function:** Scrapes prices from Amazon.ae and Noon.com.
  - **Antigravity Features:** Retry logic (3x), Proxy rotation support, Error Catching.
  - **Note:** Uses ScrapeGraphAI. Ensure credentials are set to "Header Auth" if the specific node type is unavailable.

### 2. Database (Inventory)
- `02_Inventory_Sync.json`
  - **Function:** Syncs scraped data to Google Sheets Master Inventory.
  - **Antigravity Features:** Batch processing (50 items/batch), Schema Validation, Duplicate protection.

### 3. Communications (Router)
- `03_Communications_Router.json`
  - **Function:** Handles incoming messages from WhatsApp & Telegram.
  - **Antigravity Features:** Intent Buffering, "Human Handoff" circuit breaker, Centralized logging.

### 4. Support (Bot)
- `04_RAG_Bot.json`
  - **Function:** The AI agent answering support questions using Pinecone/RAG.
  - **Source:** Originally workflow #9234.

### 5. Content (Socials)
- `05_Content_Automation.json`
  - **Function:** Publishes inventory items to Instagram/TikTok.
  - **Antigravity Features:** Image URL Pre-check (HEAD request) to prevent failed posts.

### 6. Utilities
- `99_Error_Handler.json`
  - **Function:** Centralized error logging to Telegram Manager Group.
  - **Antigravity Features:** Standardized Error Object.

## 🛠 Deployment Instructions
1. **Import:** Import all JSON files into your self-hosted n8n instance.
2. **Link Sub-Workflows:**
   - Open `01_Sourcing...`. Find the "Send to Inventory" node. Select the actual `02_Inventory_Sync` workflow from your list.
   - Open `03_Communications...`. Find "Trigger RAG Bot" and select `04_RAG_Bot`.
   - Update all "Log Error" nodes to point to `99_Error_Handler`.
3. **Configure Credentials:** Follow the guide in `CREDENTIALS.md`.
4. **Activate:** Start with `99_Error_Handler`, then the others.
