# Project 02 — FirstState Bank Loan Default Risk

**Client industry:** Community banking
**Primary client contact:** Robert Martinez, Chief Lending Officer, FirstState Community Bank
**Data URL:** `https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/final-project/Project-02-FirstState-Loan-Default/firststate_loans.csv`

---

## The Situation

FirstState Community Bank has been serving three counties in central Florida for more than sixty years. It's the kind of bank that sponsors Little League teams, where the tellers know customers by name, and where loan decisions are made in person. FirstState is proud of that. It's also why Robert Martinez, the bank's Chief Lending Officer, is nervous about how he talks about what he wants your team to build.

Here's Robert's problem. Over the last four quarters, FirstState's personal-loan default rate has drifted up from its historical 6-7% range to just over 10%. That sounds small, but at the bank's loan volume, each one-point increase in defaults costs roughly **$1.4 million a year**. A default on the average personal loan in FirstState's book costs the bank about **$18,500** in lost principal and collection expenses. In contrast, a "good" loan of the same size generates only about **$1,400 in interest income** over its life.

Robert has been tightening underwriting by hand — asking loan officers to be a little more skeptical, requesting more documentation on borderline cases — but this is slow, inconsistent across officers, and Robert worries it is *also* causing FirstState to turn away creditworthy borrowers, which is both a lost-revenue problem and, frankly, a community-reputation problem. "The whole point of a community bank," Robert says, "is that we know when to trust our neighbors. I don't want to build a machine that tells us to deny loans to good people just because their ZIP code looks statistically unfriendly."

What Robert *does* want is a second opinion. For every new loan application, he'd like a model that gives his underwriters a risk score — a probability that this particular applicant is likely to default. That score would never be the sole decision factor. Instead, it would flag the highest-risk applications for a deeper review by the senior underwriter before approval.

---

## What Robert Wants From You

From a call with his team:

> "I need three things. First, I need to know if this is even a feasible idea with the data we have. Second, I need to understand what the model is looking at — I can't put a black box in front of my underwriters and tell them to trust it. Third, I need a clear recommendation about how we should *use* the model. We lend to real people in real communities. I won't deploy anything that tells us to just deny the bottom X percent."

### Specifically

1. Build a model that estimates the probability a given loan applicant will default.
2. Identify which factors most influence that risk — in terms Robert can discuss with his board.
3. Propose a way FirstState can use the model in their workflow. How should the senior underwriter use the score? Where might it be misleading?
4. Be honest about what the model *cannot* see (demographics, unwritten relationship history with the customer, etc.) and what that implies for deployment.

---

## The Data — `firststate_loans.csv`

**Load it directly in your notebook:**

```python
import pandas as pd
DATA_URL = "https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/final-project/Project-02-FirstState-Loan-Default/firststate_loans.csv"
df = pd.read_csv(DATA_URL)
```

A random sample of 2,000 loans closed in the last three years. Each row is one approved loan, with the outcome observed.

| Column | Description |
|:-------|:------------|
| `loan_id` | Internal loan identifier (not useful as a feature) |
| `annual_income` | Borrower's stated annual income, USD |
| `credit_score` | FICO-equivalent score at origination (300-850) |
| `debt_to_income_ratio` | Total monthly debt payments divided by monthly income (0.05 - 0.80) |
| `loan_amount` | Dollar amount of the loan |
| `employment_years` | Years at current employer |
| `has_prior_default` | 1 if the borrower had any prior default on file, 0 otherwise |
| `defaulted` | **Target.** 1 if the loan defaulted, 0 if it was repaid. |

---

## A Few Things to Keep in Mind

- The cost asymmetry here is significant. An undetected default wipes out the entire principal of the loan. A wrongly-denied good borrower loses the bank only the small amount of interest they would have earned — but it also damages the bank's community reputation, which is harder to price.
- About 10% of loans in this sample defaulted. You should explicitly think about this imbalance when you evaluate the model.
- Robert's board has legal counsel who will review any adoption of a model like this. Your recommendation should note that the bank must audit for disparate impact on protected classes (age, race, ZIP code) — though that full audit is out of scope for your analysis.
- FirstState is a community bank. The tone of your deliverable should acknowledge that there are human beings on the other side of every row in this file.

---

*Robert is old-school but he's not anti-technology. He just wants to understand what he's being asked to adopt. A clear, non-technical explanation of your model's logic will go a long way with him — and with his board.*
