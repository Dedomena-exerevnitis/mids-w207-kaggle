# W207 Final Project Outline - NCAA Women

This project is to use the history data about women college basketball games (both tournament and regular season) and teams, on the purpose of predicting the winning probabilities for every possible matchup of teams of the 2018 NCAA tournament. After four group meetings and thorough discussion and analysis, so far, we have done the EDA with the process of business understanding and data understanding, and are working on the iterative process of data preparation and modeling. Below is the brief summary of the EDA，the ongoing work, and plan for completing the project.  


## Business Understanding

- What problem are we trying solve?
- What are the *relevant metrics*? How much do we plan to improve them?
- What will we deliver?

As mentioned in the brief introduction above, this project is on the purpose of modeling to predict the winning probabilities for every possible matchup of teams of the 2018 NCAA Women's tournament. The NCAA tournament is also well-known as March Madness, not only because it is happening in March, but also because the fast-pace elimination mechanism and the surprising results. Therefore, to build a better model and predict the result of the tournament is so interesting, and the prediction of the winning probabilities for every possible matchup become the first and critical part for predicting the NCAA bracket.  


## Data Understanding

In this project, the data sets include history data of tournaments and regular reason back to 1998, teams information, etc. We will focus on the data such as detailed fields performance data in tournaments and regular reason and seed number, dated back to a number of years or a number of games played (constructing new feature: moving-average), in order to explore the data and prepare for feature selection and construction.

- What are the raw data sources?

Raw data sources include .csv files from Kaggle:
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

The bulk of the information we will be using for analysis are in the results from regular season and tournament games. Each unit of data represents a game that was played between two teams, and the fields are relevant statistics.

- What are the fields (columns)?

[JB] This includes game-level statistics such as: Season (year), Day number in the season the game was played, teams participating, final score, location, and number of overtimes. Additionally, it includes team-level statistics for each team: 2 pointers attempted/made, 3 pointers attempted/made, free throws attempted/made, offensive/defensive rebounds, assists, time outs, steals, blocks, and personal fouls.

- EDA
  - Distribution of each feature

  - Overall understanding of tournaments and seeds

  Historical data on games played in tournaments back to 1998. Of the 364 teams, 252 of them have participated in the NCAA March Madness tournament since 1998. Median = 3. Mean = 5.33. Mode = 0,1. Nonzeros: 252/364. This indicates that 1) not all teams make it to the tournament, even over a 20 year period. Also, a higher mean than median suggests a positive skew, meaning that there are several teams that have appeared many times in the tournament (max = 21; UConn, Notre Dame, Stanford, Tennessee), but most teams appear infrequently or not at all.

  Our dataset also includes seeds for all teams in the tournament since 1998. Seeds are between 1 and 16, within each region (4 regions). Each year, there are 4 teams with seeds of each value. Some teams regularly perform well in the tournament, so we examined the average seed value for teams. The top 5 teams with the best (lowest) average seed are: UConn (1.24, 21 appearances), Duke (2, 20 appearances), Tennessee (2, 21 appearances), USC (2.56, 9 appearances), and Baylor (2.59, 17 appearances).

  - Insight of features of field performance

  There 13 field performance features for each team in each game of tournaments or regular seasons (FGM, FGA, FGM3, FGA3, FTM, FTA, OR, DR, Ast, TO, Stl, Blk, PF). PCA, as a tool to reduce the dimension and do the feature construction, is used to examine the feasibility of aggregate all the filed features in to one feature, overall performance. However, after PCA, the first dimension only weights the 40% of the total variance of all features, and in order to reach the 90% variance, 6 dimensions need to be kept, which violets the purpose of using PCA to aggregate  filed features into one. Therefore this case is not suitable for using PCA for feature construction or dimension reduction, we turn to use seek for other ways of feature selection and construction.   

  Below is the insights of the relationship between those features and score margin :

    *FGA* as field goal percentage: a higher field goal percentage difference is strongly associated with win margin.

    *WFGM3/WFGA3 - LFGM3/LFGA3* as the 3 point field goal percentage difference: the correlation between 3 point field goal percentage difference and win margin is not too strong. This indicates that teams that win a game with a larger margin tend to have only slightly better 3 point field goal percentage than the losing team in that game.
    Free throw performance by itself is not strongly associated with win margin. This is not surprising. Some teams have a lower 2 point field goal rate but they draw a larger number of personal fouls from the opposing team. This can lead to a difference in tactics of how the teams accumulate 2 point goals without impacting their overall success in scoring 2 point goals.

    *(WOR + WDR) - (LOR + LDR)* as relative performance in offensive and defensive rebounds: it has a significant correlation with win margin

    *WAst - LAst* as relative performance in assists: it has a strong correlation with win margin. Assists indicate a more orchestrated style of play and may be an indicator how a team collaborates and creates opportunities on the field.

    *WStl - LStl* as relative performance in steals: it has a modest correlation with win margin.

    *OR + DR* as the rebound performance: the winning team's rebound performance is strongly associated with the number of field goal attempts. The correlation is less strong for the losing team.

  Then we explores how performance on different measures has impacted game outcomes over time. Over the years, the importance of field goal performance in determining game outcomes has remained constant whereas the importance of assists and rebounds in determining game outcomes has been rising.

  - Construction new feature, moving-average

  [Arvindh] ADD HERE. It seems like Arvindh hasn't updated his file, so I only include the ideal of moving-average in the introduction of data understanding.



  - Missing values

  Right now, we do not see any missing values in the fields. There may be missing games (rows), but it is not apparent at this point. It would be too difficult to cross-reference every game played in the past 21 seasons, so we assume the data is complete.

  - Distribution of target

  The output data for training and development data set is the win or lose label for each game. Since each team is either win or lose the game, the distribution of output data is uniform distributed with equally probability of value 1 and 0.

  - Relationships between features

  [Prashant] add notes about relationship between game stats

  - Other idiosyncracies?

  [JB] One thing that was very apparent in EDA is the overall dominance of the University of Connecticut team in regular season and tournament games. As compared to NCAA men's basketball, where the....

## Ongoing work and plan for future  

After have thorough understanding of the problem and data, we are now working on the data preparation and modeling before week 13. Blew is the draft of what achieved and planed so far.  

After modeling is done, on week 14, we will step to the process of evaluation and deployment, which will be discussed in the coming groups meetings.  

## Data Preparation

- What steps are taken to prepare the data for modeling?
  - feature transformations? engineering?

  [While examining, we noticed that the regular season statistics are not necessarily indicative of tournament performance due to the difference in competitiveness between leagues. In general, ACC, The American, A-10, Big 12, Big East, Big Ten, Mountain West, Pac-12, and SEC are seen as the most competitive leagues. Leagues such as the Patriot or Ivy league, while also Division I, are not typically as competitive. We will use aggregate statistics for win percentage in the tournament as a proxy for a league's competitiveness. This seems to track with general knowledge of the more competitive leagues, particularly, for women's basketball: ACC (0.55), The American (0.24), A-10 (0.27), Big 12 (0.54), Big East (0.39), Big Ten (0.44), Mountain West (0.17), Pac-12 (0.54), and SEC (0.59).

  Eventually, more transformation has to be done so that the input for each is a 'pairing' consisting of two teams + associated stats (which may include: past tournament performance, league membership, regular season game aggregate statistics, etc.) for each.

  - table joins? aggregation?

  Currently, data on regular season + postseason play + team/league information is in separate files, with statistics for each game played. We are adding to that aggregate statistics about the strength of each team playing as well. _to expand_


- Precise description of modeling base tables.



  - What are the rows/columns of X (the predictors)?


  - What is y (the target)?

  The output data y for training and development data set is the win (1) or lose (0) label of the first team in the matchup for each game.
  However, because we are predicting the winning probability by logistic model, the target of the deployment or the output of the model y is the probability that the first team (lowest team #) will win. To minimize duplication, team pairs are always listed with the smaller number team pair first.

## Modeling

- What model are we using? Why?

  We plan to use a logistic regression model as the base model because we are dealing with a binary outcome (win vs. loss), and predicting the winning probability of the first team in each matchup. But we will try the concept of bootstrapping from random forest to improve the model.

- Assumptions?

  Because we are using the logistic regression, we assume

  1. the dependent variable to be binary

  2. each features or observation to be independent, and model have little or no multicollinearity

  3. dependent (y) and independent (x) variables are linearly related to the log odds

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
