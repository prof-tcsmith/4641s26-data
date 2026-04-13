# Project 06 — GreenLeaf Markets Direct-Mail Targeting

**Client industry:** Regional grocery chain
**Primary client contact:** Ethan Brooks, Marketing Analytics Manager, GreenLeaf Markets
**Data URL:** `https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/final-project/Project-06-GreenLeaf-Direct-Mail/greenleaf_customers.csv`

---

## The Situation

GreenLeaf Markets is a family-owned grocery chain with 62 stores across the Southeast. The company has a loyalty program — about 1.1 million active households — that underpins almost all of its marketing. Every quarter, GreenLeaf's marketing team sends out a physical direct-mail coupon book to a selected slice of the loyalty database. When a household uses one of the coupons, they typically spend about **$180 on that redemption trip** (roughly double their usual grocery basket) and the company's margin on that trip is about **$24**.

Sending the mailer costs money too. Printing, postage, and list handling run about **$2.80 per household** — add another $0.40 in list-maintenance overhead, and the realistic all-in cost is **$3.20 per household mailed**.

Last year, Ethan Brooks — who joined GreenLeaf from a direct-response agency just eighteen months ago — was asked to evaluate whether the quarterly mailer was worth doing at all. He pulled the response data: the company was mailing ~600,000 households per quarter, and about **8%** of recipients redeemed at least one coupon. Do the math and it mostly works — marginal ROI was positive — but only because the company was mailing to such a huge list. The campaign was running on volume, not on precision.

Ethan's boss, the VP of Marketing, has given him a specific goal for next quarter: *mail to fewer households, but spend about the same and get a similar amount of total redemptions.* "Basically," Ethan said in the briefing, "I'd love to cut our mailing volume in half and lose less than 10% of the redemptions." That means the mailer needs to go to the households most likely to actually redeem.

Ethan has built a simple scorecard in Excel based on average weekly spend, but he thinks a proper model could do much better. He has asked your team to build it — and to help him make the case to his VP that the model's recommendations are trustworthy.

---

## What Ethan Wants From You

> "My goal is to mail smarter, not more. Give me a model I can hand to our list-selection vendor. Tell me which households are the ones most likely to respond, and tell me what I'm giving up by *not* mailing the ones the model doesn't like. If my VP asks me what happens if we follow your recommendation, I need to be able to answer her."

### Specifically

1. Build a model that predicts, for each loyalty-program household, the probability they will redeem at least one coupon from the mailer.
2. Describe, in plain English, the *kind* of household the model thinks is a likely responder. Use the features to tell a customer-segment story.
3. Recommend a targeting rule. Use the predicted *probabilities* (`predict_proba`) to rank households from most-likely to least-likely to respond, and propose a rule like "mail to the top X% of the ranked list." Explain how you chose X — what does the response volume look like if Ethan mails the top 30%? The top 50%? — and what GreenLeaf gives up by *not* mailing the rest.
4. Quantify a reasonable expected outcome if the company adopts your recommendation — in terms of mailer cost, expected redemptions, and expected net margin.

---

## The Data — `greenleaf_customers.csv`

**Load it directly in your notebook:**

```python
import pandas as pd
DATA_URL = "https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/final-project/Project-06-GreenLeaf-Direct-Mail/greenleaf_customers.csv"
df = pd.read_csv(DATA_URL)
```

A random sample of 3,000 loyalty households drawn from the population that received the Q3 2025 mailer, with redemption outcome observed.

| Column | Description |
|:-------|:------------|
| `household_id` | Loyalty-program identifier (not useful as a feature) |
| `avg_weekly_spend` | Average weekly spend at GreenLeaf in the 12 weeks before the mailer, USD |
| `visits_per_month` | Average GreenLeaf store visits per month (12-week window) |
| `has_kids_at_home` | 1 if the household's loyalty profile indicates children under 18, 0 otherwise |
| `distance_to_store_km` | Distance from the household address to their nearest GreenLeaf store |
| `loyalty_years` | Years enrolled in the loyalty program |
| `last_coupon_used` | 1 if the household redeemed a coupon in the *previous* quarter's mailer, 0 otherwise |
| `responded` | **Target.** 1 if the household redeemed at least one coupon from the Q3 mailer, 0 otherwise. |

---

## A Few Things to Keep in Mind

- About **8% of mailed households respond**. That is — as you'd expect — a pretty imbalanced dataset. You will need to think carefully about what accuracy means here.
- GreenLeaf's cost of mailing is small per household, but the volume is huge. The dollar cost of over-sending is real, but rarely catastrophic on a per-mailer basis.
- The upside of *missing* a responder is a modest, quantifiable loss — not a safety-critical one. The math is different from (say) a fraud problem.
- Ethan's VP is focused on *total response volume*, not response rate. Your recommendation should address both of those numbers.
- Households who have responded in the past are likely to respond again, but Ethan wants the model to do more than just replay the last quarter's list. "Give me an argument for someone who *hasn't* bought yet but should."

---

*Ethan is a direct-response pragmatist — he's not looking for perfection, he's looking for measurable lift. A clean, defensible recommendation with honest numbers will carry the day. Don't oversell — his VP can smell that a mile away.*
