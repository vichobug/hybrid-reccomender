# Hybrid Recommender: Project Status and To-Do

MKTG 4604 · Fall 2026 · Group build
**Due:** Wed 11 Nov, 11:59 PM (one PDF + one notebook per group)
**Presented:** Session 19 (Thu 12 Nov Sec 02 / Fri 13 Nov Sec 01)

---

## 1. Files in this folder

| File | What it is |
|---|---|
| `Hybrid_Reco_Template_Fall26.ipynb` | **The main notebook.** All code and drafts are here. |
| `book_data_sample_ed.csv`, `ratings_data_sample_ed.csv`, `users_data_sample_ed.csv` | The data. Must sit next to the notebook (or be uploaded to Colab). |
| `grading_baseline.csv` | Grading sheet for the unchanged system (50 rows) |
| `grading_change_1__drop_already_rated_and_duplicate_titles.csv` | Grading sheet after Change 1 |
| `grading_change_2__bayesian_average_ranking.csv` | Grading sheet after Change 2 |
| `grading_change_3__ignore_zero_ratings.csv` | Grading sheet after Change 3 |
| `PROJECT_STATUS.md` | This file |

**How to run:** Google Colab → upload the notebook and the 3 data CSVs (folder icon on the left) → *Runtime → Run all*. The grading sheets are regenerated on every run (download them from the folder panel: right-click → Download).

> ⚠️ The 4 grading CSVs currently use the **placeholder readers**. If the readers change (see To-Do 1), re-run the notebook and send the **new** CSVs. Don't grade the old ones.

---

## 2. What has been done ✅

### Notebook changes

| Where in the notebook | What was added |
|---|---|
| **Part 1**, after "For Paragraph A" | A **draft of Paragraph A** in bullets: the 3 groups described in marketing terms, and what they really separate on (one bestseller and the zeros, not age or taste). |
| **Part 4**, `people` list | **10 placeholder readers** (marked `PLACEHOLDER`): 5 typical readers (Priya, Daniel, Elena, Viktor, Grace) + 5 traps (Marcus, Sam, Leo, Linda, Omar). All 30 titles match the catalogue. |
| **Part 4**, "Judge the baseline" cell | `JUDGE = ['Priya', 'Daniel', 'Marcus', 'Sam', 'Leo']` and a `judge_readers()` function. It runs the 5 readers (as known readers and as strangers), prints their lists, counts distinct titles, and saves a grading CSV. |
| **Part 5**, Change 1 | **Drop already-rated and duplicate titles** (rewrites `recommend()`). |
| **Part 5**, Change 2 | **Bayesian average ranking** (rewrites `candidate_list()`, `M = 5`). |
| **Part 5**, Change 3 | **Ignore zero ratings** in the averages (rewrites `candidate_list()`, keeps the Bayesian average). |
| End, after "Paragraph C" | A **draft of Paragraph C**: judgment, what the test can't tell us, what the bookseller should collect, and a 5-row **trace table**. Blanks are marked `[brackets]`. |

The changes stack: Change 2 keeps Change 1, and Change 3 keeps Changes 1 and 2. The baseline code (Parts 1–3) was not edited.

### What the placeholder readers are testing

| Reader | Age | Type | What it tests |
|---|---|---|---|
| Priya | 19 | typical | Fantasy fan: a "should be easy" case |
| Daniel | 22 | typical | Dystopia fan |
| Elena | 34 | typical | Romance classics |
| Viktor | 47 | typical | Russian literature |
| Grace | 41 | typical | Contemporary historical fiction |
| **Marcus** | 68 | **trap** | Loves picture books; age suggests otherwise |
| **Sam** | 29 | **trap** | Favourite (*A Brief History of Time*) is mislabelled "Historical Fiction" |
| **Leo** | 13 | **trap** | Harry Potter fan; *Goblet of Fire* appears twice in the catalogue |
| **Linda** | 55 | **trap** | Only knows the bestseller everyone rated |
| **Omar** | 36 | **trap** | Picky; highest rating is only 5/10 |

**Judged:** Priya, Daniel, Marcus, Sam, Leo (one per member, three traps).

### Results so far

| Version | Distinct titles (of 50) | Main observation |
|---|---|---|
| Baseline | 23 | Known reader and stranger get the **same 10 books** (10 of 10, every reader). 4 already-rated books shown. Leo's #1 is a duplicate of his own favourite. |
| Change 1: drop already-rated and duplicates | 20 | Already-rated books 4 → 0. Some replacements are poor (Leo, 13, gets *The Stand*). |
| Change 2: Bayesian average | 22 | Better where there is real data (Priya gets *Lord of the Rings* #1; Daniel gets adult fiction). |
| Change 3: ignore zeros | 21 | 63% of ratings in our readers' group were 0. Real favourites rise (*Giving Tree* 5.6 → 9.8), but single-vote 10s creep back in. |
| S / O / W counts | **not yet graded** | See To-Do 2 |

Problems none of the changes fixed: 9 of the 10 readers land in one group; known and stranger lists stay identical; Sam's list stays wrong because of the mislabelled genre.

---

## 3. What still needs to be done ⏳

Do these in order. Steps 1–3 block everything after them.

### To-Do 1: Decide on the test readers (whole group)
- [ ] Each member sends **2 readers** from their individual spec: `name, age, 3 books + rating (1–10)`, and whether it's a trap.
- [ ] Titles must be copied **exactly** from the `title` column of `book_data_sample_ed.csv` (lower case).
- [ ] **Coder:** replace the placeholder `people` list in Part 4, update `JUDGE` (5 names: one per member, at least 2 traps), then **Run all**. Fix any "not in the catalogue" warnings.
- [ ] If the group decides to keep the placeholders instead, say so, and make sure that's allowed by the assignment (the individual specs were meant to invent the readers).

### To-Do 2: Grade the sheets (writers)
- [ ] Open each of the 4 grading CSVs in Google Sheets.
- [ ] For every row, fill **`verdict`** with one letter and **`why`** with a few words:
  - **S** (sensible): a good pick for this person
  - **O** (obvious): they'd find it anyway, or already have it (`already_rated_by_reader = True` is an automatic O)
  - **W** (wrong): a bad fit for this person
- [ ] Watch for duplicates the sheet doesn't flag (e.g. the two *Goblet of Fire* titles).
- [ ] Grade the **baseline first**, so the later versions don't bias the baseline grades.
- [ ] Send the graded CSVs back to the coder.

### To-Do 3: Decide which changes to keep (whole group)
- [ ] Count S / O / W per version.
- [ ] For each change: **keep or reject, with one sentence why.** A rejected change still earns credit if the reason is explained.
- [ ] Optional Change 4 (coder): raise `M` (e.g. 5 → 15) to counter single-vote books returning after Change 3. Test it alone, the same way as the others.

### To-Do 4: Build the PDF tables (coder)
- [ ] **Verdict table:** the 5 readers' baseline lists with their S/O/W letters.
- [ ] **Ladder:** one row per change kept: name · S/O/W counts across the 50 · distinct titles of 50.
- [ ] **Before/after table:** 5 readers × 10 titles, baseline beside final version. Use the log cell at the end of the notebook, or the baseline and final grading CSVs.
- [ ] (Ask Claude to add a summary cell that reads the graded CSVs and builds these tables automatically.)

### To-Do 5: Write the PDF (writers)
- [ ] **Paragraph A:** rewrite the Part 1 draft bullets into prose. Re-check every number against the notebook output from the **final run**.
- [ ] **Paragraph B:** the baseline verdict table, then each change: what it was, why we tried it (link it to an audit finding), what happened. Good evidence:
  - known vs. stranger lists were identical (10 of 10)
  - already-rated books shown (4 → 0 after Change 1)
  - Leo's duplicate #1 pick
  - 63% of ratings are zeros
- [ ] **Paragraph C:** fill the `[brackets]` in the notebook draft (S/O/W counts, keep/reject decisions), then rewrite it in your own words.
- [ ] **Trace (end of the PDF, 3–6 rows):** fill the "what we changed" column. **Each member checks at least one row.** The brief says the AI can't be the only one who read it.

### To-Do 6: Final checks before submitting
- [ ] Replace *(replace with all names)* in the notebook's first cell with every group member's name.
- [ ] Notebook runs top to bottom without errors (*Runtime → Restart and run all*).
- [ ] Every number in the PDF matches the final notebook output.
- [ ] Remove or update the `PLACEHOLDER` comment in Part 4 if the readers were replaced.
- [ ] Submit **one PDF + one notebook** for the group by **Wed 11 Nov, 11:59 PM**.
- [ ] Prepare for the in-class showing (Session 19).

---

## 4. Who does what

| Role | Tasks |
|---|---|
| **Coder** | To-Do 1 (enter readers, run), To-Do 3 optional Change 4, To-Do 4 (tables), To-Do 6 (notebook runs cleanly) |
| **Writers** | To-Do 1 (send readers), To-Do 2 (grading), To-Do 5 (Paragraphs A, B, C and the trace) |
| **Everyone** | To-Do 3 (keep/reject decisions), checking one trace row each, final review |
