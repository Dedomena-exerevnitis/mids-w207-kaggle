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
  
 [JB] Historical data on games played in tournaments back to 1998. Of the 364 teams, 252 of them have participated in the NCAA March Madness tournament since 1998. Median = 3. Mean = 5.33. Mode = 0,1. Nonzeros: 252/364. This indicates that 1) not all teams make it to the tournament, even over a 20 year period. Also, a higher mean than median suggests a positive skew, meaning that there are several teams that have appeared many times in the tournament (max = 21; UConn, Notre Dame, Stanford, Tennessee), but most teams appear infrequently or not at all.
 
 [JB] Our dataset also includes seeds for all teams in the tournament since 1998. Seeds are between 1 and 16, within each region (4 regions). Each year, there are 4 teams with seeds of each value. Some teams regularly perform well in the tournament, so we examined the average seed value for teams. The top 5 teams with the best (lowest) average seed are: UConn (1.24, 21 appearances), Duke (2, 20 appearances), Tennessee (2, 21 appearances), USC (2.56, 9 appearances), and Baylor (2.59, 17 appearances). 
 
  - Missing values
  - Distribution of target
  - Relationships between features
  - Other idiosyncracies?

## Data Preparation

- What steps are taken to prepare the data for modeling?
  - feature transformations? engineering?
  
  [JB] While examining, we noticed that teh regular season statistics are not necessarily indicative of tournament performance due to the difference in competitiveness between leagues. In general, ACC, The American, A-10, Big 12, Big East, Big Ten, Mountain West, Pac-12, and SEC are seen as the most competitive leagues. Leagues such as the Patriot or Ivy league, while also Division I, are not typically as competitive. We will use aggregate statistics for win percentage in the tournament as a proxy for a league's competitiveness. This seems to track with general knowledge of the more competitive leagues, particularly, for women's basketball: ACC (0.55), The American (0.24), A-10 (0.27), Big 12 (0.54), Big East (0.39), Big Ten (0.44), Mountain West (0.17), Pac-12 (0.54), and SEC (0.59). 
  
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
