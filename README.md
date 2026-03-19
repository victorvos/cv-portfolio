# Victor Vos - Data Engineering & AI Portfolio

Data Engineer with a Computer Science BSc, focused on data pipelines, AI-assisted applications, and backend-heavy web systems. Comfortable shipping containerized services that combine LLMs with conventional data stores and APIs.

## Table of Contents
- [Core Competencies](#core-competencies)
- [Technical Skills](#technical-skills)
- [Personal Projects](#personal-projects)
- [Work Experience](#work-experience)
- [Education](#education)

## Core Competencies

### Data Engineering
- ETL/ELT pipeline design and implementation
- Cloud data warehouse integration (Snowflake, Firebase)
- Data modeling and schema design
- Real-time data processing with WebSockets
- Embedding-backed semantic search where appropriate

### AI & Machine Learning Integration
- LLM orchestration with LangGraph and LangChain
- Multi-model AI pipelines (Gemini, GPT, Grok, Perplexity)
- Prompt engineering and agentic workflows
- Vector embeddings for semantic similarity search

### Backend Development
- Python (FastAPI, Flask, Pydantic)
- Node.js (Express, Socket.io)
- Clean Architecture and SOLID principles
- Async programming patterns

### DevOps & Infrastructure
- Docker containerization
- Azure DevOps CI/CD pipelines
- Cloud deployment (Hetzner, Firebase)
- Caddy reverse proxy configuration

### Test-Driven Development & AI-Assisted Programming
- Test-first methodology enabling confident refactoring
- Comprehensive test suites as living documentation
- AI pair programming with test alignment for reduced errors
- Tests serve as guardrails for AI-generated code validation
- Rapid iteration cycles with automated regression detection

## Technical Skills

| Category | Technologies |
|----------|-------------|
| **Programming** | Python, JavaScript, TypeScript, SQL |
| **Backend Frameworks** | FastAPI, Flask, Express.js |
| **Data Platforms** | Snowflake, Firebase Firestore, Firebase Realtime DB |
| **AI/ML** | LangGraph, LangChain, OpenAI API, Google Gemini, Grok, Perplexity |
| **DevOps** | Docker, Azure DevOps, GitHub Actions |
| **Web Scraping** | Crawl4AI, Playwright, BeautifulSoup |
| **Frontend** | Jinja2, Leaflet.js, Socket.io, Tkinter |
| **Testing** | pytest, Jest, unittest |
| **Spoken** | Dutch (native), English (fluent) |
| **Legacy/Other** | Java, C#, .NET, Qlik Sense, Elastic Stack, SOAP, XML |

## Personal Projects

### [Darom - AI-Powered News Platform](projects/darom.md)
**Production app live at [daromvibenews.com](https://daromvibenews.com)**

Full-stack news site with LangGraph-backed editorial workflows and usage-based billing.

**Key Technologies:** FastAPI, Firebase, Gemini 3 Flash, Grok, Perplexity, LangGraph, WebSockets

**Highlights:**
- Multi-agent article generation with automated fact-checking
- Real-time WebSocket communication for live updates
- Credit economy with reserve-and-refund billing system
- Lower auxiliary API spend through targeted caching (e.g. social insights)

---

### [Systemic Lag Trader — BTC Agent](projects/systemic-lag-trader.md)
**[btc.daromvibenews.com](https://btc.daromvibenews.com/dashboard)**

Research-oriented trading automation: staged LLM pipeline (discovery → verification → edge estimate) with explicit risk limits and optional Polymarket integration (dry-run by default).

**Key Technologies:** FastAPI, LangGraph, Grok, Perplexity, Google Gemini, CoinGecko, Polymarket, Firestore, WebSockets, Docker

**Highlights:**
- Multi-stage “inverted pyramid” pipeline with on-disk signal memory for delayed re-verification
- Portfolio sizing, daily stop-loss context, volatility hibernate, and contextual bandit learning
- Real-time dashboard with WebSocket updates; deployed on Hetzner behind Caddy

---

### [MapsAI - Real Estate Intelligence Platform](projects/mapsai.md)
**[maps.daromvibenews.com](https://maps.daromvibenews.com)**

Interactive map for Dutch property listings: scraping, structured extraction, and search over Firestore-backed data.

**Key Technologies:** FastAPI, Firebase, Crawl4AI, OpenAI, LangChain / LangGraph, Leaflet.js, embeddings

**Highlights:**
- LLM-assisted extraction from listing pages
- Interactive map with property clustering
- Semantic search using vector embeddings
- Real-time property updates via WebSockets

---

### [Snowflake Package Sync Pipeline](projects/snowflake-pipeline.md)
**Python package sync to Snowflake stages**

Tooling and pipelines to bundle dependencies and upload them to Snowflake for in-warehouse Python workloads.

**Key technologies:** Python, Snowflake, Azure DevOps, Azure Pipelines

**Highlights:**
- ProGet and/or PyPI sources as configured
- Repeatable ZIP/stage uploads via pipeline
- Tests with mocked external calls

---

### [Media Automation Suite](projects/media-automation.md)
**Docker-based media transfer and organization**

Python CLIs for seeding a NAS from remote sources and for semi-automated sorting of media files.

**Key technologies:** Python, Docker, rclone, qBittorrent Web API, lightweight classification

**Highlights:**
- Transfer progress, integrity checks, stall detection, retries
- User-in-the-loop suggestions that improve from feedback
- Rich terminal UI; pytest coverage

## Work Experience

### STB Automatisering | Data Intern
**2018** | Houten, Netherlands

Created fundraising analysis dashboards for charity organizations.

- Developed Qlik Sense dashboards to map fundraising revenue
- Tailored solutions for specific clients like "het Reumafonds"
- **Technologies:** Qlik Sense, SQL

### A.S.R. Verzekeringen N.V. | Data Science Graduate Intern
**2019** | Utrecht, Netherlands

Developed strategic HR dashboards for the Executive Board using the Elastic Stack.

- Modeled job automation vulnerability using McKinsey robotics models
- Implemented Elastic Stack for HR data visualization
- **Technologies:** Elastic Stack (ELK), SQL, Excel

### UWV | Data Analyst
**2019 - 2021** | Utrecht, Netherlands

Improved management insights by creating automated dashboards and data pipelines.

- Built Excel dashboards fueled by data pipelines from multiple sources
- Merged and transformed data using Power Query and SQL
- Provided management with clear insights into service delivery order states
- **Technologies:** Power BI, SQL, Power Query, Excel

### PGGM | Data Engineer / Automation Engineer
**January 2023 - Present** | Zeist, Netherlands

Data Engineer specializing in automation solutions for pension fund administration. Building and maintaining data pipelines, ETL processes, and internal tooling for one of the largest pension fund service providers in the Netherlands.

**Key Responsibilities:**
- Design and implement ETL pipelines for pension fund data processing
- Develop Python CLI applications for internal automation workflows
- Build API integrations to retrieve and synchronize data from external parties
- Implement CI/CD pipelines using Azure DevOps for automated deployments
- Database development and optimization for pension administration systems
- Create and maintain unit tests to ensure code quality and enable safe refactoring

**Technologies:** Python, SQL, Azure DevOps, CI/CD Pipelines, REST APIs, Database Development

## Education

**Bachelor of Science in Computer Science**
*HBO-ICT - Software & Information Engineering | Hogeschool Utrecht (2015 - 2019)*
- Specialization in Software Architecture, Data Science, and Object-Oriented Analysis

**BSc Econometrics and Operations Research** (Coursework)
*University of Groningen (2012 - 2014)*

**University Preparation Year**
*Oxford, United Kingdom (2011 - 2012)*
- International cultural exchange and advanced English studies

### Academic Projects
- **Air Quality Analysis (Vietnam):** IoT/BI project researching air quality using smart devices (Minor).
- **Educational Math App:** Android application for children aged 4-12 (Java).
- **E-commerce Platform:** Full-stack web shop implementation (Java/JavaScript).

---

*Portfolio last updated: March 2026*

## Mirror on GitHub

This tree is also published as its own repository: [github.com/victorvos/cv-portfolio](https://github.com/victorvos/cv-portfolio).

From the monorepo root (`Developer`), after committing changes under `CV/`:

```bash
git fetch cv-portfolio
git subtree split --prefix=CV -b cv-portfolio-split
git push cv-portfolio cv-portfolio-split:master --force-with-lease=cv-portfolio/master
git branch -D cv-portfolio-split
```

The remote `cv-portfolio` must exist once:  
`git remote add cv-portfolio https://github.com/victorvos/cv-portfolio.git`

If the lease step rejects (e.g. you intend to replace whatever is on `master`), use `--force` instead of `--force-with-lease`.
