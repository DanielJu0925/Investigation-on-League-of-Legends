# Blue side Winrates in Tier-one Professional League

by Bofu Zou and Zhuoxuan Ju

## Introduction

This original dataset records the League of Legends 2022 global professional league data. These professional leagues, especially the tier-one professional league, represent League of Legends matchups at the highest skill levels in the fairest of circumstances. However, we found that the two sides (blue and red) of a game had different win rates under different leagues in tier-one league.
    For instance, the PCS league has an overall 60% winrate on the blue side. The question is: Is there a relationship between the different leagues and the winrates of the two sides?
We are interested in the tier 1 leagues'winning rate from the dataset. The reason we choose this aspect is because that question comes from the first season of League of Legneds games, and it is something normal players can feel relate with. We believe that we are not the only one who interested in this question. By analyzing this dataset, we can have an overall better understanding of competitive games, which will benefit us when we watch pro games and when we playgames outselves (make yourself pro!)

This dataset originally has 149232 rows and 123 columns. 
The relevant columns are listed below:

- gameid: This is the id for each match.
- datacompleteness: This column is a categorical column with whether the data is completely reported
- league: the different leagues from around the world
- side: the side that each group is assigned, blue or red
- playername: the player's id and the team's id
- result: whether this team is win or lose
- towers: the number of towers that each team destoried
- team kpm: this is for each team's kill per minute in each game
- totalgold: this is the gold(money) that each play and team earned in each game
- kills: it is the number of kills for each player




## Cleaning and EDA

### Data Cleaning

As we download our dataset from the website, we saved and loaded it in our notebook as csv form. After the loading process, we discovered that this dataframe had about 140000 rows and 123 columns. Inside the dataframe, we first discovered that the date column is still in a string type, and thus we convert it into datetime format. Also, we noticed that the playername column had a unusual name called unknown player. Since it is a game match data report, the name should be recorded for every player. So we consider it as missing value. In addition, we converted the columns contain 0 and 1 to boolean columns which are better for us to have a clear view for our later investigation. After that, we droped the some not related columns in order to make the dataframe clean to use. Looking into the tier 1 leagues' team data in the League of Legends matchs is what our focuing are. So we filter out the other leagues and the players information, only keeping the tier 1 league's information in our dataset. 

The head of the cleaned dataframe is from the code below:
    `print(tier1_team.head().to_markdown(index=False))`

| gameid           | datacompleteness   | url                                         | league   |   year | split   |   playoffs | date                |   game |   patch |   participantid | side   | position   |   playername |   playerid | teamname           | teamid                                  |   champion | ban1     | ban2         | ban3      | ban4     | ban5    |   gamelength | result   |   kills |   deaths |   assists |   teamkills |   teamdeaths |   doublekills |   triplekills |   quadrakills |   pentakills |   firstblood |   firstbloodkill |   firstbloodassist |   firstbloodvictim |   team kpm |   ckpm |   firstdragon |   dragons |   opp_dragons |   elementaldrakes |   opp_elementaldrakes |   infernals |   mountains |   clouds |   oceans |   chemtechs |   hextechs |   dragons (type unknown) |   elders |   opp_elders |   firstherald |   heralds |   opp_heralds |   firstbaron |   barons |   opp_barons |   firsttower |   towers |   opp_towers |   firstmidtower |   firsttothreetowers |   turretplates |   opp_turretplates |   inhibitors |   opp_inhibitors |   damagetochampions |     dpm |   damageshare |   damagetakenperminute |   damagemitigatedperminute |   wardsplaced |    wpm |   wardskilled |   wcpm |   controlwardsbought |   visionscore |   vspm |   totalgold |   earnedgold |   earned gpm |   earnedgoldshare |   goldspent |        gspd |   total cs |   minionkills |   monsterkills |   monsterkillsownjungle |   monsterkillsenemyjungle | result_str   |
|:-----------------|:-------------------|:--------------------------------------------|:---------|-------:|:--------|-----------:|:--------------------|-------:|--------:|----------------:|:-------|:-----------|-------------:|-----------:|:-------------------|:----------------------------------------|-----------:|:---------|:-------------|:----------|:---------|:--------|-------------:|:---------|--------:|---------:|----------:|------------:|-------------:|--------------:|--------------:|--------------:|-------------:|-------------:|-----------------:|-------------------:|-------------------:|-----------:|-------:|--------------:|----------:|--------------:|------------------:|----------------------:|------------:|------------:|---------:|---------:|------------:|-----------:|-------------------------:|---------:|-------------:|--------------:|----------:|--------------:|-------------:|---------:|-------------:|-------------:|---------:|-------------:|----------------:|---------------------:|---------------:|-------------------:|-------------:|-----------------:|--------------------:|--------:|--------------:|-----------------------:|---------------------------:|--------------:|-------:|--------------:|-------:|---------------------:|--------------:|-------:|------------:|-------------:|-------------:|------------------:|------------:|------------:|-----------:|--------------:|---------------:|------------------------:|--------------------------:|:-------------|
| 8401-8401_game_1 | partial            | https://lpl.qq.com/es/stats.shtml?bmid=8401 | LPL      |   2022 | Spring  |          0 | 2022-01-10 09:24:26 |      1 |   12.01 |             100 | Blue   | team       |          nan |        nan | Oh My God          | oe:team:f4c4528c6981e104a11ea7548630c23 |        nan | Renekton | Lee Sin      | Caitlyn   | Jayce    | Camille |         1365 | True     |      13 |        6 |        35 |          13 |            6 |           nan |           nan |           nan |          nan |            0 |              nan |                nan |                nan |     0.5714 | 0.8352 |           nan |         2 |             1 |               nan |                   nan |         nan |         nan |      nan |      nan |         nan |        nan |                        2 |      nan |          nan |           nan |       nan |           nan |          nan |        1 |            0 |          nan |        8 |            3 |             nan |                  nan |            nan |                nan |            1 |                0 |               40086 | 1762.02 |           nan |                2263.25 |                        nan |            79 | 3.4725 |            33 | 1.4505 |                   32 |           162 | 7.1209 |       45468 |        30167 |      1326.02 |               nan |       36908 | -0.00586225 |        nan |           nan |            172 |                      98 |                        18 | win          |
| 8401-8401_game_1 | partial            | https://lpl.qq.com/es/stats.shtml?bmid=8401 | LPL      |   2022 | Spring  |          0 | 2022-01-10 09:24:26 |      1 |   12.01 |             200 | Red    | team       |          nan |        nan | ThunderTalk Gaming | oe:team:df80f468a3f9a722df056fe9104f052 |        nan | Samira   | Diana        | Akali     | LeBlanc  | Rumble  |         1365 | False    |       6 |       13 |        11 |           6 |           13 |           nan |           nan |           nan |          nan |            0 |              nan |                nan |                nan |     0.2637 | 0.8352 |           nan |         1 |             2 |               nan |                   nan |         nan |         nan |      nan |      nan |         nan |        nan |                        1 |      nan |          nan |           nan |       nan |           nan |          nan |        0 |            1 |          nan |        3 |            8 |             nan |                  nan |            nan |                nan |            0 |                1 |               30417 | 1337.01 |           nan |                2541.89 |                        nan |            64 | 2.8132 |            34 | 1.4945 |                   26 |           155 | 6.8132 |       38538 |        23237 |      1021.41 |               nan |       37125 |  0.00586225 |        nan |           nan |            116 |                      94 |                         2 | lose         |
| 8401-8401_game_2 | partial            | https://lpl.qq.com/es/stats.shtml?bmid=8401 | LPL      |   2022 | Spring  |          0 | 2022-01-10 10:09:22 |      2 |   12.01 |             100 | Blue   | team       |          nan |        nan | Oh My God          | oe:team:f4c4528c6981e104a11ea7548630c23 |        nan | Renekton | Caitlyn      | Thresh    | Jayce    | Camille |         1444 | True     |      22 |        9 |        40 |          22 |            9 |           nan |           nan |           nan |          nan |            0 |              nan |                nan |                nan |     0.9141 | 1.2465 |           nan |         2 |             1 |               nan |                   nan |         nan |         nan |      nan |      nan |         nan |        nan |                        2 |      nan |          nan |           nan |       nan |           nan |          nan |        1 |            0 |          nan |        9 |            2 |             nan |                  nan |            nan |                nan |            1 |                0 |               59746 | 2482.52 |           nan |                3026.05 |                        nan |            67 | 2.7839 |            32 | 1.3296 |                   38 |           180 | 7.4792 |       54283 |        38176 |      1586.26 |               nan |       50858 |  0.298771   |        nan |           nan |            178 |                      88 |                        41 | win          |
| 8401-8401_game_2 | partial            | https://lpl.qq.com/es/stats.shtml?bmid=8401 | LPL      |   2022 | Spring  |          0 | 2022-01-10 10:09:22 |      2 |   12.01 |             200 | Red    | team       |          nan |        nan | ThunderTalk Gaming | oe:team:df80f468a3f9a722df056fe9104f052 |        nan | Samira   | Diana        | Jarvan IV | LeBlanc  | Akali   |         1444 | False    |       8 |       22 |        16 |           8 |           22 |           nan |           nan |           nan |          nan |            0 |              nan |                nan |                nan |     0.3324 | 1.2465 |           nan |         1 |             2 |               nan |                   nan |         nan |         nan |      nan |      nan |         nan |        nan |                        1 |      nan |          nan |           nan |       nan |           nan |          nan |        0 |            1 |          nan |        2 |            9 |             nan |                  nan |            nan |                nan |            0 |                1 |               35129 | 1459.65 |           nan |                3107.16 |                        nan |            82 | 3.4072 |            21 | 0.8726 |                   29 |           159 | 6.6066 |       41155 |        25048 |      1040.78 |               nan |       37638 | -0.298771   |        nan |           nan |            115 |                      88 |                         0 | lose         |
| 8402-8402_game_1 | partial            | https://lpl.qq.com/es/stats.shtml?bmid=8402 | LPL      |   2022 | Spring  |          0 | 2022-01-10 11:26:11 |      1 |   12.01 |             100 | Blue   | team       |          nan |        nan | FunPlus Phoenix    | oe:team:33d17f3717f58e12a3da80b377221fb |        nan | LeBlanc  | Twisted Fate | Aphelios  | Nautilus | Leona   |         1893 | True     |      12 |        8 |        25 |          12 |            8 |           nan |           nan |           nan |          nan |            0 |              nan |                nan |                nan |     0.3803 | 0.6339 |           nan |         4 |             1 |               nan |                   nan |         nan |         nan |      nan |      nan |         nan |        nan |                        4 |      nan |          nan |           nan |       nan |           nan |          nan |        2 |            0 |          nan |       10 |            3 |             nan |                  nan |            nan |                nan |            3 |                0 |               54264 | 1719.94 |           nan |                2528.49 |                        nan |           100 | 3.1696 |            59 | 1.87   |                   41 |           274 | 8.6846 |       64011 |        43324 |      1373.19 |               nan |       58619 |  0.149322   |        nan |           nan |            264 |                     162 |                        34 | win          |


### Univariate Analysis

<iframe src="assets/league_distribution.html" width=800 height=600 frameBorder=0></iframe>

In this pie chart, we are looking for which the tier 1 league has the most number of match played. It seems like LPL has the most game of matches played in 2022, and LCK has the second most game played in 2022. We can analysis further on the popularity of League of Legends in differet countries.


### Bivariate Analysis

<iframe src="assets/tkpm_win_lose.html" width=800 height=600 frameBorder=0></iframe>

For this bar chart, we are interested in the game result and the team kill per minute in tier 1 leagues. In order to have a better view of the data and distribution, we have two groups. The win groups seem to have a higher team kill per minute, and the lose group have a lower team kill per minute. From the plot, we can know team kill per minute is indeed one important element to determine the result of that match.

<iframe src="assets/tkpm_league.html" width=800 height=600 frameBorder=0></iframe>

To further explore the relationship of team kill per minute, we decide to see how it can differ in different leagues. This bar chart is looking at the team kill per minute in different tier 1 leagues. We can have a clear view of the differences in team kill per minute in different leagues. Specifically, LPL has the highest team kill per minute, and we can know their matches contain more fights comparing to other leagues.


### Interesting Aggregates

The pivot table will present from the code:
    `print(pivot_1.to_markdown())`

| league   |    lose |     win |
|:---------|--------:|--------:|
| CBLOL    | 54071.8 | 63380.4 |
| LCK      | 55021   | 64591.8 |
| LCS      | 54065.9 | 63549.6 |
| LEC      | 54671.5 | 64256.1 |
| LJL      | 51361.1 | 62458.3 |
| LLA      | 54236   | 63872.9 |
| LPL      | 52247.9 | 62091.7 |
| PCS      | 49391.1 | 60657.5 |
| VCS      | 50856.2 | 60940.1 |

This pivot table explore the relationship between mean of total gold received with the game result of tier 1 leagues. As we can see, the winning games' mean of total gold received is way higher than the losing column. From this pivot table, we can know the gold received during the game is one essential component to win the match.

## Assessment of Missingness

### NMAR Analysis
We noticed that there is missingness in the "ban5" column. There are 5 columns ("ban1" to "ban5") about ban stage during a competitive games. 
Each team can ban five champions during the ban-pick stage. However, there is no hard rules that require teams to choose no less than five champions during the ban stage.
Thus, it is reasonable and possible for a team to pick less than five champions. 
If a team only banned four or fewer champions, the "ban5" column could be a null value since there is not data to fill out for the fifth ban.
Therefore, the missingness of the "ban5" column is NMAR, the missingness of the values depends on the values themselves.
If there is additional data like one column that could tell us the coach of a team, the "ban5" column might be a MAR since some coaches have the habit 
of banning less champions. And we can find that the missingness of "ban5" depends on the coach column instead of the value themselves.

### Missingness Dependency

#### Dependent Relationship

For the dependent column part, we choose the columns `monsterkillsownjungle` and `league`. From the permutation test, the null hypothesis is that the missingness of the column `monsterkillsownjungle` is independent from the column `league`, and the alternative hypothesis is that the missingness of column `monsterkillsownjungle` is dependent on the column `league`.

Since column `league` is a categorical, we choose total variance distance as the test statistic. The observed statistic we found is 0.946987951807229. After 500 times of permutations, we have the tvd with size of 500. The p-value from the test statistic is 0.0. So we can conclude that we reject the null hypothesis and favors in alternative hypothesis. Therefore, the missingness of column `monsterkillsownjungle` is denpendent on the column `league`.

<iframe src="assets/missing_fig.html" width=800 height=600 frameBorder=0></iframe>

#### Independent Relationship

For the independent column part, we choose the columns `monsterkillsownjungle` and `kills`. From the permutation test, the null hypothesis is that the missingness of the column `monsterkillsownjungle` is independent from the column `kills`, and the alternative hypothesis is that they are dependent.

The column `kills` is a numerical. Therefore, we use absolute difference in mean as test statistic. The observed value from our test statistic is 0.15273388711023372, and we perform 500 times of our permutation test. The p-value from our permutation test is 0.43. Thus, we fail to reject the null hypythesis. So we can state the missingness of column `monsterkillsownjungle` is independent on the column `kills`.

<iframe src="assets/independent_fig.html" width=800 height=600 frameBorder=0></iframe>

## Hypothesis Testing

The question we raised at the beginning is that is there a relationship between the different leagues and the winrates of the two sides?
Since we have found that several leagues have a abnormally higher winrates on the blue side, especially PCS league, we are going to 
perform a hypothesis test to find if the PCS blue side winrate is due to random chance (under the populaton distribution)


Null hypothesis: Blue side winrate and leauges in the tie-one professional leagues are not related: 
        the high winrate of blue side in PCS league is due to random chance.
Alternative hypothesis: Blue side winrate and tie-one professional leagues are related: 
        the high winrate of blue side in PCS league is not due to random chance.

        
We will repeatedly sample (without replacement) the number of PCS games (271) from the population and 
compute the blue side winrates for 100000 times. The blueside winrates would be our test statistic, 
and the significance level is set to 5% which is a commonly used level.


After the computation of the test statistic, the p-value we got from comparing the test-statistic and 
observed statistic is around 0.0039 to 0.0048, which is lower than the significance level of 0.05. 
Thus, we are able to reject the null hypothesis. However, we cannot say that there is a relationship 
between the blue side winrates and leagues since it is statistical test instead of randomized controlled trials.
It could still be a strong evidence if we try to solve the main question further in the future.
The leagues where the games are held still have a great probabiltiy to effect the winrates of two sides, 
and the PCS league in the hypothesis test is a great example to examine that
