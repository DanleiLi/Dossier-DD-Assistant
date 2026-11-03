# Dossier

<p align="center">
  <strong>Turn a document pile into a reviewable investment brief.</strong><br />
  An evidence-first due diligence workspace with an AI agent that shows its work.
</p>

<p align="center">
  <img alt="Python FastAPI" src="https://img.shields.io/badge/Python-FastAPI-17324D?style=flat-square" />
  <img alt="React Vite" src="https://img.shields.io/badge/React-Vite-19A7A0?style=flat-square" />
  <img alt="Evidence-grounded AI" src="https://img.shields.io/badge/AI-evidence--grounded-8B6CF6?style=flat-square" />
  <img alt="Evaluation prototype" src="https://img.shields.io/badge/Evaluation-prototype-F2B84B?style=flat-square" />
</p>

Dossier helps investment analysts review product documents, find evidence and gaps, run supported checks, and draft reports for human review. It is a personal job-hunting project demonstrating product thinking, workflow design, and agent evaluation.

## The workflow

Due diligence information is scattered across disclosures, questionnaires, fee schedules, portfolio materials, and meeting notes. Dossier brings the review into one project workspace and makes unknowns visible instead of guessing through them.

```mermaid
flowchart LR
    A[Documents] --> B[Ingest and index]
    B --> C[Project evidence]
    Q[Analyst question] --> D[Agent]
    C --> D
    D --> E[Retrieve evidence]
    D --> F[Check gaps]
    D --> G[Supported analysis]
    E --> R[Draft report]
    F --> R
    G --> R
    R --> H[Human review]
    H -. follow up .-> Q
    classDef input fill:#E9F5F4,stroke:#19A7A0,color:#17324D
    classDef agent fill:#EEE9FF,stroke:#8B6CF6,color:#241C42
    classDef review fill:#FFF4D8,stroke:#F2B84B,color:#3D3218
    class A,B,C,Q input
    class D,E,F,G,R agent
    class H review
```

**Design principles:** Ground claims in project evidence; distinguish facts, conflicts, and unknowns; keep agent tools bounded; leave interpretation and approval with the analyst. The orchestrator handles persistence, while retrieval stays scoped to the active project.

## Evaluation: measure the failure modes

A useful answer must be accurate against the supplied evidence, cite it correctly, cover the task, identify gaps, and handle uncertainty. The evaluation prototype proposes paired runs on the same closed evidence bundle, with anonymized outputs, atomic rubric scoring, and human review of failures, disputes, and a sample of passes.

![Illustrative all-pass task rate: Dossier 55.2%, GPT-Luna 34.3%, Claude Sonnet 29.8%. Values are user-supplied examples, not measured results.](image/evaluation-all-pass.svg)

*Illustrative values only. No benchmark has been run; these are not measured results.*

| Evaluation area | Signals |
| --- | --- |
| **Answer quality** | Relevance, factual correctness, completeness, evidence and citation support |
| **Risk handling** | Gap detection, uncertainty, material hallucinations, human judge corrections |
| **Practicality** | Cost and latency per task |

Compare results case by case, report denominators and category breakdowns, and keep material hallucinations visible. The protocol evaluates decision support, not investment outcomes or regulatory compliance.

> **Status:** Evaluation design prototype. Cases, rubric examples, and chart values are illustrative; no benchmark has been run and no performance claim is being made. Read the [evaluation protocol](eval/README.md) for methods and limitations.

## Implementation

React + Vite frontend · FastAPI backend · project-scoped document retrieval · coverage checks · supported analyses · report drafting. The tools return findings; the orchestrator records application state. See [`backend/AGENT.md`](backend/AGENT.md) and [`specs/`](specs/).

## Run locally

### Prerequisites

Python 3.12+, [`uv`](https://docs.astral.sh/uv/), Node.js, pnpm, a Supabase project, and OpenAI and Anthropic API keys. Copy `backend/.env.example` to `backend/.env` and `frontend/.env.example` to `frontend/.env`, then fill in the values. Never put the Supabase service key in the frontend env file.

### Start the app

In one terminal:

```powershell
cd backend
uv sync
uv run alembic upgrade head
uv run python run.py
```

In another terminal:

```powershell
cd frontend
pnpm install
pnpm dev
```

For Supabase credential and migration details, see the [Supabase setup](specs/guides/supabase-setup.md), [backend guide](specs/guides/backend-setup.md), and [frontend guide](specs/guides/frontend-setup.md).

| Code and product | Evaluation and data |
| --- | --- |
| [`backend/`](backend/) API and agent · [`frontend/`](frontend/) web app · [`specs/`](specs/) product and setup notes | [`eval/`](eval/) evaluation prototype · [`data/`](data/) sample and local application data |

Dossier is a working prototype, not a production due diligence service. Its outputs support analyst work and require qualified human review.
