NBA Topps Now Demand Modeling

(2025–26 Season Baseline)

Overview

This repository documents a structured modeling exercise analyzing demand drivers for NBA Topps Now print runs during the 2025–26 season.

The objective is not to build a production-grade forecasting system, but to demonstrate a disciplined modeling workflow under limited data conditions and evaluate how product, player, and team attributes influence print volume.

This model serves as an evolving baseline and will be updated as additional cards and finalized print runs become available.

Objective

To forecast card print runs using structured features including:

Product structure (SP, Auto/Relic)

Team and team tier (market size proxy)

Superstar indicator

Rookie status

Card release sequencing

Dataset

170 cards (2025–26 season to date)

Target variable: print_run

Mixed card types (rookie, veteran, multi-player, SP, Auto/Relic)

Rows without finalized print runs were excluded from training.

Modeling Approach

The workflow follows a reproducible pipeline structure:

Target log transformation (log1p) to stabilize variance

Feature selection with explicit leakage prevention

Scikit-learn Pipeline with:

Median imputation (numeric)

OneHot encoding (categorical)

RandomForestRegressor (500 trees)

80/20 holdout validation

5-fold cross-validation

Permutation importance for business-level feature interpretation

All modeling steps are executed sequentially in a clean notebook and run end-to-end without manual intervention.

Performance (Baseline)

Holdout (Original Scale):

MAE ≈ 1,339

Median Absolute Percentage Error ≈ 26%

Cross-Validation (Log Scale):

Average Log MAE ≈ 0.51

Std Dev ≈ 0.12

Given the limited sample size and early-season data, these results represent a stable baseline rather than a finalized predictive system.

Feature Insights (Permutation Importance)

Primary demand drivers:

Team tier and team market size

Auto/Relic presence

Superstar indicator

Card release sequencing (early-season effect)

Secondary signals:

Rookie status (incremental once superstar is accounted for)

Multi-player structure

Minimal impact:

Universal parallel structures (no cross-card variation)

Permutation importance was used instead of tree split importance to evaluate true model dependency on business-level features.

Limitations

Early-season dataset only

Limited sample size (170 observations)

No external performance metrics (game stats, social signals)

No event-based NLP features

No time-aware validation yet implemented

Future Enhancements

Event-driven feature engineering (milestones, game-winners, etc.)

Player-level historical demand encoding

Gradient boosting comparison

Time-aware validation as the season progresses

Status

This repository represents Version 1 of an ongoing modeling exercise and will be iteratively refined as additional data becomes available.

Update README with cleaned v1 modeling structure
