# Darom - AI-Powered News Platform

**Live Production:** [daromvibenews.com](https://daromvibenews.com)

Full-stack AI content generation platform featuring multi-agent workflows, real-time updates, and a credit-based economy.

## Technical Stack

| Component | Technology |
|-----------|------------|
| **Backend** | FastAPI, Python 3.11+, Pydantic |
| **AI/LLM** | Gemini 3 Flash, Grok, Perplexity, LangGraph |
| **Database** | Firebase Firestore |
| **Real-time** | WebSockets, Server-Sent Events |
| **Frontend** | Jinja2, JavaScript ES6 Modules |
| **Deployment** | Docker, Hetzner VPS, Caddy |

## Architecture

```mermaid
graph TB
    subgraph "Frontend"
        A[Jinja2 Templates]
        B[WebSocket Client]
    end
    
    subgraph "Backend"
        C[FastAPI Routes]
        D[LangGraph Orchestrator]
        E[AI Service Layer]
    end
    
    subgraph "AI Models"
        F[Gemini 3 Flash]
        G[Grok xAI]
        H[Perplexity]
    end
    
    subgraph "Data"
        I[Firebase Firestore]
        J[Credit System]
    end
    
    A --> C
    B --> C
    C --> D
    D --> E
    E --> F
    E --> G
    E --> H
    C --> I
    C --> J
    
    style A fill:#e1f5fe,stroke:#01579b,stroke-width:2px,color:#000000
    style D fill:#f3e5f5,stroke:#4a148c,stroke-width:2px,color:#000000
    style F fill:#fff8e1,stroke:#e65100,stroke-width:2px,color:#000000
```

## Key Features

### Multi-Agent Article Generation
- LangGraph-powered agentic workflow for article creation
- Automated fact-checking with AI verification
- Multi-source research using Perplexity search
- Stateful editor with checkpoint/resume capability

### Credit Economy System
- Reserve-and-refund billing model
- Estimated cost calculation before generation
- Automatic refund on partial completion
- Token usage tracking across all AI providers

### Real-Time Communication
- WebSocket-based live updates during generation
- Server-Sent Events for progress streaming
- Community presence indicators

## Skills Demonstrated

- **AI/ML Integration:** Orchestrating multiple LLM providers with fallback strategies
- **Async Programming:** Complex async workflows with proper error handling
- **Clean Architecture:** SOLID principles with repository pattern
- **Cost Optimization:** 95% reduction through smart caching and model selection
- **Production Deployment:** Docker containerization with Caddy reverse proxy
