# 🔎 AI Research Agent

An AI-powered research pipeline that searches the web, extracts information from relevant sources, generates a structured research report, and critically reviews the generated report.

The project combines **LangChain agents, Groq LLMs, Tavily web search, and web scraping** to automate the research workflow.

---

## 🚀 Features

* 🔍 **Web Search Agent**

  * Searches the web for recent and relevant information.
  * Uses Tavily for web search.
  * Retrieves titles, URLs, and snippets.

* 🌐 **Web Reader Agent**

  * Identifies relevant sources from search results.
  * Scrapes webpages for detailed information.
  * Uses Requests and BeautifulSoup.

* ✍️ **Research Writer**

  * Combines search results and scraped content.
  * Generates a structured research report.
  * Includes introduction, key findings, conclusion, and sources.

* 🧐 **Research Critic**

  * Reviews the generated report.
  * Identifies strengths and weaknesses.
  * Provides structured feedback.

* ⚡ **Fast LLM Inference**

  * Uses a Groq-hosted language model through LangChain.

---

## 🏗️ Architecture

```text
                    User Topic
                        │
                        ▼
              ┌──────────────────┐
              │   Search Agent   │
              │     Tavily       │
              └────────┬─────────┘
                       │
                       ▼
                Search Results
                       │
                       ▼
              ┌──────────────────┐
              │   Reader Agent   │
              │  Web Scraping    │
              └────────┬─────────┘
                       │
                       ▼
              Scraped Web Content
                       │
                       ▼
              ┌──────────────────┐
              │  Research Writer │
              │   Groq + LLM     │
              └────────┬─────────┘
                       │
                       ▼
                Research Report
                       │
                       ▼
              ┌──────────────────┐
              │  Research Critic │
              │   Groq + LLM     │
              └────────┬─────────┘
                       │
                       ▼
                 Final Feedback
```

---

## 🛠️ Tech Stack

| Technology    | Purpose                                    |
| ------------- | ------------------------------------------ |
| Python        | Programming language                       |
| LangChain     | Agent and LLM orchestration                |
| Groq          | Fast LLM inference                         |
| Tavily        | Web search                                 |
| Requests      | HTTP requests                              |
| BeautifulSoup | Web scraping                               |
| python-dotenv | Environment variable management            |
| uv            | Virtual environment and package management |

---

## 📁 Project Structure

```text
AI-Research-Agent/
│
├── agents.py
├── tools.py
├── main.py
├── requirements.txt
├── .env
├── .gitignore
└── README.md
```

### `agents.py`

Contains:

* Groq LLM configuration
* Search Agent
* Reader Agent
* Writer Chain
* Critic Chain

### `tools.py`

Contains the tools used by the agents:

```text
web_search()
scrape_url()
```

### `main.py`

Runs the complete research pipeline.

---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/your-username/AI-Research-Agent.git
cd AI-Research-Agent
```

### 2. Create a virtual environment

This project uses `uv`.

```bash
uv venv
```

Activate it on Windows:

```powershell
.venv\Scripts\activate
```

### 3. Install dependencies

```bash
uv pip install -r requirements.txt
```

---

## 📦 Requirements

Example `requirements.txt`:

```txt
langchain
langchain-groq
tavily-python
python-dotenv
requests
beautifulsoup4
```

---

## 🔑 API Keys

Create a `.env` file in the root directory:

```env
GROQ_API_KEY=your_groq_api_key
TAVILY_API_KEY=your_tavily_api_key
```

Do **not** commit `.env` to GitHub.

Add the following to `.gitignore`:

```gitignore
.env
.venv/
__pycache__/
```

---

## 🤖 Groq Model Configuration

The project uses LangChain's Groq integration:

```python
from langchain_groq import ChatGroq
import os

llm = ChatGroq(
    model="your-groq-model",
    temperature=0,
    api_key=os.getenv("GROQ_API_KEY")
)
```

The same LLM is used by the research agents and chains.

---

## 🔍 Web Search

The Search Agent uses Tavily to find relevant web resources.

The search tool returns:

```text
Title
URL
Snippet
```

These results are then passed to the Reader Agent.

---

## 🌐 Web Scraping

The Reader Agent uses:

```text
Requests
+
BeautifulSoup
```

to retrieve webpage content.

Unnecessary HTML elements such as:

```text
<script>
<style>
<nav>
<footer>
```

are removed before the content is passed to the LLM.

---

## 🔄 Research Pipeline

### Step 1 — Search

The Search Agent receives the user's topic and searches the web.

```text
User Topic
    ↓
Tavily
    ↓
Search Results
```

### Step 2 — Read

The Reader Agent selects relevant URLs and retrieves deeper content.

```text
Search Results
      ↓
Relevant URLs
      ↓
Web Scraper
      ↓
Detailed Content
```

### Step 3 — Write

The Writer Chain combines the gathered information:

```text
Search Results
      +
Scraped Content
      ↓
Research Report
```

The report contains:

```text
Introduction

Key Findings
1. ...
2. ...
3. ...

Conclusion

Sources
```

### Step 4 — Critic

The Critic Chain reviews the generated report and produces:

```text
Score: X/10

Strengths:
- ...
- ...

Areas to Improve:
- ...
- ...

One line verdict:
...
```

---

## ▶️ Running the Project

Activate the virtual environment:

```powershell
.venv\Scripts\activate
```

Run the application:

```bash
python main.py
```

Enter a topic:

```text
Enter a research topic: Impact of artificial intelligence on education
```

The pipeline then executes:

```text
Step 1 → Search Agent
Step 2 → Reader Agent
Step 3 → Writer
Step 4 → Critic
```

---

## 🎯 Project Goal

The goal of this project is to automate the traditional research workflow:

```text
Search
  ↓
Collect Sources
  ↓
Read Information
  ↓
Generate Report
  ↓
Review Report
```

Instead of manually searching multiple websites and writing a report, the AI pipeline coordinates these tasks using agents and tools.

---

## 🔮 Future Improvements

* [ ] Improve source and URL extraction
* [ ] Scrape multiple sources instead of one
* [ ] Add source credibility verification
* [ ] Add automatic citations
* [ ] Generate PDF reports
* [ ] Add a web interface
* [ ] Add research history
* [ ] Add parallel research agents
* [ ] Add source deduplication
* [ ] Add database support
* [ ] Improve error handling
* [ ] Add LangGraph workflow orchestration

---

## ⚠️ Limitations

* Some websites may block automated scraping.
* Dynamically rendered websites may not return complete content.
* Search quality depends on Tavily results.
* AI-generated information should be verified against the original sources.
* The quality of the final report depends on the quality of retrieved sources.

---

## 👨‍💻 Author

**Your Name**

Built with:

```text
Python
LangChain
Groq
Tavily
BeautifulSoup
uv
```

---

## ⭐ Project Workflow

```text
                  ┌──────────────┐
                  │  User Topic  │
                  └──────┬───────┘
                         ↓
                  ┌──────────────┐
                  │ Search Agent │
                  │    Tavily    │
                  └──────┬───────┘
                         ↓
                  ┌──────────────┐
                  │ Reader Agent │
                  │   Scraper    │
                  └──────┬───────┘
                         ↓
                  ┌──────────────┐
                  │    Writer    │
                  │  Groq + LLM  │
                  └──────┬───────┘
                         ↓
                  ┌──────────────┐
                  │    Critic    │
                  │  Groq + LLM  │
                  └──────┬───────┘
                         ↓
                  ┌──────────────┐
                  │Final Feedback│
                  └──────────────┘
```
