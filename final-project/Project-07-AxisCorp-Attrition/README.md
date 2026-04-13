# Project 07 — AxisCorp Employee Attrition

**Client industry:** Mid-size management consulting
**Primary client contact:** Priya Desai, Vice President of People Operations, AxisCorp Consulting
**Data URL:** `https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/final-project/Project-07-AxisCorp-Attrition/axiscorp_employees.csv`

---

## The Situation

AxisCorp is a 1,400-person management consulting firm headquartered in Chicago with practice offices in Dallas, Atlanta, and Denver. Like most professional-services firms, AxisCorp lives and dies by its consultants — the billable hours those consultants generate and the client relationships they maintain. And like most professional-services firms, AxisCorp has been struggling with attrition.

Priya Desai has been VP of People Operations at AxisCorp for three years. Over that time, voluntary attrition has drifted from about 15% annually to just over 22% — with the heaviest losses concentrated in consultants with 2-4 years of tenure (the "almost-ready-to-be-managers" cohort). When one of those consultants leaves, AxisCorp's finance team pegs the all-in cost at roughly **$42,000**: recruiting fees, the gap in billable hours during the replacement search, onboarding and ramp-up for the new hire, and the client-continuity damage of changing the face on a live engagement.

Priya already runs a formal retention program. Each year, managers are asked to identify "flight risks" on their teams and to recommend retention actions — off-cycle pay adjustments, role changes, new project assignments, formal mentorship. The tools she has are crude. Managers sometimes flag the wrong people. Sometimes they flag the right people but too late. And the retention actions themselves cost money — a retention bonus or off-cycle raise for one consultant averages about **$5,500** when applied correctly.

What Priya wants is a *systematic* early-warning system. Every quarter, her team would produce a prioritized list of employees most likely to resign in the next twelve months. Managers would then focus their retention conversations on the people at the top of the list.

Priya is explicit that this is *not* a tool for performance management. "We are not going to use this to decide who to fire," she said. "We are going to use this to decide where to focus our retention attention. The goal is to save careers, not end them."

---

## What Priya Wants From You

> "I want to have an honest conversation with my managers every quarter about the two or three people on each team they should really be leaning in on. If your model tells me who those people are likely to be, that's a win. But I need to be able to explain it — I'm not going to tell a manager 'the machine said so.' And I need it to be fair. If my model systematically under-flags older employees or over-flags employees from one office, I'll get sued, and I'll deserve it."

### Specifically

1. Build a model that predicts the probability an employee will voluntarily leave within the next 12 months.
2. Describe the model's key drivers in language a practice-area manager can understand.
3. Recommend how the People Ops team should use the model. Use the predicted *probabilities* (`predict_proba`) to rank employees, and propose a top-K list per quarter that respects manager bandwidth. How should managers be coached to use the output (e.g., as input to a conversation, not as a verdict)?
4. Identify limitations. What is the model NOT seeing — qualitative team dynamics, individual circumstances, opportunities the employee is privately considering? What might happen to the data the model trains on next year if Priya's team starts acting on this year's predictions?

---

## The Data — `axiscorp_employees.csv`

**Load it directly in your notebook:**

```python
import pandas as pd
DATA_URL = "https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/final-project/Project-07-AxisCorp-Attrition/axiscorp_employees.csv"
df = pd.read_csv(DATA_URL)
```

A random sample of 1,200 consultants employed at AxisCorp over the last three years, with their exit status observed twelve months after each "snapshot" date.

| Column | Description |
|:-------|:------------|
| `employee_id` | Internal identifier (not useful as a feature) |
| `tenure_years` | Years at AxisCorp |
| `annual_salary` | Current annual base salary, USD |
| `avg_overtime_hours_per_week` | Average overtime hours logged per week over the last 12 weeks |
| `promotion_in_last_2_yrs` | 1 if the employee was promoted in the prior 24 months, 0 otherwise |
| `job_satisfaction_score` | Result of last engagement survey (1 = very dissatisfied, 5 = very satisfied) |
| `manager_rating` | Manager's last annual performance rating (1 = below expectations, 5 = far exceeds) |
| `commute_distance_km` | Distance from employee's home to their office |
| `left_within_12mo` | **Target.** 1 if the employee voluntarily left within 12 months of the snapshot date, 0 otherwise. |

---

## A Few Things to Keep in Mind

- About 20% of consultants in this sample voluntarily left within a year of their snapshot date.
- This is a use case where the cost asymmetry is meaningful but nuanced. The cost of missing a departing employee is roughly eight times the cost of a wrongly-flagged "retain" bonus — but over-flagging has its own soft costs. If managers are told to have a retention conversation with 40% of their team every quarter, those conversations stop being meaningful.
- Fairness is a real concern in HR analytics. Do not include features the model *shouldn't* see, and check the outputs for systematic bias across segments even if the model looks good on average.
- Priya's HR-leadership peer group has sued over misuse of models. Her tolerance for hype is zero. She will very much appreciate an honest discussion of what the model cannot do.

---

*Priya is calm, rigorous, and skeptical of anyone who over-promises. Take the time in your deliverable to walk her carefully through your reasoning. This project is less about maximizing a metric and more about earning her trust.*
