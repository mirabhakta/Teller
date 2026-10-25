# Teller

**A second check before AI agents move money.**

Teller reviews financial actions before they're carried out. It combines AI-based risk analysis with a rules engine to catch suspicious activity, flag missing information, and decide when a person needs to step in.

Originally built at LA Hacks 2026 for the Intuit QuickBooks challenge, Teller is now independently maintained by [Mira Bhakta](https://github.com/mirabhakta).

## The Idea

AI agents are starting to handle more financial tasks, from processing invoices to managing payments. But even when an action looks reasonable, something might be wrong.

An invoice could already be paid. A vendor's payment details might have changed. An agent might be acting without enough context.

Teller checks these actions before they go through, rather than trying to catch mistakes afterward.

## How It Works

Every proposed action goes through a series of checks:

1. **Evaluate** — Check the action against existing records and financial rules.
2. **Analyze** — Use AI to identify potential duplicates, unusual activity, or missing context.
3. **Decide** — Apply deterministic policies to determine what happens next.
4. **Review** — Send flagged actions to a human when approval or more information is needed.

The system produces four possible decisions:

| Decision | What happens |
|---|---|
| `ALLOW` | The action passes the checks. |
| `REQUIRE_APPROVAL` | A person must review the action. |
| `REQUEST_CONTEXT` | More information is needed. |
| `BLOCK` | The action is stopped. |

AI evaluates the risks, but the policy engine makes the final decision.

## Features

- **Transaction analysis** — Detect duplicate payments, unusual amounts, and suspicious changes.
- **Human review** — Review flagged actions before allowing them to proceed.
- **Decision history** — Keep a record of evaluations, approvals, and outcomes.
- **Provider comparisons** — Benchmark different models and rules-based approaches.
- **Interactive dashboard** — Explore financial scenarios, decisions, and activity.
- **Real-time updates** — Follow evaluations as they happen through Server-Sent Events.

## Built With

| | Technologies |
|---|---|
| Frontend | React, TypeScript, Vite |
| Backend | Python, FastAPI |
| AI | Gemini, System One (Jev), OpenJev |
| Workflows | LangGraph |
| Database | SQLite |
| Evaluation | Python, custom benchmarking tools |

## Getting Started

**Requirements:** Python 3.12, Node.js, and npm.

### 1. Clone the repository

```bash
git clone https://github.com/mirabhakta/Teller.git
cd Teller
```

### 2. Set up the backend

```bash
python3.12 -m venv .venv
source .venv/bin/activate
pip install -e '.[dev]'
```

On Windows, use `.venv\Scripts\Activate.ps1` to activate the environment.

Copy `.env.example` to `.env` and configure any optional API credentials.

```bash
PYTHONPATH=. uvicorn backend.app.main:app --reload
```

### 3. Start the frontend

```bash
cd frontend
npm install
npm run dev
```

Open `http://localhost:5173`.

### 4. Run tests

From the repository root:

```bash
PYTHONPATH=. pytest -q
```

The original hackathon dataset is required for some scenarios. Rules-based evaluation and offline tests can run without external AI credentials.

## Development

Teller is still a work in progress.

I'm continuing to develop it beyond the original hackathon prototype, with a focus on improving risk evaluation, expanding supported financial workflows, and making the review experience more practical.

## Documentation

- [Architecture](docs/architecture.md)
- [API Reference](docs/API_HANDOFF.md)
- [Testing](docs/FASTAPI_TESTING.md)
- [Evaluation](docs/EVAL_PLAN.md)

## Origins

Teller began as LedgerGuard, a collaborative submission to the Intuit QuickBooks challenge at LA Hacks 2026.

The original contributors remain credited in the project's Git history. Ongoing development is independently maintained by Mira Bhakta.

---

*Currently a prototype using simulated financial actions. Teller does not execute real payments or connect to live financial accounts.*
