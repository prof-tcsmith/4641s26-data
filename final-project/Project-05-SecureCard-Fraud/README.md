# Project 05 — SecureCard Credit-Card Fraud Detection

**Client industry:** Credit-card issuer
**Primary client contact:** Sophia Lin, Vice President of Fraud Risk, SecureCard Financial
**Data URL:** `https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/final-project/Project-05-SecureCard-Fraud/securecard_transactions.csv`

---

## The Situation

SecureCard is a mid-sized credit-card issuer — the kind of bank that issues cards for regional retail chains and small-bank co-brands. The portfolio has about 3.2 million active cardholders and processes roughly 92 million transactions a year. The company makes its money on interchange fees, and it loses its money when fraudsters figure out how to use a stolen card faster than SecureCard's systems can catch it.

Sophia Lin, VP of Fraud Risk, has been at SecureCard for seven years, and by her own account, the last fourteen months have been the worst she has seen. A new wave of fraud attacks — mostly automated, mostly originating overseas — has pushed SecureCard's fraud loss rate from the historical ~0.10% of transaction volume up to nearly 0.17%. In dollar terms, that's an extra **$14 million a year** the bank is eating. Each confirmed fraudulent transaction costs SecureCard an average of **$380**: the disputed amount (usually refunded to the cardholder) plus investigation costs plus interchange reversals.

SecureCard already has a fraud-detection system. It is rule-based and has not been significantly updated in four years. Sophia doesn't want to throw it out — it's a known quantity and the compliance team trusts it. But she wants a *second layer* built on top of it: a model-based score that the fraud team uses to decide whether to text a cardholder a confirmation request before letting a suspicious transaction clear.

That confirmation request is not free. When SecureCard sends a "Did you try to make this charge?" text and the charge turns out to be legitimate, the cardholder is mildly annoyed. Worse, if SecureCard declines the charge at the point of sale based on a model flag — and the cardholder was actually standing in line at a grocery store trying to buy milk — the cardholder is *deeply* annoyed. The bank's customer-experience team estimates that a wrongly-declined legitimate transaction costs SecureCard about **$12** in goodwill-recovery spending (apology notes, statement credits, some fraction of cardholders who leave entirely) — but those losses are far less catastrophic than an undetected fraud.

Sophia's charge to your team is to build that second layer.

---

## What Sophia Wants From You

> "I want a model that surfaces the real fraud and gets out of the way of everything else. My team does not have time to investigate every slightly-odd transaction. If you flag 30% of our transactions, we ignore you. If you flag 0.01% of our transactions but they're all really fraud, that's perfect. Somewhere in between is the right answer, and I need you to justify where you land."

### Specifically

1. Build a classifier that scores each transaction for fraud risk.
2. Describe, clearly, what kinds of transactions the model flags and what kinds it doesn't. Show Sophia's team the patterns.
3. Give an explicit recommendation for how the flag should be used: auto-decline? Text-to-confirm? Manual review? Mix? Use the predicted *probabilities* (`predict_proba`), not just the 0/1 predictions, to rank transactions and decide which actions go to which.
4. Quantify what *would* happen, in expected fraud dollars caught and in expected customer friction, if SecureCard deployed your recommended ranking-and-routing strategy. The fraud-ops team can manually review at most ~40,000 transactions per month — that capacity should drive your recommendation. Back-of-envelope is fine; Sophia just wants the argument.

---

## The Data — `securecard_transactions.csv`

**Load it directly in your notebook:**

```python
import pandas as pd
DATA_URL = "https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/final-project/Project-05-SecureCard-Fraud/securecard_transactions.csv"
df = pd.read_csv(DATA_URL)
```

A random sample of 5,000 transactions from the last 90 days, each labeled as fraud or legitimate by the fraud-ops team.

| Column | Description |
|:-------|:------------|
| `transaction_id` | Internal identifier (not useful as a feature) |
| `amount` | Transaction amount in USD |
| `merchant_risk_band` | SecureCard's pre-computed risk band for the merchant: **1** = low (grocery, restaurant, gas), **2** = medium ("other"), **3** = high (online, travel) |
| `hour_of_day` | 0 - 23 |
| `is_international` | 1 if the merchant is outside the USA, 0 otherwise |
| `days_since_last_transaction` | Days since the card's previous transaction |
| `distance_from_home_km` | Distance between the transaction location and the cardholder's home (km) |
| `cardholder_age_years` | Cardholder's age at time of transaction |
| `is_fraud` | **Target.** 1 if the transaction was confirmed fraudulent, 0 otherwise. |

---

## A Few Things to Keep in Mind

- Fraud is *rare*. In this sample, roughly **2% of transactions are fraud** — and even that number is inflated because fraud-ops samples biased the pulled set. Your evaluation must take this imbalance seriously. Accuracy is almost useless as a headline metric here.
- The bank has compliance obligations. A model that can't explain why it flagged a transaction is hard to defend in a customer dispute or a regulator meeting. Make sure your deliverable explains what is driving the flag for an example transaction.
- Legitimate transactions that get wrongly declined create genuine customer pain, even if the dollar cost looks small — the cardholder standing at the grocery checkout does not know their card was refused for a "statistical reason."
- Sophia's fraud-ops team has capacity for *maybe* 40,000 manual reviews per month. If your model flags more than that, the overflow just gets processed without review — which is effectively "not flagged." Keep this in mind when you make your deployment recommendation.

---

*Sophia runs her team like a control room. She expects clarity, numbers, and a readiness to defend choices. Your deliverable should feel like a risk assessment, not a class project.*
