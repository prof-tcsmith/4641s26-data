# Project 04 — HealthPath Type-2 Diabetes Screening

**Client industry:** Primary care health network
**Primary client contact:** Dr. Aisha Nwosu, Medical Director for Population Health, HealthPath Primary Care
**Data URL:** `https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/final-project/Project-04-HealthPath-Diabetes-Screening/healthpath_patients.csv`

---

## The Situation

HealthPath is a non-profit network of 38 primary care clinics across three mid-sized cities in the Midwest. Dr. Aisha Nwosu, a family physician for twenty years, serves as the network's Medical Director for Population Health. Her job is essentially to keep HealthPath's roughly 190,000 patients *healthier over time*. She measures her success in averted hospitalizations and improved chronic-disease outcomes — not in procedure volume.

The condition Aisha worries about most right now is type-2 diabetes. The USA has roughly 38 million people with diabetes and another 97 million with pre-diabetes, and the typical patient is *diagnosed seven years after* their first measurable glucose abnormalities. That delay is the main reason diabetes causes so many of the complications it does — vision loss, kidney disease, foot amputations, heart disease. Catching patients earlier, when lifestyle changes still have the strongest effect, is one of the highest-leverage things a primary care network can do.

HealthPath already has a screening protocol — a simple fasting glucose test during the annual physical — but the protocol is applied inconsistently. Some clinicians order it for every patient; some order it for no one. Aisha wants to replace this ad-hoc practice with a data-driven screening recommendation. For every adult patient whose intake forms contain the standard information, she wants a recommendation flag: "test this patient now."

The test itself is well understood: it costs HealthPath about **$45** per patient to administer (lab fee + phlebotomy time). The other side of the ledger is more serious. When type-2 diabetes goes undiagnosed for years, the downstream costs — to the patient, to HealthPath, to the insurer — typically run into the **tens of thousands of dollars** over the patient's lifetime, not to mention the human cost of avoidable complications.

Aisha is clear about her priorities:

> "My job is to not miss these patients. Every patient we fail to flag is somebody who walks out of my clinic thinking they're fine, and comes back five years from now needing dialysis or insulin. A screening test that comes back negative is the best possible outcome. But a patient I didn't screen — that's the one I can't stop thinking about. I need you to help me build a tool that errs, consistently, on the side of catching the person at risk."

---

## What Aisha Wants From You

1. Build a model that takes a patient's intake data and predicts whether they should be flagged for a diabetes screening test.
2. Explain which intake variables matter — in language an internal-medicine resident (not a data scientist) can understand.
3. Discuss the practical implications of the model's errors and recommend how clinicians should use the output.
4. Be honest about what the model *cannot* see — the patient's social and behavioral context, conditions that aren't captured in this dataset, the clinician's intuition built up over years. Discuss what those blind spots mean for how the screening flag should be used in practice.

---

## The Data — `healthpath_patients.csv`

**Load it directly in your notebook:**

```python
import pandas as pd
DATA_URL = "https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/final-project/Project-04-HealthPath-Diabetes-Screening/healthpath_patients.csv"
df = pd.read_csv(DATA_URL)
```

A de-identified sample of 1,800 patients from HealthPath's electronic health record, each of whom had both intake data at Year 0 and a confirmed diabetes diagnosis status at Year 3.

| Column | Description |
|:-------|:------------|
| `patient_id` | De-identified patient number (not useful as a feature) |
| `age_years` | Patient age, in years (18 - 85) |
| `bmi` | Body Mass Index at intake (15 - 55) |
| `family_history` | 1 if a first-degree relative has type-2 diabetes, 0 otherwise |
| `systolic_bp` | Systolic blood pressure at intake, mmHg |
| `fasting_glucose` | Fasting glucose level at intake, mg/dL |
| `total_cholesterol` | Total cholesterol at intake, mg/dL |
| `activity_level` | Self-reported activity score (1 = sedentary, 2 = light, 3 = moderate, 4 = active) |
| `needs_screening` | **Target.** 1 if the patient was diagnosed with type-2 diabetes within 3 years of intake (i.e., should have been flagged for screening), 0 otherwise. |

---

## A Few Things to Keep in Mind

- Roughly 15% of patients in the sample went on to receive a diabetes diagnosis within three years. The prevalence is meaningful; don't just look at overall accuracy.
- The clinical stakes are asymmetric. A screening test for a patient who turns out to be healthy is a mild inconvenience and a $45 line item. A patient who *should* have been screened but wasn't can suffer consequences that no spreadsheet can fully capture.
- "Flag for screening" does not mean "diagnose." Your model's output is a recommendation to the clinician, not a diagnostic.
- Aisha is a physician. She will read your notebook. Avoid ML jargon that she hasn't already heard on a podcast. If you must use a term like "precision," define it in the context of her work.

---

*Dr. Nwosu is warm, but she's seen plenty of technology vendors over-promise. What will impress her is clarity, honesty about limitations, and a recommendation that respects her clinical judgment rather than replacing it.*
