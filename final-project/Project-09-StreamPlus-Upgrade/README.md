# Project 09 — StreamPlus Premium-Tier Upgrade Targeting

**Client industry:** Direct-to-consumer streaming media
**Primary client contact:** Jordan Washington, Director of Subscription Growth, StreamPlus Media
**Data URL:** `https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/final-project/Project-09-StreamPlus-Upgrade/streamplus_subscribers.csv`

---

## The Situation

StreamPlus Media runs a general-audience streaming video service — call it a minor competitor to the big guys — with roughly **4.9 million paying subscribers** in North America. The company offers two plans:

- **Basic** — $9/month, ad-supported, one device.
- **Premium** — $17/month, ad-free, four simultaneous devices, early access to originals.

Jordan Washington runs the subscription-growth team at StreamPlus. His north-star metric is ARPU (average revenue per user), and the primary lever he pulls to move ARPU is the rate at which Basic subscribers are converted to Premium. Historical upgrade offers sent to random slices of Basic subscribers have run about an **11% conversion rate** — meaning about one in nine contacted subscribers upgrade.

Here's the part that makes Jordan's job hard. StreamPlus's retention team has shown, convincingly, that upgrade offers come with a *negative side effect*. When a subscriber receives an upgrade pitch they find irrelevant, the subscriber often becomes more likely to *cancel altogether* in the following month — to the tune of a **2.5 percentage point increase in 30-day cancellation rate** for non-responding recipients. Jordan's retention counterpart, who has been on the job longer than Jordan has, once took him aside and said: "Every campaign you run costs me customers. I'm not saying don't run them. I'm saying the price of running them sloppily is higher than you think."

Let's put numbers on this. When StreamPlus sends an upgrade offer and the subscriber accepts, the company picks up about **$96 in incremental annual revenue**. When StreamPlus sends an upgrade offer and the subscriber *doesn't* accept — and that subscriber would not have upgraded anyway — there is no direct revenue hit, but Jordan's retention counterpart estimates the expected damage from the cancellation-rate bump at roughly **$55 of expected lifetime-value loss per non-accepting recipient**. That's a surprisingly high per-recipient cost, and it fundamentally changes Jordan's optimization problem.

Jordan has asked your team to build a model that ranks Basic subscribers by their probability of accepting an upgrade offer. Rather than blanketing the Basic segment with offers, he wants to send offers *only* to the subscribers most likely to accept.

---

## What Jordan Wants From You

> "I need a list. Not a big list, but a list of the people most likely to say yes. If we run a campaign that gets a 40% conversion rate instead of 11%, my retention colleagues will stop glaring at me in the hallway. I need you to tell me what conversion rate I can realistically expect, and how many subscribers that means I'll be sending offers to."

### Specifically

1. Build a model that predicts the probability a Basic subscriber will accept an upgrade offer.
2. Tell Jordan who the model thinks is a likely accepter — describe the segment in words the marketing team will recognize.
3. Recommend a concrete targeting rule. Use the predicted *probabilities* (`predict_proba`) to rank Basic subscribers from most-likely to least-likely to accept, and propose how far down the ranked list Jordan should go. Explain *why* you stopped where you did — what is gained by extending the list, and what is lost?
4. Quantify the expected outcome of the recommended rule: how many subscribers will be contacted, what conversion rate can Jordan expect, what is the expected net LTV impact (the positive contribution from accepters, minus the cost to non-accepting recipients)?

---

## The Data — `streamplus_subscribers.csv`

**Load it directly in your notebook:**

```python
import pandas as pd
DATA_URL = "https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/final-project/Project-09-StreamPlus-Upgrade/streamplus_subscribers.csv"
df = pd.read_csv(DATA_URL)
```

A random sample of 2,500 Basic-tier subscribers who received an upgrade offer in a prior test campaign, with the outcome observed.

| Column | Description |
|:-------|:------------|
| `subscriber_id` | Internal identifier (not useful as a feature) |
| `months_subscribed` | Total months the subscriber has been on StreamPlus |
| `content_hours_per_week` | Average hours of content watched per week (trailing 12 weeks) |
| `devices_used` | Number of distinct devices logged in from in the last 30 days |
| `recent_search_rate` | Fraction of searches in the last 30 days that were for Premium-only content (0.0 - 1.0) |
| `past_offer_responses` | Number of past offers (any kind) the subscriber has engaged with |
| `age_range_code` | Self-reported age-range bucket: 1 = 18-24, 2 = 25-34, 3 = 35-49, 4 = 50+ |
| `accepted_upgrade` | **Target.** 1 if the subscriber accepted the upgrade offer, 0 otherwise. |

---

## A Few Things to Keep in Mind

- About 30% of subscribers in this sample accepted the upgrade offer. This is a *higher* conversion rate than the usual blanket campaign — the test campaign represented here was itself targeted somewhat.
- The cost asymmetry in this problem may surprise your team, because it runs *opposite* to what most classification use cases look like. Think carefully about what each type of error costs StreamPlus.
- Jordan's counterpart in retention will be in the room when you present. Make sure your recommendation holds up under that scrutiny.
- Do not recommend "just target everyone." That is the strategy StreamPlus already knows does not work.

---

*Jordan is energetic and numbers-driven. He will press you for specifics — expected contacts, expected conversions, expected dollars. Rehearse those answers.*
