# "Title of project"

by Bofu Zou and Zhuoxuan Ju

## Introduction


## Cleaning and EDA

### Data Cleaning

As we download our dataset from the website, we saved and loaded it in our notebook as csv form. After the loading process, we discovered that this dataframe had about 140000 rows and 123 columns. Inside the dataframe, we first discovered that the date column is still in a string type, and thus we convert it into datetime format. Also, we noticed that the playername column had a unusual name called unknown player. Since it is a game match data report, the name should be recorded for every player. So we consider it as missing value. In addition, we converted the columns contain 0 and 1 to boolean columns which are better for us to have a clear view for our later investigation. Looking into the tier 1 leagues' team data in the League of Legends matchs is what our focuing are. So we filter out the other leagues and the players information, only keeping the tier 1 league's information in our dataset. 

## Assessment of Missingness


## Hypothesis Testing