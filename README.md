# LedgerGuard

**A financial safety layer for AI agents.**

LedgerGuard evaluates financial actions before they're executed, combining AI-based risk detection, deterministic rules, and human review to catch potential problems before they happen.

Originally built at LA Hacks 2026 for the Intuit QuickBooks challenge. Now independently maintained and developed by [Mira Bhakta](https://github.com/mirabhakta).

## Why LedgerGuard?

As AI agents become more involved in accounting and financial workflows, they need safeguards beyond simply generating a response.

An agent might attempt to pay an invoice twice, send money to an unfamiliar account, or act without enough information.

LedgerGuard sits between an agent's proposed action and its execution, evaluating whether that action should proceed, require approval, or be blocked.

## How It Works

1. **An agent proposes an action.** A payment, vendor update, or other financial operation enters the evaluation pipeline.
2. **AI evaluates the risk.** Models examine the action and its context for duplicates, anomalies, and other warning signs.
3. **Rules make the decision.** A separate policy engine determines whether the action is allowed, blocked, or needs additional review.
4. **Humans stay in control.** Actions requiring approval are routed for review, with decisions recorded for auditing.

AI models provide risk assessments, but never directly authorize financial actions.

## Features

- **Risk detection** — Identify duplicate payments, unusual transactions, and suspicious changes.
- **Policy engine** — Enforce deterministic financial rules independently of model predictions.
- **Human review** — Approve, reject, or request additional context for flagged actions.
- **Decision history** — Track actions, explanations, and outcomes through an audit trail.
- **Provider benchmarks** — Compare Gemini, System One, OpenJev, and rules-based evaluation.
- **Interactive dashboard** — Explore simulated transactions, risk assessments, and system activity.

## Tech Stack

| Area | Technologies |
|---|---|
| Frontend | React, TypeScript, Vite |
| Backend | Python, FastAPI |
| AI | Gemini, System One (Jev), OpenJev |
| Orchestration | LangGraph |
| Database | SQLite |
| Evaluation | Python, custom benchmark framework |

## Getting Started

### Requirements

- Python 3.12
- Node.js and npm
- API keys for optional external AI providers

### Backend

```bash
git clone https://github.com/mirabhakta/LedgerGuard.git
cd LedgerGuard

python3.12 -m venv .venv
source .venv/bin/activate
pip install -e '.[dev]'
```

Copy `.env.example` to `.env` and configure the providers you want to use.

```bash
PYTHONPATH=. pytest -q
PYTHONPATH=. uvicorn backend.app.main:app --reload
```

The API runs at `http://localhost:8000`.

On Windows, activate the virtual environment using `.venv\Scripts\Activate.ps1`.

### Frontend

```bash
cd frontend
npm install
npm run dev
```

Open `http://localhost:5173`.

Some scenarios require the original hackathon dataset. See the documentation for configuration details.

## Development

LedgerGuard is an ongoing project. Current areas of development include improving risk evaluation, expanding financial scenarios, and making the review and decision workflows more useful beyond the original hackathon demo.

## Documentation

- [Architecture](docs/architecture.md)
- [API Reference](docs/API_HANDOFF.md)
- [Testing Guide](docs/FASTAPI_TESTING.md)
- [Evaluation Plan](docs/EVAL_PLAN.md)

## Project History

LedgerGuard started as a collaborative project at LA Hacks 2026. The original hackathon contributions remain credited through the repository's Git history.

Ongoing development and maintenance are led independently by Mira Bhakta.

---

**Note:** LedgerGuard is an experimental prototype. Financial actions are simulated, and the project is not intended for production payment processing.
