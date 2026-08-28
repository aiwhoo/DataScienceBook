# Unit I: Foundations Content Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Write the real content for Chapters 1-3 (What Is Data?, Data
Wrangling with Spreadsheets, Data Visualization Basics), replacing the
frontmatter-only stubs created by the infrastructure plan.

**Architecture:** Each chapter is one self-contained `.qmd` file, drafted by
a Fable-model agent against a fully-specified brief, then verified against a
concrete checklist and rendered standalone before being committed.

**Tech Stack:** Quarto 1.8, Markdown/`.qmd`, CODAP (codap.concord.org) as
the referenced student tool for Chapter 3.

**Spec:** `project/specs/2026-08-27-hs-data-science-textbook-design.md`

**Prerequisite:** `project/plans/2026-08-27-01-infrastructure-and-front-matter.md` must be complete (stub files and `_quarto.yml` exist).

## Global Constraints

- Audience: high school sophomores, no assumed programming experience.
- Tone: conversational, encouraging, concrete real-world hooks, matches the
  voice of `04-python-pandas/Chapter3-Part1.qmd` — every Fable prompt in
  this plan should tell the agent to read that file first for voice.
- Privacy guardrail: no activity may require a student's real personal
  account data or a friend's private messages; provide sample data as the
  default path, with any real-data version framed as optional/teacher-
  supervised.
- Knowledge Check callout (exact syntax, one or more per chapter after major sections):
  ```markdown
  ::: {.callout-tip .knowledge-check title="Knowledge Check"}
  Question here?

  ::: {.callout-note collapse="true" title="Reveal Answer"}
  Answer here.
  :::
  :::
  ```
- "Try With ChatGPT" callout (exact syntax, at least one per chapter):
  ```markdown
  ::: {.callout-tip .chatgpt-callout title="🤖 Try With ChatGPT"}
  A ready-to-use prompt tied to this section's concept.
  :::
  ```
- "Definition" callout for new vocabulary (existing convention, keep using it):
  ```markdown
  ::: {.callout-note}
  ### Term
  Definition text.
  :::
  ```
- Output-block convention for any shown code (no inline `<script>`/`document.write`):
  ` ```python ` fenced block, then a `**Output:**` label, then a plain fenced text block showing the sample result.
- Visualization: CODAP only for no-code student activities in this unit —
  never reference Plotly or Plotly Chart Studio (confirmed dead as of
  Oct 31, 2025).
- Every external link referenced in a chapter must be verified live via
  `WebFetch` before the chapter's task is marked done.
- Author chapter prose by dispatching the `Agent` tool with `model: "fable"`.
- **Relative links:** every file path named in this plan is relative to the
  repo root (e.g. `01-what-is-data/what-is-data.qmd`). When a chapter task
  says to link to another chapter, compute the actual Markdown link path
  relative to *the file being written*, not the repo root — e.g. a link
  from `02-spreadsheets/spreadsheets.qmd` to `01-what-is-data/what-is-data.qmd`
  is `../01-what-is-data/what-is-data.qmd`, since both are one level down
  from the root in sibling folders.

---

## File Structure

```
01-what-is-data/what-is-data.qmd               # full rewrite of stub
02-spreadsheets/spreadsheets.qmd               # full rewrite of stub
03-data-visualization/data-visualization.qmd   # full rewrite of stub
```

---

### Task 1: Write Chapter 1 — What Is Data?

**Files:**
- Modify: `01-what-is-data/what-is-data.qmd` (replace stub)

**Interfaces:**
- Consumes: nothing (first content chapter).
- Produces: glossary terms `Data`, `Structured Data`, `Unstructured Data`,
  `Data Logging`, `Bias (in data)` — each must appear in its own Definition
  callout so the back-matter plan can collect them into `glossary.qmd`.
  Also produces the "data has a point of view" theme that Chapter 7
  (Statistics & Data Ethics) explicitly builds on — this chapter should
  foreshadow it in one paragraph, not resolve it.

- [ ] **Step 1: Draft using the Fable model**

Dispatch via `Agent` tool with `model: "fable"`. Prompt:

```
Write the full content for 01-what-is-data/what-is-data.qmd, Chapter 1 of a
high school data science textbook. Read 04-python-pandas/Chapter3-Part1.qmd
in this repo first to match its voice (conversational, concrete metaphors,
Definition/Instructor-Insight callouts, a roadmap at the end).

Audience: high school sophomores, no assumed programming experience.

Source material to draw from (a past in-person version of this course):
- Big Question: "What is data? Where does it come from in our lives?"
  Big Answer: data is information that can be collected, stored, and
  analyzed — it comes from our actions, our devices, and the world
  around us.
- Structured vs. unstructured data: structured = neatly organized, easy
  for computers to analyze (step counts, GPS coordinates, calendar
  events with time/date); unstructured = no set format, harder to
  process (photos, videos, voice memos).
- What students will learn across the whole book (briefly preview, one
  sentence each): cleaning/organizing datasets, visualizations and
  dashboards, simple machine learning models, how data can be biased or
  misleading, how data is used in tech/government/business.

Required sections, in order:
1. Learning Objectives (4-5 bullets, standard format matching existing chapters).
2. "The Big Question" — hook framing above.
3. "Structured vs. Unstructured Data" — the definitions above, each in
   its own `::: {.callout-note}` Definition box (term: "Structured Data",
   term: "Unstructured Data"), with 3 concrete examples each.
4. "You Are a Data Source" — an activity where the student logs their own
   day (screen time, steps, what they ate, when they slept) for 24 hours
   and looks for patterns. This is safe by design (self-chosen, not an
   account data export) — do not add any account-login or personal-data-
   export step here.
5. "A Different Kind of Data Source" — briefly describe, as a *read-only,
   optional, ask-a-parent-or-teacher-first* aside (use a `::: {.callout-important}`
   or similar box, clearly marked optional), that services like Google
   keep a detailed history of your searches and activity ("Google
   Takeout" lets you download it) — but the book's actual exercise here
   uses a **provided sample** of what such an export looks like (make up
   3-4 realistic-but-fake sample rows: a search query, a video watched, a
   calendar event, each with a timestamp) so every student can do the
   exercise without exposing real account data. Ask: what does this
   sample suggest about the person? What's missing or could be
   misread?
6. "Data Has a Point of View" — introduce bias and incompleteness:
   define "Bias (in data)" in a Definition callout, with a short example
   (e.g., a step-counter undercounts activity for someone using a
   wheelchair). End with 1-2 sentences explicitly previewing that Chapter
   7 (Descriptive Statistics & Data Ethics) goes much deeper on this.
7. At least 2 Knowledge Check callouts (exact syntax provided in this
   plan's Global Constraints) placed after sections 3 and 6.
8. One "Try With ChatGPT" callout (exact syntax provided) — e.g. asking
   ChatGPT to help brainstorm what other everyday things generate data
   the student hadn't thought of.
9. "Your Turn" activity — a slightly bigger version of the 24-hour data
   log from section 4: log data for 2-3 days and write 3 sentences on
   what surprised them.
10. A short roadmap paragraph previewing Chapter 2 (spreadsheets).

Do NOT include: any activity requiring pasting real text messages into a
third-party site, any required account login/export, or any webcam/pose-
detection activity (these don't fit a self-paced reading format safely —
they're fine as in-person supervised activities but this is a textbook).

Output only the final Markdown content, starting with YAML frontmatter
(`title: "What Is Data?"`, `author: "Technical Instructional Team"`,
`format: html`).
```

- [ ] **Step 2: Save and render standalone**

Save the output to `01-what-is-data/what-is-data.qmd`, run:
`quarto render 01-what-is-data/what-is-data.qmd 2>&1 | tail -30`
Expected: renders with no errors.

- [ ] **Step 3: Run the content checklist**

Open `docs/01-what-is-data/what-is-data.html` and confirm:
- [ ] Learning Objectives section present with 4-5 bullets
- [ ] "Structured Data" and "Unstructured Data" each have their own Definition callout
- [ ] No activity requires real account data export or real private messages
- [ ] At least 2 Knowledge Check callouts, each collapsed by default and expanding on click
- [ ] Exactly 1+ "Try With ChatGPT" callout present, styled with the green accent from `styles.css`
- [ ] A "Your Turn" activity is present near the end
- [ ] No leftover template content (no cat image, no Codecademy table)

- [ ] **Step 4: Commit**

```bash
git add 01-what-is-data/what-is-data.qmd
git commit -m "Write Chapter 1: What Is Data?"
```

---

### Task 2: Write Chapter 2 — Data Wrangling with Spreadsheets

**Files:**
- Modify: `02-spreadsheets/spreadsheets.qmd` (replace stub)

**Interfaces:**
- Consumes: the "structured data" concept from Chapter 1 (link back to it:
  `[Chapter 1](../01-what-is-data/what-is-data.qmd)`).
- Produces: glossary terms `Formula`, `Filter (spreadsheet)`, `Pivot Table`,
  `Cell Reference`. Also produces the "sorting/filtering/grouping" mental
  model that Chapter 4's `.loc`/`.query()` filtering and Chapter 5's
  `groupby`/aggregation sections explicitly parallel — this chapter should
  say, in one sentence near the end, that these same ideas come back in
  Python.

- [ ] **Step 1: Draft using the Fable model**

Dispatch via `Agent` tool with `model: "fable"`. Prompt:

```
Write the full content for 02-spreadsheets/spreadsheets.qmd, Chapter 2 of a
high school data science textbook. Read 04-python-pandas/Chapter3-Part1.qmd
and 04-python-pandas/Chapter3-Part4.qmd in this repo first to match voice
and to see how this book already talks about filtering (this chapter is
the "before Python" version of that same skill).

Audience: high school sophomores, no assumed programming experience.
Assume they've used Google Sheets casually but never for real analysis.

Source material to draw from (a past in-person version of this course
used Google Sheets to prep data before charting it):
- Using `=UNIQUE(range)` to list distinct values in a column (example:
  finding the distinct weekdays in a crash-date column).
- Using `=COUNTIF(range, criteria)` to count how many rows match a value
  (example: counting how many crashes happened on each weekday).
- Using filters (Data menu → Create a filter) to narrow a large dataset
  down to a manageable subset (example: filtering 500,000+ rows of
  Delaware crash data down to one county and a 5-year window).

Required sections, in order:
1. Learning Objectives (4-5 bullets).
2. "Why Spreadsheets First?" — sorting/filtering by eye works for 20 rows
   and breaks down fast; a real dataset might have hundreds of thousands.
   Reference the Delaware Open Data Portal (https://data.delaware.gov/)
   crash dataset (539,947 rows) the same way 04-python-pandas/Chapter3-Part1.qmd
   does, to keep the running example consistent across chapters.
3. "Sorting and Filtering" — Data menu → Create a filter, filtering to one
   category and a numeric range, with a Definition callout for "Filter
   (spreadsheet)".
4. "Formulas That Do the Counting For You" — `=UNIQUE()` and `=COUNTIF()`
   with the crash-data-by-weekday example above, each formula shown in a
   fenced code block (use plain text fenced blocks, not Python — these are
   spreadsheet formulas), with a Definition callout for "Formula" and one
   for "Cell Reference".
5. "Pivot Tables: Grouping Made Visual" — introduce pivot tables as a
   drag-and-drop way to do what COUNTIF does but for many categories at
   once (e.g., total crashes per weekday per year in one table). Definition
   callout for "Pivot Table". End this section with one sentence: "This
   exact idea — group rows by a category and summarize them — comes back
   later as Python's `groupby()` in Chapter 5."
6. At least 2 Knowledge Check callouts after sections 3 and 5.
7. One "Try With ChatGPT" callout — e.g. asking ChatGPT to explain what a
   specific COUNTIF formula does, or to suggest a formula for a stated goal.
8. "Your Turn" — download a small dataset from the Delaware Open Data
   Portal or Kaggle, use UNIQUE + COUNTIF to summarize one categorical
   column, and build one pivot table.
9. A short roadmap paragraph previewing Chapter 3 (turning that summarized
   data into charts).

Output only the final Markdown content, starting with YAML frontmatter
(`title: "Data Wrangling with Spreadsheets"`, `author: "Technical
Instructional Team"`, `format: html`).
```

- [ ] **Step 2: Save and render standalone**

Save to `02-spreadsheets/spreadsheets.qmd`, run:
`quarto render 02-spreadsheets/spreadsheets.qmd 2>&1 | tail -30`
Expected: renders with no errors.

- [ ] **Step 3: Run the content checklist**

Open `docs/02-spreadsheets/spreadsheets.html` and confirm:
- [ ] Learning Objectives present
- [ ] `UNIQUE`, `COUNTIF`, and pivot tables each have a worked example
- [ ] Definition callouts present for Formula, Filter, Cell Reference, Pivot Table
- [ ] The `groupby()` foreshadowing sentence is present
- [ ] At least 2 Knowledge Checks, 1+ Try With ChatGPT callout, 1 Your Turn activity
- [ ] Link to Chapter 1 resolves (check the relative path matches `01-what-is-data/what-is-data.qmd`)

- [ ] **Step 4: Commit**

```bash
git add 02-spreadsheets/spreadsheets.qmd
git commit -m "Write Chapter 2: Data Wrangling with Spreadsheets"
```

---

### Task 3: Write Chapter 3 — Data Visualization Basics

**Files:**
- Modify: `03-data-visualization/data-visualization.qmd` (replace stub)

**Interfaces:**
- Consumes: the "filtered/summarized data" output of Chapter 2 (this
  chapter's hands-on activity should say "use the summarized data from
  Chapter 2's Your Turn activity, or make a new one the same way").
- Produces: glossary terms `Dashboard`, `Trace`, `Dual-Axis Chart`, `Data
  Visualization`. Establishes CODAP as the book's no-code tool — every
  later reference to "build a chart without code" (if any) should point
  back to this chapter, not introduce a different tool.

- [ ] **Step 1: Research current CODAP workflow before drafting**

CODAP's UI is not something to describe from memory — verify the actual
current steps. Run:
`WebFetch` on `https://codap.concord.org/` and on `https://learn.concord.org/resources/2036/a-tool-for-doing-data-science-codap`
with the prompt: "Describe the concrete steps to: (1) import a CSV file
into CODAP, (2) create a graph from two columns, (3) change the graph
type (e.g., to a bar or scatter graph), (4) add a second attribute to
compare multiple variables. List exact menu/button names if visible."

Keep the returned steps — they go directly into the Fable prompt below in
place of `<CODAP_STEPS>`.

- [ ] **Step 2: Draft using the Fable model**

Dispatch via `Agent` tool with `model: "fable"`. Prompt (fill in
`<CODAP_STEPS>` with the real result from Step 1 before sending):

```
Write the full content for 03-data-visualization/data-visualization.qmd,
Chapter 3 of a high school data science textbook. Read
04-python-pandas/Chapter3-Part1.qmd in this repo first to match voice.

Audience: high school sophomores, no assumed programming experience.

The verified, current, step-by-step workflow for CODAP (codap.concord.org),
the free no-code tool this chapter teaches (use these exact steps, don't
invent different ones):
<CODAP_STEPS>

Required sections, in order:
1. Learning Objectives (4-5 bullets).
2. "Dataset vs. Dashboard" — a dataset is the raw data; a dashboard is the
   visual display of results (car dashboard / phone lock screen analogy).
3. "Choosing the Right Chart" — for each of bar, line, pie, and scatter:
   one sentence on what it's for and one concrete example (e.g., bar =
   compare categories like "number of crashes per weekday"; line = trends
   over time like "temperature throughout the day"; pie = proportions of a
   whole like "percent of students who prefer each sport"; scatter =
   relationships between two things like "does height predict weight?").
4. "Hands-On: Building Your First Chart in CODAP" — walk through the
   verified CODAP steps above using the Chapter 2 summarized crash-by-
   weekday data as the running example (import it, build a bar chart of
   crashes per weekday, add titles).
5. "Comparing Multiple Variables" — using CODAP to show a second
   attribute/graph so two variables can be compared side by side (adapt
   this from the verified steps — CODAP does this differently than the
   old Plotly "dual Y-axis" approach; do not describe a dual-Y-axis
   workflow unless the verified CODAP steps actually support one).
6. "Build Your Own Dashboard" — rather than watching an external demo
   dashboard (a previously-used demo link is now dead), have the student
   build a small 2-chart dashboard themselves in CODAP using the same
   crash dataset, then answer: which chart tells the story better, and
   why?
7. "How Charts Can Mislead" — new content: truncated/non-zero-start axes
   exaggerating differences, mismatched scales making two things look
   equal when they aren't, cherry-picking a time window that hides the
   real trend. One short example of each, described in words (no need for
   actual images).
8. At least 2 Knowledge Check callouts, placed after sections 3 and 7.
9. One "Try With ChatGPT" callout — e.g. describing a chart in words and
   asking ChatGPT whether a different chart type would tell the story
   more clearly.
10. "Your Turn" — pick a dataset (Delaware Open Data Portal or Kaggle),
    build at least two chart types in CODAP, and write 2-3 sentences on
    what pattern each chart reveals (or hides).
11. Definition callouts for "Dashboard", "Trace" (a layer of data shown on
    a chart), "Dual-Axis Chart" (only if the verified CODAP research
    supports this concept — otherwise define it as a general chart-
    literacy term, not a CODAP-specific feature), and "Data Visualization".
12. A short roadmap paragraph previewing Chapter 4 (doing this same kind
    of filtering/summarizing with actual code, for when a dataset is too
    big even for a spreadsheet).

Do not mention Plotly, Plotly Chart Studio, or link to any Heroku-hosted
demo — Chart Studio shut down October 31, 2025 and the old demo link is
dead.

Output only the final Markdown content, starting with YAML frontmatter
(`title: "Data Visualization Basics"`, `author: "Technical Instructional
Team"`, `format: html`).
```

- [ ] **Step 3: Save and render standalone**

Save to `03-data-visualization/data-visualization.qmd`, run:
`quarto render 03-data-visualization/data-visualization.qmd 2>&1 | tail -30`
Expected: renders with no errors.

- [ ] **Step 4: Verify every external link**

Run `WebFetch` on every URL that appears in the rendered chapter (at minimum
`https://codap.concord.org/` and `https://data.delaware.gov/`) and confirm
each resolves to a live, relevant page. Fix or remove any that don't.

- [ ] **Step 5: Run the content checklist**

Open `docs/03-data-visualization/data-visualization.html` and confirm:
- [ ] No mention of Plotly, Chart Studio, or the dead Heroku demo link
- [ ] CODAP steps match what was actually verified in Step 1 (not invented)
- [ ] Bar/line/pie/scatter each have a "what it's for" example
- [ ] "How Charts Can Mislead" section present with 3 concrete failure modes
- [ ] At least 2 Knowledge Checks, 1+ Try With ChatGPT callout, 1 Your Turn activity
- [ ] Definition callouts present for Dashboard, Trace, Data Visualization

- [ ] **Step 6: Commit**

```bash
git add 03-data-visualization/data-visualization.qmd
git commit -m "Write Chapter 3: Data Visualization Basics (CODAP-based, replaces dead Plotly Chart Studio content)"
```

---

## Self-Review Notes

- **Spec coverage:** all three Unit I chapters from spec §4 are covered
  (What Is Data, Spreadsheets, Data Visualization), including the §2
  privacy guardrail (Task 1) and the §3 tool-replacement requirement
  (Task 3).
- **Placeholder scan:** every Fable prompt specifies exact required
  sections, exact source material, and exact things to avoid — no task
  says "write good content" without that detail attached.
- **Type/interface consistency:** Chapter 2 links to Chapter 1 by the
  same path Task 1 creates it at (`01-what-is-data/what-is-data.qmd`);
  Chapter 3's "Your Turn" explicitly reuses Chapter 2's summarized-data
  output rather than assuming an unrelated dataset.
