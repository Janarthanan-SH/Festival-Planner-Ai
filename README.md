# 🎉 Festiva Planner AI

> AI-powered event planning assistant with ML budget prediction, RAG knowledge base, and multi-agent orchestration.

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                      FRONTEND (React + TypeScript)               │
│  HomePage | PlannerPage | AssistantPage (RAG Chat)              │
│  recharts | framer-motion | react-icons                         │
└───────────────────────────┬─────────────────────────────────────┘
                            │ REST API
┌───────────────────────────▼─────────────────────────────────────┐
│                      BACKEND (FastAPI)                           │
│                                                                  │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────────┐  │
│  │ Planner Agent│  │ Budget Agent │  │  Knowledge Agent     │  │
│  │  (Timeline,  │  │  (ML Cost    │  │  (RAG Retriever)     │  │
│  │  Checklist,  │  │  Prediction) │  │                      │  │
│  │  Vendors)    │  │              │  │                      │  │
│  └──────┬───────┘  └──────┬───────┘  └──────────┬───────────┘  │
│         │                 │                       │              │
│  ┌──────▼─────────────────▼───────────────────────▼───────────┐ │
│  │              OrchestratorAgent (Multi-Agent Pipeline)      │ │
│  └────────────────────────────────────────────────────────────┘ │
│                                                                  │
│  ┌─────────────────┐  ┌──────────────────┐  ┌──────────────┐   │
│  │ Budget Predictor│  │ Event Classifier │  │ RAG System   │   │
│  │ (RandomForest   │  │ (TF-IDF +        │  │ (TF-IDF +    │   │
│  │  MultiOutput)   │  │  LogisticReg)    │  │  FAISS)      │   │
│  └─────────────────┘  └──────────────────┘  └──────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🚀 Quick Start

### Prerequisites
- Python 3.10+
- Node.js 18+

### Backend Setup

```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```

The backend starts on `http://localhost:8000`  
API docs: `http://localhost:8000/docs`

### Frontend Setup

```bash
cd frontend
npm install
npm start
```

The frontend starts on `http://localhost:3000`

---

## 🐳 Docker (Full Stack)

```bash
docker-compose up --build
```

- Frontend: http://localhost:3000
- Backend API: http://localhost:8000
- API Docs: http://localhost:8000/docs

---

## 📡 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/plan/generate` | Generate complete event plan (multi-agent) |
| POST | `/api/plan/parse` | NLP parse natural language event description |
| POST | `/api/budget/predict` | ML budget breakdown prediction |
| POST | `/api/budget/analyze` | Full budget analysis + feasibility |
| POST | `/api/budget/compare` | Compare budget scenarios |
| POST | `/api/knowledge/query` | RAG knowledge query |
| POST | `/api/knowledge/guide` | Get planning guide by event type |
| POST | `/api/vendors/for-event` | Get vendors for event type + city |
| GET  | `/api/knowledge/chat-suggestions` | Get suggested questions |

---

## 🧠 AI & ML Components

### Week 1 — Data & EDA
- **`data/event_data.py`** — 8 event types, vendor categories, timelines, budget percentages
- **`data/vendor_data.py`** — City-wise vendor database (Bangalore, Mumbai, Delhi, etc.)
- Synthetic dataset generation (2000 records) for ML training

### Week 2 — ML Model
- **`models/budget_predictor.py`** — RandomForest + MultiOutputRegressor
- Trained on 2000 synthetic records with city, event type, guest count, season features
- Predicts cost allocation per category with MAPE evaluation

### Week 3 — NLP
- **`models/event_classifier.py`** — TF-IDF + Logistic Regression
- Classifies free-text descriptions into event types
- Extracts city, budget, guest count from natural language

### Week 4 — RAG System
- **`rag/knowledge_base.py`** — 12 curated event planning documents
- **`rag/retriever.py`** — TF-IDF vectorizer + cosine similarity retrieval
- RAG Assistant with context-aware answers

### Week 5 — Multi-Agent System
- **`agents/planner_agent.py`** — Event plan generation
- **`agents/budget_agent.py`** — Budget optimization
- **`agents/knowledge_agent.py`** — RAG knowledge retrieval
- **`OrchestratorAgent`** — Multi-agent pipeline coordinator

### Week 6 — Deployment
- FastAPI backend with auto-generated OpenAPI docs
- React TypeScript frontend with recharts visualizations
- Docker + docker-compose setup

---

## 🎯 Example Usage

### Input
```
Event Type: Wedding
City: Bangalore
Budget: ₹10 Lakhs
Guests: 200
```

### Output
- ✅ Complete 14-step event timeline
- 💰 ML-predicted budget breakdown (venue 25%, catering 30%, etc.)
- 🏢 Top-rated vendors per category
- 📚 RAG-powered planning insights
- 💡 5 expert planning tips

---

## 📁 Project Structure

```
Festival Planner AI/
├── backend/
│   ├── main.py              # FastAPI app entry point
│   ├── requirements.txt
│   ├── Dockerfile
│   ├── agents/
│   │   ├── planner_agent.py  # Event plan generation
│   │   ├── budget_agent.py   # ML budget optimization
│   │   └── knowledge_agent.py # RAG + Orchestrator
│   ├── models/
│   │   ├── budget_predictor.py # RandomForest ML
│   │   └── event_classifier.py # NLP classifier
│   ├── rag/
│   │   ├── knowledge_base.py  # 12 event planning docs
│   │   └── retriever.py       # TF-IDF retrieval
│   ├── data/
│   │   ├── event_data.py      # Event types & timelines
│   │   └── vendor_data.py     # City vendor database
│   └── routers/
│       ├── plan.py    # /api/plan/*
│       ├── budget.py  # /api/budget/*
│       ├── rag.py     # /api/knowledge/*
│       └── vendors.py # /api/vendors/*
└── frontend/
    ├── src/
    │   ├── App.tsx
    │   ├── api.ts           # Axios API client
    │   ├── pages/
    │   │   ├── HomePage.tsx
    │   │   ├── PlannerPage.tsx
    │   │   └── AssistantPage.tsx
    │   └── components/
    │       ├── Navbar.tsx
    │       ├── EventForm.tsx
    │       ├── BudgetChart.tsx
    │       ├── Timeline.tsx
    │       └── VendorCards.tsx
    └── Dockerfile
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | FastAPI, Python 3.11 |
| ML | Scikit-learn (RandomForest), Pandas, NumPy |
| NLP | TF-IDF, Logistic Regression |
| RAG | FAISS, TF-IDF vectorizer, cosine similarity |
| Agents | Custom multi-agent orchestration |
| Frontend | React, TypeScript, Recharts |
| Deployment | Docker, docker-compose |

---

## 🔮 Future Enhancements

- [ ] LLM integration (GPT-4 / Gemini) for richer plan generation
- [ ] Sentence-transformers for semantic RAG (replace TF-IDF)
- [ ] LangChain agent tools with web search
- [ ] User authentication & saved plans
- [ ] WhatsApp/Telegram bot integration
- [ ] Real vendor API integrations
- [ ] PDF export of plans
