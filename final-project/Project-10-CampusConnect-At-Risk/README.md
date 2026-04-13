# Project 10 — CampusConnect At-Risk Student Identification

**Client industry:** Higher education (large public university learning center)
**Primary client contact:** Dr. Helen Ramirez, Director, CampusConnect Learning Center
**Data URL:** `https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/final-project/Project-10-CampusConnect-At-Risk/campusconnect_students.csv`

---

## The Situation

CampusConnect is the student success center at Midwestern State University (a 38,000-student public research university). The center offers free tutoring, academic coaching, workshop series, and one-on-one advising to any undergraduate who requests it. Dr. Helen Ramirez has directed CampusConnect for five years. She leads a team of 14 full-time professional advisors and a rotating cast of 80 peer tutors.

Helen's defining operational problem is triage. Of the roughly **7,000 undergraduates who take a gateway course each term** (calculus, introductory statistics, general chemistry, and so on), a meaningful fraction will struggle enough to fail or withdraw. Research across universities suggests that students who fail a gateway course in their first or second year are significantly more likely to leave the university entirely — a deeply bad outcome for the student and a **$35,000+** enrollment-loss for Midwestern State in future tuition.

Helen has long had a reactive model for identifying at-risk students: instructors refer struggling students mid-semester, or the registrar's "early alert" system fires after a failing mid-term. Both of these signals arrive *late*. By the time Helen's team is notified, a student is often past the point where advising and tutoring can change the trajectory — and even when earlier help would still be effective, the sheer volume of alerts in the last third of the semester overwhelms her staff.

What Helen wants is to get ahead of the problem. For every student enrolled in a gateway course, she wants a **Week-4 risk score** — computed from the first four weeks of the semester — that her advisors can use to reach out *proactively* to the students most likely to struggle. Her advising team has capacity to have sustained outreach conversations with roughly **500 students per term**. That's a real constraint. If Helen's model says "all 7,000 of these students are at risk," it's useless.

Helen is also thoughtful about the *human* side of this. "A student whose name comes up on the at-risk list," she has said, "is a student who has just failed to ask for help, who may not know help exists, or who may be afraid to raise their hand. I do not want the outreach to feel like surveillance. I want it to feel like someone noticed them."

---

## What Helen Wants From You

> "Give me a thoughtful tool that I can use to spend our limited advising hours where they will matter most. I need to understand what the model looks at, because when one of my advisors asks 'why is this student on the list?', I need to be able to answer them. And I need to be honest with our students about how the system works — this is a public university, and we will not hide a triage algorithm behind opaque procedures."

### Specifically

1. Build a model that predicts, by Week 4 of the term, whether a student enrolled in a gateway course will fail (earn below a C-).
2. Describe the factors the model uses, in the language Helen's advisors use — not the language of data science.
3. Recommend how the model should be integrated into CampusConnect's workflow. Use the predicted *probabilities* (`predict_proba`) to rank students by risk, and propose how Helen's team should work down the list given their **500-student outreach capacity per term**.
4. Discuss the practical limitations of predictive triage in this setting. What is the model NOT seeing about a student's circumstances? What kinds of errors could harm students if the model is used carelessly? How should Helen's team build safeguards into how they reach out?

---

## The Data — `campusconnect_students.csv`

**Load it directly in your notebook:**

```python
import pandas as pd
DATA_URL = "https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/final-project/Project-10-CampusConnect-At-Risk/campusconnect_students.csv"
df = pd.read_csv(DATA_URL)
```

A random sample of 1,700 students who took a gateway course in the last academic year, with the final course outcome observed.

| Column | Description |
|:-------|:------------|
| `student_id` | De-identified student number (not useful as a feature) |
| `current_gpa` | Student's cumulative GPA at the start of the term (0.0 - 4.0) |
| `credit_hours_taken` | Number of credit hours the student is taking this term |
| `assignments_on_time_pct` | Percentage of Week 1-4 assignments submitted on time (0.0 - 1.0) |
| `test_average_first_4wks` | Average on-assessment score in the first 4 weeks (0-100) |
| `attendance_rate` | Fraction of class sessions attended in the first 4 weeks (0.0 - 1.0) |
| `lms_logins_per_week` | Average Learning-Management-System logins per week, first 4 weeks |
| `first_generation` | 1 if the student reported being the first in their family to attend college, 0 otherwise |
| `at_risk` | **Target.** 1 if the student ultimately earned below a C- in the gateway course, 0 otherwise. |

---

## A Few Things to Keep in Mind

- About **15% of students in this sample failed the gateway course**. Your evaluation of the model should explicitly consider this imbalance.
- The asymmetry here is moral as much as financial. A student who should have been flagged but wasn't is a student who loses a semester — or a degree. A student who was flagged but would have been fine is a student whose advisor checked in on them — not, on its own, a terrible outcome.
- *But* — advisor time is not infinite. A model that flags 3,000 students a term gives the center no guidance. Your recommendation has to respect the 500-student outreach capacity.
- Be alert to the possibility that some features reflect structural inequities more than individual risk. First-generation status, for example, is correlated with outcomes — but is *not itself* a cause of failure. Your report should discuss this carefully.
- Helen's university has an Institutional Review Board and a strong student-privacy culture. Your recommendation should acknowledge that the model's use will have to be reviewed through that process before any real deployment.

---

*Helen is a student-success practitioner first and a data person second. She will appreciate clarity, humility, and care about student wellbeing far more than she will appreciate a high F1 score.*
