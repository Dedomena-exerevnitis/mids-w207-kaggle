# W207 Final Project: Google Cloud & NCAA® ML Competition 2018-Women's

## Business Understanding

- What problem are we trying solve? 
- What are the relevant metrics? How much do we plan to improve them?
- What will we deliver?

## Data Understanding

- What are the raw data sources? 

[JB] Raw data sources include .csv files from Kaggle: 
1. WCities
2. WGameCities
3. WNCAATourneyCompactResults
4. WNCAATourneyDetailedResults
5. WNCAATourneySeeds
6. WNCAATourneySeeds
7. WRegularSeasonCompactResults
8. WRegularSeasonDetailedResults
9. WSeasons
10. WTeams
11. WTeamSpellings

- What does each 'unit' (e.g. row) of data represent?

[JB] The bulk of the information we will be using for analysis are in the results from regular season and tournament games. Each unit of data represents a game that was played between two teams, and the fields are relevant statistics. 

- What are the fields (columns)?

[JB] This includes game-level statistics such as: Season (year), Day number in the season the game was played, teams participating, final score, location, and number of overtimes. Additionally, it includes team-level statistics for each team: 2 pointers attempted/made, 3 pointers attempted/made, free throws attempted/made, offensive/defensive rebounds, assists, time outs, steals, blocks, and personal fouls.

- EDA
  - Distribution of each feature
 
  [Prashant] ADD HERE
 
  [Arvindh] ADD HERE
  
   [JB] Historical data on games played in tournaments back to 1998. Of the 364 teams, 252 of them have participated in the NCAA March Madness tournament since 1998. Median = 3. Mean = 5.33. Mode = 0,1. Nonzeros: 252/364. This indicates that 1) not all teams make it to the tournament, even over a 20 year period. Also, a higher mean than median suggests a positive skew, meaning that there are several teams that have appeared many times in the tournament (max = 21; UConn, Notre Dame, Stanford, Tennessee), but most teams appear infrequently or not at all.
 
  [JB] Our dataset also includes seeds for all teams in the tournament since 1998. Seeds are between 1 and 16, within each region (4 regions). Each year, there are 4 teams with seeds of each value. Some teams regularly perform well in the tournament, so we examined the average seed value for teams. The top 5 teams with the best (lowest) average seed are: UConn (1.24, 21 appearances), Duke (2, 20 appearances), Tennessee (2, 21 appearances), USC (2.56, 9 appearances), and Baylor (2.59, 17 appearances). 
 
  - Missing values
  
  [JB] Right now, we do not see any missing values in the fields. There may be missing games (rows), but it is not apparent at this point. It would be too difficult to cross-reference every game played in the past 21 seasons, so we assume the data is complete. 
 
  - Distribution of target
  
  ???

  - Relationships between features
  
  [Prashant] add notes about relationship between game stats
  
  - Other idiosyncracies?
  
  [JB] One thing that was very apparent in EDA is the overall dominance of the University of Connecticut team in regular season and tournament games. As compared to NCAA men's basketball, where the 

## Data Preparation

- What steps are taken to prepare the data for modeling?
  - feature transformations? engineering?
  
  [JB] While examining, we noticed that teh regular season statistics are not necessarily indicative of tournament performance due to the difference in competitiveness between leagues. In general, ACC, The American, A-10, Big 12, Big East, Big Ten, Mountain West, Pac-12, and SEC are seen as the most competitive leagues. Leagues such as the Patriot or Ivy league, while also Division I, are not typically as competitive. We will use aggregate statistics for win percentage in the tournament as a proxy for a league's competitiveness. This seems to track with general knowledge of the more competitive leagues, particularly, for women's basketball: ACC (0.55), The American (0.24), A-10 (0.27), Big 12 (0.54), Big East (0.39), Big Ten (0.44), Mountain West (0.17), Pac-12 (0.54), and SEC (0.59). 
  
  Eventually, more transformation has to be done so that the input for each is a 'pairing' consisting of two teams + associated stats (which may include: past tournament performance, league membership, regular season game aggregate statistics, etc.) for each.
  
  - table joins? aggregation?
  
  [JB] Currently, data on regular season + postseason play + team/league information is in separate files, with statistics for each game played. We are adding to that aggregate statistics about the stregnth of each team playing as well. _to expand_
  
  
- Precise description of modeling base tables.



  - What are the rows/columns of X (the predictors)?
  
  
  - What is y (the target)?

  [JB] y = probability that the first team (lowest team #) will win. To minimize duplication, team pairs are always listed with the smaller number team pair first.

## Modeling

- What model are we using? Why?

  [JB] We plan to use a logisitic regression model because we are dealing with a binary outcome (win vs. loss).

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
