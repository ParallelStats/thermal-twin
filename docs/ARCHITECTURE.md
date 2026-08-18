# HeatShift — Technical Architecture

## Objective

Build the simplest architecture capable of demonstrating:

thermal intelligence
→ cooling/energy estimate
→ workload optimization
→ measurable comparison

---

## Architecture

Browser
    |
    v
Next.js Frontend
    |
    v
FastAPI Backend
    |
    +--> FortyGuard Adapter
    |
    +--> Thermal Model
    |
    +--> Energy / Cooling Model
    |
    +--> HeatShift Optimizer
    |
    +--> Demo Scenario Provider

---

## Frontend

Stack:

- Next.js
- TypeScript
- Tailwind CSS
- MapLibre GL

Responsibilities:

- site map
- thermal visualization
- workload queue
- timeline
- baseline/HeatShift comparison
- charts
- workload explanations

Frontend must contain no API secrets.

---

## Backend

Stack:

- Python
- FastAPI
- Pydantic
- httpx

Responsibilities:

- API integration
- thermal normalization
- energy calculations
- workload scheduling
- scenario management
- comparison metrics
- frontend API

---

## FortyGuard Adapter

Create one isolated integration layer.

Responsibilities:

- authentication
- request execution
- asynchronous task handling if required
- status polling
- response validation
- errors / timeouts
- conversion into internal thermal models

No optimizer code should consume raw FortyGuard API JSON.

---

## Internal Thermal Model

Suggested conceptual models:

ThermalSnapshot:
- site_id
- timestamp
- temperature
- optional additional environmental parameters

ThermalProfile:
- site_id
- snapshots[]

The exact schema may evolve.

---

## Compute Site Model

Site:
- id
- name
- latitude
- longitude
- GPU types
- GPU capacity
- baseline facility parameters

---

## Workload Model

Workload:
- id
- name
- GPU type
- GPU count
- duration
- earliest_start
- deadline
- priority
- movable_sites

---

## Energy Model

Build a transparent model connecting:

compute workload
+ site characteristics
+ environmental conditions
→ estimated total facility energy

Keep the first implementation simple and documented.

Do not pretend the model has production-grade physical accuracy.

---

## Optimizer

Use deterministic optimization.

Preferred:
- Google OR-Tools

Input:
- sites
- workloads
- capacities
- time slots
- thermal profiles
- energy model
- weights

Output:
- site assignment
- start time
- finish time
- objective breakdown
- estimated energy/cost metrics

---

## Baseline Optimizer

Use identical operational constraints.

Exclude thermal-aware cooling optimization.

This isolates the value contributed by HeatShift.

---

## API

Initial endpoints may include:

GET /health

GET /api/scenario

POST /api/thermal/analyze

POST /api/schedule/baseline

POST /api/schedule/optimize

POST /api/compare

Keep routes simple and revise if needed.

---

## Demo Mode

DEMO_MODE=true

Demo mode supports:

- deterministic sites
- deterministic workloads
- deterministic energy assumptions
- cached thermal fixtures where appropriate

Clearly label demo/cached/synthetic data.

---

## Testing

Optimizer tests:
- capacity
- incompatible hardware
- deadlines
- insufficient capacity
- deterministic result
- thermal differences influence placement

Energy-model tests:
- reproducibility
- boundary cases
- monotonic behavior where expected

Backend:
- API validation
- adapter error handling

Frontend:
- type checking
- critical UI behavior

---

## Security

Server-side environment variables only.

Never expose API credentials in:
- browser bundles
- NEXT_PUBLIC variables
- Git
- logs

---

## Architectural Rule

Do not optimize infrastructure before the end-to-end product works.

The most important pipeline is:

real/cached thermal data
→ energy estimate
→ optimizer
→ visible workload movement
→ cost comparison
