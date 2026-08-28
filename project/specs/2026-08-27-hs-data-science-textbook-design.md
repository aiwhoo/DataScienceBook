# High School Data Science Textbook — Design Spec

Date: 2026-08-27
Status: Approved by user, pending spec review pass

## 1. Purpose and Context

This repository holds the start of a Quarto book meant to be the standalone
**textbook** for a sophomore-level high school data science course. The book
must stand on its own — a student should be able to learn from it
independent of whatever a given teacher's lecture or syllabus covers that
term.

The repo currently contains two complete chapters (Python & Pandas; ETL)
adapted from an existing 6-session course whose slide decks live in
`../Lecture Material/`. Those slides are background material, not a
contract — the book is free to diverge in scope, order, and depth. This spec
expands the original 6-session course into a fuller 11-chapter textbook.

Research done before writing this spec (see "Verified facts" below)
confirmed two things the user flagged from memory: **Plotly Chart Studio**
(the no-code drag-and-drop tool the course used for Chapter/Session 2) shut
down permanently on **October 31, 2025**, and the Heroku-hosted dashboard
demo linked from the same session is also dead (free Heroku hosting ended in
2022). Both need replacing.

## 2. Audience and Tone

- **Audience:** high school sophomores (roughly age 15-16). No assumed prior
  programming experience; general middle-school math (percentages, basic
  algebra, coordinate planes) is assumed.
- **Tone:** the existing Python/ETL chapters set the bar — conversational,
  encouraging, concrete real-world hooks (the LEGO metaphor, "iPhone of
  coding," Instructor Insight callouts). New and revised chapters should
  match this voice, not shift to a drier textbook register.
- **Privacy/safety guardrail:** any activity that touches a student's real
  personal data (e.g., the original course's "browse your own Google
  Takeout export," "paste real text messages into a sentiment tool") must be
  redesigned for a self-serve textbook: make the activity optional/teacher-
  supervised, or substitute a provided sample dataset so no student is
  required to expose their own data or a friend's private messages to a
  third-party website to complete the reading.

## 3. Verified Facts (tool/link research)

| Item | Status | Action |
|---|---|---|
| `chart-studio.plotly.com` (Plotly Chart Studio) | Confirmed dead (shut down Oct 31, 2025) | Replace with **CODAP** (codap.concord.org) for all student-facing drag-and-drop charting |
| `tracking-dashboard-app.herokuapp.com` (Session 2 dashboard demo) | Confirmed dead (stuck on "Loading...", Dash app, free Heroku dynos killed 2022) | Replace with a dashboard example built in CODAP or a static screenshot + description; do not link to it |
| `danielsoper.com/sentimentanalysis` (Session 1 texting activity) | Confirmed live and working | May keep, but redesign the activity itself (see §2 privacy guardrail) so it uses provided sample text, not students' real messages |
| CODAP (codap.concord.org) | Confirmed free, no login/account, no student data stored, built for grades 5-14 by Concord Consortium, actively maintained (v3 beta in progress in 2026) | Adopt as the book's primary no-code visualization tool |

## 4. Table of Contents

Front matter, 11 chapters in 4 units, back matter. Numbering is driven by
order in `_quarto.yml`, not by folder names, so folders use topic slugs
(see §6) rather than chapter numbers — this avoids ever having to rename
folders again if a chapter is inserted or reordered later.

**Front matter**
- Preface (real one, replacing the current placeholder `index.qmd`)
- How to Use This Book
- Using AI Responsibly (primer: ChatGPT as a tutor, not a ghostwriter;
  verify what it tells you; ask your teacher what's allowed for graded
  work; it can be confidently wrong)

**Unit I — Foundations**
1. What Is Data? *(revise existing Session 1 material)*
   - Data is everywhere: structured vs. unstructured data
   - You are a data source (redesigned activity — see §2)
   - Data has a point of view: bias and incompleteness (seeds Ch. 7)
2. Data Wrangling with Spreadsheets *(new)*
   - Sorting, filtering, and why "just eyeballing it" breaks down
   - Core formulas: `UNIQUE`, `COUNTIF`, `SUM`, basic `VLOOKUP`
   - Pivot tables as a preview of `groupby`
3. Data Visualization Basics *(rebuild of Session 2 on CODAP)*
   - Choosing a chart type: bar, line, pie, scatter
   - Hands-on dashboard building in CODAP
   - How charts mislead (truncated axes, dual-axis tricks, cherry-picking)

**Unit II — Programming for Data Science**
4. Python & Pandas: Working with Big Data *(existing — polish only)*
5. ETL in Action: Cleaning & Preprocessing *(existing — polish only)*
6. Where Data Comes From: APIs & Real-World Sources *(new)*
   - Files vs. databases vs. APIs vs. sensors
   - Hands-on: pulling JSON from one free public API with `requests`
   - Ethics/legality of web scraping, rate limits, terms of service

**Unit III — Understanding and Modeling Data**
7. Descriptive Statistics & Data Ethics *(new)*
   - Mean, median, mode, spread; when each is misleading
   - Correlation vs. causation
   - Bias, privacy, and fairness in data and algorithms
8. Introduction to Machine Learning *(new, from Session 5)*
   - Regression vs. classification
   - Train/test split and overfitting
   - Linear regression and decision trees with scikit-learn; MSE and R²
9. How AI Learns From Data *(new)*
   - What a large language model is, in one page
   - How ChatGPT was trained: data at massive scale (ties directly to
     Chs. 1, 4, 5, 7)
   - Prompting as a skill; hallucination and other limits

**Unit IV — Communicating and Applying Data Science**
10. Designing Your Own Data Science Project *(new, from Session 6 pt. 1)*
    - Choosing a dataset and a research question
    - Project workflow and rubric, mapped back to Chs. 4-9
11. Telling Your Data Story *(new, from Session 6 pt. 2)*
    - The four elements of data storytelling (context, narrative, data,
      visual design)
    - Matching visuals to narrative; audience Q&A prep
    - Using ChatGPT to pressure-test and polish a data story

**Back matter**
- Glossary (collects every "Definition" callout from the chapters)
- Getting Set Up (PyCharm, from the existing Ch. "Python" content, **plus** a
  Google Colab no-install alternative for school Chromebooks)
- Dataset & Tool Directory (Delaware Open Data Portal, Kaggle, CODAP, Google
  Sheets, PyCharm, Colab, scikit-learn docs — one-page quick reference)

## 5. Pedagogy Components (apply to every chapter, old and new)

**Knowledge checks.** One short check after each major section: a
multiple-choice or fill-in question plus a one-line reflection prompt,
using Quarto's native collapsible callout so the answer is hidden until
clicked:

```markdown
::: {.callout-tip title="Knowledge Check"}
Which pandas method would you use to see if a column is numeric or text?

::: {.callout-note collapse="true" title="Reveal Answer"}
`df.info()` — it lists each column's data type.
:::
:::
```

This replaces the old pattern of "Your Turn" open-ended activities — it
doesn't remove them, it adds a lighter-weight check students can use to
confirm they followed the section before moving on. "Your Turn" activities
stay as the larger, open-ended application exercise near the end of each
chapter.

**"Try With ChatGPT" callout.** One per chapter (sometimes more, where a
concept naturally invites it), giving a copy-pasteable prompt tied to that
section's concept:

```markdown
::: {.callout-tip title="🤖 Try With ChatGPT"}
Paste your `df.info()` output into ChatGPT and ask: *"Which of these columns
are actually categorical, even though they look numeric? How can you tell?"*
:::
```

This generalizes what Sessions 2 and 6 already did ad hoc into a consistent,
recurring feature across all 11 chapters, per the user's request.

**Fixing a fragile existing pattern.** Chapters 3-4 (existing) simulate
console output using inline `<script>`/`document.write` blocks. This works
in HTML but is unnecessary complexity and fragile (breaks silently if
JavaScript is disabled or the format ever changes). New chapters will use a
plain, clearly-labeled output block instead:

```markdown
​```python
df.info()
​```

**Output:**
```
<class 'pandas.core.frame.DataFrame'>
...
```
```

The existing JS-based examples in Chs. 4-5 (old 3-4) can be converted to this
pattern during the polish pass — low-risk, mechanical, improves robustness.

## 6. Repository Structure

```
DataScienceBook/
  index.qmd                          # real preface (rewritten)
  how-to-use-this-book.qmd           # new
  using-ai-responsibly.qmd           # new
  01-what-is-data/
  02-spreadsheets/
  03-data-visualization/
  04-python-pandas/                  # renamed from Chapter3/ (content kept)
  05-etl/                            # renamed from Chapter4/ (content kept)
  06-apis-data-sources/
  07-statistics-ethics/
  08-machine-learning/
  09-ai-and-llms/
  10-capstone-project/
  11-data-storytelling/
  glossary.qmd                       # new
  getting-set-up.qmd                 # new (PyCharm + Colab)
  dataset-and-tool-directory.qmd     # new
  _quarto.yml                        # updated chapter list/order
  styles.css                         # extended with a shared callout style
```

`Chapter3/` → `04-python-pandas/` and `Chapter4/` → `05-etl/` are `git mv`
renames that preserve history; file contents inside are polished in place,
not rewritten from scratch.

## 7. Visualization Approach (two distinct tools, don't conflate them)

1. **Student-facing, no-code tool (Ch. 3 Data Visualization Basics):**
   CODAP. Free, no login, privacy-safe, purpose-built for this age group.
   Replaces Plotly Chart Studio everywhere in the book.
2. **In-book code examples that produce a chart (Chs. 5, 8, etc.):**
   `matplotlib`/`seaborn`, static images. This matches what the existing
   Session 5/Chapter 8 machine-learning script already does (scatter plots
   of actual vs. predicted values) — no change needed there, and it keeps
   every code chapter on one plotting library instead of introducing Plotly
   (or another interactive JS library) as a second one. The book stays
   render-reliable and consistent; the *drag-and-drop, interactive*
   experience students get is CODAP, not a Python chart.

Large datasets (e.g., the 539,947-row Delaware crash data) are **not**
bundled in the repo — chapters continue to instruct students to download
them from the Delaware Open Data Portal, exactly as today. Code blocks that
depend on such files remain non-executed (` ```python `, not ` ```{python} `)
with a labeled sample **Output:** block, per §5. The one dataset small
enough to bundle — the 3-person/3-day activity dataset reused across
Ch. 5 (ETL) and Ch. 8 (Machine Learning) — is a candidate for bundling as a
real CSV so those code blocks can execute for real; this is a nice-to-have,
not required for v1, and can be deferred to a follow-up if it adds too much
implementation risk.

## 8. Authoring Workflow

Per the user's request, chapter prose is drafted/revised using the **Fable**
model (`Agent` tool, `model: "fable"`). Each chapter is an independent unit
of work (own file(s), own topic, cross-references only by hyperlink), so
chapters are well suited to being drafted in parallel once this spec and its
implementation plan are approved — the implementation plan (next step, via
`writing-plans`) will lay out the concrete per-chapter task breakdown and
decide sequencing/parallelism there.

## 9. Testing / Validation

- `quarto render` must complete without errors after every chapter is added
  and after the `Chapter3`/`Chapter4` → `04-python-pandas`/`05-etl` renames.
- Every external link added or kept in the book (CODAP, Delaware Open Data
  Portal, Kaggle, Colab, PyCharm, the sentiment tool) is checked live before
  the chapter is considered done, not just carried over from the old slides.
- Spot-check that knowledge-check reveal callouts actually collapse/expand
  correctly in the rendered HTML output.

## 10. Out of Scope (for this pass)

- Translating the book to non-English.
- A PDF/EPUB output target (the book currently only renders to HTML; no
  request was made to change that).
- Autograding or an LMS integration for the knowledge checks — they are
  self-check only.
- Rewriting the existing Ch. 4/5 (Python/ETL) content wholesale — only a
  polish pass (pedagogy components + output-block fix) is planned for them.
