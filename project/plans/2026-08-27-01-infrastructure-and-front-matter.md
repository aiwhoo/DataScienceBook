# Textbook Infrastructure & Front Matter Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Stand up the full 11-chapter/4-unit book skeleton (renamed folders,
complete `_quarto.yml`, stub files for every unwritten chapter) so it renders
cleanly end-to-end, then fill in the real front matter (preface, how-to-use,
AI-use policy, setup guide) that every later content plan depends on.

**Architecture:** One Quarto book project. Existing content is relocated,
not rewritten. New chapters get minimal frontmatter-only stub files so
`_quarto.yml` can reference the final table of contents immediately —
later per-unit plans replace each stub's content wholesale, never touching
`_quarto.yml` again except to add appendices.

**Tech Stack:** Quarto 1.8 (book project, HTML output), Markdown/`.qmd`,
plain CSS.

**Spec:** `project/specs/2026-08-27-hs-data-science-textbook-design.md`

## Global Constraints

- Repo root for all paths below: `DataScienceBook/` (this is where `_quarto.yml` lives).
- `docs/` is the Quarto output directory and is gitignored — never put source content or plan/spec docs there.
- Folders use topic slugs, not chapter numbers baked into filenames inside them — see spec §6 for the exact list.
- `Chapter3/` → `04-python-pandas/` and `Chapter4/` → `05-etl/` must be `git mv` (history-preserving) renames; file contents inside are untouched by this plan.
- Every task in this plan ends with `quarto render` succeeding with zero errors.
- New front-matter files use tone matching the existing Python/ETL chapters: conversational, encouraging, concrete — not a dry textbook register.
- No placeholder/TBD prose anywhere in committed `.qmd` files — stub files contain only YAML frontmatter (a title), no placeholder body text.

---

## File Structure

```
DataScienceBook/
  _quarto.yml                        # rewritten: full 11-chapter TOC + appendices
  index.qmd                          # rewritten: real preface
  how-to-use-this-book.qmd           # new
  using-ai-responsibly.qmd           # new
  styles.css                         # extended: callout styling
  01-what-is-data/what-is-data.qmd               # new stub
  02-spreadsheets/spreadsheets.qmd               # new stub
  03-data-visualization/data-visualization.qmd   # new stub
  04-python-pandas/Chapter3-Part1.qmd            # moved from Chapter3/ (unchanged)
  04-python-pandas/Chapter3-Part2.qmd            # moved from Chapter3/ (unchanged)
  04-python-pandas/Chapter3-Part3.qmd            # moved from Chapter3/ (unchanged)
  04-python-pandas/Chapter3-Part4.qmd            # moved from Chapter3/ (unchanged)
  05-etl/Chapter4-Part1.qmd                      # moved from Chapter4/ (unchanged)
  05-etl/Chapter4-Part2.qmd                      # moved from Chapter4/ (unchanged)
  05-etl/Chapter4-Part3.qmd                      # moved from Chapter4/ (unchanged)
  05-etl/Chapter4-Part4.qmd                      # moved from Chapter4/ (unchanged)
  05-etl/Chapter4-Part5.qmd                      # moved from Chapter4/ (unchanged)
  06-apis-data-sources/apis-data-sources.qmd     # new stub
  07-statistics-ethics/statistics-ethics.qmd     # new stub
  08-machine-learning/machine-learning.qmd       # new stub
  09-ai-and-llms/ai-and-llms.qmd                 # new stub
  10-capstone-project/capstone-project.qmd       # new stub
  11-data-storytelling/data-storytelling.qmd     # new stub
  glossary.qmd                       # new stub (filled in final polish plan)
  getting-set-up.qmd                 # new, fully written in this plan
  dataset-and-tool-directory.qmd     # new stub (filled in final polish plan)
```

---

### Task 1: Restructure repository layout and rebuild the book config

**Files:**
- Move: `Chapter3/*.qmd` → `04-python-pandas/*.qmd` (git mv, filenames unchanged)
- Move: `Chapter4/*.qmd` → `05-etl/*.qmd` (git mv, filenames unchanged)
- Create: `01-what-is-data/what-is-data.qmd`
- Create: `02-spreadsheets/spreadsheets.qmd`
- Create: `03-data-visualization/data-visualization.qmd`
- Create: `06-apis-data-sources/apis-data-sources.qmd`
- Create: `07-statistics-ethics/statistics-ethics.qmd`
- Create: `08-machine-learning/machine-learning.qmd`
- Create: `09-ai-and-llms/ai-and-llms.qmd`
- Create: `10-capstone-project/capstone-project.qmd`
- Create: `11-data-storytelling/data-storytelling.qmd`
- Create: `glossary.qmd`
- Create: `dataset-and-tool-directory.qmd`
- Create: `how-to-use-this-book.qmd` (stub only in this task — full content in Task 4)
- Create: `using-ai-responsibly.qmd` (stub only in this task — full content in Task 5)
- Modify: `_quarto.yml` (full rewrite)

**Interfaces:**
- Produces: the exact chapter file paths every later content plan (Units I-IV, back matter) writes into. Those plans must not create new top-level files outside this structure without updating `_quarto.yml`.

- [ ] **Step 1: Move the existing chapters into topic-slug folders**

```bash
cd "DataScienceBook"
mkdir -p 04-python-pandas 05-etl
git mv Chapter3/Chapter3-Part1.qmd 04-python-pandas/Chapter3-Part1.qmd
git mv Chapter3/Chapter3-Part2.qmd 04-python-pandas/Chapter3-Part2.qmd
git mv Chapter3/Chapter3-Part3.qmd 04-python-pandas/Chapter3-Part3.qmd
git mv Chapter3/Chapter3-Part4.qmd 04-python-pandas/Chapter3-Part4.qmd
git mv Chapter4/Chapter4-Part1.qmd 05-etl/Chapter4-Part1.qmd
git mv Chapter4/Chapter4-Part2.qmd 05-etl/Chapter4-Part2.qmd
git mv Chapter4/Chapter4-Part3.qmd 05-etl/Chapter4-Part3.qmd
git mv Chapter4/Chapter4-Part4.qmd 05-etl/Chapter4-Part4.qmd
git mv Chapter4/Chapter4-Part5.qmd 05-etl/Chapter4-Part5.qmd
rmdir Chapter3 Chapter4
```

- [ ] **Step 2: Create minimal stub files for every unwritten chapter**

Each stub is frontmatter-only — no body content. Use this exact content per file (only the `title` differs):

`01-what-is-data/what-is-data.qmd`:
```markdown
---
title: "What Is Data?"
author: "Technical Instructional Team"
format: html
---
```

`02-spreadsheets/spreadsheets.qmd`:
```markdown
---
title: "Data Wrangling with Spreadsheets"
author: "Technical Instructional Team"
format: html
---
```

`03-data-visualization/data-visualization.qmd`:
```markdown
---
title: "Data Visualization Basics"
author: "Technical Instructional Team"
format: html
---
```

`06-apis-data-sources/apis-data-sources.qmd`:
```markdown
---
title: "Where Data Comes From: APIs & Real-World Sources"
author: "Technical Instructional Team"
format: html
---
```

`07-statistics-ethics/statistics-ethics.qmd`:
```markdown
---
title: "Descriptive Statistics & Data Ethics"
author: "Technical Instructional Team"
format: html
---
```

`08-machine-learning/machine-learning.qmd`:
```markdown
---
title: "Introduction to Machine Learning"
author: "Technical Instructional Team"
format: html
---
```

`09-ai-and-llms/ai-and-llms.qmd`:
```markdown
---
title: "How AI Learns From Data"
author: "Technical Instructional Team"
format: html
---
```

`10-capstone-project/capstone-project.qmd`:
```markdown
---
title: "Designing Your Own Data Science Project"
author: "Technical Instructional Team"
format: html
---
```

`11-data-storytelling/data-storytelling.qmd`:
```markdown
---
title: "Telling Your Data Story"
author: "Technical Instructional Team"
format: html
---
```

`glossary.qmd`:
```markdown
---
title: "Glossary"
format: html
---
```

`dataset-and-tool-directory.qmd`:
```markdown
---
title: "Dataset & Tool Directory"
format: html
---
```

`how-to-use-this-book.qmd`:
```markdown
---
title: "How to Use This Book"
format: html
---
```

`using-ai-responsibly.qmd`:
```markdown
---
title: "Using AI Responsibly"
format: html
---
```

- [ ] **Step 3: Rewrite `_quarto.yml` with the full table of contents**

```yaml
project:
  type: book
  output-dir: docs

book:
  title: "Data Science for High School"
  author: "Technology Service Center, University of Delaware"

  chapters:
    - index.qmd
    - how-to-use-this-book.qmd
    - using-ai-responsibly.qmd
    - part: "Unit I: Foundations"
      chapters:
        - 01-what-is-data/what-is-data.qmd
        - 02-spreadsheets/spreadsheets.qmd
        - 03-data-visualization/data-visualization.qmd
    - part: "Unit II: Programming for Data Science"
      chapters:
        - 04-python-pandas/Chapter3-Part1.qmd
        - 04-python-pandas/Chapter3-Part2.qmd
        - 04-python-pandas/Chapter3-Part3.qmd
        - 04-python-pandas/Chapter3-Part4.qmd
        - 05-etl/Chapter4-Part1.qmd
        - 05-etl/Chapter4-Part2.qmd
        - 05-etl/Chapter4-Part3.qmd
        - 05-etl/Chapter4-Part4.qmd
        - 05-etl/Chapter4-Part5.qmd
        - 06-apis-data-sources/apis-data-sources.qmd
    - part: "Unit III: Understanding and Modeling Data"
      chapters:
        - 07-statistics-ethics/statistics-ethics.qmd
        - 08-machine-learning/machine-learning.qmd
        - 09-ai-and-llms/ai-and-llms.qmd
    - part: "Unit IV: Communicating and Applying Data Science"
      chapters:
        - 10-capstone-project/capstone-project.qmd
        - 11-data-storytelling/data-storytelling.qmd

  appendices:
    - glossary.qmd
    - getting-set-up.qmd
    - dataset-and-tool-directory.qmd

format:
  html:
    theme:
      - cosmo
      - brand
    css: styles.css
    toc: true
```

Note: `getting-set-up.qmd` is referenced here but not created until Task 4 of
this same plan — that's fine as long as Task 4 lands before this task is
considered "done" (see Step 4 below, which is run again after Task 4).

- [ ] **Step 4: Verify the render fails only on the missing `getting-set-up.qmd`, not on anything else**

Run: `quarto render 2>&1 | tail -30`
Expected: an error naming `getting-set-up.qmd` as missing, and no other
errors (no YAML parse errors, no broken chapter paths). This confirms the
rename and stub creation were done correctly before moving on.

- [ ] **Step 5: Commit**

```bash
git add -A
git commit -m "Restructure book into topic-slug folders with full 11-chapter TOC

Chapter3/ and Chapter4/ become 04-python-pandas/ and 05-etl/ (content
unchanged). Adds stub files for the 9 new chapters plus glossary and
dataset-and-tool-directory appendices, and rewrites _quarto.yml with
the complete table of contents from the design spec."
```

---

### Task 2: Add shared callout styling for pedagogy components

**Files:**
- Modify: `styles.css`

**Interfaces:**
- Consumes: nothing from other tasks.
- Produces: two reusable classes, `.knowledge-check` and `.chatgpt-callout`,
  that every later content-authoring task applies to its callout `div`s
  (see spec §5 for the exact Markdown each callout uses — this task only
  makes them visually distinct).

- [ ] **Step 1: Read the current `styles.css`**

Run: `cat styles.css` — confirm its current contents so the addition below doesn't duplicate or clash with anything already there.

- [ ] **Step 2: Append callout styling**

Add to the end of `styles.css`:

```css
/* Knowledge Check callouts: a lighter-weight self-check than a full
   "Your Turn" activity. Applied via `::: {.callout-tip .knowledge-check}`. */
.knowledge-check {
  border-left-color: #6f42c1 !important;
}
.knowledge-check .callout-title-container {
  color: #6f42c1;
}

/* "Try With ChatGPT" callouts: a recurring, copy-pasteable AI prompt tied
   to the surrounding section. Applied via `::: {.callout-tip .chatgpt-callout}`. */
.chatgpt-callout {
  border-left-color: #10a37f !important;
}
.chatgpt-callout .callout-title-container {
  color: #10a37f;
}
```

- [ ] **Step 3: Verify the CSS is picked up**

Run: `quarto render index.qmd 2>&1 | tail -20`
Expected: succeeds (index.qmd doesn't need `getting-set-up.qmd` since it's
rendered standalone, not as the full book) with no CSS parse warnings.

- [ ] **Step 4: Commit**

```bash
git add styles.css
git commit -m "Add shared CSS for Knowledge Check and Try-With-ChatGPT callouts"
```

---

### Task 3: Write the real preface (`index.qmd`)

**Files:**
- Modify: `index.qmd` (full rewrite — the current content is Quarto's placeholder template)

**Interfaces:**
- Consumes: the final chapter list from Task 1's `_quarto.yml`, to describe the book's four units accurately.
- Produces: nothing other tasks depend on structurally, but it is the first page every reader sees — tone set here should match across `how-to-use-this-book.qmd` and `using-ai-responsibly.qmd` (Tasks 4-5).

- [ ] **Step 1: Draft the preface using the Fable model**

Dispatch via the `Agent` tool with `model: "fable"`. Prompt:

```
Write the full replacement content for index.qmd, the preface of a Quarto
book titled "Data Science for High School." Keep the existing YAML
frontmatter pattern (title, a `## Motivation` style structure is fine to
depart from) but replace ALL placeholder content — the cat image, the
Codecademy merch table, the Plotly demo, the Google Maps iframe are all
leftover Quarto template junk and must not appear.

Audience: high school sophomores, no assumed programming experience.
Tone: conversational, encouraging, concrete — matches the style of
04-python-pandas/Chapter3-Part1.qmd in this repo (read it for voice).

Cover, in this order:
1. A short, engaging hook: why data science matters to a 15-16 year old's
   actual life (not an abstract "data is the new oil" cliché — use
   concrete examples like the phone/social media/gaming examples this
   book uses elsewhere).
2. What this book covers: briefly name the four units (Foundations;
   Programming for Data Science; Understanding and Modeling Data;
   Communicating and Applying Data Science) in one sentence each.
3. A pointer to "How to Use This Book" and "Using AI Responsibly" (the
   next two pages) rather than repeating their content here.
4. Keep it to roughly 300-500 words total — this is a preface, not a
   chapter.

Output only the final Markdown content for index.qmd, starting with the
YAML frontmatter block.
```

- [ ] **Step 2: Save the draft and render it standalone**

Save the agent's output to `index.qmd`, then run: `quarto render index.qmd 2>&1 | tail -20`
Expected: renders with no errors, no leftover references to cats/Plotly/merch/maps.

- [ ] **Step 3: Read the rendered output and confirm tone/length**

Run: `cat docs/index.html | python3 -c "import sys,re; t=sys.stdin.read(); print(len(re.findall(r'\w+', re.sub('<[^>]+>','',t))))"`
Expected: a word count roughly in the 300-600 range (preface, not a full chapter). If far outside that range, revise.

- [ ] **Step 4: Commit**

```bash
git add index.qmd
git commit -m "Replace placeholder index.qmd with real book preface"
```

---

### Task 4: Write `getting-set-up.qmd`

**Files:**
- Create: `getting-set-up.qmd`
- Read (source material, do not modify): `04-python-pandas/Chapter3-Part2.qmd`

**Interfaces:**
- Consumes: the PyCharm installation steps already written in
  `04-python-pandas/Chapter3-Part2.qmd` (do not duplicate verbatim — summarize
  and cross-link back to it for the full walkthrough).
- Produces: `getting-set-up.qmd`, which `_quarto.yml`'s `appendices:` list
  (Task 1) already references. This is the file that made Task 1's render
  fail; after this task, a full `quarto render` (not just single-file) must
  succeed.

- [ ] **Step 1: Draft the setup guide using the Fable model**

Dispatch via `Agent` tool with `model: "fable"`. Prompt:

```
Write the full content for getting-set-up.qmd, a back-matter appendix in a
Quarto book for high school data science students. It gives students two
paths to a working Python environment, since not every school issues
laptops that allow software installs (many issue Chromebooks).

Audience: high school sophomores, no assumed programming experience.
Tone: conversational, encouraging — matches 04-python-pandas/Chapter3-Part2.qmd
in this repo (read it first for voice and for the PyCharm steps already
written, which this page should summarize and link to rather than repeat
verbatim).

Structure:
1. A one-paragraph intro: "you need a place to write and run Python code —
   here are two options, pick whichever your school/computer supports."
2. Option A: PyCharm (for a school-issued laptop where you can install
   software) — summarize in ~5 bullet points and link to
   04-python-pandas/Chapter3-Part2.qmd for the full walkthrough. This file
   (getting-set-up.qmd) lives at the repo root, so the link path is
   `[Part 2 of the Python chapter](04-python-pandas/Chapter3-Part2.qmd)`
   — no `../` prefix.
3. Option B: Google Colab (for a Chromebook or any browser, no install) —
   full walkthrough at the same level of step-by-step detail as the
   PyCharm chapter: what Colab is, going to colab.research.google.com,
   creating a new notebook, running a code cell with print('hello Python'),
   and how uploading/reading a CSV file differs slightly in Colab
   (`files.upload()` or mounting Google Drive) versus a local PyCharm
   project.
4. A short "Which should I use?" comparison callout (a Quarto
   `::: {.callout-tip}` block) with 2-3 sentences of guidance.

Use the same callout types (`.callout-note` for definitions,
`.callout-tip` for instructor-insight-style asides) as the existing
chapters. Output only the final Markdown content for getting-set-up.qmd,
starting with YAML frontmatter (`title: "Getting Set Up"`, `format: html`).
```

- [ ] **Step 2: Verify the Colab steps are accurate**

Run a WebFetch on `https://colab.research.google.com/` to confirm the entry flow described (new notebook creation, running a cell) matches what the drafted page says. Fix any drift between the draft and the real current UI.

- [ ] **Step 3: Save and render the full book**

Save the agent's output to `getting-set-up.qmd`, then run: `quarto render 2>&1 | tail -40`
Expected: the **entire book** now renders successfully — this is the first
point in the plan where a full `quarto render` (not a single file) must
pass with zero errors, since every chapter referenced in `_quarto.yml` now
exists (as either a stub or real content).

- [ ] **Step 4: Commit**

```bash
git add getting-set-up.qmd
git commit -m "Add Getting Set Up appendix (PyCharm + Google Colab paths)"
```

---

### Task 5: Write `how-to-use-this-book.qmd`

**Files:**
- Modify: `how-to-use-this-book.qmd` (replace Task 1's stub with real content)

**Interfaces:**
- Consumes: the pedagogy component definitions from spec §5 (Knowledge Check
  and Try-With-ChatGPT callout formats) — this page is where a student
  first learns what those boxes mean when they hit one in Chapter 1.
- Produces: nothing structural; read before Task 6.

- [ ] **Step 1: Draft using the Fable model**

Dispatch via `Agent` tool with `model: "fable"`. Prompt:

```
Write the full content for how-to-use-this-book.qmd. Audience: high school
sophomores. Tone: conversational, matches 04-python-pandas/Chapter3-Part1.qmd
in this repo.

This page explains the recurring features a student will see in every
chapter, so they know what to do with them the first time they appear.
Cover each of these, with one short example of each rendered inline
(use real Quarto callout syntax, not a description of it):

1. "Definition" callouts (`::: {.callout-note}`) — key vocabulary, also
   collected in the Glossary appendix at the back of the book.
2. "Instructor Insight" callouts (`::: {.callout-tip}`) — a tip or
   shortcut from someone who's taught this before.
3. "Knowledge Check" callouts — a short self-check after major sections,
   with the answer hidden until clicked. Show a real working example:
   ::: {.callout-tip .knowledge-check title="Knowledge Check"}
   Sample question here?

   ::: {.callout-note collapse="true" title="Reveal Answer"}
   Sample answer here.
   :::
   :::
4. "Try With ChatGPT" callouts (`::: {.callout-tip .chatgpt-callout title="🤖 Try With ChatGPT"}`)
   — a ready-to-use prompt for exploring the current topic further with
   ChatGPT. Point students to using-ai-responsibly.qmd (the next page) for
   the ground rules on using these.
5. "Your Turn" activities — the larger, open-ended hands-on exercise near
   the end of each chapter, versus the lighter Knowledge Checks.

Keep it under ~400 words plus the four example callouts. Output only the
final Markdown, starting with YAML frontmatter (`title: "How to Use This
Book"`, `format: html`).
```

- [ ] **Step 2: Save and render**

Save to `how-to-use-this-book.qmd`, run: `quarto render how-to-use-this-book.qmd 2>&1 | tail -20`
Expected: renders successfully; visually confirm in `docs/how-to-use-this-book.html` that the Knowledge Check example's "Reveal Answer" is collapsed by default and expands on click.

- [ ] **Step 3: Commit**

```bash
git add how-to-use-this-book.qmd
git commit -m "Write How to Use This Book, documenting the recurring callout types"
```

---

### Task 6: Write `using-ai-responsibly.qmd`

**Files:**
- Modify: `using-ai-responsibly.qmd` (replace Task 1's stub with real content)

**Interfaces:**
- Consumes: nothing.
- Produces: the page every "Try With ChatGPT" callout in every later
  chapter should implicitly assume the reader has already seen (no
  chapter needs to link back to it explicitly every time, but the first
  "Try With ChatGPT" callout in Chapter 1 should link to it once).

- [ ] **Step 1: Draft using the Fable model**

Dispatch via `Agent` tool with `model: "fable"`. Prompt:

```
Write the full content for using-ai-responsibly.qmd, a primer on using
ChatGPT (or similar AI tools) while working through this data science
textbook. Audience: high school sophomores. Tone: direct and respectful of
the reader's intelligence — not preachy, not a legal disclaimer wall.

Cover:
1. What this book means by "Try With ChatGPT" callouts: a tool for
   exploring a concept further, checking your understanding, or getting
   unstuck — not a way to skip understanding the concept.
2. The core rule: AI is a tutor, not a ghostwriter. If you paste an
   answer you don't understand into your own work, you haven't learned
   anything, and it will show up later (a test, a follow-up question, the
   capstone project in Chapter 10).
3. Always verify: AI can be confidently wrong, especially about specific
   numbers, dates, or library function behavior. Cross-check against this
   book or by actually running the code.
4. Ask your teacher: every classroom has different rules about what's
   allowed on graded work. This book's callouts are suggestions for
   self-study; they don't override your teacher's policy.
5. One concrete good-use example and one concrete bad-use example, phrased
   for this course specifically (e.g., good: "asking ChatGPT to explain
   why your pandas filter returned zero rows"; bad: "asking ChatGPT to
   write your whole capstone project analysis for you").

Keep it under ~350 words. Output only the final Markdown, starting with
YAML frontmatter (`title: "Using AI Responsibly"`, `format: html`).
```

- [ ] **Step 2: Save and render**

Save to `using-ai-responsibly.qmd`, run: `quarto render using-ai-responsibly.qmd 2>&1 | tail -20`
Expected: renders successfully.

- [ ] **Step 3: Full book render check**

Run: `quarto render 2>&1 | tail -60`
Expected: the entire book renders with zero errors. This closes out the
infrastructure plan — every file `_quarto.yml` references now exists (as
either finished content or an intentional stub), and every unit content
plan can now proceed independently.

- [ ] **Step 4: Commit**

```bash
git add using-ai-responsibly.qmd
git commit -m "Write Using AI Responsibly primer"
```

---

## Self-Review Notes

- **Spec coverage:** §6 (repo structure) → Task 1. §5 (CSS hooks for
  pedagogy components) → Task 2. §4 front matter (preface, how-to-use,
  AI-use policy) → Tasks 3, 5, 6. §4 back matter setup guide →
  Task 4. Glossary and Dataset/Tool Directory stubs are created here
  (Task 1) but their real content is explicitly deferred to the final
  back-matter plan (they depend on chapters that don't exist yet) —
  this is intentional, not a gap.
- **Placeholder scan:** stub files contain only YAML frontmatter, no
  placeholder prose. No task step says "add appropriate content" without
  a full agent prompt or literal file content attached.
- **Type/interface consistency:** every file path used in `_quarto.yml`
  (Task 1, Step 3) matches a file created in the same task or an existing
  file moved in the same task. `getting-set-up.qmd` is the one intentional
  exception, called out explicitly with its own verification step.
