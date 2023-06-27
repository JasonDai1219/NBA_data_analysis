# NBA_data_analysis
** this project mainly focues on making a basic model to predict NBA players' `Salaries` using their stats and experiences.**

## Web Scraping of NBA players' salaries data.
- specific details are in this jupyter notebook : https://github.com/JasonDai1219/NBA_data_analysis/blob/main/NBA%20Data%20Web%20Scraping.ipynb

## Data Exploration
- we merge together the `players_stats` and `salaries` data frames together to let each player gets their corresponding salary in each season.
- As we do not have missing data in these datasets, so we do not need to work on data cleaning part that much, and we only need to make the salary variable in string format through `merged['Salary'] = merged['Salary'].str.strip('$').str.replace(',', '').astype('float')`.
- To also adjust the problem of inflation, we searched about the `cumulative inflation rate` from each season in our dataset to now, and adjusted each player's salaries accordingly. 

add dataframes and graphs later on.

## Feature Engineering

People may think that if a player has ever played in a city that has huge market and fans, won an MVP award, or played in the national team in Olympics, then the player will be more likely to gain higher salary. Thus we added these features in our original dataframe.
1. `popular_teams = [
    "CHI",  # Chicago Bulls
    "DAL",  # Dallas Mavericks
    "DET",  # Detroit Pistons
    "GSW",  # Golden State Warriors
    "HOU",  # Houston Rockets
    "LAC",  # Los Angeles Clippers
    "LAL",  # Los Angeles Lakers
    "TOR",  # Toronto Raptors
    "NYK",  # New York Knicks
    "BOS",  # Boston Celtics
    merged_inflated['Played_In_Popular_Teams'] = merged_inflated['TEAM'].apply(lambda x : x in popular_teams)
]`

2. `mvp_winners = [
    "Bob Pettit",
    "Bob Pettit",
    "Bill Russell",
    "Bob Pettit",
    "Wilt Chamberlain",
    "Wilt Chamberlain",
    "Bill Russell",
    "Bill Russell",
    "Bill Russell",
    "Bill Russell",
    "Wilt Chamberlain",
    "Wilt Chamberlain",
    "Wilt Chamberlain",
    "Wes Unseld",
    "Willis Reed",
    "Kareem Abdul-Jabbar",
    "Kareem Abdul-Jabbar",
    "Dave Cowens",
    "Kareem Abdul-Jabbar",
    "Bob McAdoo",
    "Kareem Abdul-Jabbar",
    "Kareem Abdul-Jabbar",
    "Bill Walton",
    "Moses Malone",
    "Kareem Abdul-Jabbar",
    "Julius Erving",
    "Moses Malone",
    "Moses Malone",
    "Larry Bird",
    "Larry Bird",
    "Larry Bird",
    "Magic Johnson",
    "Michael Jordan",
    "Magic Johnson",
    "Magic Johnson",
    "Magic Johnson",
    "Michael Jordan",
    "Charles Barkley",
    "Hakeem Olajuwon",
    "David Robinson",
    "Michael Jordan",
    "Karl Malone",
    "Michael Jordan",
    "Karl Malone",
    "Shaquille O'Neal",
    "Allen Iverson",
    "Tim Duncan",
    "Tim Duncan",
    "Kevin Garnett",
    "Steve Nash",
    "Steve Nash",
    "Dirk Nowitzki",
    "Kobe Bryant",
    "LeBron James",
    "LeBron James",
    "Derrick Rose",
    "LeBron James",
    "LeBron James",
    "Kevin Durant",
    "Stephen Curry",
    "Stephen Curry",
    "Russell Westbrook",
    "James Harden",
    "Giannis Antetokounmpo",
    "Giannis Antetokounmpo",
    "Nikola Jokić",
    "Nikola Jokić",
    "Joel Embiid"
]
merged_inflated['Won_MVP_award'] = merged_inflated['PLAYER'].apply(lambda x : x in mvp_winners)
`

3. `Olympics_nba_players = [
    "Michael Jordan",
    "Magic Johnson",
    "Larry Bird",
    "Charles Barkley",
    "Karl Malone",
    "Scottie Pippen",
    "John Stockton",
    "David Robinson",
    "Patrick Ewing",
    "Clyde Drexler",
    "Chris Mullin",
    "Christian Laettner",
    "Shaquille O'Neal",
    "Hakeem Olajuwon",
    "Grant Hill",
    "Gary Payton",
    "Reggie Miller",
    "Alonzo Mourning",
    "Vin Baker",
    "Ray Allen",
    "Tim Duncan",
    "Allan Houston",
    "Steve Smith",
    "Kevin Garnett",
    "Jason Kidd",
    "Vince Carter",
    "Antonio McDyess",
    "Gary Trent",
    "Jermaine O'Neal",
    "Richard Jefferson",
    "Stephon Marbury",
    "Lamar Odom",
    "Emeka Okafor",
    "Amare Stoudemire",
    "Shawn Marion",
    "Carlos Boozer",
    "LeBron James",
    "Dwyane Wade",
    "Carmelo Anthony",
    "Chris Bosh",
    "Dwight Howard",
    "Chris Paul",
    "Deron Williams",
    "Jason Kidd",
    "Kobe Bryant",
    "Tayshaun Prince",
    "Michael Redd",
    "Carlos Boozer",
    "Chris Bosh",
    "Dwight Howard",
    "LeBron James",
    "Antawn Jamison",
    "Joe Johnson",
    "Jason Kidd",
    "Chris Paul",
    "Tayshaun Prince",
    "Michael Redd",
    "Dwyane Wade",
    "Deron Williams",
    "Kobe Bryant",
    "Carmelo Anthony",
    "Tyson Chandler",
    "Kevin Durant",
    "James Harden",
    "Andre Iguodala",
    "LeBron James",
    "Kevin Love",
    "Chris Paul",
    "Russell Westbrook",
    "Anthony Davis",
    "Blake Griffin",
    "Andre Drummond",
    "DeMarcus Cousins",
    "DeMar DeRozan",
    "Kyrie Irving",
    "Klay Thompson",
    "Draymond Green",
    "Paul George",
    "Jimmy Butler",
    "Kyle Lowry",
    "Harrison Barnes",
    "Kemba Walker",
    "Jayson Tatum",
    "Donovan Mitchell",
    "Bam Adebayo",
    "Zach LaVine",
    "Jrue Holiday",
    "Devin Booker",
    "Jerami Grant"
]
merged_inflated['Played_Olympics'] = merged_inflated['PLAYER'].apply(lambda x : x in Olympics_nba_players)
`