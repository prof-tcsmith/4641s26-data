# Project 01 — TeleMax Customer Churn

**Client industry:** Consumer telecom (home internet + mobile)
**Primary client contact:** Maya Chen, Chief Customer Officer, TeleMax Communications
**Data URL:** `https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/final-project/Project-01-TeleMax-Churn/telemax_customers.csv`

---

## The Situation

TeleMax is a regional telecom carrier with about 420,000 subscribers across four states. Maya Chen was hired as Chief Customer Officer eighteen months ago with a single mandate from TeleMax's board: "stop the bleeding." In the two years before Maya arrived, TeleMax was losing roughly 24% of its subscriber base each year — much of it to larger national carriers offering aggressive promotional pricing on bundled plans.

Maya's team has made real progress. A revamped onboarding experience and a new 24/7 technical-support line have pulled churn down to about 22% annually — but that is still painful. Every churned customer represents lost lifetime value. TeleMax's finance team estimates that the average customer who leaves takes about **$820 in annual revenue** with them (and about $1,650 over the full expected lifetime). Over a year, that's somewhere north of **$75 million of attrition** the company cannot afford to keep eating.

Maya wants to get ahead of the problem. Rather than react after a customer calls to cancel, she wants her retention team to *proactively* reach out to customers who look like they're about to leave — ideally with a personalized retention offer (a month of free service, a bill credit, an upgraded plan at the same price). The retention team has run small pilots like this before and knows roughly what they cost: about **$35 per outreach** (agent time, offer value, postage for the mailed follow-up packet).

The pilots have shown something interesting. When Maya's team blankets large customer segments with these offers, the retention rate barely moves — they're mostly sending offers to customers who weren't going to leave anyway. But when they're *targeted* at customers who genuinely look at risk, the conversion rate is around 40% — meaning four out of ten at-risk customers can be "saved" with a well-timed offer.

Maya has asked your team to analyze TeleMax's customer data and build a model she can use to rank the customer base by churn risk. The retention team can then focus their outreach on the highest-risk group each month.

---

## What Maya Wants From You

In her own words:

> "I have a finite outreach budget. If you can tell me *who* to call, we can change the trajectory of this company. I'm not looking for a fancy algorithm. I'm looking for something I can defend to the CFO and something my team can act on next week. And for goodness' sake, don't tell me to just target everyone — I've been told that before, and we tried it, and it didn't work."

### Specifically

1. Build a model that predicts whether a customer will churn in the next 90 days.
2. Tell Maya, in business terms, what factors seem to drive churn at TeleMax — and what the data suggests about *why*.
3. Recommend a concrete way Maya's team can use your model. Who should they call first? How should she explain this to her CFO?
4. Be honest about where the model falls short. The CFO will ask.

---

## The Data — `telemax_customers.csv`

**Load it directly in your notebook:**

```python
import pandas as pd
DATA_URL = "https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/final-project/Project-01-TeleMax-Churn/telemax_customers.csv"
df = pd.read_csv(DATA_URL)
```

A random sample of 1,500 current and recently-churned customers pulled from the billing system. Each row is one customer.

| Column | Description |
|:-------|:------------|
| `customer_id` | Internal customer identifier (not useful as a feature) |
| `tenure_months` | How long the customer has been a TeleMax subscriber |
| `monthly_charges` | Current monthly bill in dollars |
| `support_calls_last_6mo` | Number of times the customer has called TeleMax support in the last 6 months |
| `contract_term_months` | Length of the customer's current contract, in months: **1** = month-to-month, **12** = one-year contract, **24** = two-year contract |
| `paperless_billing` | 1 if on paperless billing, 0 otherwise |
| `streaming_services_count` | Number of add-on streaming services (0 to 3) |
| `churned` | **Target.** 1 if the customer has churned (cancelled), 0 otherwise. |

---

## A Few Things to Keep in Mind

- Maya's team has **about 2,000 retention-team staff-hours per month** available for outreach. Your recommendation should respect that constraint.
- TeleMax's customers are *not* 50% churners — that would be an existential crisis. Pay attention to the class balance before you interpret accuracy.
- The CFO is skeptical of "AI." He is more comfortable with coefficients and odds ratios than with black boxes. Make sure your report explains *why* the model makes the predictions it does.
- "Churn" in this dataset means "cancelled all services with TeleMax." Downgrades are not counted.

---

*Good luck. Maya is a no-nonsense executive and she'll appreciate a crisp, evidence-backed recommendation over a meandering technical tour.*
