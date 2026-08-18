# HeatShift — Product Specification

## One-Line Pitch

HeatShift uses hyperlocal thermal intelligence to move flexible compute workloads to the best site and time window, reducing cooling and energy costs without violating workload requirements.

## Tagline

MOVE COMPUTE. NOT HEAT.

---

## Problem

Compute orchestration commonly considers:

- GPU availability
- hardware type
- workload priority
- latency
- deadline
- capacity
- electricity cost

But the physical environment surrounding compute infrastructure also influences cooling requirements.

Thermal conditions vary across space and time.

Flexible workloads create an opportunity:

If a workload can execute at several eligible sites or times, workload placement can incorporate predicted thermal conditions rather than treating environmental conditions as irrelevant.

---

## Product

HeatShift adds temperature intelligence to compute scheduling.

Inputs:

- compute sites
- GPU capacity
- hardware types
- workload queue
- workload duration
- deadlines
- location
- thermal conditions
- energy assumptions
- optional electricity prices

Output:

- workload assignment
- site
- start time
- completion time
- estimated compute energy
- estimated cooling overhead
- estimated total cost
- comparison against baseline

---

## Target Customer

Initial commercial concept:

Operators of geographically distributed AI / compute infrastructure with flexible workloads.

Potential future customers:

- GPU cloud providers
- edge compute operators
- private AI infrastructure
- distributed rendering infrastructure
- research compute networks
- large enterprise GPU fleets

The hackathon MVP does not need integrations with real customer infrastructure.

---

## MVP Scenario

Create several realistic compute sites.

Each site has:

- geographic location
- available GPU capacity
- supported GPU type
- base efficiency characteristics

Create a workload queue.

Each workload has:

- ID
- required GPU count
- required GPU type
- expected duration
- earliest start
- deadline
- flexibility
- priority

HeatShift receives thermal information for each site over time.

It then chooses workload placement.

---

## Baseline

The baseline scheduler uses the same:

- sites
- workloads
- hardware
- capacity
- deadlines

but does NOT optimize based on hyperlocal thermal conditions.

This produces a fair comparison.

---

## HeatShift Objective

Conceptually:

minimize:

Compute Energy Cost
+ Cooling Energy Cost
+ Delay Penalties
+ Migration Penalties
+ SLA Penalties

while satisfying all hard operational requirements.

---

## Core Metrics

Display only calculated metrics.

Primary:

- workloads completed
- deadlines met
- total GPU-hours
- estimated compute energy
- estimated cooling energy
- estimated total energy
- estimated total electricity cost

Secondary:

- peak demand
- workloads moved
- average delay
- thermal exposure of facility workload

---

## Killer Demo

Show a map containing multiple compute sites.

Show a timeline:

NOW ---------------- +12 HOURS

Thermal conditions evolve on the map.

Show a queue of workloads.

Run:

BASELINE

Then show:
- workload placement
- cost
- energy

Then click:

OPTIMIZE WITH HEATSHIFT

Animate flexible workloads moving between sites/time windows.

Then display:

BASELINE vs HEATSHIFT

The strongest demo output is a simple measurable tradeoff such as:

Same workloads completed
Same deadlines satisfied
Lower estimated operating cost

The actual improvement must be calculated by the system.

---

## Explainability

Selecting a workload should show something like:

Workload #184

Baseline:
Site A
14:00

HeatShift:
Site C
11:30

Reason:
- compatible GPU capacity
- deadline preserved
- lower estimated cooling overhead during execution window

Estimated impact:
calculated from the model

---

## Safety / Productivity Slider Equivalent

Stretch feature:

COST SAVINGS <-----> SPEED

or:

LOWEST COST <-----> EARLIEST COMPLETION

Changing weighting reruns optimization.

This is not MVP-critical.

---

## Scientific Integrity

The hackathon system is an operational prototype, not a certified data-center energy simulator.

Cooling-energy estimates must:

- use documented formulas
- expose assumptions
- be reproducible
- avoid exaggerated precision

Never claim real-world savings that were not measured.

Phrase results as:

"estimated operating cost under the current model"

not:

"guaranteed savings."

---

## MVP Success Criteria

The product is successful if:

1. thermal data can be associated with compute sites
2. thermal conditions visibly vary over time/location
3. baseline scheduling works
4. HeatShift scheduling works
5. identical workloads are used in both comparisons
6. HeatShift reacts to thermal differences
7. all important numbers come from calculations
8. a judge understands the business value quickly
9. the full demo runs reliably

---

## Non-Goals

Not initially building:

- real Kubernetes integration
- real cloud workload migration
- billing systems
- authentication
- full CFD cooling simulation
- production data-center control
- hardware telemetry systems
- a medical/environmental dashboard
- a generic AI assistant

---

## North-Star Statement

"We run the same compute and meet the same requirements, but use hyperlocal temperature intelligence to make smarter decisions about where and when that compute executes."
