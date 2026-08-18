# HeatShift

**Move compute. Not heat.**

HeatShift is a temperature-aware compute orchestration prototype built for the FortyGuard Hackathon'26.

It uses hyperlocal thermal intelligence to optimize where and when flexible compute workloads execute.

## Core Idea

Traditional compute schedulers consider variables such as:

- GPU availability
- hardware compatibility
- capacity
- workload deadlines

HeatShift adds another input:

**the physical thermal environment.**

By incorporating time-varying thermal conditions into workload scheduling, HeatShift evaluates whether flexible workloads can be shifted between eligible sites or execution windows to reduce estimated cooling and electricity costs.

## Repository

- `frontend/` — Next.js interface
- `backend/` — FastAPI application
- `optimizer/` — scheduling/optimization logic
- `tests/` — integration tests
- `docs/` — product and technical documentation
- `AGENTS.md` — instructions for coding agents

## Status

Initial development.
