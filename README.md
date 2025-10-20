# NBA-Data-SQL-DAY-1
A small portfolio of my recent projects

I wanted to start some NBA projects since that is the field I'm hoping
to get into. I want to run data analysis for an NBA team.

Team Efficiency Report

-I learned how to use the RANK() function for the first time in this prompt. It
is really helpful to be able to rank values. Because then whoever sees the data knows who 
has been performing the best.

-This was the first task. Find out and give an efficiency rank to all the teams
in the league.

SELECT
    team,
    ROUND(AVG(field_goal_pct), 3) AS avg_fg_pct,
    ROUND(AVG(three_pt_pct), 3) AS avg_3pt_pct,
    SUM(points) AS total_points,
    RANK() OVER (ORDER BY AVG(field_goal_pct) DESC) AS efficiency_rank
FROM nba_sql_practice_dataset_clean
GROUP BY team;

Identify the most well-rounded players in the league.

-This prompt helped me understand how I can manipulate the numbers through SQL.
--(points + assists*1.5 + rebounds*1.2) AS contribution_score --
This line was especially helpful.

- I think this query would be helpful in the real world when teams
are at the trade deadline and they need to know out of all the freee agents, who they
should choose. This is a quick way to sort through a group of players and see who would
be the most valuable asset overall to add to the team.


SELECT
	player_name,
    team,
    season,
    points,
    assists,
    rebounds,
    (points + assists*1.5 + rebounds*1.2) AS contribution_score
FROM nba_sql_practice_dataset_clean
ORDER BY contribution_score DESC






Which players improved the most over time?

I thought this was great because the answer to question can
help teams keep track of someone they have been wanting to trade for or
this also works to evaluate player salaries. If a player is showing steady growth
a team might want to give them a raise.

SELECT
	player_name,
    MIN(season) AS first_season,
    MAX(season) AS last_season,
    ROUND(AVG(points), 2) AS avg_ppg,
    ROUND(MAX(points) - MIN(points), 2) AS point_growth,
    ROUND(MAX(assists) - MIN(assists), 2) AS asts_growth,
    ROUND(MAX(rebounds) - MIN(rebounds), 2) AS rbds_growth
FROM nba_sql_practice_dataset_clean
GROUP BY player_name
ORDER BY point_growth DESC







*All data used to practice these prompts are not accurate of real NBA players, but the SQL queries
are accurate steps in answering the prompts. My data set had players on all different teams
and it had players who never score in real life, averaging 30 ppg. So it was funny to see some of that
in the data.

