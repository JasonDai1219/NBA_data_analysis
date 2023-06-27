# NBA_data_analysis
** this project mainly focues on making a basic model to predict NBA players' `Salaries` using their stats and experiences.**

## Web Scraping of NBA players' salaries data.
- specific details are in this jupyter notebook : https://github.com/JasonDai1219/NBA_data_analysis/blob/main/NBA%20Data%20Web%20Scraping.ipynb

** Introduction on datasets
- `players_stats` : this dataframe contains information of each player's performance `on court` from the season 2012-13 to now.
- `salaries` : this dataframe contains information of each player's salary from the season 2012-13 to now.

## Data Exploration
- we merge together the `players_stats` and `salaries` data frames together to let each player gets their corresponding salary in each season.
- As we do not have missing data in these datasets, so we do not need to work on data cleaning part that much, and we only need to make the salary variable in string format through `merged['Salary'] = merged['Salary'].str.strip('$').str.replace(',', '').astype('float')`.
- To also adjust the problem of inflation, we searched about the `cumulative inflation rate` from each season in our dataset to now, and adjusted each player's salaries accordingly. 

add dataframes and graphs later on.

## Feature Engineering

People may think that if a player has ever played in a city that has huge market and fans, won an MVP award, or played in the national team in Olympics, then the player will be more likely to gain higher salary. Thus we added these features in our original dataframe.
add heads of datasets later on.

## Justification on model selection
- We can tell that the `Salary` of NBA players has a roughly linear relationship with other numerical variables, thus, we would use `Linear Regression`. However, it is important to verify that degree 1 polynomial regression(Linear Regression) is indeed the best choice, so we would perform a `cross-validation` to see which degree works the best for us.
