# W207 Final Project Outline - NCAA Women

This project is to use the history data about women's college basketball games (both tournament and regular season) and teams, with the purpose of predicting the winning probabilities for every possible matchup of teams of the 2018 NCAA tournament. After four group meetings and thorough discussion and analysis, so far, we have completed the EDA with the process of business understanding and data understanding, and are working on the iterative process of data preparation and modeling. Below is the brief summary of the EDA，the ongoing work, and plan for completing the project.  


## Business Understanding

As mentioned in the brief introduction above, this purpose of this project is to build a model to predict the winning probabilities for every possible matchup of teams of the 2018 NCAA Women's basketball tournament. The NCAA tournament is also well-known as March Madness, not only because it is happening in March, but also because of the fast-paced elimination mechanism (single elimination) and the surprising results that often arise when pairing teams across leagues that have previously never played each other. Therefore, building a better model to predict the results of the tournament is interesting and difficult, and the prediction of the winning probabilities for every possible matchup becomes the first and most critical part for predicting the NCAA bracket.  


## Data Understanding

In this project, the data sets include historical data of tournaments and regular season games back to 1998, team information, etc. We will begin exploring the data such as detailed performance data for tournaments and regular season games and previous and current seed numbers in the tournament.

- What are the raw data sources?

  Raw data sources include .csv files from Kaggle:
  1. WCities - city number and associated English city/state names
  2. WGameCities - winning team id, losing team id, and city id
  3. WNCAATourneyCompactResults - season, day number, winning team id, winning score, losing team id, losing score, location, and number of overtimes for each tournament game since 1998
  4. WNCAATourneyDetailedResults - in addition to the above, for each team, includes 2 pointers attempted/made, 3 pointers attempted/made, free throws attempted/made, offensive/defensive rebounds, assists, time outs, steals, blocks, and personal fouls for each tournament game since 1998
  5. WNCAATourneySeeds - seed number and associated team for each tournament since 1998
  6. WNCAATourneySlots - indicates seeds of teams that play at each round of 64 'slot'  
  7. WRegularSeasonCompactResults - season, day number, winning team id, winning score, losing team id, losing score, location, and number of overtimes for each regular season game since 1998
  8. WRegularSeasonDetailedResults - in addition to the above, for each team, includes 2 pointers attempted/made, 3 pointers attempted/made, free throws attempted/made, offensive/defensive rebounds, assists, time outs, steals, blocks, and personal fouls for each tournament game since 1998
  9. WSeasons - locations of championship game played in each region for tournaments since 1998
  10. WTeams - team id and associated English spelling team name
  11. WTeamSpellings - alternative spellings and abbreviations for each team

- What does each 'unit' (e.g. row) of data represent?

  The bulk of the information we plan to use for analysis are in the detailed results from regular season and tournament games. Each unit of data represents a game that was played between two teams, and the fields are relevant statistics.

- What are the fields (columns)?

  These include game-level statistics such as: season (year), day number in the season the game was played, teams participating, final score, location, and number of overtimes. Additionally, it includes team-level statistics for each team: 2 pointers attempted/made, 3 pointers attempted/made, free throws attempted/made, offensive/defensive rebounds, assists, time outs, steals, blocks, and personal fouls.

- EDA
  - Distribution of each feature

    [Arvindh] ADD HERE. It seems like Arvindh hasn't updated his file, so I only include the ideal of moving-average in the introduction of data understanding.


    
    Additionally, we explore the possibility of using past game performance (regular season and in the tournament) as a feature. Of the 364 teams, 252 of them have participated in the NCAA March Madness tournament at least once since 1998. Median = 3 appearances; mean = 5.33; mode = 0,1. Nonzeros: 252/364. This indicates that 1) not all teams make it to the tournament, even over a 21 year period. Also, a higher mean than median suggests a positive skew, meaning that there are several teams that have appeared many times in the tournament (max = 21; UConn, Notre Dame, Stanford, Tennessee), but most teams appear infrequently or not at all.

    Our dataset also includes seeds for all teams in the tournament since 1998. Seeds are between 1 and 16, within each region (4 regions). Each year, there are 4 teams with seeds of each value. Some teams seem to regularly perform well in the tournament, so we examined the average seed value for teams. The top 5 teams with the best (lowest) average seed are: UConn (1.24, 21 appearances), Duke (2, 20 appearances), Tennessee (2, 21 appearances), USC (2.56, 9 appearances), and Baylor (2.59, 17 appearances).

  - Missing values

    Right now, we do not see any missing values in the fields. There may be missing games (rows), but it is not apparent at this point. It would be too difficult to cross-reference every game played in the past 21 seasons, so we assume the data is complete.

  - Distribution of target

    The output data for training and development data set is the win or lose label for each game. Since each team will either win or lose the game, the distribution of output data is uniform distributed with equally probability of value 1 and 0.

  - Relationships between features

    There 13 field performance features for each team in each game of tournaments or regular seasons (FGM, FGA, FGM3, FGA3, FTM, FTA, OR, DR, Ast, TO, Stl, Blk, PF). PCA, as a tool to reduce the dimension and do the feature construction, is used to examine the feasibility of aggregate all the filed features in to one feature, overall performance. However, after PCA, the first dimension only weights the 40% of the total variance of all features, and in order to reach the 90% variance, 6 dimensions need to be kept, which violets the purpose of using PCA to aggregate  filed features into one. Therefore this case is not suitable for using PCA for feature construction or dimension reduction, we turn to use seek for other ways of feature selection and construction.   

    Below is the insights of the relationship between those features and score margin :

      **FGA** as field goal percentage: a higher field goal percentage difference is strongly associated with win margin.

      **WFGM3/WFGA3 - LFGM3/LFGA3** as the 3 point field goal percentage difference: the correlation between 3 point field goal percentage difference and win margin is not too strong. This indicates that teams that win a game with a larger margin tend to have only slightly better 3 point field goal percentage than the losing team in that game.
      Free throw performance by itself is not strongly associated with win margin. This is not surprising. Some teams have a lower 2 point field goal rate but they draw a larger number of personal fouls from the opposing team. This can lead to a difference in tactics of how the teams accumulate 2 point goals without impacting their overall success in scoring 2 point goals.

      **(WOR + WDR) - (LOR + LDR)** as relative performance in offensive and defensive rebounds: it has a significant correlation with win margin

      **WAst - LAst** as relative performance in assists: it has a strong correlation with win margin. Assists indicate a more orchestrated style of play and may be an indicator how a team collaborates and creates opportunities on the field.

      **WStl - LStl** as relative performance in steals: it has a modest correlation with win margin.

      **OR + DR** as the rebound performance: the winning team's rebound performance is strongly associated with the number of field goal attempts. The correlation is less strong for the losing team.

    Then we explores how performance on different measures has impacted game outcomes over time. Over the years, the importance of field goal performance in determining game outcomes has remained constant whereas the importance of assists and rebounds in determining game outcomes has been rising.


  - Other idiosyncracies?

    [JB] One thing that was very apparent in EDA is the overall dominance of the University of Connecticut team in regular season and tournament games. As compared to NCAA men's basketball, where the....
    
     [todo], dated back to a number of years or a number of games played (constructing new feature: moving-average), in order to explore the data and prepare for feature selection and construction.

## Ongoing work and plan for future  

After have thorough understanding of the problem and data, we are now working on the data preparation and modeling before week 13. Blew is the draft of what achieved and planed so far for data preparation and modeling.  

## Data Preparation

- What steps are taken to prepare the data for modeling?
  - feature transformations? engineering?

    [While examining, we noticed that the regular season statistics are not necessarily indicative of tournament performance due to the difference in competitiveness between leagues. In general, ACC, The American, A-10, Big 12, Big East, Big Ten, Mountain West, Pac-12, and SEC are seen as the most competitive leagues. Leagues such as the Patriot or Ivy league, while also Division I, are not typically as competitive. We will use aggregate statistics for win percentage in the tournament as a proxy for a league's competitiveness. This seems to track with general knowledge of the more competitive leagues, particularly, for women's basketball: ACC (0.55), The American (0.24), A-10 (0.27), Big 12 (0.54), Big East (0.39), Big Ten (0.44), Mountain West (0.17), Pac-12 (0.54), and SEC (0.59).

    Eventually, more transformation has to be done so that the input for each is a 'pairing' consisting of two teams + associated stats (which may include: past tournament performance, league membership, regular season game aggregate statistics, etc.) for each.

  - table joins? aggregation?

    Currently, data on regular season + postseason play + team/league information is in separate files, with statistics for each game played. We are adding to that aggregate statistics about the strength of each team playing as well. _to expand_


- Precise description of modeling base tables.

  - What are the rows/columns of X (the predictors)?

    After finalizing the data preparation, especially feature selection and construction, we will have a detailed explanation of X.

  - What is y (the target)?

    The output data y for training and development data set is the win (1) or lose (0) label of the first team in the matchup for each game.
    However, because we are predicting the winning probability by logistic model, the target of the deployment or the output of the model y is the probability that the first team (lowest team #) will win. To minimize duplication, team pairs are always listed with the smaller number team pair first.

## Modeling

- Model that we are using

  We plan to use a logistic regression model as the base model because we are dealing with a binary outcome (win vs. loss), and predicting the winning probability of the first team in each matchup. But we will try the concept of bootstrapping from random forest to improve the model.

- Assumptions

  Because we are using the logistic regression, we assume

  1. the dependent variable to be binary

  2. each features or observation to be independent, and model have little or no multicollinearity

  3. dependent (y) and independent (x) variables are linearly related to the log odds

- Regularization

  We will discuss the regularization after model is build.


## Evaluation and Deployment

After modeling is done, on week 14, we will step to the process of evaluation and deployment, which will be discussed in the coming groups meetings.  
