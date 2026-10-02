# German Credit Risk Classification

Cost-sensitive credit risk classification using logistic regression, decision trees, and neural networks in R — built around a real 5:1 cost asymmetry between approving a bad applicant and approving a good one.

## Overview

Financial institutions approving credit face two very different kinds of mistakes: rejecting a good applicant costs nothing, but approving a bad one is expensive. In this dataset, a false positive (approving a bad applicant) costs **−500 DM**, while a true positive (approving a good applicant) earns only **+100 DM** — a **5:1** cost asymmetry.

This project builds and compares three classification models on the German Credit dataset, shows that all of them are unprofitable under a standard 0.5 classification threshold, and then uses a decile-wise lift chart to find a profit-maximizing decision cutoff — turning a **−4,600 DM loss into a ~+6,000 DM profit** without changing the underlying model.

## Dataset

- **Source:** German Credit dataset — 1,000 historical loan applicants
- **Target:** `RESPONSE` — good credit (1, 700 cases) / bad credit (0, 300 cases)
- **Predictors:** 30 variables covering financial history, employment, loan purpose, demographics, and property ownership
- No direct income variable is present; income is inferred through proxies (employment duration, job type, installment rate)

## Methodology

1. **Data preparation** — cleaned column names, dropped non-predictive index column, verified no missing/duplicate values
2. **Exploratory analysis** — reviewed all predictors' expected role in a credit decision; flagged ethical concerns around gender and foreign-worker-status variables
3. **Partitioning** — 70/30 train/validation split (700 / 300 records)
4. **Model building** — logistic regression, classification tree (`rpart`), neural network (`nnet`, 5 hidden nodes)
5. **Evaluation** — confusion matrices and a business cost/gain matrix (+100 DM / −500 DM) on the validation set
6. **Threshold optimization** — decile-wise lift chart on ranked predicted probabilities to find the profit-maximizing cutoff
7. **Extended analysis** — stepwise logistic regression for feature selection; classification tree pruning (min. xerror and 1-SE rule)

## Results

| Model | Accuracy | Sensitivity | Specificity | Net Profit (0.5 threshold) |
|---|---|---|---|---|
| Logistic Regression | 75.33% | 86.06% | 51.09% | −4,600 DM |
| Neural Network (5 nodes) | 69.00% | 75.48% | 54.35% | −5,300 DM |
| Classification Tree | 71.33% | 85.10% | 40.22% | −9,800 DM |
| Stepwise Logistic Regression | 75.67% | 86.06% | 52.17% | −4,100 DM |

**Optimized strategy:** Approving only the top 40% of applicants ranked by predicted probability (cutoff ≈ 0.82) yields a peak cumulative net profit of **~+6,000 DM**.

## Key Findings

- All three models are unprofitable at the default 0.5 threshold — accuracy does not imply profitability under asymmetric costs
- False positives are the dominant cost driver across every model
- Ranking applicants and approving only the top 40% converts every model's loss into a substantial profit
- Stepwise feature selection reduced the model from 30 to 19 predictors while improving both fit (AIC) and profit
- Several statistically useful predictors (gender/marital status encoding, foreign worker status) raise fair-lending concerns and are flagged for ethical/regulatory review rather than blind deployment

## Repository Structure

```
├── data/
│   └── GermanCredit.csv              # Raw dataset
├── docs/
│   └── Variable_Dictionary.docx      # Data dictionary
├── analysis/
│   └── german_credit_analysis.Rmd    # Full R Markdown analysis
├── presentation/
│   └── GermanCredit_Presentation.pdf # Final business presentation
└── README.md
```

> Adjust the paths above to match your actual repository layout.

## Tools & Libraries

- **Language:** R / R Markdown
- **Libraries:** `caret`, `rpart`, `rpart.plot`, `nnet`, `gains`

## How to Run

```r
# Install required packages
install.packages(c("caret", "rpart", "rpart.plot", "nnet", "gains"))

# Open and knit the analysis
rmarkdown::render("analysis/german_credit_analysis.Rmd")
```

## Final Recommendation

Deploy logistic regression as the primary model, using a probability cutoff of ≈0.82 (approve only the top 30–40% of ranked applicants) instead of the default 0.5 threshold. The stepwise-refined model is recommended as a leaner production candidate, and demographic/nationality variables should undergo compliance review before real-world use.

## Skills Demonstrated

Data Cleaning & Preparation · Exploratory Data Analysis · Classification Modeling · Cost-Sensitive Model Evaluation · Threshold/Cutoff Optimization · Lift/Gains Analysis · Stepwise Feature Selection · R / R Markdown · Business Communication
