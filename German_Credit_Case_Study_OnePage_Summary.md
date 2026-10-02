# German Credit Risk Classification — Project Summary

**Cost-sensitive credit risk classification using logistic regression, decision trees, and neural networks in R**

## What it was
Built and evaluated three classification models to predict credit risk (good vs. bad) on the 1,000-record German Credit dataset, then optimized the decision strategy around a real 5:1 cost asymmetry between false positives and true positives — rather than optimizing for accuracy alone.

## What I did
- Cleaned and explored 30 predictor variables; flagged ethical/fair-lending concerns in the data
- Partitioned data 70/30 and built **logistic regression**, a **classification tree**, and a **neural network** in R
- Evaluated models via confusion matrices and a business-defined **cost/gain matrix** (+100 DM / −500 DM)
- Discovered all three models were **unprofitable** at the standard 0.5 threshold
- Built a **decile-wise lift chart** using ranked predicted probabilities to find the profit-maximizing cutoff
- Extended the analysis with **stepwise feature selection**, improving model fit and profitability further

## Key result
Shifting from a default classification threshold to a **ranked, top-40% approval strategy** turned a **−4,600 DM loss** into a **~+6,000 DM profit** — without changing the underlying model.

## Tools
R, R Markdown, `caret`, `rpart`, `nnet`, `gains`

## Skills
Classification Modeling · Cost-Sensitive Evaluation · Threshold Optimization · Lift/Gains Analysis · Stepwise Feature Selection · Business Communication
