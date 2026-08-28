# Unit IV: Communicating and Applying Data Science Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Write Chapters 10-11 (Designing Your Own Data Science Project,
Telling Your Data Story), replacing their frontmatter-only stubs. These are
the book's capstone chapters — they explicitly tie every earlier chapter
together into one project workflow.

**Architecture:** Each chapter is one self-contained `.qmd` file, drafted by
a Fable-model agent against a fully-specified brief, sourced from the
existing course's Session 6 material (project workflow + data storytelling
+ using ChatGPT for communication).

**Tech Stack:** Quarto 1.8, Markdown/`.qmd`.

**Spec:** `project/specs/2026-08-27-hs-data-science-textbook-design.md`

**Prerequisite:** `project/plans/2026-08-27-01-infrastructure-and-front-matter.md` must be complete. Ideally Units II-III are also complete, since these two chapters reference nearly every earlier chapter by name — if they aren't done yet, use the chapter titles/paths from this plan's Interfaces sections regardless (they're fixed by the infrastructure plan's `_quarto.yml`).

## Global Constraints

(Same callout syntaxes, tone, and Fable-authoring requirement as
`project/plans/2026-08-27-02-unit1-foundations.md`.)

- **Relative links:** every file path named in this plan is relative to the
  repo root. All literal link examples given in this plan's Fable prompts
  are already written correctly relative to the chapter file being
  authored (e.g. `../02-spreadsheets/spreadsheets.qmd` from within
  `10-capstone-project/`) — use them as given.

---

## File Structure

```
10-capstone-project/capstone-project.qmd     # full rewrite of stub
11-data-storytelling/data-storytelling.qmd   # full rewrite of stub
```

---

### Task 1: Write Chapter 10 — Designing Your Own Data Science Project

**Files:**
- Modify: `10-capstone-project/capstone-project.qmd` (replace stub)

**Interfaces:**
- Consumes: every prior chapter by name — this chapter's workflow maps
  each step to a specific earlier chapter (Ch. 2/4 for loading and
  cleaning, Ch. 5 for ETL, Ch. 3 for visualization, Ch. 7 for statistics,
  Ch. 8 for modeling). Link to each by its real path.
- Produces: glossary term `Research Question`. Produces the project
  scaffold that Chapter 11's "Your Turn" (the final capstone deliverable)
  assumes exists — Chapter 11 should not redefine the project steps, only
  reference them.

- [ ] **Step 1: Draft using the Fable model**

Dispatch via `Agent` tool with `model: "fable"`. Prompt:

```
Write the full content for 10-capstone-project/capstone-project.qmd,
Chapter 10 of a high school data science textbook — this is the start of
the book's capstone unit. Read 04-python-pandas/Chapter3-Part1.qmd for
voice.

Audience: high school sophomores who have completed Chapters 1-9 and are
about to start an independent final project.

Source material to draw from (a past in-person version of this course ran
a capstone project with these steps):
1. Choose a dataset (Delaware Open Data Portal or another source) —
   something the student actually finds interesting (sports, environment,
   health, local events), with enough rows and columns to explore.
2. Define a research question — a specific, answerable question, e.g. "Do
   traffic accidents happen more on weekends than weekdays?" rather than
   a vague topic like "traffic accidents."
3. Load the data into Python or Google Sheets.
4. Clean and preprocess the data (remove missing/irrelevant rows, fix
   formats, apply transformations like normalization or encoding if
   needed).
5. Analyze and visualize findings (filtering, grouping, calculations;
   bar/line/pie/scatter charts to make results clear).
6. Optionally build a prediction model (Linear Regression or Decision
   Tree) and compare results using MSE and R².
7. Plan how to present results as a story (this is Chapter 11).

Required sections, in order:
1. Learning Objectives (4-5 bullets).
2. "Your Capstone Project" — a short framing paragraph: this is where
   every skill from the book comes together into one project you choose
   and own.
3. "Step 1: Choose a Dataset" — the guidance above, plus a link to
   `[Chapter 2](../02-spreadsheets/spreadsheets.qmd)` and
   `[Chapter 6](../06-apis-data-sources/apis-data-sources.qmd)` as
   reminders of where to find data (Delaware Open Data Portal, Kaggle, a
   public API).
4. "Step 2: Define a Research Question" — a Definition callout for
   "Research Question," with 2 examples of vague topics turned into
   specific, answerable questions.
5. "Step 3: Load and Clean Your Data" — link to
   `[Chapter 4](../04-python-pandas/Chapter3-Part1.qmd)` and
   `[Chapter 5](../05-etl/Chapter4-Part1.qmd)` as where these skills were
   taught; this section just reminds the student of the checklist (missing
   values, correct formats, encoding if needed) rather than re-teaching it.
6. "Step 4: Analyze and Visualize" — link to
   `[Chapter 3](../03-data-visualization/data-visualization.qmd)` (CODAP)
   and `[Chapter 7](../07-statistics-ethics/statistics-ethics.qmd)`
   (descriptive statistics) as where these skills were taught.
7. "Step 5 (Optional): Build a Prediction Model" — link to
   `[Chapter 8](../08-machine-learning/machine-learning.qmd)`; note this
   step is optional and depends on whether the chosen research question
   is actually a prediction question.
8. "What Makes a Good Project?" — a simple rubric as a bulleted list: a
   specific research question; real data, actually loaded and explored (not
   just described); at least one cleaning/transformation step justified in
   the student's own words; at least one chart that actually answers part
   of the research question; an honest account of a limitation (missing
   data, small sample size, a variable that might be a confounder).
9. At least 2 Knowledge Check callouts, placed after sections 4 and 8.
10. One "Try With ChatGPT" callout — brainstorming 3 possible research
    questions for a dataset the student is considering, then picking the
    most specific/answerable one.
11. "Your Turn" — write down a candidate dataset and a first-draft research
    question for the capstone project, and check it against the "What
    Makes a Good Project?" rubric.
12. A short roadmap paragraph previewing Chapter 11 (turning this project
    into a story someone else would actually want to hear).

Output only the final Markdown content, starting with YAML frontmatter
(`title: "Designing Your Own Data Science Project"`, `author: "Technical
Instructional Team"`, `format: html`).
```

- [ ] **Step 2: Save and render standalone**

Save to `10-capstone-project/capstone-project.qmd`, run:
`quarto render 10-capstone-project/capstone-project.qmd 2>&1 | tail -30`
Expected: renders with no errors.

- [ ] **Step 3: Run the content checklist**

Open `docs/10-capstone-project/capstone-project.html` and confirm:
- [ ] Every one of the 5 project steps links to the correct real chapter path
- [ ] Rubric in "What Makes a Good Project?" has concrete, checkable items (not vague adjectives like "good analysis")
- [ ] Definition callout present for Research Question
- [ ] At least 2 Knowledge Checks, 1+ Try With ChatGPT callout, 1 Your Turn activity

- [ ] **Step 4: Commit**

```bash
git add 10-capstone-project/capstone-project.qmd
git commit -m "Write Chapter 10: Designing Your Own Data Science Project"
```

---

### Task 2: Write Chapter 11 — Telling Your Data Story

**Files:**
- Modify: `11-data-storytelling/data-storytelling.qmd` (replace stub)

**Interfaces:**
- Consumes: the project scaffold from Chapter 10
  (`10-capstone-project/capstone-project.qmd`) — this chapter's "Your Turn"
  is the final capstone deliverable and should say so explicitly, and the
  "Using AI Responsibly" framing from `using-ai-responsibly.qmd` and the
  prompting lesson from Chapter 9 (`09-ai-and-llms/ai-and-llms.qmd`) — this
  chapter's ChatGPT-for-communication techniques are a direct, concrete
  application of both.
- Produces: glossary terms `Data Storytelling`, `Key Message`. This is the
  last content chapter in the book — its closing paragraph should feel
  like a close of the whole book, not just the chapter.

- [ ] **Step 1: Draft using the Fable model**

Dispatch via `Agent` tool with `model: "fable"`. Prompt:

```
Write the full content for 11-data-storytelling/data-storytelling.qmd,
Chapter 11 — the final chapter of a high school data science textbook.
Read 10-capstone-project/capstone-project.qmd and using-ai-responsibly.qmd
in this repo first for continuity and voice.

Audience: high school sophomores partway through their capstone project
(Chapter 10), about to present it.

Source material to draw from (a past in-person version of this course
taught data storytelling this way):
- Data storytelling is combining data, visual design, and narrative so an
  audience understands and cares about your findings, not just seeing a
  chart.
- Four essential elements: context (why does this matter to the
  audience), narrative (the story arc), data (the actual evidence), visual
  design (how it's shown).
- Example transformation: data alone — "Accident rates increased by 20% in
  2024." Story version — "In 2024, as more people returned to offices,
  rush-hour traffic surged, leading to a 20% increase in accidents — most
  during the evening commute." The tip: always connect findings to
  real-life implications the audience cares about.
- Five concrete ways to use ChatGPT for communication (used in this
  course previously, now folded into this book's ongoing "Try With
  ChatGPT" pattern):
  1. Check clarity: paste your analysis into ChatGPT and ask "Is this
     easy to follow for a high school audience?"
  2. Make it engaging: ask for more attention-grabbing ways to phrase your
     key message.
  3. Polish language: use ChatGPT to improve titles, captions, and
     conclusions.
  4. Simulate audience Q&A: ask "What tough questions might people ask
     about this?" and prepare answers.
  5. Match visuals to narrative: describe your chart to ChatGPT and ask
     "Does this match the story I'm telling?"
  Example: before — "This is a line chart of accidents." after — "This
  chart shows how Friday night accidents spike right when people are
  driving home from work."

Required sections, in order:
1. Learning Objectives (4-5 bullets).
2. "Data Alone Isn't Enough" — people remember stories more than numbers;
   the accident-rate example above (data version vs. story version), with
   a Definition callout for "Data Storytelling."
3. "The Four Elements of a Data Story" — context, narrative, data, visual
   design, each with one sentence of what it means for the student's
   capstone project specifically.
4. "Define Your Key Message" — a Definition callout for "Key Message": the
   one-to-two-sentence core takeaway you want your audience to remember,
   answering "why should my audience care?" Give one example key message
   for a fictional student project.
5. "Using ChatGPT to Sharpen Your Story" — all five techniques above, each
   as its own numbered subsection with the concrete before/after example
   given, framed explicitly as an application of Chapter 9's prompting
   lesson and bounded by using-ai-responsibly.qmd's "always verify" rule
   (a suggestion from ChatGPT to make something "more engaging" should
   never make it less accurate).
6. "Preparing for Audience Questions" — briefly: use the "simulate
   audience Q&A" technique from the previous section to prepare, and
   think about one limitation of your project (from Chapter 10's rubric)
   you should be ready to explain if asked.
7. At least 2 Knowledge Check callouts, placed after sections 3 and 5.
8. One "Try With ChatGPT" callout that ties directly into the "Your Turn"
   below — use technique #4 (simulate audience Q&A) on their own project's
   key message right before presenting it.
9. "Your Turn: Present Your Data Story" — the capstone deliverable: write
   your key message, pick your single best chart from the project, and
   outline a short presentation (context → key message → chart → what you'd
   ask the audience to take away).
10. A short closing section, "You've Built a Full Pipeline" — briefly look
    back across the whole book (foundations → programming → modeling →
    communicating) as one continuous pipeline the student now owns
    end-to-end, and end on an encouraging note about what comes next
    (a real dataset, a real question, a real audience).

Output only the final Markdown content, starting with YAML frontmatter
(`title: "Telling Your Data Story"`, `author: "Technical Instructional
Team"`, `format: html`).
```

- [ ] **Step 2: Save and render standalone**

Save to `11-data-storytelling/data-storytelling.qmd`, run:
`quarto render 11-data-storytelling/data-storytelling.qmd 2>&1 | tail -30`
Expected: renders with no errors.

- [ ] **Step 3: Run the content checklist**

Open `docs/11-data-storytelling/data-storytelling.html` and confirm:
- [ ] All 5 ChatGPT-for-communication techniques present with the before/after example
- [ ] "always verify" guardrail explicitly stated in that section, not just implied
- [ ] Definition callouts present for Data Storytelling and Key Message
- [ ] "Your Turn" is explicitly framed as the capstone deliverable, referencing Chapter 10
- [ ] At least 2 Knowledge Checks, 1+ Try With ChatGPT callout
- [ ] Closing section reads as a close of the whole book

- [ ] **Step 4: Commit**

```bash
git add 11-data-storytelling/data-storytelling.qmd
git commit -m "Write Chapter 11: Telling Your Data Story"
```

---

## Self-Review Notes

- **Spec coverage:** both Unit IV chapters from spec §4 are covered,
  including the user's explicit request for a dedicated storytelling
  chapter (Chapter 11, separate from Chapter 10's project logistics).
- **Placeholder scan:** every project-workflow step and every ChatGPT
  technique is given as fully worked content in the Fable prompts, not a
  reference to "the usual steps."
- **Type/interface consistency:** every cross-chapter link in Chapter 10
  and Chapter 11 uses the exact file paths established by the
  infrastructure plan's `_quarto.yml` (Task 1 of that plan).
