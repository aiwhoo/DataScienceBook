# Back Matter & Final Polish Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Compile the Glossary and Dataset & Tool Directory from the now-
complete set of chapters, then run a whole-book link and render audit
before calling the textbook done.

**Architecture:** This plan runs last, after all 11 chapters have real
content (Units I-IV plans complete). The Glossary is mechanically extracted
from every chapter's Definition callouts rather than hand-authored from
scratch, so it can't drift from what the chapters actually define.

**Tech Stack:** Quarto 1.8, Python 3 (for the extraction script), `grep`.

**Spec:** `project/specs/2026-08-27-hs-data-science-textbook-design.md`

**Prerequisite:** All of:
- `project/plans/2026-08-27-01-infrastructure-and-front-matter.md`
- `project/plans/2026-08-27-02-unit1-foundations.md`
- `project/plans/2026-08-27-03-unit2-programming.md`
- `project/plans/2026-08-27-04-unit3-modeling.md`
- `project/plans/2026-08-27-05-unit4-communicating.md`

must be complete — every chapter file has real content, not a stub.

## Global Constraints

- Every external URL in the finished book must resolve live — this plan's
  Task 2 is the final, whole-book check, catching anything an individual
  chapter task missed and any pre-existing link in the untouched parts of
  Chapters 4-5.
- No new prose chapters are written in this plan — only back matter
  (Glossary, Dataset & Tool Directory) and verification.

---

## File Structure

```
glossary.qmd                       # full rewrite of stub (extracted content)
dataset-and-tool-directory.qmd     # full rewrite of stub
```

---

### Task 1: Compile the Glossary

**Files:**
- Modify: `glossary.qmd` (replace stub)
- Create (scratch, not committed): `/tmp/extract_definitions.py`

**Interfaces:**
- Consumes: every Definition callout (`::: {.callout-note}` containing a
  `### Term` or `### Definition: Term` heading) across all 11 chapters and
  front matter.
- Produces: `glossary.qmd`, a single alphabetized reference page.

- [ ] **Step 1: Write and run the extraction script**

```python
# /tmp/extract_definitions.py
import re
import glob

entries = []
files = sorted(glob.glob("[0-9][0-9]-*/*.qmd")) + ["01-what-is-data/what-is-data.qmd"]
# (glob pattern above covers every numbered chapter folder; front matter
# files don't currently define new terms, so they're not scanned)
files = sorted(set(glob.glob("[0-9][0-9]-*/*.qmd")))

callout_pattern = re.compile(
    r"::: \{\.callout-note\}\s*\n### (?:Definition: )?(.+?)\n(.*?)\n:::",
    re.DOTALL,
)

for path in files:
    with open(path) as f:
        text = f.read()
    for match in callout_pattern.finditer(text):
        term = match.group(1).strip()
        body = match.group(2).strip()
        # Skip nested "Reveal Answer" callouts, which use collapse="true"
        # and a different title attribute rather than a `###` heading —
        # they won't match this pattern at all, so no extra filtering
        # needed, but double-check none slipped through:
        if "collapse=" in term:
            continue
        entries.append((term, body, path))

entries.sort(key=lambda e: e[0].lower())
for term, body, path in entries:
    print(f"## {term}\n\n{body}\n\n*(from {path})*\n")
```

Run: `python3 /tmp/extract_definitions.py > /tmp/glossary_draft.md`
Then: `cat /tmp/glossary_draft.md` to review the raw extraction.

- [ ] **Step 2: Verify extraction completeness**

Cross-check the extracted term count against the full list this book's
plans committed to defining. Run:
`grep -c '^## ' /tmp/glossary_draft.md`

Expected count is at least 34 (the sum of every glossary term named across
the five plans: Ch1 has 5, Ch2 has 4, Ch3 has 4, Ch4/5 existing chapters
have 7 pre-existing terms — Big Data, Library, pip, DataFrame, String,
Boolean Masking, Data Preparation, ETL, Transform, Encoding, The Load Phase
— Ch6 has 4, Ch7 has 7, Ch8 has 8, Ch9 has 4, Ch10 has 1, Ch11 has 2). If
the count is meaningfully lower, some chapter's Definition callouts used a
heading format the regex didn't catch — inspect that chapter's raw
Markdown and adjust the pattern, then re-run.

- [ ] **Step 3: Assemble `glossary.qmd`**

Take the reviewed output from Step 1, remove the `*(from path)*` debug
lines, deduplicate any term defined more than once (keep the clearer
definition, or merge both into one entry if they're genuinely
complementary), and write the final file:

```markdown
---
title: "Glossary"
format: html
---

Every term introduced in this book, collected in one place. Each entry
links back to the chapter where it's first taught, if you want the fuller
explanation and worked example.

## <Term>

<Definition text.> — see [<Chapter Title>](<relative path>)

<!-- ...one entry per term, alphabetically... -->
```

- [ ] **Step 4: Render and verify**

Run: `quarto render glossary.qmd 2>&1 | tail -20`
Expected: renders with no errors. Open `docs/glossary.html` and spot-check
5 random terms against their source chapters to confirm the definitions
weren't garbled by the extraction.

- [ ] **Step 5: Commit**

```bash
git add glossary.qmd
git commit -m "Compile Glossary from every chapter's Definition callouts"
```

---

### Task 2: Write the Dataset & Tool Directory

**Files:**
- Modify: `dataset-and-tool-directory.qmd` (replace stub)

**Interfaces:**
- Consumes: every external tool/dataset source named across the book
  (Delaware Open Data Portal, Kaggle, CODAP, Google Sheets, PyCharm,
  Google Colab, scikit-learn docs, and whichever public API Chapter 6
  ended up verifying and using).
- Produces: `dataset-and-tool-directory.qmd`, a one-page quick reference.

- [ ] **Step 1: Collect the actual list of tools/datasets referenced**

Run: `grep -rhoE 'https?://[^ )"'"'"']+' *.qmd */*.qmd | sort -u`
This gives the full, real list of every external URL currently in the
book. Use this list — not a list written from memory — to build the
directory below, so nothing referenced in a chapter is missing from the
directory and nothing in the directory is unused/invented.

- [ ] **Step 2: Verify each unique domain is still live**

For each distinct domain in the Step 1 output, run one `WebFetch` call
confirming the page is live and matches what the book says it is (e.g.
codap.concord.org is still CODAP, not a squatted/expired domain).

- [ ] **Step 3: Write the directory**

```markdown
---
title: "Dataset & Tool Directory"
format: html
---

A quick reference to every tool and data source this book uses, gathered
in one place.

## Where to Find Data

- **[Delaware Open Data Portal](https://data.delaware.gov/)** — real
  government datasets (traffic crashes, school enrollment, park locations,
  COVID-19 trends, and more). Used throughout this book, starting in
  Chapter 4.
- **[Kaggle](https://www.kaggle.com/)** — a huge library of datasets and a
  learning community, mentioned as an alternative data source starting in
  Chapter 4.

## Tools Used in This Book

- **[CODAP](https://codap.concord.org/)** — free, no-login drag-and-drop
  data visualization, used in Chapter 3.
- **Google Sheets** — spreadsheet formulas and filtering, used in
  Chapter 2.
- **PyCharm** — a Python IDE, set up in Chapter 4 (see also
  [Getting Set Up](getting-set-up.qmd)).
- **[Google Colab](https://colab.research.google.com/)** — a no-install
  alternative to PyCharm, covered in [Getting Set Up](getting-set-up.qmd).
- **[scikit-learn](https://scikit-learn.org/)** — the machine learning
  library used in Chapter 8.

<!-- Add an entry here for whichever public API Chapter 6 verified and
     used (Open-Meteo or its substitute), using the real name/URL from
     that chapter, not a placeholder. -->
```

Fill in the Chapter 6 API entry with the real tool that chapter ended up
using (check `06-apis-data-sources/apis-data-sources.qmd` for the final
choice), and remove/adjust any other entry that Step 1's actual grep
results show isn't really used, or add any this list missed.

- [ ] **Step 4: Render and verify**

Run: `quarto render dataset-and-tool-directory.qmd 2>&1 | tail -20`
Expected: renders with no errors.

- [ ] **Step 5: Commit**

```bash
git add dataset-and-tool-directory.qmd
git commit -m "Write Dataset & Tool Directory appendix"
```

---

### Task 3: Whole-book link audit

**Files:**
- Modify: any `.qmd` file found to contain a dead link (exact files
  determined by this task's Step 1 output — cannot be listed in advance).

**Interfaces:**
- Consumes: every `.qmd` file in the repository.
- Produces: a book with zero known-dead external links.

- [ ] **Step 1: Enumerate every unique external URL in the book**

```bash
grep -rhoE 'https?://[^ )"'"'"']+' *.qmd */*.qmd | sort -u > /tmp/all_urls.txt
cat /tmp/all_urls.txt
```

- [ ] **Step 2: Check every URL**

For each URL in `/tmp/all_urls.txt`, run `WebFetch` with the prompt "Is
this page live and working, or is it an error/dead page?" Keep a running
list of any that come back dead or clearly wrong.

- [ ] **Step 3: Fix any dead links found**

For each dead link found in Step 2, open the `.qmd` file(s) containing it
(`grep -rl '<dead-url>' *.qmd */*.qmd`) and either replace it with a live
equivalent (re-verify the replacement with another `WebFetch` before using
it) or remove the reference if no good replacement exists, adjusting the
surrounding sentence so it still reads naturally.

- [ ] **Step 4: Commit any fixes**

```bash
git add -A
git commit -m "Fix dead links found in whole-book link audit"
```

(Skip this commit if Step 2 found no dead links.)

---

### Task 4: Full-book render and cross-reference check

**Files:** none (verification only).

**Interfaces:**
- Consumes: the entire finished book.
- Produces: confirmation the book is done.

- [ ] **Step 1: Full render**

Run: `quarto render 2>&1 | tail -80`
Expected: zero errors, all 11 chapters + front matter + appendices present
in the output.

- [ ] **Step 2: Verify the table of contents matches the spec**

Open `docs/index.html` and confirm the left-nav shows, in order: Preface,
How to Use This Book, Using AI Responsibly, then the four units each with
their chapters in the order listed in spec §4, then the three appendices
(Glossary, Getting Set Up, Dataset & Tool Directory).

- [ ] **Step 3: Spot-check Knowledge Check collapsibility across units**

Open one rendered chapter from each unit (e.g.
`docs/01-what-is-data/what-is-data.html`,
`docs/04-python-pandas/Chapter3-Part1.html`,
`docs/08-machine-learning/machine-learning.html`,
`docs/11-data-storytelling/data-storytelling.html`) and confirm each
Knowledge Check's "Reveal Answer" is collapsed by default and expands on
click.

- [ ] **Step 4: Verify no `<script>`-based fake output remains anywhere**

Run: `grep -rl '<script>' *.qmd */*.qmd`
Expected: no output (empty result). If anything is found, it was missed by
the Unit II polish plan — convert it using the same rule from
`project/plans/2026-08-27-03-unit2-programming.md`'s Global Constraints.

- [ ] **Step 5: Final commit**

```bash
git add -A
git commit -m "Final render and cross-reference verification pass"
```

(Skip if Steps 1-4 found nothing to change beyond what Tasks 1-3 already committed.)

---

## Self-Review Notes

- **Spec coverage:** spec §4's back-matter requirements (Glossary, Dataset
  & Tool Directory) are covered, and spec §9 ("Testing / Validation") is
  covered by Tasks 3-4.
- **Placeholder scan:** the Glossary is generated from real extracted
  content, not hand-waved; the Dataset & Tool Directory's one intentional
  gap (the Chapter 6 API entry) is explicitly called out as something to
  fill from that chapter's real, verified choice — not left vague.
- **Type/interface consistency:** the extraction script's glob pattern
  (`[0-9][0-9]-*/*.qmd`) matches the exact folder-naming convention the
  infrastructure plan established in Task 1.
