# HeatShift — Agent Instructions

## Mission

We are building HeatShift for the FortyGuard Hackathon'26.

HeatShift is a temperature-aware compute orchestration platform.

It uses FortyGuard's hyperlocal, time-varying thermal intelligence to determine where and when flexible compute workloads should run in order to reduce total operating cost while respecting workload deadlines, hardware requirements, capacity constraints, and service requirements.

Core idea:

MOVE COMPUTE. NOT HEAT.

The objective is not maximum feature count.

The objective is to create the strongest possible hackathon product:
- immediately understandable
- technically credible
- commercially compelling
- visually impressive
- genuinely dependent on FortyGuard
- fully demonstrable

---

## Product Thesis

AI infrastructure consumes substantial electricity and requires cooling.

Compute workloads differ in flexibility.

Some workloads must run immediately.
Others can move:
- between eligible compute sites
- between time windows
- or both

Thermal conditions also vary by location and time.

HeatShift combines these facts.

Instead of scheduling flexible compute based only on GPU availability, it incorporates predicted local thermal conditions and estimated cooling overhead into workload placement.

HeatShift should answer:

"Given these workloads and compute sites, where and when should each workload run to minimize total operating cost while satisfying all operational constraints?"

---

## Winning Principle

Do not build a temperature dashboard.

Do not build a generic chatbot.

Do not simply display hotter and cooler data centers.

Every important feature should move the product toward:

"Because thermal conditions will change this way, this workload should execute HERE at THIS TIME, producing THIS measurable economic effect."

---

## Core Demonstration

The demo compares two schedulers operating on exactly the same:

- compute sites
- GPU capacities
- workloads
- deadlines
- hardware requirements
- electricity pricing assumptions
- thermal conditions

### Baseline Scheduler

Optimizes workload placement without hyperlocal thermal intelligence.

### HeatShift Scheduler

Adds the thermal/cooling component to workload placement.

Compare calculated metrics such as:

- workloads completed
- workload deadlines satisfied
- GPU-hours
- estimated computing energy
- estimated cooling energy
- estimated total energy
- estimated electricity cost
- peak demand
- workload migrations/delays

Never fabricate improvement percentages.

Every displayed result must be calculated by the system.

---

## Product Priorities

In order:

1. Killer 3-minute demo
2. Clear monetary value
3. Technically defensible calculations
4. Meaningful FortyGuard dependency
5. Reliable end-to-end functionality
6. Excellent visualization
7. Explainability
8. Additional functionality

Never sacrifice priorities 1-6 for feature count.

---

## MVP User Flow

1. User opens a map of several compute sites.
2. User sees pending compute workloads.
3. User views thermal conditions evolving over time.
4. Baseline scheduler runs.
5. Baseline cost/energy metrics are displayed.
6. User clicks "Optimize with HeatShift."
7. HeatShift calculates optimized workload placement.
8. Workloads visibly move between sites and/or time windows.
9. Baseline and HeatShift metrics are compared.
10. User can inspect a workload and understand why it moved.

---

## Engineering Stack

Default stack unless a clearly better reason emerges:

Frontend:
- Next.js
- TypeScript
- Tailwind CSS
- MapLibre GL
- charting library only when needed

Backend:
- Python
- FastAPI
- Pydantic
- httpx

Optimization:
- Python
- Google OR-Tools

Testing:
- pytest
- TypeScript type checking
- frontend tests where valuable

Do not introduce unnecessary infrastructure.

---

## Architecture

Preferred direction:

Browser
→ Next.js
→ FastAPI
→ FortyGuard Adapter
→ Thermal Model
→ Cooling/Energy Model
→ HeatShift Optimizer

The optimizer must not depend directly on raw FortyGuard response structures.

External APIs should be behind adapters.

---

## Data Integrity

Every number shown to users must belong to one of these categories:

1. External observed/forecast data
2. Derived/calculated value
3. Explicit modeling assumption
4. Synthetic demo input

These categories must never be silently mixed.

Never fabricate:
- temperatures
- energy savings
- electricity prices
- cooling efficiencies
- PUE values
- carbon reductions
- workload performance
- API responses

Assumptions must be documented.

---

## Thermal / Energy Modeling

The hackathon prototype does not need to claim perfect physical simulation.

It DOES need a model that is:

- transparent
- documented
- internally consistent
- testable
- defensible

Start simple.

Example conceptual relationship:

Outside thermal conditions
→ estimated cooling overhead
→ facility energy
→ operating cost

If stronger validated models become practical, they may replace simpler assumptions later.

---

## Optimization

The optimizer should be deterministic for identical inputs.

Conceptually minimize something like:

total_cost =
    compute_energy_cost
    + cooling_energy_cost
    + workload_delay_penalty
    + migration_penalty
    + SLA_penalty

Subject to constraints such as:

- site GPU capacity
- hardware compatibility
- workload duration
- earliest start
- deadline
- workloads cannot execute twice
- mandatory workloads must complete
- site availability

Do not use an LLM to numerically assign workloads.

---

## AI Usage

LLMs may be used for:

- explaining optimizer decisions
- summarizing tradeoffs
- interpreting results
- natural-language interaction

Preferred flow:

FortyGuard
→ thermal model
→ energy model
→ optimizer
→ structured result
→ optional LLM explanation

Not:

FortyGuard
→ LLM
→ guessed scheduling decision

---

## Demo Mode

Support deterministic demo operation.

Demo mode may contain:

- synthetic compute sites
- synthetic workload queue
- deterministic GPU capacities
- documented electricity-price assumptions
- cached real thermal responses where permitted

Demo/synthetic information must always be clearly distinguishable from live information.

The demo must not completely fail because an external endpoint is temporarily unavailable.

---

## Security

Never commit:

- API keys
- credentials
- access tokens
- secrets

Use environment variables.

Never expose server-side credentials to browser code.

---

## Scope Control

Do NOT build unless clearly justified:

- authentication
- billing
- user accounts
- Kubernetes
- microservices
- production databases
- mobile apps
- generic chatbot
- custom foundation models
- complicated admin systems
- unnecessary infrastructure

---

## Demo-First Development

Before implementing a substantial feature ask:

"Does this materially improve the final judging demonstration?"

If not, deprioritize it.

Maintain a functional end-to-end demo throughout development.

---

## Engineering Rules

Before implementation:

1. Read relevant project documentation.
2. Inspect existing code.
3. Understand current interfaces.
4. Choose the simplest defensible solution.

Before declaring a task complete:

1. Run relevant tests.
2. Run type checking.
3. Run linting where configured.
4. Verify builds.
5. Check primary demo flow.
6. Report anything that could not be verified.

Never claim code works merely because it was written.

---

## Decision Rule

When several approaches are viable, prefer the approach that:

1. improves the judging demo
2. produces measurable economic value
3. strengthens FortyGuard's role
4. is technically defensible
5. can be completed reliably
6. is easy to explain
7. minimizes complexity

---

## Definition of Done

A feature is done when:

- it functions end-to-end
- important logic is tested
- failures are handled
- assumptions are documented
- outputs are traceable to data/calculation
- no secrets are exposed
- the demo remains functional
