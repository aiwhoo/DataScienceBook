# Unit II: Programming for Data Science Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Polish the existing Chapter 4 (Python & Pandas) and Chapter 5
(ETL) content with the new pedagogy components and a more robust output
convention, and write the new Chapter 6 (APIs & Real-World Sources).

**Architecture:** Chapters 4 and 5 keep their existing prose — this plan
only *adds* Knowledge Check / Try-With-ChatGPT callouts and *converts* the
fragile JS-based fake console output to plain labeled output blocks.
Chapter 6 is new content, drafted the same way as Unit I's chapters.

**Tech Stack:** Quarto 1.8, Markdown/`.qmd`, Python `requests` library for
Chapter 6's API example.

**Spec:** `project/specs/2026-08-27-hs-data-science-textbook-design.md`

**Prerequisite:** `project/plans/2026-08-27-01-infrastructure-and-front-matter.md` must be complete (files already live at `04-python-pandas/` and `05-etl/`).

## Global Constraints

(Same callout syntaxes, tone, and Fable-authoring requirement as
`project/plans/2026-08-27-02-unit1-foundations.md` — see that plan's Global
Constraints section for the exact Knowledge Check / Try-With-ChatGPT /
Definition callout Markdown. Repeated here only where this plan adds a new
constraint.)

- **Output-block conversion rule:** any `` ```{=html} `` block containing a
  `<script>` tag that exists purely to *simulate a console/output result*
  (e.g., prints a fixed string via `document.write` or `innerText`) is
  replaced with:
  ```markdown
  **Output:**
  ```
  ```
  <the literal text the script was displaying>
  ```
  ```
  Any `` ```{=html} `` block that is instead *explaining* the code (not
  showing output) — e.g. a box labeled "Code Logic" or "Interactive Logic"
  that describes what a variable or method does — is replaced with a
  `::: {.callout-note}` box using the same heading text as its title,
  containing the same explanatory bullet points as plain Markdown.
- Never change the surrounding prose, headings, learning objectives, or
  existing "Your Turn"/"Instructor Insight" content in Chapters 4-5 — this
  is a targeted addition/conversion, not a rewrite.
- **Relative links:** every file path named in this plan is relative to the
  repo root. When Chapter 6 links to Chapter 5, compute the path relative
  to `06-apis-data-sources/apis-data-sources.qmd` itself — i.e.
  `../05-etl/Chapter4-Part2.qmd`, since both chapters are sibling folders
  one level below the root.
- Verification for the output-block conversion is mechanical:
  `grep -c '<script>' <file>` must return `0` for every file touched.

---

## File Structure

```
04-python-pandas/Chapter3-Part1.qmd   # modified in place (polish)
04-python-pandas/Chapter3-Part2.qmd   # modified in place (polish)
04-python-pandas/Chapter3-Part3.qmd   # modified in place (polish)
04-python-pandas/Chapter3-Part4.qmd   # modified in place (polish)
05-etl/Chapter4-Part1.qmd             # modified in place (polish)
05-etl/Chapter4-Part2.qmd             # modified in place (polish)
05-etl/Chapter4-Part3.qmd             # modified in place (polish)
05-etl/Chapter4-Part4.qmd             # modified in place (polish)
05-etl/Chapter4-Part5.qmd             # modified in place (polish)
06-apis-data-sources/apis-data-sources.qmd   # full rewrite of stub
```

---

### Task 1: Polish Chapter 4 (Python & Pandas)

**Files:**
- Modify: `04-python-pandas/Chapter3-Part1.qmd`
- Modify: `04-python-pandas/Chapter3-Part2.qmd`
- Modify: `04-python-pandas/Chapter3-Part3.qmd`
- Modify: `04-python-pandas/Chapter3-Part4.qmd`

**Interfaces:**
- Consumes: existing chapter content (read, do not rewrite prose).
- Produces: no new glossary terms (this chapter's existing Definition
  callouts — Big Data, Library, pip, DataFrame, String, Boolean Masking,
  Data Preparation — are already collected by the back-matter plan; this
  task doesn't add new ones).

- [ ] **Step 1: Convert `Chapter3-Part1.qmd`'s output-simulation block**

Read the file, find the `` ```{=html} `` block containing
`Console Output: ${output}` (the `hello Python` simulation). Replace it
with:
```markdown
**Output:**
```
```
hello Python
```
```

- [ ] **Step 2: Add a Knowledge Check to `Chapter3-Part1.qmd`**

Add this, placed just before the "## Roadmap for Part 1" heading:

```markdown
::: {.callout-tip .knowledge-check title="Knowledge Check"}
Why does Google Sheets struggle with a dataset of 539,000 rows, while
Python and Pandas handle it easily?

::: {.callout-note collapse="true" title="Reveal Answer"}
Spreadsheet programs like Google Sheets try to keep the entire dataset
in view and recalculate formulas across all visible cells, which gets
slower and more memory-intensive as rows grow. Pandas processes data
programmatically in memory without needing to render every row, so it
stays fast even at very large scales.
:::
:::
```

- [ ] **Step 3: Render and verify `Chapter3-Part1.qmd`**

Run: `grep -c '<script>' 04-python-pandas/Chapter3-Part1.qmd` — expect `0`.
Run: `quarto render 04-python-pandas/Chapter3-Part1.qmd 2>&1 | tail -20` — expect no errors.

- [ ] **Step 4: Convert `Chapter3-Part2.qmd`'s output-simulation block**

Find the `` ```{=html} `` block simulating the PyCharm console (`Simulated
Console Output:` / `Process finished with exit code 0`). Replace it with:
```markdown
**Output:**
```
```
hello Python

Process finished with exit code 0
```
```

- [ ] **Step 5: Add a Knowledge Check to `Chapter3-Part2.qmd`**

Add this, placed just before the final "### Instructor Insight: The 'Thumbs Up'" callout:

```markdown
::: {.callout-tip .knowledge-check title="Knowledge Check"}
You named a project "my first project" with spaces in the name. What's
likely to go wrong, and what should you do instead?

::: {.callout-note collapse="true" title="Reveal Answer"}
Spaces in file and folder names can confuse some tools and command-line
operations. Use underscores (`my_first_project`) or CamelCase
(`MyFirstProject`) instead.
:::
:::
```

- [ ] **Step 6: Render and verify `Chapter3-Part2.qmd`**

Run: `grep -c '<script>' 04-python-pandas/Chapter3-Part2.qmd` — expect `0`.
Run: `quarto render 04-python-pandas/Chapter3-Part2.qmd 2>&1 | tail -20` — expect no errors.

- [ ] **Step 7: Convert `Chapter3-Part3.qmd`'s explanatory block and add the chapter's "Try With ChatGPT" callout**

Find the `` ```{=html} `` block titled "Code Logic:" (explaining `df`,
`pd.read_csv()`, and file path). Replace it with:

```markdown
::: {.callout-note}
### Code Logic
1. **`df`**: A variable that stores your entire dataset — you can name it
   anything (e.g., `records`, `crash_data`).
2. **`pd.read_csv()`**: The specific tool that opens the CSV.
3. **File Path**: The text in quotes tells Python exactly where the file
   lives on your computer.
:::
```

Then add this "Try With ChatGPT" callout right after the "Case Study: The
Delaware Crash Data" section's Instructor Insight box (this is the one
Try-With-ChatGPT callout for the whole chapter):

```markdown
::: {.callout-tip .chatgpt-callout title="🤖 Try With ChatGPT"}
Copy the text output of `df.info()` from your own dataset and paste it into
ChatGPT. Ask: *"Which of these columns are actually categorical, even
though they might look numeric? How can you tell from this output?"*
:::
```

- [ ] **Step 8: Add a Knowledge Check to `Chapter3-Part3.qmd`**

Add this, placed just before "## Your Turn: Explore a Dataset":

```markdown
::: {.callout-tip .knowledge-check title="Knowledge Check"}
You run `df.describe()` on a column called `weather_code` and get a mean,
min, and max back — but the results don't make sense. What probably went
wrong?

::: {.callout-note collapse="true" title="Reveal Answer"}
`weather_code` is probably categorical data (a coded label) stored as
numbers, not truly numeric data. `.describe()` treats it as numeric
anyway, producing meaningless statistics. Running `.info()` first would
have revealed this.
:::
:::
```

- [ ] **Step 9: Render and verify `Chapter3-Part3.qmd`**

Run: `grep -c '<script>' 04-python-pandas/Chapter3-Part3.qmd` — expect `0`.
Run: `quarto render 04-python-pandas/Chapter3-Part3.qmd 2>&1 | tail -20` — expect no errors. Visually confirm the Try-With-ChatGPT callout renders with the green accent from `styles.css`.

- [ ] **Step 10: Convert `Chapter3-Part4.qmd`'s explanatory block**

Find the `` ```{=html} `` block titled "Interactive Logic:" (explaining
`.query()`). Replace it with:

```markdown
::: {.callout-note}
### Why `.query()` Reads Like a Sentence
The `.query()` method is ideal for large datasets because it is concise
and highly readable for collaborators.
:::
```

- [ ] **Step 11: Add a Knowledge Check to `Chapter3-Part4.qmd`**

Add this, placed just before "## Your Mission: Filter Like a Pro":

```markdown
::: {.callout-tip .knowledge-check title="Knowledge Check"}
You filter for `df["COUNTY NAME"] == "New Castle"` and get zero rows back,
even though you can see "New Castle" in the data. What's the most likely
cause?

::: {.callout-note collapse="true" title="Reveal Answer"}
Invisible leading or trailing whitespace in the county name values.
Running `.str.strip()` on the column before filtering usually fixes this.
:::
:::
```

- [ ] **Step 12: Render and verify `Chapter3-Part4.qmd`**

Run: `grep -c '<script>' 04-python-pandas/Chapter3-Part4.qmd` — expect `0`.
Run: `quarto render 04-python-pandas/Chapter3-Part4.qmd 2>&1 | tail -20` — expect no errors.

- [ ] **Step 13: Commit**

```bash
git add 04-python-pandas/
git commit -m "Polish Chapter 4 (Python & Pandas): add Knowledge Checks and a Try-With-ChatGPT callout, replace JS output simulation with plain output blocks"
```

---

### Task 2: Polish Chapter 5 (ETL in Action)

**Files:**
- Modify: `05-etl/Chapter4-Part1.qmd`
- Modify: `05-etl/Chapter4-Part2.qmd`
- Modify: `05-etl/Chapter4-Part3.qmd`
- Modify: `05-etl/Chapter4-Part4.qmd`
- Modify: `05-etl/Chapter4-Part5.qmd`

**Interfaces:**
- Consumes: existing chapter content (read, do not rewrite prose).
- Produces: no new glossary terms (existing Definition callouts — ETL,
  Data Preparation, Transform, Encoding, The Load Phase — are already
  collected by the back-matter plan).

- [ ] **Step 1: Add a Knowledge Check to `Chapter4-Part1.qmd`**

No script block to convert in this file (its only `` ```{=html} `` block
is a genuine output simulation — convert it too). Find the block showing
`Checking data alignment...` and replace with:
```markdown
**Output:**
```
```
Checking data alignment...
[OK] 11 columns identified
[OK] 3 daily sheets unified
```
```

Then add this Knowledge Check, placed just before "## Putting It All Together: The ETL Mindset":

```markdown
::: {.callout-tip .knowledge-check title="Knowledge Check"}
A hospital wants to combine patient records from three different clinics,
each using a different field name for "date of birth." Which stage of ETL
handles renaming these fields so they match?

::: {.callout-note collapse="true" title="Reveal Answer"}
Transform. Extract just pulls the raw data in from each source;
standardizing field names happens during Transform, before Load.
:::
:::
```

- [ ] **Step 2: Render and verify `Chapter4-Part1.qmd`**

Run: `grep -c '<script>' 05-etl/Chapter4-Part1.qmd` — expect `0`.
Run: `quarto render 05-etl/Chapter4-Part1.qmd 2>&1 | tail -20` — expect no errors.

- [ ] **Step 3: Convert `Chapter4-Part2.qmd`'s output-simulation block**

Find the `` ```{=html} `` block simulating `df_all.head()`. Replace it with:
```markdown
**Output:**
```
```
Loading 3 worksheets... Done.
Unifying 216 records... Done.

Output: df_all.head()
        Date        Hour   Name     Steps  HeartRate
0  2025-07-28  09:00  Alice     1200  72
1  2025-07-28  10:00  Alice     3500  85
2  2025-07-28  11:00  Alice     4200  90
3  2025-07-28  09:00  Charlie    800  68
4  2025-07-28  10:00  Charlie   5600  110
```
```

Add this Knowledge Check, placed just before "## Transformation Roadmap":

```markdown
::: {.callout-tip .knowledge-check title="Knowledge Check"}
Why does the code use `sheet_name=None` when loading the Excel file, and
`ignore_index=True` when combining the sheets?

::: {.callout-note collapse="true" title="Reveal Answer"}
`sheet_name=None` tells pandas to load every sheet in the workbook — not
just the first one — into a dictionary of DataFrames. `ignore_index=True`
renumbers the combined rows continuously instead of restarting the row
index at 0 for each sheet.
:::
:::
```

- [ ] **Step 4: Render and verify `Chapter4-Part2.qmd`**

Run: `grep -c '<script>' 05-etl/Chapter4-Part2.qmd` — expect `0`.
Run: `quarto render 05-etl/Chapter4-Part2.qmd 2>&1 | tail -20` — expect no errors.

- [ ] **Step 5: Convert `Chapter4-Part3.qmd`'s three output blocks and add the chapter's "Try With ChatGPT" callout**

Convert the `norm-output` block to:
```markdown
**Output:**
```
```
Normalized Steps: 0.7
```
```

Convert the `sort-output` block to:
```markdown
**Output:**
```
```
Data Discovery: Alice's steps jumped from 0.06 at 9 AM to 1.00 at 8 PM on July 30.
```
```

Convert the `geo-output` block to:
```markdown
**Output:**
```
```
Individual Variation Found:
- Diana: 0.07 km (On Campus)
- Charlie: 0.58 km (Off Campus)
```
```

Then add this "Try With ChatGPT" callout right after the Normalization
section's Instructor Insight box (this is the one Try-With-ChatGPT callout
for the whole chapter):

```markdown
::: {.callout-tip .chatgpt-callout title="🤖 Try With ChatGPT"}
Describe a column from your own dataset to ChatGPT (its name, minimum, and
maximum values) and ask: *"Would normalizing this column to a 0-1 range
make sense here? Why or why not?"*
:::
```

- [ ] **Step 6: Add a Knowledge Check to `Chapter4-Part3.qmd`**

Add this, placed just before "## Summary: Shaping the Story":

```markdown
::: {.callout-tip .knowledge-check title="Knowledge Check"}
Alice's heart rate normalizes to 1.0, while the group average normalizes to
about 0.2. What does that tell you, and what doesn't it tell you?

::: {.callout-note collapse="true" title="Reveal Answer"}
It tells you Alice's heart rate reading was the highest in the dataset
relative to everyone else's range — an outlier on the high end. It doesn't
tell you her actual heart rate in beats per minute, since normalization
strips out the original units and scale.
:::
:::
```

- [ ] **Step 7: Render and verify `Chapter4-Part3.qmd`**

Run: `grep -c '<script>' 05-etl/Chapter4-Part3.qmd` — expect `0`.
Run: `quarto render 05-etl/Chapter4-Part3.qmd 2>&1 | tail -20` — expect no errors.

- [ ] **Step 8: Convert `Chapter4-Part4.qmd`'s three output blocks**

Convert the `label-output` block to:
```markdown
**Output:**
```
```
Encoding Verification:
- Alice (Female) -> 0
- Diana (Female) -> 0
- Charlie (Male)  -> 1
[Status] Encoding consistent across all 216 rows.
```
```

Convert the `oh-output` block to:
```markdown
**Output:**
```
```
New Feature Columns Created:
- ActivityType_Cycling [0 or 1]
- ActivityType_Resting [0 or 1]
- ActivityType_Running [0 or 1]
In each row, exactly one column equals 1.
```
```

Convert the `merge-output` block to:
```markdown
**Output:**
```
```
Insights Revealed:
- Alice: Most Active (Peak: 21,025 steps on July 28)
- Diana: Rising Trend (7,900 -> 10,877 -> 18,608 steps)
- Charlie: Lower activity detected (Only 2 days recorded)
```
```

- [ ] **Step 9: Add a Knowledge Check to `Chapter4-Part4.qmd`**

Add this, placed just before "## The ETL Endgame: One Pipeline":

```markdown
::: {.callout-tip .knowledge-check title="Knowledge Check"}
Why is one-hot encoding safer than label encoding for a column like
`ActivityType` (Cycling, Running, Resting)?

::: {.callout-note collapse="true" title="Reveal Answer"}
Label encoding assigns arbitrary numbers (e.g., Cycling=0, Resting=1,
Running=2), which implies a false order or magnitude a model might learn
from. One-hot encoding creates separate binary columns so no category
outranks another.
:::
:::
```

- [ ] **Step 10: Render and verify `Chapter4-Part4.qmd`**

Run: `grep -c '<script>' 05-etl/Chapter4-Part4.qmd` — expect `0`.
Run: `quarto render 05-etl/Chapter4-Part4.qmd 2>&1 | tail -20` — expect no errors.

- [ ] **Step 11: Convert `Chapter4-Part5.qmd`'s output-simulation block**

Find the `status-box`/`status-msg` block. Replace it with:
```markdown
**Output:**
```
```
Success: 'aggregated_daily_activity.csv' generated in local directory.
```
```

- [ ] **Step 12: Add a Knowledge Check to `Chapter4-Part5.qmd`**

Add this, placed just before "## The Full Journey: ETL from Start to Finish":

```markdown
::: {.callout-tip .knowledge-check title="Knowledge Check"}
What does `index=False` do in `aggregated_df.to_csv("file.csv", index=False)`, and why does it matter?

::: {.callout-note collapse="true" title="Reveal Answer"}
It tells pandas not to write the DataFrame's row-number index as an extra
column in the CSV. Without it, the exported file gets a meaningless extra
column that can confuse other programs or people reading the file.
:::
:::
```

- [ ] **Step 13: Render and verify `Chapter4-Part5.qmd`**

Run: `grep -c '<script>' 05-etl/Chapter4-Part5.qmd` — expect `0`.
Run: `quarto render 05-etl/Chapter4-Part5.qmd 2>&1 | tail -20` — expect no errors.

- [ ] **Step 14: Commit**

```bash
git add 05-etl/
git commit -m "Polish Chapter 5 (ETL in Action): add Knowledge Checks and a Try-With-ChatGPT callout, replace JS output simulation with plain output blocks"
```

---

### Task 3: Write Chapter 6 — Where Data Comes From: APIs & Real-World Sources

**Files:**
- Modify: `06-apis-data-sources/apis-data-sources.qmd` (replace stub)

**Interfaces:**
- Consumes: the "Extract" phase concept from Chapter 5
  (`05-etl/Chapter4-Part2.qmd`) — this chapter generalizes extraction
  beyond flat files to APIs, and should link back to it.
- Produces: glossary terms `API`, `JSON`, `Endpoint`, `Rate Limit`.

- [ ] **Step 1: Verify a free, no-key public API before drafting**

Run `WebFetch` on `https://open-meteo.com/en/docs` with the prompt:
"Confirm this is a free weather API that requires no API key and no
signup. Show one example request URL and what its JSON response looks
like." If Open-Meteo is no longer free/keyless, substitute a different
verified free no-key public API (e.g. `https://api.open-notify.org/` for
ISS location) and use that instead throughout this task.

- [ ] **Step 2: Draft using the Fable model**

Dispatch via `Agent` tool with `model: "fable"`. Prompt (fill in
`<API_NAME>`, `<API_BASE_URL>`, and `<EXAMPLE_JSON>` from Step 1's verified
result before sending):

```
Write the full content for 06-apis-data-sources/apis-data-sources.qmd,
Chapter 6 of a high school data science textbook. Read
05-etl/Chapter4-Part2.qmd in this repo first to match voice and to see how
this book already introduces "Extract" as pulling data from files — this
chapter broadens that to APIs.

Audience: high school sophomores who have completed Chapter 5 (ETL) and
know what pandas/DataFrames are, but have never made a web request in code.

Verified, currently-free, no-signup public API to use for the hands-on
example:
- Name: <API_NAME>
- Base URL: <API_BASE_URL>
- Example JSON response: <EXAMPLE_JSON>

Required sections, in order:
1. Learning Objectives (4-5 bullets).
2. "Four Ways Data Reaches You" — files (CSVs/Excel, what Chapter 5 already
   covered), databases (structured, queryable, mention briefly this book
   doesn't go deep here), APIs (live, on-demand data from another
   computer), sensors (devices generating a constant stream, like a
   fitness tracker). One paragraph each.
3. "What Is an API?" — a Definition callout: an API (Application
   Programming Interface) is a way for one program to ask another program
   for data, usually over the internet, and get back a structured answer.
   Use a restaurant-menu-and-waiter analogy or similar concrete metaphor
   in this book's existing style.
4. "JSON: The Language APIs Speak" — a Definition callout for JSON
   (JavaScript Object Notation): a text format for structured data that
   looks like nested Python dictionaries and lists. Show the actual
   example JSON response from <API_NAME> in a fenced ` ```json ` block and
   walk through 2-3 of its fields in plain English.
5. "Hands-On: Calling Your First API" — Python code using the `requests`
   library:
   ```python
   import requests

   response = requests.get("<API_BASE_URL>")
   data = response.json()
   print(data)
   ```
   followed by a **Output:** block showing (a shortened version of) the
   real JSON from Step 1, and a short walkthrough of pulling one or two
   specific fields out of the resulting Python dictionary
   (e.g. `data["some_field"]`).
6. "Endpoint" and "Rate Limit" — each as its own Definition callout:
   an endpoint is one specific URL/URL-pattern an API exposes for a
   specific kind of data; a rate limit is a cap on how many requests you
   can make in a given time window, and why that matters (being polite to
   a free service, avoiding getting blocked).
7. "Is It OK to Take This Data?" — a short, concrete section on the
   ethics/legality of extracting data from the web: APIs that are
   documented and offered for public use (like <API_NAME>) are meant to be
   used this way; scraping a website that doesn't offer an API or
   explicitly forbids it in its terms of service is a different, riskier
   situation. Encourage checking a site's terms of service or `robots.txt`
   before writing a scraper, and preferring an official API whenever one
   exists.
8. At least 2 Knowledge Check callouts, placed after sections 4 and 7.
9. One "Try With ChatGPT" callout — e.g. pasting a confusing chunk of raw
   JSON and asking ChatGPT to explain what each field probably means.
10. "Your Turn" — call <API_NAME> (or another free no-key API of the
    student's choice) from Python, print three specific fields from the
    response, and write 2 sentences on what that data could be used for.
11. A short roadmap paragraph previewing Unit III (turning data like this
    into statistics and, eventually, predictions).

Output only the final Markdown content, starting with YAML frontmatter
(`title: "Where Data Comes From: APIs & Real-World Sources"`, `author:
"Technical Instructional Team"`, `format: html`).
```

- [ ] **Step 3: Save and render standalone**

Save to `06-apis-data-sources/apis-data-sources.qmd`, run:
`quarto render 06-apis-data-sources/apis-data-sources.qmd 2>&1 | tail -30`
Expected: renders with no errors.

- [ ] **Step 4: Actually run the API example**

Run the exact Python code shown in the "Hands-On" section locally
(`python3 -c "import requests; print(requests.get('<API_BASE_URL>').json())"`)
and confirm the real output matches what the chapter's Output: block shows
closely enough to not mislead a student (exact values like weather/ISS
position will differ since they're live, but the structure/fields must
match).

- [ ] **Step 5: Run the content checklist**

Open `docs/06-apis-data-sources/apis-data-sources.html` and confirm:
- [ ] Files/databases/APIs/sensors all covered in "Four Ways Data Reaches You"
- [ ] Definition callouts present for API, JSON, Endpoint, Rate Limit
- [ ] The `requests.get(...)` example actually works (Step 4)
- [ ] Ethics/ToS section present and not hand-wavy (names a concrete check: terms of service or robots.txt)
- [ ] At least 2 Knowledge Checks, 1+ Try With ChatGPT callout, 1 Your Turn activity
- [ ] Link to Chapter 5 resolves

- [ ] **Step 6: Commit**

```bash
git add 06-apis-data-sources/apis-data-sources.qmd
git commit -m "Write Chapter 6: Where Data Comes From (APIs & Real-World Sources)"
```

---

## Self-Review Notes

- **Spec coverage:** §5 pedagogy retrofit for existing chapters and §4
  Chapter 6 are both covered. The §5 "fragile JS pattern" fix is applied
  to every identified script block across both existing chapters (9 part
  files, all named explicitly with their exact conversion).
- **Placeholder scan:** every polish step gives the literal before/after
  content, not a description of the change. Chapter 6's Fable prompt
  requires a live-verified API and forbids inventing response data.
- **Type/interface consistency:** Chapter 6 links back to
  `05-etl/Chapter4-Part2.qmd` using its real (post-rename) path, matching
  Task 1 of the infrastructure plan.
