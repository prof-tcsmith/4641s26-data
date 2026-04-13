# Final Project — ISM 4641 Summer 2026

**Total points:** 50 (25% of final grade)
**Team size:** 3 to 5 students
**Deliverables due:** Friday, July 17, 2026 (end of Week 10)

---

## Overview

Your final project is a team consulting engagement. Each team will choose **one** of the 10 project scenarios in this folder and deliver a complete classification analysis to the fictional business client described in the narrative. Every scenario requires building, evaluating, and defending a **logistic regression classifier**.

You will submit two graded deliverables (the second is made up of two files that are graded together):

1. A **Jupyter notebook** that reads as a written report (heavy use of Markdown cells, not just code).
2. A **presentation** to the business client (the character named in the project narrative), consisting of:
   - a **PowerPoint deck**, and
   - a **7 to 9 minute video walkthrough** of that deck.

The scenarios vary widely in business context, data size, class imbalance, and which classification errors are most costly to the business. You are expected to read the narrative carefully and figure out, from context, which kinds of errors the business cares about most — and then choose metrics, models, and recommendations accordingly.

---

## Team Formation and Project Selection

- Teams must have **3 to 5 students**. Teams of 1, 2, or 6+ are not permitted.
- **To register a team:** email the professor (with the TA cc'd) with the names of every team member. One email per team is enough; all members should be cc'd on it so it's clear everyone agreed.
- **Team-formation deadline:** **April 15 at 11:59 PM**. After that date, any students not yet on a full team will be randomly assigned into teams of 3 to 5.
- **To declare a final project:** once your team is registered, send a second email to the professor (TA cc'd) listing your **top three project choices**, in rank order.
- **Project-selection deadline:** **April 17 at 11:59 PM**. Each project can be assigned to **at most two teams** across the class. The professor assigns projects using the submitted preference lists, doing the best he can to honor each team's highest-ranked available choice on a first-come-first-served basis. Any team that has not submitted a preference list by the April 17 deadline will be **randomly assigned** to a project from those still available.
- The team earns one **team grade** for the submitted artifacts. Each student's individual final-project grade is then computed by multiplying the team grade by their peer-evaluation average (see "Peer Evaluation" below).

---

## Project Scenarios

The 10 scenarios are in the subfolders below. Each subfolder contains:

- a `README.md` with the business narrative, the people involved, and what the client needs;
- a CSV file with the historical data you will analyze.

| # | Folder | Industry | The prediction task |
|:--|:-------|:---------|:--------------------|
| 1 | `Project-01-TeleMax-Churn` | Telecom | Will a customer cancel their subscription? |
| 2 | `Project-02-FirstState-Loan-Default` | Community bank | Will a loan applicant default? |
| 3 | `Project-03-NovaMail-Spam-Filter` | Enterprise IT | Is an incoming email spam? |
| 4 | `Project-04-HealthPath-Diabetes-Screening` | Primary care health network | Should this patient be flagged for a diabetes screening test? |
| 5 | `Project-05-SecureCard-Fraud` | Credit-card issuer | Is this transaction fraudulent? |
| 6 | `Project-06-GreenLeaf-Direct-Mail` | Grocery chain | Will a cardholder respond to a direct-mail coupon? |
| 7 | `Project-07-AxisCorp-Attrition` | Mid-size consulting | Will this employee leave within 12 months? |
| 8 | `Project-08-PrecisionParts-QC` | Aerospace parts manufacturer | Will this part fail final inspection? |
| 9 | `Project-09-StreamPlus-Upgrade` | Streaming service | Will this customer accept a premium-tier upgrade offer? |
| 10 | `Project-10-CampusConnect-At-Risk` | University learning center | Will this student be at risk of failing a course? |

Each scenario was written with a different class imbalance and a different cost structure for the two kinds of errors. The imbalance ranges from about 2% positive (very rare) to about 35% positive (mildly imbalanced). Understanding how these differences should shape your analysis is part of what this project assesses.

---

## Deliverables

### 1. Jupyter notebook (report)  `group{N}-report.ipynb`

Treat the notebook as a written consulting report, not just a scratchpad. Use Markdown cells generously to explain your thinking. Code cells should be used for analysis; every section of analysis should be introduced and interpreted in prose.

**Required sections (in order):**

1. **Executive Summary** (Markdown only) — 1-2 paragraphs. Who your client is, the business question, your recommended model, your headline metric, and your bottom-line recommendation. Written so a busy executive can skim in 30 seconds.
2. **The Business Problem** — Restate the business context in your own words. Identify the decision the client needs to make and *which type of classification error is more costly, and why*. Ground this in specific details from the narrative — dollar amounts, operational consequences, risk to customers, regulatory exposure, brand impact, etc.
3. **Data Exploration** — Load the CSV. Show the shape, column types, target-class balance, basic summary statistics, at least two visualizations of the relationships between features and the target. Commentary in Markdown before and after each code block.
4. **Model Building** — Train/test split (use `stratify=y`), build a logistic regression model. Report the coefficients as odds ratios and explain what each one means for the business.
5. **Model Evaluation** — Report the confusion matrix, accuracy, precision, recall, and F1. Explicitly tie these back to the business context — do not just report numbers.
6. **Metric Selection** — Argue clearly which metric the client should most care about and *why*. Connect your argument to the cost/risk structure you identified in section 2. A good report here explicitly considers the class imbalance in the data.
7. **Recommendation** — What should the client do with this model? Explain how they should use the probabilities (`predict_proba`) versus the binary predictions (`predict`). Suggest at least one concrete action they can take.
8. **Limitations and Next Steps** — Every model has limitations. List at least three, and describe what additional data, features, or follow-up work would strengthen the analysis.

Markdown should make up **at least 40% of the notebook by cell count**. A notebook that is 90% code with a sentence of commentary per section will not receive full credit.

### 2. Presentation — deck + video walkthrough  `group{N}-deck.pptx` and `group{N}-video.mp4` (or video link)

The presentation is a single graded deliverable made up of two files:

- a **PowerPoint deck** — client-facing, 10-14 slides typical, one clear idea per slide, minimal text, readable visuals;
- a **7 to 9 minute video walkthrough** of that deck — hard cutoff at 10 minutes, every team member must speak, presented as if you are in the client's boardroom.

The audience is the named character(s) in the narrative, not the professor. You will be evaluated on the clarity and business-appropriateness of both the slides and the spoken delivery — together — and on how well you tailor your communication to a business (not a technical) audience. See "Presentation Pointers" below.

---

## Grading — 50 points

The team grade is built from two components:

| Component | Weight | Points |
|:----------|:-------|:-------|
| **Notebook report** | 60% | 30 |
| **Presentation (deck + video)** | 40% | 20 |
| **Total team grade** | 100% | **50** |

The presentation is graded as a single deliverable: the **deck** and the **7-9 minute video walkthrough** of that deck are evaluated together.

> **Peer Evaluation (applied to each individual student's grade):**
>
> After the project is submitted, every team member privately completes a peer-evaluation form on Canvas, scoring each teammate (and themselves) on a 0-10 scale for things like: contribution to the analysis, contribution to the deck and video, reliability, and professionalism.
>
> A student's **individual final-project grade** is computed as:
>
> **(team grade) × (that student's peer-eval average / 10)**
>
> For example, if the team earns 100% on the project (50/50) and a particular student's peer-eval average across their teammates is 9 out of 10, that student receives **100% × 9/10 = 90%** for the project.
>
> A student whose peer-eval average comes back at 10/10 keeps the full team grade. A student whose teammates rate them noticeably lower than the others will see their grade reduced proportionally — this is how the project handles uneven contribution. The instructor reserves the right to adjust peer-eval averages if responses look retaliatory or otherwise unrepresentative.

### Detailed rubric

#### A. Notebook report (30 points)

| Criterion | Excellent (full) | Adequate | Weak / missing |
|:----------|:-----------------|:---------|:---------------|
| **Executive Summary (3 pts)** | Crisp, accurate, client-facing; a non-technical reader understands the recommendation in 30 sec. | Present but vague or too technical. | Missing or misleading. |
| **Business problem framing (4 pts)** | Restated in the team's own words; identifies which error type is costlier, **with specific reasoning from the narrative**. | Identifies the costlier error but reasoning is thin. | Does not address cost asymmetry at all. |
| **Data exploration (3 pts)** | Class balance reported, at least 2 meaningful visualizations with commentary, clear summary of each feature. | Some exploration, but missed a key pattern or lacks commentary. | Minimal exploration — just `.describe()` with no insights. |
| **Model building (4 pts)** | Correct use of `train_test_split(stratify=y)` and `LogisticRegression`; odds ratios explained in business terms. | Model built correctly but coefficients either not converted to odds ratios or not interpreted. | Code errors, or model built without stratification on an imbalanced target. |
| **Model evaluation (4 pts)** | Reports confusion matrix AND all four core metrics; explains them in context. | Reports the numbers but doesn't connect to the business. | Only reports accuracy, or math errors. |
| **Metric selection argument (5 pts)** | Compellingly argues for the right metric priority **given the narrative's cost asymmetry**; considers class imbalance; uses specific numbers. | Argues for a metric but reasoning is loose. | Picks a metric without justification or picks one inconsistent with the narrative. |
| **Recommendation (4 pts)** | Concrete, actionable, tied to predicted probabilities; includes at least one specific business action. | Recommendation present but generic. | Recommendation is just "deploy the model." |
| **Limitations & next steps (3 pts)** | At least 3 thoughtful limitations, each with a mitigation or follow-up. | Some limitations noted. | Missing or trivial. |

#### B. Presentation — deck + video (20 points)

The deck and the 7-9 minute video walkthrough are graded as one deliverable. Submit both; the grade considers them together.

| Criterion | Points | Notes |
|:----------|:-------|:------|
| **Time on target (7-9 min)** | 2 | Under 7 min or over 9 min: -1 pt per minute off. Over 10 min is an automatic 0 on this line. |
| **All members speak** | 1 | Every team member must take a visible speaking role in the video. |
| **Slide design and clarity** | 3 | Readable, uncluttered, consistent styling. One clear idea per slide. Visuals beat dense tables. |
| **Client-appropriate framing** | 4 | The deck and the spoken delivery treat the named client as the audience, not the professor. Appropriate vocabulary; minimal Python jargon. |
| **Clarity of spoken explanation** | 4 | Each speaker delivers their section clearly, confidently, and at an appropriate pace. Smooth handoffs between speakers. |
| **Metric & recommendation argument** | 5 | The case for your chosen metric and your recommendation is made explicitly and is the heart of the presentation. Connects to the narrative's cost structure with specific numbers. |
| **Polish and engagement** | 1 | Camera, audio, slide transitions, opening hook, closing. |

---

## Presentation Pointers

### What the deck and video should cover (in order)

1. **Who is your client? What is their problem?** — Name the client by their role (e.g., "Maria Chen, COO at PrecisionParts"). Frame the business problem the way the *client* would frame it, not the way a data scientist would.
2. **Why a classification model is the right tool.** — Make the "yes/no" structure of the question explicit.
3. **A glance at the data.** — Two to three slides at most. Highlight the class imbalance if it is meaningful.
4. **Your model, in plain English.** — What features does it use? What is the intuition for *why* each one matters? Show odds ratios, not log-odds.
5. **How good is it?** — Show the confusion matrix and the two or three metrics you centered on. Tie every number to business meaning.
6. **Which error is costlier for this business, and why.** — This is the heart of the project. Spend at least one dedicated slide here.
7. **Your recommendation.** — What should the client do? Be specific.
8. **Risks and caveats.** — Where should the client be careful?
9. **Q & A.** — Be ready to answer questions from the client.

### Tips for a good presentation

- **Open with the bottom line.** Don't make the client wait 6 minutes to hear your recommendation.
- **Talk to a person, not a grader.** You are in the client's conference room. Address them by name.
- **Skip the Python vocabulary.** Avoid terms like "sklearn", "DataFrame", and "predict_proba" unless the client would actually use them. Say "our model" not "our LogisticRegression instance".
- **One idea per slide.** Dense slides are harder to present from.
- **Visualize, don't tabulate.** A chart the client can read in 3 seconds beats a 10-row table.
- **Practice handoffs.** Decide who says what, and how you transition between speakers.
- **Time yourselves.** Most teams speak slower on camera than they think. Rehearse at least twice.
- **End with a question.** "Mr. Patel, do you have any questions, or would you like us to show you how the model would score a specific applicant?"

---

## Submission

All artifacts (notebook, deck, video) are submitted to a single Canvas assignment ("Final Project"), due **Friday, July 17, 2026 at 11:59 PM**. Late work policy from the main syllabus applies.

The notebook and PPT are uploaded directly. The video may be uploaded directly (MP4) or submitted as an unlisted link (YouTube, OneDrive, Google Drive) — make sure the link is accessible to the instructor.

---

## Academic Integrity

- Use of AI tools is encouraged for coding and drafting, **subject to the course's AI-transcript requirement**: every team member must include their own AI chat transcript as part of the submission (see the integrative-assignment policy in the syllabus).
- The narrative analysis, metric-selection argument, and final recommendation must be in your team's own words. Submitting AI-generated text verbatim as your "analysis" is not acceptable.
- Teams may **not** share draft material, code, or slides across teams. Each team's work must be its own.

---

*Questions? Ask during office hours or post on the "#final-project" Canvas discussion channel.*
