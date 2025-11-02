# 🗺️ Value Stream Mapping (VSM)

## 🤔 What is VSM?
Value Stream Mapping is a lean visual tool that documents, analyzes and improves the flow of materials and information required to bring a product or service to a customer. In software, VSM shows every step from idea to production, highlighting value‑added vs non‑value‑added time (waste).

---

## 🎯 Core concepts
- Value‑added time: work that changes the product toward customer requirements.  
- Non‑value‑added time (waste): waiting, handoffs, rework, unnecessary processes.  
- Lead time: total time from request to delivery.  
- Cycle time: time one process step takes while actively working.  
- Takt time: customer demand rate (helps pace work).  
- Kaizen: continuous incremental improvement.

---

## 📝 How to create a VSM (concise steps)
1. Select a product family or feature type.  
2. Define start/end points (request → production).  
3. Walk the process and list all steps (including waits).  
4. Measure for each step: cycle time, lead time, uptime, defects, resources.  
5. Draw current state map (process boxes, inventories, information flow).  
6. Identify waste and bottlenecks.  
7. Design future state with improvements (pull, WIP limits, automation).  
8. Implement improvements, measure, iterate (kaizen).

---

## 💡 Simple example: "New Feature" stream
- Steps: Idea → Backlog → Ready → Development → Code Review → QA → Release.  
- Example metrics (per feature):
    - Backlog wait = 12 days  
    - Dev cycle time = 2 days  
    - Code review wait = 7 days  
    - QA cycle time = 1 day  
    - Release wait = 3 days  
    - Lead time = 12+2+7+1+3 = 25 days  
    - Value‑added time = Dev + QA = 3 days → Value ratio = 3 / 25 = 12%

Use VSM to reduce waits (Backlog, Review, Release) and increase value ratio.

---

## 📊 Flowchart (Basic)
Linear flow (simple text):
Customer Request / Idea -> Backlog / Grooming -> Ready for Dev -> Development -> Code Review -> QA / Testing -> Release / Production

ASCII diagram showing queues and flow:
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

Optional information flows and notes:
- Feedback/requirements flow from Customer to Backlog.  
- Deployment notifications and monitoring flow from Release back to stakeholders.  
- Inventories (queues) indicate where waits typically accumulate.

---

## 🚗 Toyota‑Inspired Case Study: Lean Software Transformation
- Context: A mid‑size product team struggled with long lead times and unpredictable releases.  
- Lean principles applied:
    - Visualize the flow (VSM across feature types).  
    - Reduce batch size: smaller features, feature flags.  
    - Limit WIP with Kanban and explicit policies.  
    - Automate repetitive processes (CI, automated tests, automated deployments).  
    - Implement pull (work pulled when capacity available) and standardize workflows.  
    - Continuous improvement cycles (weekly kaizen meetings).
- Outcomes (typical):
    - Lead time reduced from ~30 days to ~7–10 days.  
    - Increase in value ratio as waits cut.  
    - Fewer defects and faster customer feedback loop.

---

## 💼 Real‑World Example: Applying VSM at "AcmeSoft"
1. Current state: New customer feature average lead time = 40 days. Value‑add = 5 days. Key wastes: backlog prioritization (15d), code review queue (10d), manual deployment queue (7d), rework from late QA (3d).  
2. VSM findings: 87% of time was waiting. Bottlenecks: prioritization and review queues.  
3. Future state improvements:
     - Adopt weekly prioritization and shorter grooming windows (cut backlog wait to 5d).  
     - Enforce code review SLAs, pair programming to reduce review wait to 1d.  
     - CI/CD pipeline automates deploys (deploy wait → 0d).  
     - Shift‑left QA and automated regression to cut rework.  
4. Result: Lead time = 5 + 2 + 1 + 1 + 0 = 9 days. Value ratio increased from 5/40 (12.5%) to 8/9 (≈89%) if additional automation reduces cycle times.
5. Next steps: continue VSM for other product families, measure metrics continuously, run kaizen experiments.

---

## 💡 Practical tips
- Start small: map one product family or feature type.  
- Measure real times (not estimates). Use ticket timestamps, CI logs.  
- Focus on biggest sources of wait first.  
- Combine VSM with other lean practices: Kanban, CI/CD, trunk‑based development, automated tests.  
- Re-map regularly (every quarter or after major changes).

---

Further reading or templates can be added on request.