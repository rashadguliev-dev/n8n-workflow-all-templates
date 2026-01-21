# 🏗️ Antigravity Architecture: UAE Electronics Dropshipping

This document visualizes the **production-ready logic** implemented in the JSON workflows.

## 🔄 System Pipeline

```mermaid
graph TD
    %% ZONE 1: SOURCING
    subgraph Sourcing ["01_Sourcing (Antigravity)"]
        Timer(Schedule 1h) --> Batch[Split Batches]
        Batch --> TryScrape{Try AI Scrape}
        TryScrape -->|Success| Norm[Normalize Data]
        TryScrape -->|Fail| Puppeteer[Fallback Scraper]
        Puppeteer --> Norm
        Norm --> WebhookSync[Call Inventory Sync]
    end

    %% ZONE 2: DATABASE
    subgraph Database ["02_Inventory (Antigravity)"]
        WebhookSync --> Valid{Validate Schema}
        Valid -->|Invalid| Error[Throw Error]
        Valid -->|Valid| Update[Atomic Update Sheets]
    end

    %% ZONE 3: ROUTING
    subgraph Router ["03_Communications (Antigravity)"]
        Msg(Webhook WA/TG) --> Buffer[Wait 2s]
        Buffer --> Classify{AI Intent}
        Classify -->|Buy| Notify[Notify Manager]
        Classify -->|Support| RAG[Trigger RAG Bot]
        Classify -->|Spam| Ignore((Drop))
    end

    %% ZONE 4: ERROR HANDLING
    subgraph Monitor ["99_Error_Handler"]
        GlobalError(Error Trigger) --> LogTG[Log to Admin Group]
    end

    %% CONNECTIONS
    TryScrape -.->|Error| GlobalError
    Update -.->|Error| GlobalError
    Notify -.->|Error| GlobalError
```

## 🛡️ Antigravity Principles Applied

1.  **Strict Isolation:** Sourcing does not touch the database directly; it sends data to the Inventory Sync workflow via Webhook. This decouples the scrapers from the storage logic.
2.  **Schema Validation:** The Inventory workflow *rejects* data that doesn't match the strict schema (Price > 0, Title present), protecting the database from "garbage in".
3.  **Graceful Fallback:** If the expensive AI scraper fails, the system automatically falls back to the cheaper Puppeteer scraper.
4.  **Intent Buffering:** The Chat Router waits 2 seconds to collect potential multi-message bursts from users before processing, saving AI tokens and reducing noise.
5.  **Centralized Logging:** All errors flow to a single `99_Error_Handler` workflow, ensuring no silent failures.
