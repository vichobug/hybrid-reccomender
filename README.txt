MKTG 4604 — Hybrid Recommender (Fall 2026)
=========================================

What is in this zip
-------------------
Hybrid_Reco_Template_Fall26.ipynb            START HERE. A working recommender for a small bookseller,
                                             written by hand, deliberately basic. Runs as given.
                                             Part 4: add your readers. Part 5: make your changes.
ratings_data_sample_ed.csv                   Who rated which book (User-ID, ISBN, Book-Rating).
users_data_sample_ed.csv                     The readers (User-ID, Location, Age).
book_data_sample_ed.csv                      The books (title, genres, description, year, author, ...).
                                             Copy titles for your invented readers from its `title` column.
User_Item_Collaborative_Filter.ipynb         Reference: user-based collaborative filtering, step by step.
Content_Based_Reco_using_NLP.ipynb           Reference: content-based filtering, step by step.

Dates
-----
The full instructions and rubric are on the Canvas assignment page.
Individual Critique and Spec   Sun 8 Nov, 11:59 PM  (one page, PDF; invents your two test readers)
Group build                    Wed 11 Nov, 11:59 PM (PDF + notebook, one per group),
                               then shown in class at Session 19 (Thu 12 Nov Sec 02 / Fri 13 Nov Sec 01).

Running the notebook
--------------------
Google Colab: upload the notebook, then the three CSV files (folder icon on the left), then
Runtime -> Run all. Everything runs as given. Jupyter or VS Code also work; keep the CSVs beside the
notebook. Libraries: pandas, numpy, matplotlib, scikit-learn, scipy (preinstalled in Colab).

To add your readers: fill the `people` list in Part 4 and run from the top again. Titles must match the
book file exactly; the notebook tells you if one does not.
