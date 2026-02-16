# nba-topps-now-demand-model
# NBA Topps Now Print Run Forecasting

This project explores demand modeling for NBA Topps Now cards using structured card, player, and team attributes from the 2025 season onward.

The goal is not to build a production-grade forecasting system, but to demonstrate a structured modeling workflow under limited data conditions and evaluate how product and player attributes influence print volume.

## Objective

To model and forecast card print runs using:

- Product structure (Short Prints (SP), Autogrpahs/Relics)
- Team tier and market size
- Superstar indicators
- Rookie flags
- Card release sequencing

## Dataset

- 170 cards (2025-26 season to date)
- Target variable: `print_run`
- Mixed card types (rookie, veteran, multi-player, SP, Auto/Relic)

This dataset will expand as additional cards and finalized print runs become available.

## Modeling Approach

- Target log transformation to stabilize variance
- Scikit-learn Pipeline for reproducibility
- ColumnTransformer preprocessing
- RandomForestRegressor (500 trees)
- 80/20 holdout validation
- 5-fold cross-validation
- Permutation importance for feature validation

Modeling decisions were designed to minimize leakage and evaluate feature influence at the variable level rather than relying solely on tree-based split importance.

## Current Performance

- Holdout MAE ≈ 1,339
- Median absolute percentage error ≈ 26%
- Cross-validated log MAE ≈ 0.51 (std ≈ 0.12)

Results are considered a baseline and will evolve as additional data becomes available.
Rows with missing print runs were excluded from training.

## Key Observations

- Team market size and team tier materially influence demand.
- Auto/Relic presence significantly increases print runs.
- Superstar indicators provide stronger signal than rookie labels alone.
- Early-season releases exhibited elevated demand, captured via card sequencing.
- Universal card parallel structures (i.e. SN50, SN25...) contribute minimal explanatory variance.

## Limitations

- Early-season dataset only
- Limited sample size (170 observations)
- No external performance metrics (game stats, social signals)
- No event-based NLP features yet implemented

## Future Work

- Event keyword feature engineering
- Player-level historical encoding
- Gradient boosting comparison
- Time-based cross-validation as season progresses

This project is maintained as an ongoing modeling exercise.
