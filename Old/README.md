##INTRODUCTION

This program performs a webscrape of college football data (FBS schools only) from http://www.sports-reference.com. The data is retrieved from the website are stored in an SQLite database, from which a sample analysis is performed. The purpose of this repository is educational. It provides useful, real-world examples of webscraping, simple database manipulation, and analysis of data using Python's Pandas library.

The data collected is for the past 10 years. 10 years is an arbitrary number, of course, and can be changed. The code does take some time to run (i.e. several hours). Each script is independent of the others. This allows you to populate whichever tables you want/need.

**Note:** Changes to a website to the website used are continuous, often, and unpredictable. These changes will create bugs with the scripts as they currently stand and potentially make new information available or previously displayed information unavailable.


##REQUIREMENTS

Python 3 is required, along with several libraries, all of which comes standard in Continuum's Anaconda Python distrbution (found here: https://www.continuum.io/downloads).

Jupyter Notebook is required to use the SampleAnalysisUsingPython&JupyterNotebook.ipynb. This package also comes standard in Continuum's Anaconda Python distributon, or it can be downloaded separately (found here: https://jupyter.org/). 

SQLite DB Browser is recommended, though not required (found here: http://sqlitebrowser.org/). All the data can be accessed using Python. However, using SQLite DB Browser may make some manipulations easier. Also, at any point during the scrape, you can open up the DB Browser and view the data which has been written.


##INSTALLATION

Once the requirements described above have been met the available scripts can be run in an environment of your choosing (e.g. Spyder, contained in the Anaconda Python distribution) without modification. Each script creates one or more tables in an SQLite database. Each table is described below. All tables and scripts are independent of each other. It is not necessary to run each script. Please take a moment to read about the available outputs and the scripts which create them below.

**Running all scripts may take several hours to complete.**


##EXPLANATION OF TABLE OUTPUTS IN SQLITE

Each Python scripts creates one or more tables in SQLite. Below identifies potential tables which can be created, what information and columns that table contains, and which script is responsible for populating it.

###Coach Table
This table displays each school's head coach by year. If the coach was not retained throughout the entire season, that given year will be duplicated and each coach, including interim head coaches, will have a separate row.

**Columns**: SchoolName, Year, Coach

**Source Script:** PushToTeamSplits.py

###Conference Table
This table displays each school's conference by year. Schools do not change conferencse mid-season, therefore no school has multiple conference values for a given year. 

**Columns**: SchoolName, Year, Conference

**Source Script:** PushToTeamSplits.py

###GameResults Table
This table displayes individual game statistics by opponent. If the opponent was a non-FBS team, no statistics are provided (this data is unavailable on http://www.sports-reference.com).

**Columns**: SchoolName, Year, GameDate, Opponent, HomeOrAway, TotalYards, TotalRushes, RushingYards, RushingTDs, NumberOfPassingAtmpts, PassingCompletions, PassingYards, PassingTDs, PassingINTs, FirstDowns, NumberOfFumbles, LostFumbles, Turnovers, NumberOfPenalties, PenaltyYards, opponentTotalYards, opponentTotalRushes, opponentRushingYards, opponentRushingTDs,  opponentNumberOfPassingAtmpts, opponentPassingCompletions, opponentPassingYards, opponentPassingTDs, opponentPassingINTs, opponentFirstDowns, opponentNumberOfFumbles, opponentLostFumbles, opponentTurnovers, opponentNumberOfPenalties, opponentPenaltyYards

**Source Script**: PushToGameResults.py

###PlayerDefense Table
This table displays player statistics related to defense.

**Columns:** SchoolName, Year, PlayerName, SoloTackles, AssistedTackles, TotalTackles, TacklesForLoss, Sacks, Interceptions, PassesDefended, FumblesRecovered, ForcedFumbles

**Source Script**: PushToPlayers.py

###PlayerKickingPunting Table
This table displays player statistics related to kicking and punting.

**Columns:** SchoolName, Year, PlayerName, ExtraPointsMade, ExtraPointsAttempted, ExtraPointsPct, FieldGoalsMade, FieldGoalsAttempted, FieldGoalsPct, Punts, PuntsYds, PuntsAvgYds

**Source Script**: PushToPlayers.py

###PlayerKickPuntReturns Table
This table displays player statistics related to kick and punt returns.

**Columns:** SchoolName, Year, PlayerName, KickoffReturns, KickoffReturnYds, KickoffReturnAvgYds, KickoffReturnTDs, PuntReturns, PuntReturnYds, PuntReturnAvgYds, PuntReturnTDs

**Source Script**: PushToPlayers.py

###PlayerPassing Table
This table displays player statistics related to passing.

**Columns:** SchoolName, Year, PlayerName, PassingCompletions, PassingAtmpts, PassingCompletePct, PassingTotYds, PassingYardsPerAttmpt, PassingTDs, PassingINTs, PasserRating

**Source Script**: PushToPlayers.py

###PlayerRushingReceiving Table
This table displays player statistics related to rushing and receiving.

**Columns:** SchoolName, Year, PlayerName, RushingAtmpts, RushingTotYds, RushingAvgYds, RushingTDs, Receptions, ReceivingTotYds, ReceivingAvgYds, ReceivingTDs

**Source Script**: PushToPlayers.py

###SeasonResults Table
This table displays the outcome of each game a school played in a given year, and a running view of the team's win/loss "streak".

**Columns**: SchoolName, Year, GameOfYear, Date, Time, Day, HomeOrAway, Opponent, Outcome, PointsFor, PointsAgainst, Wins, Losses, Streak

**Source Script:** PushToSeasonResults.py

###TeamSplits Table
This table displays statistics of each school's performance in a given year broken down first by Offense and Defense, then by Home, Road, Win, and Loss. This table is currently not populating data in the Wins and Losses columns for games played at a Neutral site.

**Columns:** SchoolName, Year, Side, Value, GamesPlayed, Wins, Losses, PassCompletions, PassAtmpts, PassCompletionPct, TotalPassYds, PassTDs, TotalPlays, TotalYds, AvgYdsPerPlay, FirstDownsByPass, FirstDownsByRush, FirstDownsByPenalty, TotalFirstDowns, PenaltiesNumber, PenaltiesYds, TurnoversByFumble, TurnoversByInt, TotalTurnovers 

**Source Script:** PushToTeamSplits.py

###TeamStatistics Table
This table displays statistics of each school's performance in a given year broken out by Offense and Defense. Compared to the TeamSplits table, this table provides a higher level of aggregation.

**Columns**: SchoolName, Year, Side, GamesPlayed, PassingCompletions, PassingAtmpts, PassingCompletePct, PassingTotYds,PassingTDs, RushingAtmpts, RushingTotYds, RushingAvgYds, RushingTDs, TotalOffensePlays, TotalOffenseTotYds, TotalOffenseAvgYds, FirstDownsByPassing, FirstDownsByRushing, FirstDownsByPenalty, FirstDownsTot, PenaltiesTot, PenaltiesYds, TurnoversByFumble, TurnoversByInt, TurnoversTot

**Source Script:** PushToTeamYearStats.py


##OTHER FILES

* CFBData.db: sample database which shows the tables and data to be expected.
* SampleAnalysisUsingPython&JupyterNotebook.ipynb: example code constructed in Jupyter Notebook which can used as the jumping off point for analysis of the data


##KNOWN BUGS / TODO

* TeamSplits table is currently not populating Wins and Losses columns for games played at a Neutral site.
