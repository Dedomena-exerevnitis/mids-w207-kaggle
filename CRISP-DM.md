# Project Name

## Business Understanding

- What problem are we trying solve?
- What are the relevant metrics? How much do we plan to improve them?
- What will we deliver?

## Data Understanding

- What are the raw data sources?
- What does each 'unit' (e.g. row) of data represent?
- What are the fields (columns)?
- EDA
  - Distribution of each feature
  
 [JB] Historical data on games played in tournaments back to 1998. Of the 364 teams, 252 of them have participated in the NCAA March Madness tournament since 1998. Median = 3. Mean = 5.33. Mode = 0,1. Nonzeros: 252/364. This indicates that 1) not all teams make it to the tournament, even over a 20 year period. Also, a higher mean than median suggests a positive skew, meaning that there are several teams that have appeared many times in the tournament (max = 21, University of Connecticut), but most teams appear infrequently or not at all.
  - Missing values
  - Distribution of target
  - Relationships between features
  - Other idiosyncracies?

## Data Preparation

- What steps are taken to prepare the data for modeling?
  - feature transformations? engineering?
  - table joins? aggregation?
  [JB] Currently, data on regular season + postseason play is in separate files, with statistics for each game played. We are adding to that aggregate statistics about the stregnth of each team playing as well. _to expand_
- Precise description of modeling base tables.
  - What are the rows/columns of X (the predictors)?
  - What is y (the target)?

## Modeling

- What model are we using? Why?
- Assumptions?
- Regularization?

## Evaluation

- How well does the model perform?
  - Accuracy
  - ROC curves
  - Cross-validation
  - other metrics? performance?

- AB test results (if any)

## Deployment

- How is the model deployed?
  - prediction service?
  - serialized model?
  - regression coefficients?
- What support is provided after initial deployment?
