# 🧠 Career AI Suite
### Multi-Agent System for Career Development

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=flat-square&logo=python)
![Gemini](https://img.shields.io/badge/LLM-Google%20Gemini-orange?style=flat-square&logo=google)
![LangChain](https://img.shields.io/badge/Framework-LangChain-green?style=flat-square)
![FAISS](https://img.shields.io/badge/Vector%20Store-FAISS-purple?style=flat-square)
![Gradio](https://img.shields.io/badge/UI-Gradio-red?style=flat-square)
![Colab](https://img.shields.io/badge/Platform-Google%20Colab-yellow?style=flat-square&logo=googlecolab)
![License](https://img.shields.io/badge/License-MIT-lightgrey?style=flat-square)

> An advanced multi-agent LLM system that unifies three AI-powered career tools — resume optimization, interview coaching, and data storytelling — into a single Gradio interface. Built with Google Gemini, LangChain, and FAISS-backed RAG.

---

## 📌 Overview

Career AI Suite addresses three critical friction points in the modern job search:

| Problem | Solution |
|---|---|
| ATS resume rejections & keyword gaps | **ResumeMatch AI** — scores resumes 1–10, computes JD match %, surfaces missing keywords |
| Expensive or generic interview coaching | **InterviewPrep AI** — generates role-specific questions, evaluates answers via STAR method |
| Data insights locked behind technical skills | **DataStory AI** — auto-profiles CSVs, generates insights, answers NL queries |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        User Input                           │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│               Gradio UI  ·  6 Active Tabs                   │
└────┬──────────────┬──────────────┬───────────────────────────┘
     │              │              │
     ▼              ▼              ▼
┌──────────┐  ┌──────────┐  ┌──────────┐
│ Resume   │  │Interview │  │DataStory │
│ Match AI │  │ Prep AI  │  │    AI    │
├──────────┤  ├──────────┤  ├──────────┤
│ Agent 1  │  │ Agent 3  │  │ Agent 5  │
│ Resume   │  │Interview │  │  Data    │
│ Analyzer │  │  Coach   │  │ Analyst  │
├──────────┤  ├──────────┤  ├──────────┤
│ Agent 2  │  │ Agent 4  │  │ Agent 6  │
│   Job    │  │Feedback  │  │ Insight  │
│ Matcher  │  │   Gen    │  │ Narrator │
└────┬─────┘  └────┬─────┘  └────┬─────┘
     │              │              │
     └──────────────┴──────────────┘
                    │
                    ▼
     ┌──────────────────────────┐
     │   Google Gemini (LLM)    │
     │  + FAISS RAG Pipeline    │
     └──────────────────────────┘
```

### Multi-Agent Design
- Each agent extends an abstract `BaseAgent` class with role-specific system prompts
- `AgentRole` enum enforces strict domain boundaries across 6 specialized agents
- `AgentMessage` dataclass handles typed inter-agent communication
- All agents return **structured JSON** — no raw text parsing required downstream

---

## ✨ Features

### 📄 ResumeMatch AI
- Scores resumes on a **1–10 scale** with section-level feedback (summary, experience, education, skills)
- Parses job descriptions and computes **ATS match percentage**
- Surfaces **missing keywords** and skill gaps with prioritized action items
- Generates **optimized STAR-method bullet points** tailored to the target JD
- Uses **FAISS RAG** to retrieve relevant JD requirements before analysis

### 🎯 InterviewPrep AI
- Generates **role-specific behavioral and technical questions** from the JD
- Evaluates submitted answers using the **STAR framework** (Situation, Task, Action, Result)
- Identifies weak points and drafts **improved answer suggestions**
- Supports **multi-turn mock interview** sessions with conversation history

### 📊 DataStory AI
- Auto-profiles uploaded **CSV datasets** — shape, types, distributions, missing values
- Generates **5 key insights** with supporting evidence and so-what analysis
- Supports **natural language Q&A** over the dataset via Gemini
- Produces **interactive Plotly visualizations** (bar, line, scatter, pie, heatmap, box)
- Generates structured **executive reports** in markdown format

---

## 🛠️ Tech Stack

| Component | Technology | Purpose |
|---|---|---|
| LLM Engine | Google Gemini (gemini-1.5-flash) | Core reasoning across all 6 agents |
| Orchestration | LangChain | LLM routing, prompt templates, message handling |
| Vector Store | FAISS (langchain-community) | RAG retrieval for JD matching and interview context |
| Embeddings | GoogleGenerativeAIEmbeddings | Semantic chunking and similarity search |
| UI Framework | Gradio | 6-tab interactive interface with public URL |
| Document Parsing | PyPDF2, python-docx | PDF and DOCX resume ingestion |
| Data Processing | Pandas, NumPy | CSV profiling and DataStory analysis |
| Visualization | Plotly, Matplotlib, Seaborn | Interactive and static charts |
| Platform | Google Colab | Zero-setup deployment, shareable URL |

---

## 📁 Project Structure

```
career-ai-suite/
│
├── FinalProject_Code_GENAI.ipynb   # Full implementation notebook
│
├── agents/
│   ├── base_agent.py               # Abstract BaseAgent + AgentRole enum
│   ├── resume_analyzer.py          # Agent 1: Resume scoring & feedback
│   ├── job_matcher.py              # Agent 2: ATS match + RAG JD retrieval
│   ├── interview_coach.py          # Agent 3: Question generation
│   ├── feedback_generator.py       # Agent 4: STAR evaluation
│   ├── data_analyst.py             # Agent 5: CSV profiling & NL Q&A
│   └── insight_narrator.py         # Agent 6: Narrative + report generation
│
├── core/
│   ├── rag_system.py               # FAISS RAG pipeline
│   ├── document_processor.py       # PDF / DOCX / TXT parser
│   └── visualization.py            # Plotly chart generator
│
└── app.py                          # Gradio UI — 6 tabs
```

---

## 🚀 Quickstart

### 1. Open in Google Colab
```
# Clone or upload FinalProject_Code_GENAI.ipynb to Google Colab
```

### 2. Add your Gemini API Key
In Colab, go to **Secrets** (🔑 icon) and add:
```
GEMINI_API_KEY = your_key_here
```
Get a free key at [aistudio.google.com](https://aistudio.google.com)

### 3. Run all cells
```
Runtime → Run All  (Ctrl+F9)
```

### 4. Access the app
Gradio will generate a **public shareable URL** — open it in any browser, no local setup required.

---

## 💡 Example Queries

| Tool | Example Input | What Happens |
|---|---|---|
| ResumeMatch AI | Paste resume + JD | Returns match %, missing keywords, improved bullets |
| InterviewPrep AI | Paste JD + role | Generates 5–10 tailored questions with STAR hints |
| InterviewPrep AI | Submit your answer | Scores answer, identifies weak STAR components, rewrites it |
| DataStory AI | Upload CSV | Auto-generates 5 insights + interactive charts |
| DataStory AI | "What's the highest revenue month?" | Returns plain-English answer backed by data |

---

## 📈 Key Metrics

| Metric | Value |
|---|---|
| Specialized Agents | 6 |
| Functional UI Tabs | 6 |
| Average Response Time | 2–5 seconds |
| Document Formats Supported | PDF, DOCX, TXT, CSV |
| Deployment Setup Time | < 2 minutes |

---

## 🔮 Roadmap (v2.0)

- [ ] Upgrade LLM core to Gemini 1.5 Pro for deeper analysis
- [ ] Voice-based mock interview support
- [ ] Direct PDF/DOCX resume upload in ResumeMatch UI
- [ ] Persistent user accounts with session history
- [ ] LinkedIn profile import via API
- [ ] Live job board integration for real-time JD matching
- [ ] Mobile app deployment

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

---

*Built as a final project for IE 5250 Applied Generative AI, Spring 2026, Northeastern University.*
