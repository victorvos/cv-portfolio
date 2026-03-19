# Systemic Lag Trader — BTC / prediction-market agent

**Dashboard:** [btc.daromvibenews.com](https://btc.daromvibenews.com)

*Experimental system—not financial advice; intended for research and controlled environments.*

Pipeline that looks for **systemic lag** between fast headlines (social / RSS) and slower wire-style confirmation: staged LLM passes reduce noise, estimate short-horizon edge using live crypto context, then apply risk rules before any optional execution (Polymarket path; dry-run by default).

## Technical Stack

| Component | Technology |
|-----------|------------|
| **Backend** | FastAPI, Python 3.12+, Pydantic Settings |
| **Orchestration** | LangGraph (`StateGraph`), scheduled multi-agent cycles |
| **AI / LLM** | xAI Grok (discovery), Perplexity (verification), Google Gemini (edge / regime) |
| **Market data** | CoinGecko (BTC/ETH/SOL context), Polymarket CLOB/Gamma |
| **Persistence** | Firebase Firestore (production audits), JSONL signal memory & trade logs |
| **Frontend** | Dashboard UI with WebSocket live updates |
| **Deployment** | Docker on VPS; TLS and routing via Caddy |

## Architecture (inverted pyramid)

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'darkMode': true, 'background': '#121212', 'primaryColor': '#1e1e1e', 'primaryTextColor': '#ffffff', 'primaryBorderColor': '#f7931a', 'lineColor': '#808080', 'textColor': '#ffffff'}}}%%
flowchart TB
    subgraph Discovery
        G[Grok + RSS feeds]
        M[Signal memory JSONL]
    end
    subgraph Filter
        P[Perplexity verification]
    end
    subgraph Edge
        GM[Gemini + price context]
        R[Regime: Bull / Bear / Sideways]
    end
    subgraph Action
        B[Contextual bandit]
        PF[Portfolio / risk limits]
        PM[Polymarket gateway]
    end
    G --> M
    M --> P
    P --> GM
    GM --> R
    R --> B
    B --> PF
    PF --> PM
```

## Key features

### Pipeline
- Discovery via Grok and RSS; short retention of pending headlines for later re-checks.
- Verification pass (e.g. Perplexity) against secondary sources.
- Edge estimation with Gemini using BTC/ETH/SOL context from CoinGecko.

### Risk and feedback
- Position sizing caps, daily loss context, and explicit exit / panic rules.
- Optional hibernation when markets are quiet to limit API use.
- Outcome backfill to tune a contextual bandit and regret-style cutoffs.

### Operations
- Scheduled cycles plus manual `POST /run-once`; dashboard with WebSocket metrics for monitoring.

## Skills demonstrated

- **Orchestration:** LangGraph graphs that merge persisted signals with fresh feeds.
- **LLM boundaries:** Separate stages for breadth vs. verification vs. decision support.
- **Observability:** Structured logs, optional Firestore audit trail, containerized deployment.
- **Decision hygiene:** Bandit-style exploration with explicit risk and regime hooks—not always-on trading.
