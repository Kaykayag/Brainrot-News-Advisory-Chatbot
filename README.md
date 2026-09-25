```markdown
# ⚡ Brainrot AI — WhatsApp Community Outage & Advisory Chatbot

An automated WhatsApp chatbot designed to provide real-time barangay outage alerts, public utility interruptions (power/water), and community updates wrapped in an energetic Gen Z Pinoy / Taglish "brainrot" persona (`accla`, `solulu`, `no cap`, `fr fr`).

The bot leverages Retrieval-Augmented Generation (RAG) powered by ChromaDB, Groq's high-speed inference engine, Meta WhatsApp Cloud API, and automated scrapers/bulletin ingestion to deliver accurate, localized information without hallucinations.

---

## 🚀 Key Features

* **Persistent User Location:** Saves each user's designated barangay/city in `registered_users.json` via commands like `set location <Barangay, City>` so users don't have to specify their location repeatedly.
* **Brainrot / Gen Z Persona:** Delivers helpful civic information in engaging, modern Taglish slang with deterministic triggers (e.g., `"pwede magtanong?"` -> `"never grow old? Huyyy bawal mag-inarte, drop the tea accla!"`).
* **Semantic RAG Retrieval:** Uses `sentence-transformers/all-MiniLM-L6-v2` embeddings stored in ChromaDB to retrieve relevant local news, power distributor advisories, and official bulletins.
* **Proactive Outage Scanner:** A background worker running on APScheduler scans for local advisories every 15 minutes and pushes alerts to registered residents.
* **Admin Bulletin Ingestion:** Secure administrative endpoints (`/admin/captain-update`) and scrapers to feed social media announcements, Facebook page notes, and barangay captain posts into the vector store.

---

## 🛠️ Tech Stack

* **Language:** Python 3.10+
* **Framework:** FastAPI, Uvicorn
* **Tunneling:** ngrok
* **LLM Engine:** Groq API (`qwen/qwen3.8-27b`)
* **Vector Store & Embeddings:** ChromaDB (`langchain-chroma`), HuggingFace Embeddings (`sentence-transformers/all-MiniLM-L6-v2`)
* **Messaging Platform:** Meta WhatsApp Cloud API (Graph API v19.0+)
* **Scheduler:** APScheduler

---

## 📁 Project Structure

- created in google Colab 

```

---

## ⚙️ Environment Variables & Secrets

Google Colab Secrets (🔑):

| Variable Name | Description |
| --- | --- |
| `GROQ_API_KEY` | API key from Groq Console |
| `GROQ_MODEL` | Active model ID (e.g., `qwen/qwen3.8-27b`) |
| `META_ACCESS_TOKEN` | System User or Temporary Access Token from Meta Developer Dashboard |
| `META_PHONE_NUMBER_ID` | Test or Production Phone Number ID assigned by Meta |
| `META_VERIFY_TOKEN` | Custom verification token string for the webhook callback |
| `NGROK_AUTHTOKEN` | Your ngrok authentication token |
| `ADMIN_SECRET_KEY` | Header key required to push manual updates to `/admin/captain-update` |

---

## 💬 Core WhatsApp Commands

* **`set location <Barangay, City>`**: Registers or updates your default community location.
* **`pwede magtanong?`**: Hardcoded trigger returning the bot's custom slang opener.
* **`ano latest balita kay kapitan?`**: Queries ChromaDB for the latest barangay announcements and summarizes them.
* **`May brownout ba ngayon?`**: Retrieves active power interruptions and advisory schedules for your registered area.

---

## 📅 Development Roadmap & Weekly TODO

### Week 1: Core Reliability & Webhooks (Current)

* [x] Integrate Meta WhatsApp Cloud API inbound/outbound webhooks.
* [x] Establish ngrok tunnel and FastAPI server on Google Colab.
* [ ] Configure ChromaDB vector persistence and document ingestion. [NOTE:Still need some inprovement]
* [x] Implement persistent user location tracking (`registered_users.json`).
* [ ] Automate permanent system access token generation to replace 24-hour temporary tokens. [NOTE: as of the moment, were using temporart access token from meta developer]

### Week 2: Targeted Scraping & Social Ingestion

* [ ] Build automated scraper for public utility advisory pages (e.g., Visayan Electric, Manila Water, Maynilad).
* [ ] Add RSS / public web monitoring for local Barangay Facebook/LGU portals.
* [ ] Implement deduplication logic in `ingest_document()` to prevent duplicate news chunks in ChromaDB.

### Week 3: Multi-User Experience & Memory

* [ ] Migrate `registered_users.json` to an SQLite or PostgreSQL database for thread-safe concurrent writes.
* [ ] Add session conversation history (short-term buffer memory) to retain context across multi-turn chats.
* [ ] Implement broadcast notifications: auto-push advisories to all registered numbers in an affected barangay.

### Week 4: Persona Refinement & Moderation

* [ ] Add dynamic Taglish slang dictionary expansion for regional variations.
* [ ] Implement confidence scoring: if no retrieved RAG chunk matches > 0.7 score, cleanly state no official news exists.
* [ ] Deploy from Google Colab to a permanent containerized host (Render, Railway, or AWS EC2).

---

## 📄 License

This project is open-source and available under the [MIT License](https://www.google.com/search?q=LICENSE&utm_source=gemini).

```
