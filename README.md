# Evidence-Grounded Assignment Requirement Checker

PE6201 end-of-course individual project by Yao Fangxuan. The runnable system is `PE6201_Complete_Prototype_and_Evaluation.ipynb`. It accepts one requirement and student submission text and returns a three-way judgment with exact quotes and missing evidence.

## Run in Google Colab

1. Open the notebook in Colab. Add `OPENROUTER_API_KEY` to **Secrets** and grant notebook access. Never paste the key into a notebook or GitHub.
2. Run the setup cell; upload `PE6201_Synthetic_60_Gold.csv` in the file upload cell.
3. Run the checker definition cell and the **single paid call** example. Edit its two input strings to demonstrate your own requirement and submission.
4. For evaluation, run the 30-case development batch once; save the downloaded checkpoint. Run the abstention selection cell, then the 30-case test batch once. The latter incurs additional API charges. Do not use **Run all** to resume a partially completed batch.
5. Run the final metrics cell. Development and test results must be reported separately.

The notebook uses standard Colab libraries (`pandas`, `numpy`, `scikit-learn`) and Python's built-in HTTP client; there is no package installation step. The OpenRouter model ID is written in the notebook and may need adjustment if the provider changes. A live connection and a user-supplied key are needed for new calls. The result CSV is generated at runtime and downloaded; it is not a trained model.

## Files and provenance

- `PE6201_Synthetic_60_Gold.csv`: 20 selected requirement texts × three manually written synthetic submissions, with fixed intended labels and grouped dev/test split. The model sees only the `requirement` and `submission` fields. Never send `gold_label` in its prompt.
- `build_next.py`: reproducible construction script for the CSV and notebook. It reads the user's original `PE6201_A1_Dataset_Clean.xlsx` at `upload/PE6201_A1_Dataset_Clean.xlsx`; include that source workbook if asking someone else to regenerate artifacts with the script. The finished notebook and CSV run without it.
- `PE6201_Tradeoff_Analysis_Draft.md`: ≤1,200-word analysis draft. The real PE6203 report and group attachments are excluded from this public bundle.

## Scope and known limitations

The synthetic cases are intentionally short. Their initial partial labels have four disputed cases; results are reported without retrospective relabeling. After the development run, four held-out *test inputs* were clarified before any test predictions. The dataset has not undergone an independent blind label audit. The evidence-quality threshold chosen on development accepts every observed result at the 80% selective-accuracy target. Quote validation confirms text presence, not factual truth. The real-material exploratory run is discussed separately; it does not justify a three-class accuracy claim.

The teacher's final submission also requires a problem statement, ≤1,200-word trade-off analysis, a GitHub repository with working code, and a recorded presentation/demo. Confirm the latest extension and upload location from the course notice.
