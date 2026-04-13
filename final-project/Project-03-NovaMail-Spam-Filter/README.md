# Project 03 — NovaMail Enterprise Spam Classifier

**Client industry:** Enterprise email security / managed IT services
**Primary client contact:** Daniel Okoye, Chief Information Officer, NovaMail
**Data URL:** `https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/final-project/Project-03-NovaMail-Spam-Filter/novamail_messages.csv`

---

## The Situation

NovaMail is a business-to-business email service. It doesn't compete with Gmail or Outlook for consumers — its 1,800 clients are law firms, investment banks, hospitals, and midsize manufacturers. These are organizations for which email is not just communication: it's *the record of record*. A merger agreement, a client briefing, a patient referral — these live in email.

Daniel Okoye became CIO of NovaMail a year ago after fifteen years on the other side of the table, as CIO of a large law firm that was one of NovaMail's early customers. He knows first-hand what happens when the spam filter gets too aggressive. "I lost a deal once," Daniel told the sales team in his first week, "because a time-sensitive document from opposing counsel ended up in a quarantine folder. Nobody checked the folder for four days. That mistake cost my firm about $1.4 million. And it cost me three nights of sleep."

NovaMail's current spam filter is a mess. It's an ancient rule-based system, layered over with patches, and nobody at the company fully understands it anymore. Reviews of client tickets for the past quarter show two repeating complaints:

1. **"You're letting too much spam through."** This is real, and it's annoying, but the cost is small — a user has to spend a couple seconds clicking delete.
2. **"You quarantined another email from [our largest client / the opposing counsel / the hospital administrator / the IRS]."** This one is not an annoyance. This one ends engagements. NovaMail's sales team estimates that *each* "important message quarantined" incident costs the company about **$8,000 in client-retention spend** and, over time, churns clients who lose trust.

Daniel has asked your team to replace the old rule-based filter with a proper classifier — one that he can train, measure, and iterate on. He is explicit that the new system cannot be worse than the old one at the thing that hurts NovaMail's clients the most.

---

## What Daniel Wants From You

Daniel's written briefing to the team:

> "I do not want you to tell me that our new filter catches more spam. I expect it to. That is table stakes. What I want you to tell me is *how much we will never quarantine a client's legitimate email again*. My clients will forgive a rogue pharma ad in their inbox. They will not forgive a missed contract. Build me something that understands the difference."

### Specifically

1. Build a classifier that predicts whether a given incoming email is spam.
2. Report on the classifier's behavior with a very clear, *very* honest account of how often it misclassifies legitimate business email as spam.
3. Argue what target you think the classifier should aim for — and what Daniel should be comfortable telling his clients about its expected behavior.
4. Recommend how NovaMail should *deploy* the classifier. Should low-confidence spam go straight to quarantine, or to a "review" folder? Why?

---

## The Data — `novamail_messages.csv`

**Load it directly in your notebook:**

```python
import pandas as pd
DATA_URL = "https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/final-project/Project-03-NovaMail-Spam-Filter/novamail_messages.csv"
df = pd.read_csv(DATA_URL)
```

A labeled sample of 2,500 messages drawn from NovaMail's existing quarantine + delivered-message logs over the past six weeks.

| Column | Description |
|:-------|:------------|
| `message_id` | Internal identifier (not useful as a feature) |
| `num_links` | Number of URLs in the message body |
| `capitals_ratio` | Fraction of alphabetical characters in the message body that are upper-case (0.0 - 1.0) |
| `exclamation_count` | Number of `!` characters in the body |
| `contains_unsubscribe` | 1 if the message body contains the word "unsubscribe" (case-insensitive), 0 otherwise |
| `sender_reputation` | NovaMail's own score of the sender domain (0-100, higher = more reputable) |
| `attachment_count` | Number of attachments |
| `body_length` | Character length of the plain-text body |
| `is_spam` | **Target.** 1 if spam, 0 if legitimate. |

---

## A Few Things to Keep in Mind

- About 35% of messages in this sample are spam. That is *higher* than the true inbound rate because the sample over-represents quarantined items; acknowledge this if it matters for how you interpret your metrics.
- Daniel's clients include law firms and hospitals. The language of "we probably won't quarantine your email" is a terrible thing to say to these clients. Your recommendation and your presentation should be written with that sensitivity in mind.
- The existing rule-based filter is Daniel's baseline. If your model is *worse* than what he already has on the dimension he cares about, he is going to ask you why.
- Daniel is technical (he was a CIO). You may use the vocabulary of classification metrics — but he'll still expect you to argue from business first, math second.

---

*Daniel is measured and thoughtful, but he has been burned before. He will remember every caveat you give — so be careful with absolute claims.*
