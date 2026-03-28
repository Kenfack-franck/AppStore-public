# JobFinder — AI-Powered Job Search Assistant

> **HrFlow.ai Hackathon Submission**

![JobFinder](assets/preview.png)

## 🌐 Live Demo

**→ [https://jobfinder.franckkenfack.works](https://jobfinder.franckkenfack.works)**

| Page | URL |
|---|---|
| Landing page | https://jobfinder.franckkenfack.works |
| Job search | https://jobfinder.franckkenfack.works/jobs |
| AI Chat assistant | https://jobfinder.franckkenfack.works/chat |
| Applications tracker | https://jobfinder.franckkenfack.works/applications |
| Profile | https://jobfinder.franckkenfack.works/profile |

---

## 👥 Team

| Name | Role |
|---|---|
| **Franck Ulrich Kenfack** | Full-stack development, HrFlow.ai integration, DevOps |
| **Nkouatio** | Backend development, AI services |
| **Kuate Dematino** | Frontend development, UI/UX |

---

## What it does

JobFinder automates your entire job search using **HrFlow.ai** for intelligent matching — from CV parsing to compatibility scoring and interview preparation — combined with **Claude (Anthropic)** for personalized career advice and document generation.

### Core workflow

```
1. Upload your CV  →  HrFlow.ai parses it  →  Profile indexed in Source
2. Search / scrape jobs  →  Jobs indexed in Board
3. HrFlow.ai scores jobs  →  Personalized ranked feed
4. Click a job  →  HrFlow.ai explains match (strengths/weaknesses)
5. Ask the AI Chat  →  Claude + HrFlow context gives tailored advice
6. Generate CV/Cover letter  →  Claude produces personalized documents
```

---

## HrFlow.ai Integration

| HrFlow.ai API | How it's used in JobFinder |
|---|---|
| `profile.parsing.add_file` | Upload PDF/DOCX CV → extract structured profile automatically |
| `profile.storing.add_json` | Index candidate profile into HrFlow Source |
| `profile.storing.get` | Retrieve full profile from Source |
| `job.storing.add_json` | Index scraped job offers into HrFlow Board |
| `job.scoring.list` | Rank all board jobs by compatibility with the user's profile |
| `job.searching.list` | Semantic search across boards by keyword/skills |
| `job.reasoning.get` | Explain why a job matches: list strengths & weaknesses |
| `text.tagging.post` | Extract skills/keywords from job descriptions |
| `text.embedding.post` | Vectorize text for semantic similarity |
| `profile.asking.get` | Answer natural-language questions about a profile |
| `job.asking.get` | Answer natural-language questions about a job offer |

---

## AI Chat Demo

Visit [/chat](https://jobfinder.franckkenfack.works/chat) — the assistant uses HrFlow.ai data in real time:

1. Click **"🔍 Trouve-moi des offres Python à Paris"**
   → Ranked job cards with HrFlow.ai compatibility scores

2. Click **"📊 Analyse ma compatibilité avec Senior Python Developer"**
   → Score bar + strengths (Python, FastAPI…) + weaknesses (Kubernetes…)

3. Click **"💡 Prépare-moi pour l'entretien chez TechCorp"**
   → Interview questions with personalized coaching tips

---

## Architecture

```
┌─────────────────────┐     ┌──────────────────────────┐
│   Next.js 14        │────▶│   FastAPI + SQLAlchemy    │
│   React 18 / TS     │     │   Python 3.11, async      │
│   Tailwind CSS      │     │   JWT auth, Alembic       │
└─────────────────────┘     └────────────┬─────────────┘
                                          │
              ┌───────────────────────────┼─────────────────┐
              ▼                           ▼                 ▼
    ┌──────────────────┐       ┌──────────────────┐  ┌──────────┐
    │  HrFlow.ai SDK   │       │  Claude (haiku)   │  │  Redis   │
    │  v3.3 — 11 APIs  │       │  Chat + CV gen    │  │  Celery  │
    └──────────────────┘       └──────────────────┘  └──────────┘
```

**Stack:** Python 3.11 · FastAPI · Next.js 14 · PostgreSQL + pgvector · Redis · Docker

---

## Quick Start

```bash
git clone https://github.com/Kenfack-franck/hackaton_hrflow.git
cd hackaton_hrflow
cp .env.example .env
# Fill in: HRFLOW_API_KEY, HRFLOW_USER_EMAIL, HRFLOW_SOURCE_KEY,
#          HRFLOW_BOARD_KEY, CLAUDE_API_KEY, SECRET_KEY
docker-compose up -d
docker-compose exec backend alembic upgrade head
# Frontend: http://localhost:3000  |  API docs: http://localhost:8000/docs
```

---

## Source Code

**GitHub:** https://github.com/Kenfack-franck/hackaton_hrflow
