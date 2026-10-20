# DSCI 552 Homework 4 — AReM classification

**Yash Desai**

## Observed results

| Method | Mean CV accuracy | Test accuracy |
|---|---:|---:|
| Binary backward RFE | 98.57% | 94.74% (18/19) |
| Binary L1 logistic | 98.57% | 94.74% (18/19) |
| Seven-class L1 multinomial | 91.34% | 89.47% (17/19) |
| Seven-class GaussianNB | 88.48% | 89.47% (17/19) |
| Seven-class MultinomialNB | 82.68% | 84.21% (16/19) |

The notebook explains the selected settings and all numerical conclusions.
Unpenalized coefficients exhibit complete separation, so the reported nominal
Wald p-values are explicitly labeled as unreliable for inference.

## Open and run

Use Python 3.11–3.13. Open this extracted folder in VS Code. In its terminal:

```bash
python -m pip install -r requirements.txt
```

Open `Yash_Desai_DSCI552_HW4_AReM_Explained.ipynb`, select the Python environment
where you installed these requirements, and choose **Run All**. The notebook
contains the complete analysis code, explanations, and saved execution outputs.
It runs from the repository root, where `data/arem/` is located. The source
archive is not required because all 88 source recordings are included.

You can also run the equivalent script:

```bash
python run_hw4.py
```

The complete CV searches can take several minutes or longer depending on the
computer. Each completed segment count is printed. Re-running writes the tables
and figures under `results/`. The fixed seed and pinned numerical packages
support reproducibility; small solver/platform differences are possible.

## Files

- `Yash_Desai_DSCI552_HW4_AReM_Explained.ipynb`: main submission, all answers and code.
- `run_hw4.py`: equivalent executable Python source, with notebook-style sections.
- `data/arem/`: seven activity folders, 88 CSV recordings, original dataset documentation.
- `results/`: full parameter grids, individual fold scores, selected coefficients,
  per-recording test predictions, comparison tables, and figures.
- `HW3_reference.ipynb`: prior feature extraction for reference; not the HW4 answer.
- `requirements.txt`: execution dependencies.

## Question coverage

| Required question | Location in notebook |
|---|---|
| 2(a)(i) | Nine-variable training scatter matrix: mean, median, q3; channels 1,2,6 |
| 2(a)(ii) | Eighteen-variable scatter matrix after splitting each series into two halves; interpretation |
| 2(a)(iii) | Joint l/p search with recursive backward elimination; five stratified folds; CV leakage explanation |
| 2(a)(iv) | Training confusion matrix, ROC, AUC, coefficients, nominal Wald p-values and inference limitations |
| 2(a)(v) | Fixed test-set evaluation using the selected segmentation and features; comparison to CV |
| 2(a)(vi) | Linear-programming separation check and coefficient stability diagnostic |
| 2(a)(vii) | Balanced case-control sample and intercept prior correction; matrices and ROC/AUC |
| 2(b)(i) | Joint l/C search for L1 binary logistic regression |
| 2(b)(ii) | Numerical and methodological comparison with backward selection |
| 2(c)(i) | Joint multinomial L1 model; test error, seven-class confusion matrix, one-versus-rest ROC/AUC |
| 2(c)(ii) | GaussianNB and MultinomialNB searches and evaluation |
| 2(c)(iii) | Comparison and interpretation of the three multiclass methods |
| 3: ISLR 4.8.3 | Quadratic Bayes discriminant derivation |
| 4: ISLR 4.8.7 | Dividend probability calculation with Bayes' rule |

Part 1 is the HW3 feature-extraction assignment and is explicitly not a separate
HW4 submission requirement. The loader and feature extraction needed for HW4
are included. Part 5 exercises are extra practice and not required.

## Method choices

- One row per recording; all temporal segments stay in that recording's row.
- Prescribed split: 69 training, 19 test recordings. Binary training counts are
  60 other and 9 bending. Scaling and feature selection are fitted within folds.
- All l values 1 through 20 are searched. The finite p/C/smoothing grids are
  printed and documented in the notebook. No held-out labels are used for tuning.
- The assignment permits recursive backward elimination instead of p-value pruning.
  This implementation takes that route. Final nominal Wald p-values are shown
  with an explicit separation/post-selection limitation, not treated as valid
  significance tests when their assumptions fail.
- Binary CV uses five stratified folds. Seven-class CV uses four stratified folds
  because the rarest training class has only four recordings; all multiclass
  methods use the same folds.
- Case-control correction uses original training prevalence, not test prevalence.
- Multinomial logistic regression uses SAGA, which fits a joint multinomial model.
  Binary L1 uses liblinear. MultinomialNB uses nonnegative min-max scaled features;
  its count likelihood is acknowledged as an approximation for continuous summaries.

## Sources

Dataset: [UCI AReM](https://archive.ics.uci.edu/dataset/366/activity+recognition+system+based+on+multisensor+data+fusion+arem).
The dataset documentation and citation are included under `data/arem/`.
Textbook: James, Witten, Hastie, Tibshirani, *An Introduction to Statistical
Learning*, second edition (2021), Chapter 4, exercises 3 and 7.
See the notebook's References section for software and sampling references.

## GitHub submission

Upload the extracted contents as the repository files, including `data/arem/`.
Create a public repository as requested by the instructor. Verify that GitHub
shows the main notebook, its outputs, README, requirements, and data folders.
Submit the repository URL through the course's designated submission channel.
