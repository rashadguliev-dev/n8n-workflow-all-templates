# DeenFlow System Architecture

```mermaid
graph TD
    User((User))
    WebUI[Workflow 01: Dashboard Web UI]
    AIAgent[Workflow 02: Iman Assistant]
    Tracker[Workflow 03: Spiritual Tracker]

    GSheets[(Google Sheets Database)]
    Telegram[Telegram Notifications]

    QuranAPI[Quran API / Tanzil]
    HadithAPI[Hadith API / Sunnah]
    AdhanAPI[Adhan API / Prayer Times]

    User <--> WebUI
    User <--> AIAgent

    WebUI --> AdhanAPI
    WebUI --> QuranAPI
    WebUI --> HadithAPI

    AIAgent --> QuranAPI
    AIAgent --> HadithAPI
    AIAgent --> AIAgent_Model[GPT-4o Athari Grounding]

    Tracker --> GSheets
    Tracker --> Telegram
    User -- Log Actions --> Tracker
```

## Data Flow
- **Dashboard**: Serves as the primary entry point, aggregating real-time data from AlAdhan, Quran Cloud, and Hadith APIs to present a "Today" view. Support for dynamic city/country via query params.
- **Assistant**: Uses an AI Agent with a strict system prompt. Grounding is provided via search tools targeting authentic Quranic and Hadith datasets.
- **Tracker**:
    - **Reminders**: Scheduled triggers (Fajr, Isha) with "Life Mode" logic (Student/Worker) send tailored Telegram reminders.
    - **Logging**: A dedicated Webhook endpoint accepts POST requests to log spiritual progress to Google Sheets.
