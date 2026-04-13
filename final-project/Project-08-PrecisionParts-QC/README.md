# Project 08 — PrecisionParts Quality Control Flagging

**Client industry:** Aerospace parts manufacturing
**Primary client contact:** Raj Patel, Vice President of Quality Operations, PrecisionParts Inc.
**Data URL:** `https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/final-project/Project-08-PrecisionParts-QC/precisionparts_runs.csv`

---

## The Situation

PrecisionParts Inc. is a 540-person machine shop in Wichita that makes precision-turned aluminum and titanium components for aerospace customers. The company's parts end up in engine mounts, landing-gear assemblies, and avionics enclosures — which is to say, in places where a defective part can, in the worst case, kill people. There has never been a safety incident attributable to a PrecisionParts component. Raj Patel, PrecisionParts' VP of Quality Operations, intends to keep it that way.

The company already has a conservative, expensive final inspection process. Every single finished part is inspected before it leaves the facility. But Raj has been told by his CFO and his COO that the final-inspection stage is a bottleneck — the inspection staff work three full shifts and the company still can't keep up with customer demand for turnaround. What Raj has been asked to explore is whether the company can use *run-level* data — data captured during the actual machining of a part — to *pre-flag* parts that are likely to fail inspection, so those parts can be routed to an enhanced inspection process that catches real defects more reliably, while the remaining parts move through a lighter touch-inspection process. Parts that the model does *not* flag would still be inspected, but with less scrutiny — and faster.

The cost math is important. An enhanced inspection costs PrecisionParts about **$55 in labor and equipment time**. Sending a part to enhanced inspection that turns out to be fine is a small tax on the process — worth it to speed everything else up, but not free. On the other side: a defective part that escapes PrecisionParts' doors and reaches a customer is catastrophic. Customer warranty claims are measured in hundreds of thousands of dollars per incident, regulatory exposure can be much more, and the reputational damage to a parts vendor in an industry with this many alternatives is almost impossible to repair. The worst-case scenario — a PrecisionParts part implicated in a safety incident — is existentially threatening.

Raj has been clear about what he wants:

> "I want a flag I can trust. If your model says 'this part is fine,' I need to believe it, because we're going to pull inspection resources away from those parts. If your model says 'enhanced inspection,' I don't mind being wrong sometimes — that's what enhanced inspection is for. What I cannot tolerate is a model that misses real defects. I will not sign off on deploying this until I understand exactly how often that would happen."

---

## What Raj Wants From You

1. Build a model that predicts whether a given machining run will produce a part that fails final inspection.
2. Clearly communicate the model's behavior — especially how often it would, in production, let a defective part pass through enhanced inspection unflagged.
3. Recommend a conservative deployment strategy. How should the shop integrate your model's flag into the inspection workflow? Where should a human review override the model?
4. Acknowledge what the model *cannot* see (wear patterns developing across shifts, material lot variance not captured at run time, environmental conditions) and what that means for monitoring once it's in production.

---

## The Data — `precisionparts_runs.csv`

**Load it directly in your notebook:**

```python
import pandas as pd
DATA_URL = "https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/final-project/Project-08-PrecisionParts-QC/precisionparts_runs.csv"
df = pd.read_csv(DATA_URL)
```

A random sample of 2,200 completed machining runs over the past year, with the final-inspection outcome observed.

| Column | Description |
|:-------|:------------|
| `run_id` | Internal identifier (not useful as a feature) |
| `machine_age_years` | Age of the CNC machine that ran the part, in years |
| `operator_experience_years` | Years of experience of the operator who ran the machine |
| `batch_size` | Number of parts in the batch that run belonged to |
| `material_variance` | Dimensional variance observed on the incoming material stock (thousandths of an inch) |
| `ambient_temp_c` | Shop-floor ambient temperature during the run, Celsius |
| `cycle_time_seconds` | Total cycle time for the run, in seconds |
| `prior_failures_this_shift` | Number of parts from this shift that had already failed inspection before this run |
| `failed_inspection` | **Target.** 1 if the finished part failed final inspection, 0 otherwise. |

---

## A Few Things to Keep in Mind

- About **5% of runs in this sample produced a part that failed final inspection**. That is a small number, but the stakes for each failure are high.
- Aerospace is a regulated industry. Any model that affects inspection intensity must be *auditable*. Your deliverable should make clear that a production deployment would need documentation the FAA can review.
- There is no world in which Raj is comfortable accepting more missed defects in exchange for less rework. Raj's universe is asymmetric. Build your argument around that asymmetry.
- The model will *not* replace inspection. It will *route* inspection. Your recommendation should respect that design.

---

*Raj is a careful, process-oriented engineer. He will read every word of your report. Show your work, be honest about uncertainty, and do not promise more than the data can support.*
