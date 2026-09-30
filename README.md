# Evidence-Grounded Assignment Requirement Checker

This is Yao Fangxuan's individual end-of-course project for PE6201 Emerging AI Technologies. The working system is a Google Colab notebook that checks one assignment requirement against a student's submission. It returns **Fully Satisfied**, **Partially Satisfied**, or **Not Satisfied**, together with exact supporting quotes or an explanation of what evidence is missing.

## Run the working system

1. Open `PE6201_Complete_Prototype_and_Evaluation.ipynb` in Google Colab.
2. Add your OpenRouter API key as a Colab Secret named `OPENROUTER_API_KEY` and grant the notebook access. Do not put the key in the notebook or on GitHub.
3. Run the setup cell and upload `PE6201_Synthetic_60_Gold.csv` when prompted.
4. Run the checker definition cell. In the single-check example, replace the example `requirement` and `submission` text with your own to see a judgment and evidence.
5. To reproduce the evaluation, run the 30 development cases, choose the abstention threshold using development results only, and then run the 30 held-out test cases. These model calls incur API charges. Save the downloaded checkpoint files; do not use **Run all** to restart a partially completed batch.
6. Run the final metrics cell to see development and test results separately.

The notebook uses Python and common Colab libraries. New model calls require an internet connection and your own API key.

## Repository files

- `PE6201_Complete_Prototype_and_Evaluation.ipynb` — runnable checker, development evaluation, threshold selection, and held-out test evaluation.
- `PE6201_Synthetic_60_Gold.csv` — 60 synthetic cases: 20 assignment requirements, each paired with three example submissions and a fixed intended label.
- `PE6201_End_of_Course_Project_Dataset.xlsx` — the one-sheet Part 1 source dataset containing the original assignment requirements.
- `build_next.py` — script that reads the source Excel file and regenerates the synthetic CSV and notebook. Keep it in the same folder as the Excel file when running it.
- `PE6201_results_60.csv` — recorded outputs and costs from the development and test runs.
- `PE6201_Tradeoff_Analysis_Draft.md` — project analysis draft.

The model receives the requirement and submission text, **not** the gold label. The development and test sets are separated by requirement so that examples based on the same requirement do not appear in both sets.

## Results and limitations

The 30-case development set achieved 27/30 label agreement (90.0%); the 30-case held-out test set achieved 29/30 (96.7%). The three-class majority baseline is 33.3%. All 60 recorded outputs passed the exact-quote substring check. The 60 model calls had a recorded provider cost of approximately US$0.0123 in total, or US$0.000205 per check.

These figures describe a small, balanced, synthetic dataset. Exact-quote validation checks whether a quoted string appears in the submission; it cannot prove that the quote supports the judgment. Some partial-case gold labels are debatable and were not changed after seeing predictions. The development-selected threshold accepted all observed results, so this experiment does not demonstrate a useful abstention benefit. A separate exploratory check using ten requirements and a real PE6203 report exposed additional limitations, including evidence located in separate attachments.

The final course submission also includes the problem statement, a trade-off analysis of at most 1,200 words, the GitHub repository with working code, and a recorded presentation/demo.
