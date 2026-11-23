# Model Evaluation: The Curve, and What It Cannot Tell You

## Objective
I explored how model evaluation metrics, classification thresholds, and misclassification costs affect model comparison and decision-making for a rare outcome.

## Methodology
- Simulated 8,000 cases of a rare outcome, with 283 positive cases (11.8%) in the test set.
- Fitted a logistic regression model and plotted ROC and precision-recall curves.
- Compared logistic regression with a boosted-tree model using ROC AUC and average precision.
- Used 500 paired bootstrap resamples to calculate a 95% confidence interval for the difference in ROC AUC.
- Built an expected-cost curve where a false negative costs ten times as much as a false positive.
- Selected the lowest-cost threshold using the training data and evaluated its cost on the test data.
- Compared both models across cost ratios ranging from 2:1 to 50:1.
- Wrote and tested a function, `roc_point()`, to calculate the false positive rate and true positive rate at a given threshold.

## Key Findings
- My logistic regression model achieved a ROC AUC of 0.8468 and an average precision of 0.4651.
- The boosted-tree model achieved a ROC AUC of 0.8431. The AUC difference was 0.0038, with a 95% confidence interval of [-0.0020, 0.0094]. Since the interval includes zero, I could not establish that either model had better ROC AUC.
- At a 10:1 cost ratio, my optimal training threshold was 0.0905. This produced a test cost of 0.4692 per case, compared with 0.9437 at the default threshold of 0.5.
- The cheaper model changed depending on the cost ratio. The boosted-tree model was cheaper at 5:1, while logistic regression was cheaper at all other tested ratios.
- My `roc_point()` function passed the validation checks. At the selected threshold, the false positive rate was 0.296 and the true positive rate was 0.823.
- I found that ROC AUC alone does not determine which model is better for a particular decision. Outcome prevalence, classification thresholds, and the relative costs of errors all matter when choosing a model.
