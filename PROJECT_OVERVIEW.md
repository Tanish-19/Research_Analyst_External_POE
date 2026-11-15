# Project Overview: Research Analyst Agents 🔬

> **A simple, plain-English guide to what this project is, why it was built, and how it works.**

---

## 💡 What is This Project?

**Research Analyst Agents** is an AI-powered system designed to do high-level research the way a human analyst team at a top consulting firm or think tank would.

Instead of asking one single AI chatbot to answer a complex question (which often leads to shallow answers or "hallucinations" where the AI makes things up), this system uses **three specialized AI agents that collaborate in an assembly line**:

1. The first agent **gathers the facts and evidence**.
2. The second agent **checks the facts and weeds out mistakes or bias**.
3. The third agent **writes a publication-grade executive research report**.

You can ask it complex questions about technology, energy, quantum computing, or semiconductors, or even give it research papers (PDFs), web articles, and data charts to analyze.

---

## 🎯 What Problem Does It Solve? (The Purpose)

When professionals research new technologies or business decisions, they face three big problems with standard AI chatbots:

1. **Hallucinations & Inaccurate Numbers:** Single-prompt AI often guesses numbers or cites papers that do not exist.
2. **Lack of Critical Fact-Checking:** A standard chatbot agrees with whatever prompt you give it without questioning assumptions or methodology.
3. **Shallow Reports:** One-shot answers are usually generic summaries rather than actionable executive memoranda with cited evidence and risk assessments.

### How this project solves it:
By breaking the research process into **three distinct roles**, no single agent has to do everything alone:
- The writer agent only writes about facts that the fact-checker agent has already audited.
- The fact-checker only audits claims backed by evidence the researcher actually found in grounding benchmarks or uploaded papers.

This separation of concerns makes the final research report significantly more accurate, thorough, and trustworthy.

---

## 👥 Meet the 3 Collaborating Agents

Here is the team working behind the scenes on every research request:

```
[ User Inquiry / PDF / URL ]
            │
            ▼
┌────────────────────────────────────────┐
│  Agent 1: Research Agent               │
│  • Searches benchmarks & literature    │
│  • Reads uploaded PDFs & scrapes URLs  │
│  • Catalogues hard data & facts        │
└──────────────────┬─────────────────────┘
                   │ Empirical Evidence
                   ▼
┌────────────────────────────────────────┐
│  Agent 2: Analysis & Verification      │
│  • Audits evidence for accuracy        │
│  • Filters out hallucinations & bias   │
│  • Extracts non-obvious insights       │
└──────────────────┬─────────────────────┘
                   │ Validated Insights
                   ▼
┌────────────────────────────────────────┐
│  Agent 3: Report Generation Agent      │
│  • Structures the final report         │
│  • Adds Executive Summary & Risks      │
│  • Links evidence, charts, and sources │
└──────────────────┬─────────────────────┘
                   │
                   ▼
[ Verified Executive Research Report ]
```

### 1. 🔍 Agent 1: Research Agent (The Gatherer)
- **Role:** Information scout and librarian.
- **What it does:** It breaks your topic into focused search queries. It searches the built-in knowledge base (which covers benchmarks on AI, battery storage, post-quantum cryptography, 2nm microchips, biomedical AI, and tech economics).
- **Extra Powers:** It can ingest uploaded PDF papers using chunking (RAG), scrape live web URLs, and pull relevant vector data charts.

### 2. 🛡️ Agent 2: Analysis & Verification Agent (The Auditor)
- **Role:** Fact-checker and strategic analyst.
- **What it does:** It rigorously examines everything Agent 1 gathered. It asks: *"Is this claim supported by data? Are these numbers consistent? Is there uncertainty or bias?"*
- **Value:** It eliminates AI hallucinations before anything reaches the final report and uncovers strategic insights that connect different pieces of evidence.

### 3. 📑 Agent 3: Report Generation Agent (The Executive Writer)
- **Role:** Chief editor and synthesis specialist.
- **What it does:** It takes the verified findings and turns them into a structured, executive memorandum.
- **Output Structure:**
  - **Executive Summary:** The core takeaway upfront.
  - **Evidence Base & Methodology:** What datasets and sources were consulted.
  - **Key Analytical Findings:** Detailed breakdown of trends and metrics.
  - **Risk Assessment & Trade-offs:** Potential bottlenecks, costs, and failure modes.
  - **Strategic Recommendations:** Actionable guidance for decision-makers.

---

## 🌟 Key Features of the System

- **📄 Document & PDF Understanding (RAG):** Upload any PDF whitepaper or research document. The system breaks it into chunks, finds the most relevant sections, and cites them.
- **🌐 Live Web Scraping:** Paste an article or paper URL, and the system extracts the clean text and ingests it as evidence.
- **📊 Embedded Visual Charts & Diagrams:** Comes with technical benchmark vector charts (like qubit scaling curves or battery cost trends) and an interactive full-screen Lightbox to inspect diagrams.
- **🌓 Dual-Theme User Interface:** Features a modern executive web application with an instant **Dark / Light mode toggle**, pipeline step indicators, and one-click **Markdown (.md) download**.
- **⚡ Two Frontend Interfaces:**
  1. **Web Dashboard (FastAPI):** Fast, modern single-page dashboard at [http://localhost:8000](http://localhost:8000).
  2. **Streamlit App:** Interactive data app at [http://localhost:8501](http://localhost:8501).
- **🤖 Powered by Modern AI:** Runs by default on Google's Gemini models (`gemini-3.5-flash-lite` or similar), with fallback support for Groq (`qwen/qwen3.8-27b`).

---

## 🔄 Step-by-Step: How a Request Works

1. **You ask a question:** For example, *"Evaluate multi-agent LLM reasoning benchmarks and hallucination reduction vs single-prompt models."*
2. **Grounding:** You can optionally attach a research PDF or select a preset benchmark chart.
3. **Agent 1 acts:** Queries the knowledge base and pulls empirical numbers (e.g. 94.6% factual consistency in multi-agent pipelines vs 58.2% in monolithic models).
4. **Agent 2 audits:** Checks that the benchmark methodology is solid, notes latency trade-offs, and verifies the citations.
5. **Agent 3 writes:** Formats the final executive report with clear headers, bullet points, citations, and risk analyses.
6. **You get the report:** In under 10 seconds, the complete memorandum appears on your screen with options to **Copy**, **Download as .md**, or **Print/Save as PDF**.

---

## 🛠️ How to Run the Services

### Running Locally with Python:

1. **Start the Web UI & API (Port 8000):**
   ```bash
   python -m uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
   ```
   Open **http://localhost:8000** in your browser.

2. **Start the Streamlit App (Port 8501):**
   ```bash
   streamlit run streamlit_app.py --server.port=8501 --server.address=0.0.0.0
   ```
   Open **http://localhost:8501** in your browser.

### Running Automated Tests:
```bash
pytest -v
```
All 23 unit and integration tests validate the agents, health checks, media endpoints, and RAG pipeline.

---

## 📁 File Structure at a Glance

- [`app/main.py`](file:///Users/tanishpatgaonkar/Downloads/Research%20Analyst/app/main.py) — The FastAPI backend server and API endpoints (`/research`, `/health`).
- [`app/agents/research_team.py`](file:///Users/tanishpatgaonkar/Downloads/Research%20Analyst/app/agents/research_team.py) — Definitions of the 3 collaborating Agno agents.
- [`app/agents/tools.py`](file:///Users/tanishpatgaonkar/Downloads/Research%20Analyst/app/agents/tools.py) — Search and retrieval tools for the agents.
- [`app/agents/rag.py`](file:///Users/tanishpatgaonkar/Downloads/Research%20Analyst/app/agents/rag.py) — PDF extraction, BM25 chunk scoring, and web scraping logic.
- [`app/static/index.html`](file:///Users/tanishpatgaonkar/Downloads/Research%20Analyst/app/static/index.html) — The web dashboard user interface.
- [`app/static/style.css`](file:///Users/tanishpatgaonkar/Downloads/Research%20Analyst/app/static/style.css) — Modern stylesheet with Dark and Light theme styling.
- [`app/static/app.js`](file:///Users/tanishpatgaonkar/Downloads/Research%20Analyst/app/static/app.js) — Interactive browser logic, theme switching, and download features.
- [`streamlit_app.py`](file:///Users/tanishpatgaonkar/Downloads/Research%20Analyst/streamlit_app.py) — Streamlit alternative user interface.
- [`docker-compose.yml`](file:///Users/tanishpatgaonkar/Downloads/Research%20Analyst/docker-compose.yml) — Container setup to run both services together.

