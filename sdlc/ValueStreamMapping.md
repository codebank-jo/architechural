# Value Stream Mapping (VSM)

## What is VSM?
Value Stream Mapping is a lean visual tool that documents, analyzes, and improves the flow of information and work required to deliver a product or feature. In software, VSM shows every step from request to production and highlights value‑added versus non‑value‑added time (waste).

---

## Core concepts
- Value‑added time: work that moves the product toward customer requirements.  
- Non‑value‑added time (waste): waiting, handoffs, rework, unnecessary processes.  
- Lead time: total time from request to delivery.  
- Cycle time: time one process step takes while actively working.  
- Takt time: customer demand rate (used to pace work).  
- Kaizen: continuous incremental improvement.

---

## How to create a VSM (concise steps)
1. Select a product family or feature type.  
2. Define start and end points (request → production).  
3. Walk the process and list all steps (include waits and handoffs).  
4. Measure for each step: cycle time, lead time, uptime, defects, resources.  
5. Draw the current state map (process boxes, inventories, information flow).  
6. Identify waste and bottlenecks.  
7. Design a future state with improvements (pull, WIP limits, automation).  
8. Implement improvements, measure outcomes, iterate.

---

## Simple example: "New Feature" stream
Steps: Idea → Backlog → Ready → Development → Code Review → QA → Release

Example metrics (per feature):
- Backlog wait = 12 days  
- Development cycle time = 2 days  
- Code review wait = 7 days  
- QA cycle time = 1 day  
- Release wait = 3 days  
- Lead time = 12 + 2 + 7 + 1 + 3 = 25 days  
- Value‑added time = Development + QA = 3 days → Value ratio = 3 / 25 = 12%

Use VSM to reduce waits (Backlog, Review, Release) and increase the value ratio.

---

## Flowchart (basic)
Linear flow:
Customer Request / Idea -> Backlog / Grooming -> Ready for Dev -> Development -> Code Review -> QA / Testing -> Release / Production

ASCII diagram:
```
Customer Request / Idea
        |
        v
  Backlog / Grooming
        |
        v
   [Backlog Queue]
        |
        v
   Ready for Dev
        |
        v
   Development
        |
        v
   [Review Queue]
        |
        v
   Code Review
        |
        v
   QA / Testing
        |
        v
   [Release Queue]
        |
        v
  Release / Production
```

Notes:
- Show information flows (requirements, feedback, monitoring).  
- Mark inventories/queues where waits occur.

---

## Case study: Lean software transformation
Context: A mid‑size product team had long lead times and unstable releases.

Approach:
- Map current state across feature types.  
- Reduce batch size: smaller features, feature flags.  
- Limit WIP with Kanban and explicit policies.  
- Automate CI, tests, and deployments.  
- Implement pull and standardize workflows.  
- Run regular kaizen experiments.

Typical outcomes:
- Lead time reduced from ~30 days to ~7–10 days.  
- Increased value ratio as waits are cut.  
- Fewer defects and faster customer feedback loop.

---

## Real‑world example: "AcmeSoft"
1. Current state: average lead time = 40 days; value‑add = 5 days. Major wastes: backlog prioritization (15d), review queue (10d), manual deployment (7d), rework (3d).  
2. VSM findings: 87% of time was waiting; primary bottlenecks were prioritization and review.  
3. Future state improvements:
   - Weekly prioritization to cut backlog wait to 5d.  
   - Enforce review SLAs and pair programming to reduce review wait to 1d.  
   - CI/CD to eliminate manual deploy wait.  
   - Shift‑left QA and automated regression to cut rework.  
4. Result: lead time ≈ 9 days; value ratio increases significantly.  
5. Next steps: apply VSM to other product families and measure continuously.

---

## Practical tips
- Start with one product family or feature type.  
- Use real timestamps (ticket events, CI logs) instead of estimates.  
- Focus on the largest sources of wait first.  
- Combine VSM with Kanban, trunk‑based development, and CI/CD.  
- Revisit and remap periodically (quarterly or after major changes).

---

Further reading:
- Introduction: sa/Introduction.md  
- SDLC overview: sdlc/SoftwareDevelopmentLifeCycle.md