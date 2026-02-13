# SocialPulse SaaS 📊

A production-grade, multi-user WhatsApp analytics platform with AI-powered insights.

## Features

- 🔐 **User Authentication** - Secure signup/login with bcrypt
- 📤 **Chat Upload** - Parse WhatsApp exports with robust error handling
- 📊 **SQL Analytics** - Database-level aggregations for performance
- 🕸️ **Social Graph** - NetworkX + PageRank influence analysis
- 🤖 **AI Chat** - RAG-powered Q&A using Gemini 1.5 Flash

## Tech Stack

- **Frontend:** Streamlit
- **Backend:** SQLAlchemy + PostgreSQL
- **Analytics:** NetworkX, Pandas
- **AI:** LangChain, Google Gemini, FAISS, HuggingFace Embeddings

## Installation

### Prerequisites
- Python 3.9+
- PostgreSQL installed and running

### Setup

1. **Clone repository**
```bash
git clone <repo-url>
cd SocialPulse
```

2. **Create virtual environment**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

4. **Configure PostgreSQL**
```bash
# Create database
createdb socialpulse

# Or via psql
psql -U postgres
CREATE DATABASE socialpulse;
\q
```

5. **Set environment variables**
```bash
cp .env.example .env
# Edit .env with your credentials
export GEMINI_API_KEY='your-key-here'
```

6. **Initialize database**
```bash
python -c "from src.db import init_database; init_database()"
```

## Running the Application
```bash
streamlit run app.py
```

Navigate to `http://localhost:8501`

## Project Structure
```
SocialPulse/
├── app.py                  # Main Streamlit app
├── requirements.txt
├── src/
│   ├── models.py          # SQLAlchemy ORM
│   ├── db.py              # Database management
│   ├── auth.py            # Authentication
│   ├── parser.py          # WhatsApp parser
│   ├── analytics.py       # SQL + NetworkX analytics
│   └── ai_engine.py       # RAG pipeline
└── data/
    └── faiss_indexes/     # Vector stores
```

## Key Architectural Decisions

### 120-Second Reply Heuristic
In `src/analytics.py`, we use a 120-second window to determine if one message is a "reply" to another. This creates directed edges in our social graph and enables PageRank-based influence scoring.

### SQL-First Analytics
Rather than using pandas groupby, we write raw SQL queries to demonstrate database-level analytical skills suitable for technical interviews.

### RAG Architecture
Each chat group gets its own FAISS index, persisted to disk. This enables fast, group-specific AI queries without cross-contamination.

## Usage

1. **Sign up** for an account
2. **Upload** a WhatsApp chat export (.txt)
3. **Analyze** using three tabs:
   - Overview: Metrics and activity patterns
   - Social Graph: Influence network visualization
   - AI Chat: Natural language queries

## Export WhatsApp Chat

1. Open WhatsApp chat
2. Tap ⋮ (menu)
3. More → Export chat
4. **Without media**
5. Save as .txt file

## License

MIT

## Author

Senior Full-Stack Data Engineer
Portfolio Project - 2024