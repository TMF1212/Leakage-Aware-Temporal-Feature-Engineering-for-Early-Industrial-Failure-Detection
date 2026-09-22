Overview

Predictive maintenance models are often reported with near-perfect discrimination, but these figures frequently come from random train/test splits that let information from the same machine — or the same failure episode — leak into both training and evaluation data. This project:

Builds an initial model and demonstrates severe target leakage (spurious ROC-AUC of 1.00) caused by features derived from the failure countdown variable.
Conducts a structured leakage audit and constructs a leakage-safe feature set (raw sensor readings, observation-based lag features, and timestamp-aware one-hour rolling statistics).
Runs a feature-family ablation (logistic regression, four chronological folds) to measure the incremental value of each feature family.
Evaluates a Random Forest classifier under two realistic validation regimes: complete machine-level holdout (unseen machines) and a later, non-overlapping historical period (chronological validation).
Dataset

A synthetic multi-machine sensor dataset:

20 machines across 4 machine types
24,042 observations over a 14-day period
14.8% positive rate for a 24-hour failure horizon

The dataset was constructed to resemble industrial condition-monitoring data; it does not involve human participants or real production systems.

Key Results
Stage	ROC-AUC	PR-AUC
Initial model (leaked features)	1.00 (spurious)	—
Ablation: raw features only (mean)	0.946	0.821
Ablation: + lag/rolling features (mean)	0.978	0.923
Final Random Forest (unseen machines)	0.994	0.951
