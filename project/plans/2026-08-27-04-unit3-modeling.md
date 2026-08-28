# Unit III: Understanding and Modeling Data Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Write Chapters 7-9 (Descriptive Statistics & Data Ethics,
Introduction to Machine Learning, How AI Learns From Data), replacing their
frontmatter-only stubs.

**Architecture:** Each chapter is one self-contained `.qmd` file, drafted by
a Fable-model agent against a fully-specified brief. Chapter 8 is grounded
in a verified real script run (`Lecture Material/Session 5_ Machine
Learning/DataScienceS5.py`) — its numbers are not invented.

**Tech Stack:** Quarto 1.8, Markdown/`.qmd`, `scikit-learn`/`matplotlib`
(described in code, not executed against a bundled dataset — see spec §7).

**Spec:** `project/specs/2026-08-27-hs-data-science-textbook-design.md`

**Prerequisite:** `project/plans/2026-08-27-01-infrastructure-and-front-matter.md` must be complete.

## Global Constraints

(Same callout syntaxes, tone, privacy guardrail, and Fable-authoring
requirement as `project/plans/2026-08-27-02-unit1-foundations.md`.)

- Chapter 8's machine-learning results (MSE and R² values) must match the
  real, verified run recorded in
  `../Lecture Material/Session 5_ Machine Learning/DataScienceS5.py`
  and its accompanying slide deck — do not invent different numbers.
- Any chart described in Chapters 8-9 uses `matplotlib` (per spec §7),
  never Plotly.
- **Relative links:** every file path named in this plan is relative to the
  repo root. When Chapter 8 links to Chapter 7 or Chapter 5, compute the
  path relative to `08-machine-learning/machine-learning.qmd` itself — e.g.
  `../07-statistics-ethics/statistics-ethics.qmd` and
  `../05-etl/Chapter4-Part3.qmd` — since all are sibling folders one level
  below the root.

---

## File Structure

```
07-statistics-ethics/statistics-ethics.qmd   # full rewrite of stub
08-machine-learning/machine-learning.qmd     # full rewrite of stub
09-ai-and-llms/ai-and-llms.qmd               # full rewrite of stub
```

---

### Task 1: Write Chapter 7 — Descriptive Statistics & Data Ethics

**Files:**
- Modify: `07-statistics-ethics/statistics-ethics.qmd` (replace stub)

**Interfaces:**
- Consumes: the "Data Has a Point of View" foreshadowing from Chapter 1
  (`01-what-is-data/what-is-data.qmd`) — this chapter is where that theme
  is resolved in depth; link back to it explicitly.
- Produces: glossary terms `Mean`, `Median`, `Mode`, `Correlation`,
  `Causation`, `Algorithmic Bias`, `Data Privacy`. Establishes MSE/R²
  vocabulary groundwork (mean and spread) that Chapter 8 uses directly —
  Chapter 8's Fable prompt (Task 2 of this plan) references this chapter.

- [ ] **Step 1: Draft using the Fable model**

Dispatch via `Agent` tool with `model: "fable"`. Prompt:

```
Write the full content for 07-statistics-ethics/statistics-ethics.qmd,
Chapter 7 of a high school data science textbook. Read
01-what-is-data/what-is-data.qmd in this repo first (it ends with a "Data
Has a Point of View" section on bias that this chapter explicitly resolves
in depth) and 04-python-pandas/Chapter3-Part1.qmd for voice.

Audience: high school sophomores. Assume basic arithmetic (they can compute
an average by hand) but no prior statistics course.

Required sections, in order:
1. Learning Objectives (4-5 bullets).
2. "Three Ways to Describe the Middle" — mean, median, and mode, each with
   a Definition callout and a worked numeric example using the same small
   dataset (e.g., 7 students' quiz scores, one of which is an outlier).
   Show explicitly how an outlier drags the mean but not the median, and
   when mode is the only one that makes sense (categorical data, e.g. most
   common favorite subject).
3. "Spread: How Different Are the Numbers From Each Other?" — introduce
   the idea of spread/variation informally (e.g., two classes can have the
   same mean test score but very different spreads) without requiring the
   standard deviation formula — just the intuition that "how spread out"
   matters as much as "what's typical." Note in one sentence that Chapter
   8 (Machine Learning) uses a related idea — Mean Squared Error — to
   measure how spread out a model's mistakes are.
4. "Correlation Is Not Causation" — a Definition callout for each term,
   plus the classic ice-cream-sales-and-drowning-rates example (both rise
   in summer heat; neither causes the other) and one more example the
   student can evaluate themselves (e.g., "cities with more fire trucks
   dispatched to a fire also tend to have more damage — do fire trucks
   cause damage?").
5. "Data Has a Point of View" (revisited from Chapter 1) — go deeper on
   algorithmic bias: define "Algorithmic Bias" in a Definition callout,
   with one concrete, factual, age-appropriate example (e.g., a hiring
   algorithm trained on a company's past hiring decisions can learn and
   repeat whatever bias existed in those past decisions, even without
   being told anyone's gender or race directly, because other data fields
   can correlate with them). Keep this factual and educational, not
   politically charged — the point is "bias in, bias out," not any
   specific policy debate.
6. "Your Data, Your Privacy" — define "Data Privacy" in a Definition
   callout. Cover: most apps/services collect more data about you than
   you might realize (tie back to Chapter 1's data-logging activity);
   consent and terms of service are how companies are supposed to tell
   you what they collect; think about what you're comfortable sharing
   before you share it.
7. At least 2 Knowledge Check callouts, placed after sections 2 and 5.
8. One "Try With ChatGPT" callout — e.g. asking ChatGPT for another
   real-world correlation/causation mix-up, then researching whether
   ChatGPT's example actually holds up (reinforces "always verify" from
   using-ai-responsibly.qmd).
9. "Your Turn" — given a small provided dataset (invent 8-10 rows of
   something concrete and relatable, e.g. minutes of homework per night
   for 10 students, with one clear outlier), compute mean, median, and
   mode by hand or in a spreadsheet, and write 2-3 sentences on which
   measure best represents the group and why.
10. A short roadmap paragraph previewing Chapter 8 (using these same
    ideas — spread, patterns, evaluating whether a relationship is real —
    to build a model that makes predictions).

Output only the final Markdown content, starting with YAML frontmatter
(`title: "Descriptive Statistics & Data Ethics"`, `author: "Technical
Instructional Team"`, `format: html`).
```

- [ ] **Step 2: Save and render standalone**

Save to `07-statistics-ethics/statistics-ethics.qmd`, run:
`quarto render 07-statistics-ethics/statistics-ethics.qmd 2>&1 | tail -30`
Expected: renders with no errors.

- [ ] **Step 3: Run the content checklist**

Open `docs/07-statistics-ethics/statistics-ethics.html` and confirm:
- [ ] Mean/median/mode each have a worked numeric example, and the outlier
      effect is shown explicitly, not just asserted
- [ ] Correlation-vs-causation has two examples, one the student evaluates themselves
- [ ] Algorithmic bias example is factual/educational, not politically charged
- [ ] Definition callouts present for all 7 required terms
- [ ] At least 2 Knowledge Checks, 1+ Try With ChatGPT callout, 1 Your Turn activity
- [ ] Link to Chapter 1 resolves

- [ ] **Step 4: Commit**

```bash
git add 07-statistics-ethics/statistics-ethics.qmd
git commit -m "Write Chapter 7: Descriptive Statistics & Data Ethics"
```

---

### Task 2: Write Chapter 8 — Introduction to Machine Learning

**Files:**
- Modify: `08-machine-learning/machine-learning.qmd` (replace stub)
- Read (source material, do not modify): `../Lecture Material/Session 5_ Machine Learning/DataScienceS5.py`

**Interfaces:**
- Consumes: the "spread"/MSE foreshadowing from Chapter 7
  (`07-statistics-ethics/statistics-ethics.qmd`) and the activity dataset
  (Alice/Charlie/Diana, Steps/HeartRate/Gender/DistanceFromSchool) already
  familiar from Chapter 5 (`05-etl/Chapter4-Part3.qmd` and
  `Chapter4-Part4.qmd`) — reuse this same dataset as the running example
  rather than introducing a new one.
- Produces: glossary terms `Machine Learning`, `Regression`,
  `Classification`, `Overfitting`, `Train/Test Split`, `Mean Squared Error
  (MSE)`, `R² Score`, `Decision Tree`.

- [ ] **Step 1: Draft using the Fable model**

Dispatch via `Agent` tool with `model: "fable"`. Prompt:

```
Write the full content for 08-machine-learning/machine-learning.qmd,
Chapter 8 of a high school data science textbook. Read
07-statistics-ethics/statistics-ethics.qmd and 05-etl/Chapter4-Part3.qmd
and Chapter4-Part4.qmd in this repo first — this chapter reuses the same
three-person activity dataset (Alice, Charlie, Diana; columns include
Steps, HeartRate, Gender, DistanceFromSchool, Hour of Day, MoneySpent) that
Chapter 5 already cleaned and encoded, and it reuses "spread"/MSE
vocabulary Chapter 7 already introduced informally.

Audience: high school sophomores who've completed Chapters 5 and 7.

This chapter's numbers are grounded in a real, verified script run — do
not invent different results. The actual code and results:

```python
import pandas as pd
from sklearn.model_selection import train_test_split

df = pd.read_csv("processed_full_activity_data.csv")

X = df[['Steps', 'Gender_code', 'Age', 'DistanceFromSchool', 'Hour of Day', 'MoneySpent($)']]
y = df['HeartRate']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

from sklearn.linear_model import LinearRegression
model = LinearRegression()
model.fit(X_train, y_train)
y_pred = model.predict(X_test)

from sklearn.metrics import mean_squared_error, r2_score
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)
print("Mean Squared Error:", mse)   # 484
print("R² Score:", r2)              # -1.8
```

Linear Regression result: MSE = 484, R² = -1.8 (very poor — worse than
just guessing the average every time, because the real dataset used for
this run was small and the relationship between the features and heart
rate isn't a straight line).

```python
from sklearn.tree import DecisionTreeRegressor
tree_model = DecisionTreeRegressor(random_state=42)
tree_model.fit(X_train, y_train)
y_pred_tree = tree_model.predict(X_test)

mse_tree = mean_squared_error(y_test, y_pred_tree)
r2_tree = r2_score(y_test, y_pred_tree)
print("Mean Squared Error:", mse_tree)  # 82
print("R² Score:", r2_tree)             # 0.52
```

Decision Tree result: MSE = 82, R² = 0.52 (much better — explains about
52% of the variation in heart rate).

Required sections, in order:
1. Learning Objectives (4-5 bullets).
2. "What Is Machine Learning?" — a Definition callout: teaching a computer
   to find patterns in data and make predictions from them, by showing it
   many examples, instead of writing exact rules by hand. 2-3 real-world
   examples students recognize (a recommendation feed, a self-driving
   car's obstacle detection).
3. "Regression vs. Classification" — Definition callout for each: regression
   predicts a number (continuous value), classification predicts a
   category (label). Table or list of real-world examples for each (predict
   tomorrow's temperature / estimate a house price = regression; spam vs.
   not spam / safe vs. toxic plant = classification). Ask the student which
   one predicting HeartRate from Steps/Age/etc. is (regression).
4. "Train/Test Split and Overfitting" — Definition callouts for both
   terms. Explain training data teaches the model, test data checks it on
   data it's never seen. Use the "memorizes practice questions but fails
   the real test" analogy for overfitting. List 2-3 ways to reduce
   overfitting (train/test split itself, simpler models, more data).
5. "Hands-On: Predicting Heart Rate with Linear Regression" — the verified
   code and MSE/R² = 484/-1.8 result above, in fenced Python code blocks
   with **Output:** blocks showing the printed values. Explain what MSE
   and R² mean in plain language (Definition callout for each): MSE is the
   average size of the model's mistakes, squared, so bigger mistakes count
   extra — lower is better; R² says what fraction of the pattern in the
   data the model actually explains, from 0 (no better than guessing the
   average) up to 1 (perfect), and it can even go negative when a model is
   worse than just guessing the average, which is what happened here.
   Describe (in words, following this book's existing "Reflective Code"
   pattern of code + description rather than an actual embedded image)
   what a matplotlib scatter plot of actual-vs-predicted heart rate would
   show for this result: points scattered far from the diagonal
   "perfect prediction" line.
6. "Why Did the Model Do So Poorly? And What Can We Try Instead?" — the
   three real limitations from the source material: a small/possibly noisy
   test set, linear regression assuming a straight-line relationship when
   the real one may not be, and possibly missing/wrong features. Then
   introduce Decision Trees as a different approach.
7. "Hands-On: Trying a Decision Tree" — the verified code and MSE/R² =
   82/0.52 result above, same Output: block treatment. Describe the
   matplotlib scatter plot again: points noticeably closer to the diagonal
   line than the Linear Regression version.
8. "Comparing the Two Models" — a short table: task type, how each model
   works (straight line vs. if/else rule splits), strengths, weaknesses,
   which did better here and why (the Decision Tree could capture a
   non-linear relationship the straight line couldn't).
9. At least 2 Knowledge Check callouts, placed after sections 4 and 8.
10. One "Try With ChatGPT" callout — e.g. pasting their own model's MSE
    and R² and asking ChatGPT to explain in plain English whether that's a
    good result.
11. "Your Turn" — using their own dataset (or the activity dataset from
    Chapter 5), pick a target column to predict, try both
    `LinearRegression()` and `DecisionTreeRegressor()`, compare MSE and R²,
    and write 2-3 sentences on which did better and why they think so.
12. A short roadmap paragraph previewing Chapter 9 (a much, much bigger
    version of "learning patterns from data" — how tools like ChatGPT
    itself were trained).

Output only the final Markdown content, starting with YAML frontmatter
(`title: "Introduction to Machine Learning"`, `author: "Technical
Instructional Team"`, `format: html`).
```

- [ ] **Step 2: Save and render standalone**

Save to `08-machine-learning/machine-learning.qmd`, run:
`quarto render 08-machine-learning/machine-learning.qmd 2>&1 | tail -30`
Expected: renders with no errors.

- [ ] **Step 3: Verify the numbers weren't altered**

Run: `grep -E '484|-1\.8|82|0\.52' 08-machine-learning/machine-learning.qmd`
Expected: all four verified figures (484, -1.8, 82, 0.52) appear in the
file. If any are missing or changed, the draft invented different numbers
— fix before proceeding.

- [ ] **Step 4: Run the content checklist**

Open `docs/08-machine-learning/machine-learning.html` and confirm:
- [ ] Regression vs. classification examples match the ones specified
- [ ] Both hands-on sections use the exact verified MSE/R² values
- [ ] MSE and R² are each explained in plain language, not just defined by formula
- [ ] Comparison table/section explains *why* the Decision Tree did better
- [ ] At least 2 Knowledge Checks, 1+ Try With ChatGPT callout, 1 Your Turn activity
- [ ] Links to Chapter 5 and Chapter 7 resolve

- [ ] **Step 5: Commit**

```bash
git add 08-machine-learning/machine-learning.qmd
git commit -m "Write Chapter 8: Introduction to Machine Learning"
```

---

### Task 3: Write Chapter 9 — How AI Learns From Data

**Files:**
- Modify: `09-ai-and-llms/ai-and-llms.qmd` (replace stub)

**Interfaces:**
- Consumes: `using-ai-responsibly.qmd` (front matter) and the "Machine
  Learning" concept from Chapter 8 — this chapter should say explicitly
  that an LLM is trained the same basic way (learn from labeled examples,
  test on unseen data) but at a vastly larger scale.
- Produces: glossary terms `Large Language Model (LLM)`, `Training Data
  (AI)`, `Prompt`, `Hallucination (AI)`. This chapter is the natural home
  for a deeper prompting lesson that every earlier "Try With ChatGPT"
  callout in the book implicitly assumed — it should say so explicitly.

- [ ] **Step 1: Draft using the Fable model**

Dispatch via `Agent` tool with `model: "fable"`. Prompt:

```
Write the full content for 09-ai-and-llms/ai-and-llms.qmd, Chapter 9 of a
high school data science textbook. Read using-ai-responsibly.qmd and
08-machine-learning/machine-learning.qmd in this repo first — this chapter
is the payoff for every "Try With ChatGPT" callout used earlier in the
book, and it should explicitly connect back to Chapter 8's "train on
examples, test on unseen data" idea, just at enormous scale.

Audience: high school sophomores who've completed Chapter 8 and have used
several "Try With ChatGPT" callouts already without a deep explanation of
what's on the other end of that prompt.

Required sections, in order:
1. Learning Objectives (4-5 bullets).
2. "What Is a Large Language Model?" — a Definition callout for "Large
   Language Model (LLM)": a machine learning model trained on enormous
   amounts of text to predict what word (or word-fragment) is most likely
   to come next, given everything before it. Explicitly connect to Chapter
   8: same basic idea as the heart-rate model — learn a pattern from
   examples — but trained on a giant fraction of publicly available text
   instead of 216 rows of activity data, and predicting the next word
   instead of a heart rate number.
3. "Where Does the Training Data Come From?" — a Definition callout for
   "Training Data (AI)": books, websites, articles, code, and other text
   gathered at massive scale. Tie back to Chapter 1's "Data Has a Point of
   View" and Chapter 7's "Algorithmic Bias" — if the training data
   reflects biases or gaps (e.g., overrepresenting some languages,
   viewpoints, or time periods), the model's responses can reflect those
   same biases or gaps, for the exact same reason a hiring algorithm can.
4. "Prompting Is a Skill" — a Definition callout for "Prompt": the text
   you give the model to get a response. Show one vague prompt and one
   specific, well-structured prompt about the same topic (pick a topic
   from earlier in this book, e.g. asking about `.loc` vs `.query()` from
   Chapter 4) side by side, and explain concretely why the specific one
   gets a more useful answer (context, a clear question, a stated format
   for the answer).
5. "When AI Gets It Confidently Wrong" — a Definition callout for
   "Hallucination (AI)": when a model states something false as if it
   were fact, often fluently and confidently. Explain why this happens in
   one plain-language sentence (the model is predicting plausible-sounding
   text, not looking up guaranteed-true facts unless it's specifically
   connected to a search/tool). Reinforce using-ai-responsibly.qmd's
   "always verify" rule with one concrete example relevant to this course
   (e.g., asking ChatGPT for a pandas method name that sounds right but
   doesn't actually exist).
6. At least 2 Knowledge Check callouts, placed after sections 3 and 5.
7. One larger "Try With ChatGPT" callout than usual — have the student
   write a vague prompt and a specific prompt about the same data-science
   question, compare the two responses, and note which parts (if any) of
   either response they should double-check before trusting.
8. "Your Turn" — pick any factual claim ChatGPT makes in response to one
   of their own prompts and actually verify it (against this book, a
   search, or by running code), then write 2-3 sentences on whether it
   held up.
9. A short roadmap paragraph previewing Unit IV (Chapters 10-11): using
   everything so far — data cleaning, statistics, visualization, models,
   and now AI as a tool — to build and present an original project.

Output only the final Markdown content, starting with YAML frontmatter
(`title: "How AI Learns From Data"`, `author: "Technical Instructional
Team"`, `format: html`).
```

- [ ] **Step 2: Save and render standalone**

Save to `09-ai-and-llms/ai-and-llms.qmd`, run:
`quarto render 09-ai-and-llms/ai-and-llms.qmd 2>&1 | tail -30`
Expected: renders with no errors.

- [ ] **Step 3: Run the content checklist**

Open `docs/09-ai-and-llms/ai-and-llms.html` and confirm:
- [ ] Explicit connection made back to Chapter 8's ML framing
- [ ] Vague-vs-specific prompt example is concrete and shows a real difference
- [ ] Hallucination example is specific to this course's domain (not generic)
- [ ] Definition callouts present for all 4 required terms
- [ ] At least 2 Knowledge Checks, the one larger Try-With-ChatGPT exercise, 1 Your Turn activity
- [ ] Links to using-ai-responsibly.qmd and Chapter 8 resolve

- [ ] **Step 4: Commit**

```bash
git add 09-ai-and-llms/ai-and-llms.qmd
git commit -m "Write Chapter 9: How AI Learns From Data"
```

---

## Self-Review Notes

- **Spec coverage:** all three Unit III chapters from spec §4 are covered,
  including the "inserted before Machine Learning" ordering decision from
  the brainstorming phase (Ch. 7 before Ch. 8) and the §7 matplotlib-only
  visualization constraint.
- **Placeholder scan:** Chapter 8's Fable prompt embeds the actual verified
  script and its actual results rather than describing them abstractly;
  Task 2 Step 3 mechanically checks the numbers survived the draft intact.
- **Type/interface consistency:** Chapter 8 reuses the exact column names
  (`Steps`, `Gender_code`, `DistanceFromSchool`, etc.) already established
  in Chapter 5's encoding section, rather than introducing new ones.
