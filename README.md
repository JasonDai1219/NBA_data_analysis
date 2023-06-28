# NBA_data_analysis
**this project mainly focues on making a basic model to predict NBA players' `Salaries` using their stats and experiences.**

## Web Scraping of NBA players' salaries data.
- specific details are in this jupyter notebook : https://github.com/JasonDai1219/NBA_data_analysis/blob/main/NBA%20Data%20Web%20Scraping.ipynb

## Introduction on datasets
- `players_stats` : this dataframe contains information of each player's performance `on court` from the season 2012-13 to now. This is a preview of the dataframe:

| Year    | Season_Type      |   PLAYER_ID |   RANK | PLAYER          |    TEAM_ID | TEAM   |   GP |   MIN |   FGM |   FGA |   FG_PCT |   FG3M |   FG3A |   FG3_PCT |   FTM |   FTA |   FT_PCT |   OREB |   DREB |   REB |   AST |   STL |   BLK |   TOV |   PTS |   EFF |
|:--------|:-----------------|------------:|-------:|:----------------|-----------:|:-------|-----:|------:|------:|------:|---------:|-------:|-------:|----------:|------:|------:|---------:|-------:|-------:|------:|------:|------:|------:|------:|------:|------:|
| 2012-13 | Regular%20Season |        2546 |      1 | Carmelo Anthony | 1610612752 | NYK    |   67 |  37   |  10   |  22.2 |    0.449 |    2.3 |    6.2 |     0.379 |   6.3 |   7.6 |    0.83  |    2   |    4.9 |   6.9 |   2.6 |   0.8 |   0.5 |   2.6 |  28.7 |  23.2 |
| 2012-13 | Regular%20Season |      201142 |      2 | Kevin Durant    | 1610612760 | OKC    |   81 |  38.5 |   9   |  17.7 |    0.51  |    1.7 |    4.1 |     0.416 |   8.4 |   9.3 |    0.905 |    0.6 |    7.3 |   7.9 |   4.6 |   1.4 |   1.3 |   3.5 |  28.1 |  30.4 |
| 2012-13 | Regular%20Season |         977 |      3 | Kobe Bryant     | 1610612747 | LAL    |   78 |  38.6 |   9.5 |  20.4 |    0.463 |    1.7 |    5.2 |     0.324 |   6.7 |   8   |    0.839 |    0.8 |    4.7 |   5.6 |   6   |   1.4 |   0.3 |   3.7 |  27.3 |  24.6 |
| 2012-13 | Regular%20Season |        2544 |      4 | LeBron James    | 1610612748 | MIA    |   76 |  37.9 |  10.1 |  17.8 |    0.565 |    1.4 |    3.3 |     0.406 |   5.3 |   7   |    0.753 |    1.3 |    6.8 |   8   |   7.3 |   1.7 |   0.9 |   3   |  26.8 |  32.2 |
| 2012-13 | Regular%20Season |      201935 |      5 | James Harden    | 1610612745 | HOU    |   78 |  38.3 |   7.5 |  17.1 |    0.438 |    2.3 |    6.2 |     0.368 |   8.6 |  10.2 |    0.851 |    0.8 |    4.1 |   4.9 |   5.8 |   1.8 |   0.5 |   3.8 |  25.9 |  24   |

- `salaries` : this dataframe contains information of each player's salary from the season 2012-13 to now. This is a preview of the dataframe: 

| PLAYER            | Salary      | Year    |
|:------------------|:------------|:--------|
| Kobe Bryant       | $30,453,805 | 2012-13 |
| Dirk Nowitzki     | $20,907,128 | 2012-13 |
| Amar'e Stoudemire | $19,948,799 | 2012-13 |
| Joe Johnson       | $19,752,645 | 2012-13 |
| Carmelo Anthony   | $19,444,503 | 2012-13 |

## Data Exploration
- we merge together the `players_stats` and `salaries` data frames together to let each player gets their corresponding salary in each season.
- As we do not have missing data in these datasets, so we do not need to work on data cleaning part that much, and we only need to make the salary variable in string format through `merged['Salary'] = merged['Salary'].str.strip('$').str.replace(',', '').astype('float')`.
- To also adjust the problem of inflation, we searched about the `cumulative inflation rate` from each season in our dataset to now, and adjusted each player's salaries accordingly.
- After all, we take the mean of all players' data across all these seasons to make the result more informativr, and the result could potentially `tell a NBA player how much income he is going to make each season approximately`.

add dataframes and graphs later on.

## Feature Engineering

- People may think that if a player has ever played in a city that has huge market and fans, won an MVP award, or played in the national team in Olympics, then the player will be more likely to gain higher salary. Thus we added these features in our original dataframe.
add heads of datasets later on.
- - As we could also see that due to the shift in coaches' tactics, which focuses on three pointer shooting in later seasons, we should perform a within group transformation to standardize each player's `on-court` performance within each season to have a better interpretability.

## Justification on model selection
- We can tell that the `Salary` of NBA players has a roughly linear relationship with other numerical variables, thus, we would use `Linear Regression`. However, it is important to verify that degree 1 polynomial regression(Linear Regression) is indeed the best choice, so we would perform a `cross-validation` to see which degree works the best for us.

## Model creation
- **Getting rid of unuseful variables** : we need to drop all IDs, since they are not relevant in our analysis, and could bring potential noise to the model. We are also dropping all attempted counts and made counts on shootings, as the percentage variable is a good enough representation of those two variable; the same reason applies to REB and OREb, DREB, and EFF. Therefore, we want to avoid `Multicolinearity` through dropping REB variable also.
- **Best Hyperparameter** : After using `cross validation`, we realized that degree x is the most optimal degree to use in our model.
- **Overall Model** : 
- **Model performance** : 
