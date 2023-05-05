---
summary: "**Request:** I am an instructor in a newly opened tennis club LUNA.
  Many students come to learn some basic tennis skills and desire to have
  personalized training. Professional tennis matches will be good examples for
  my students to understand them. So, could you help me by providing some
  practical suggestions to my students?"
authors:
  - admin
lastMod: 2019-09-05T00:00:00.000Z
title: Luna Tennis Club
subtitle: ""
date: 2019-02-05T00:00:00.000Z
tags: []
categories: []
projects: []
image:
  caption: ""
  focal_point: top
  filename: ""
---
![](luna.png)

## Request

```none
Hello Database Team member,

I am an instructor in a newly opened tennis club LUNA. Many students come to learn some basic tennis skills and desire to have personalized training. Professional tennis matches will be good examples for my students to understand them. So, could you help me by providing some practical suggestions to my students?

The questions will cover basic information about the match, the court, and some tennis skills. Hope the tennis terms will not make it difficult for you to understand. It is fine to use the public data collected between 2018 and 2022.

Basic Information
1.	Will age be a big concern to the tennis player? Please analyze whether the older player will be likely to lose the game as well as the age distribution of the winner and the loser. 
2.	How long will each game take on average for different tourney levels and surfaces (i.e., clay, grass, and hard)? The expected time will help my students to wisely allocate their physical energy.
3.	Is there a clear relationship between the surface and the number of aces and double faults in one game? Please analyze the average aces and double faults in each kind of surface.

Tennis Skills
4.	Would you like to find the top 5 tennis players who finish the match faster with a winning rate over 0.8 in best-three-out-of-five matches? These players’ skills may be very valuable for my students.
5.	Some of my students feel panic when facing break points. Would you like to find the top 10 players who save the most break points they have faced and rank top 50 in 2022-09-12? Please order them by the descending order of the ratio of the break points saved to the break points faced, and then by the ascending order of average break points faced and player id.
6.	Some young students want to learn ace because it is so cool! Could you find the top 10 players who have the average ace but the lowest double faults in each match? And I hope these players have ranked in the top 100 once after June 2022.

Tennis Player
7.	Novak Djokovic is my favorite tennis player. Are there any changes in him in recent years like the aces, double faults, or the duration of the match? Please separately analyze the game he won and didn’t win and the type of match (with 3 or 5 sets at maximum).
8.	Can you find all the matches between Roger Federer and Rafael Nadal between 2018 and 2022?

Please provide all the queries and the answer. Hope it will not be so difficult. Thank you for helping me and my students in advance.

Thanks,
Andrew
```

## Reply

It’s my great pleasure to help you and your students in tennis. Actually, I sometimes play tennis in my spare time. I am also curious about the questions you mention. I use the data from ATP players from 2018 to 2022 and obtain the following results.

#### **Basic Information**

**1. Will age be a big concern to the tennis player? Please analyze whether the older player will be likely to lose the game as well as the age distribution of the winner and the loser.**\
I first use the query to find the frequency of the match that the older wins the younger

```sql
select avg(winner_age > loser_age) as avg_old_win from matches;
```

We can find that the frequency of the match where the older wins is roughly closer to 0.48. So, it is hard to say the age will significantly influence the results.\
Plus, I also aggregate and get the following distribution

```sql
select w.age, win_cnt, lose_cnt
from (select round(winner_age) as age, count(1) as win_cnt from matches group by round(winner_age)) w
join (select round(loser_age) as age, count(1) as lose_cnt from matches group by round(loser_age)) l
on w.age = l.age order by w.age;
```

So, we can find the distribution is almost similar.

**2. How long will each game take on average for different tourney levels and surfaces (i.e., clay, grass, and hard)?**\
I use the following query

```sql
select description, surface, avg_time from (
	select surface_id, tourney_level, avg(minutes / (w_game + l_game)) as avg_time from matches m
	join tourney t on m.tourney_id = t.id group by surface_id, tourney_level
) a
join surface s on a.surface_id = s.id
join level l on a.tourney_level = l.id
order by description, surface;
```

So, it is interesting to find that the average time per game is around 4.3 minutes. The average time in clay is the largest, while that in the grass is the shortest. Perhaps, it is because the bouncing speed of ball in the grass is fast, while the ball speed in the clay is slow. However, it is not clear that the tourney levels will affect the average time.

**3. Analyze the average aces and double faults in each kind of surface**\
I use the query and obtain the following

```sql
select  surface, avg(d1.ace + d2.ace) as avg_ace, avg(d1.df + d2.df) as avg_df from matches m
join (select match_id, player_id, ace, df from match_details) d1 on m.id = d1.match_id and m.winner_id = d1.player_id
join (select match_id, player_id, ace, df from match_details) d2 on m.id = d2.match_id and m.loser_id = d2.player_id
join tourney t on m.tourney_id = t.id
join level l on t.tourney_level = l.id
join surface s on t.surface_id = s.id
group by surface;
```

We can clearly find that there are less aces and double faults in clay. So, I may recommend the player good at serving not to play on the clay.

#### **Tennis Skills**

**4. Would you like to find the top 5 tennis players who finish the match faster with a winning rate over 0.8 in best-three-out-of-five matches?**\
I use the query and obtain the following

```sql
select player_id, min(name_first) as firstname, min(name_last) as lastname, avg(minutes) as avg_min,
    avg(IF(m.winner_id = d.player_id, 1, 0)) as avg_win from match_details d
join  matches m on d.match_id = m.id
join players p on d.player_id = p.id
where best_of = 5
group by player_id
having avg_win > 0.8
order by avg_min limit 5;
```

I think the results meet the expectation. We find many famous players like Roger Federer, Novak Djokovic, and Rafael Nadal. Hope this results will help your students.

**5. Would you like to find the top 10 players who save the most break points they have faced and rank top 50 in 2022-09-12? Please order them by the descending order of the ratio of the break points saved to the break points faced, and then by the ascending order of average break points faced and player id.**\
I use the query and find that

```sql
select player_id, min(name_first) as firstname, min(name_last) as lastname,
       avg(bpFaced) as avg_bpFaced, avg(bpSaved/bpFaced) as avg_saveRate from (
	select player_id, bpFaced, bpSaved from match_details d
	join (select id, winner_id from matches) m on d.match_id = m.id
	where player_id in (select player_id from rankings where ranking_date = "2022-09-12" and ranking <= 50)
) as dmr
join players p on dmr.player_id = p.id
group by player_id
order by avg_saveRate desc, avg_bpFaced, player_id
limit 10;
```

**6. Could you find the top 10 players who have the average ace but the lowest double faults in each match? And I hope these players have ranked in the top 100 once after June 2022.**\
I use the query and obtain that

```sql
select player_id, min(name_first) as firstname, min(name_last) as lastname,
       avg(ace) as avg_ace, avg(df) as avg_df from match_details d
join (select id, tourney_id from matches) m on m.id = d.match_id
join tourney t on t.id = m.tourney_id
join players p on d.player_id = p.id
where player_id in (
	select distinct player_id from rankings
	where year(ranking_date) = 2022 and month(ranking_date) >= 6 and ranking <= 100
)
group by player_id
order by avg_ace desc, avg_df
limit 10;
```

Interestingly, I find some names that have appeared in the previous question like John Isner, Reilly Opelka, and Nick Kyrgios. There may be some correlation between these statistics.

#### **Tennis Player**

**7. Are there any changes of Novak Djokovic in recent years like the aces, double faults, or the duration of the match? Please separately analyze the game he won and didn’t win and the type of match (with 3 or 5 sets at maximum).**\
I use the following query and find that

```sql
select year(m.tourney_date) as year, best_of, m.winner_id = md.player_id as is_win,
       count(*) as cnt, avg(ace) as avg_ace, avg(df) as avg_df, avg(minutes) as avg_min from matches m
join (
    select * from match_details
    where player_id in (select id from players where name_first = "Novak" and name_last = "Djokovic")
) md on m.id = md.match_id
group by year, best_of, is_win
order by year, best_of, is_win;
```

**8. Can you find all the matches between Roger Federer and Rafael Nadal between 2018 and 2022?**\
I use the following query and obtain that

```sql
select tourney_date, best_of, (m.winner_id = d1.player_id) as RF_win,
       (m.winner_id = d2.player_id) as RN_win,
       IF(m.winner_id = d1.player_id, w_game, l_game) as RF_game,
       IF(m.winner_id = d2.player_id, w_game, l_game) as RN_game
       from matches m
join (
	select * from match_details
    where player_id in (select id from players where name_first = "Roger" and name_last = "Federer")
) d1 on d1.match_id = m.id
join (
	select * from match_details
    where player_id in (select id from players where name_first = "Rafael" and name_last = "Nadal")
) d2 on d2.match_id = m.id
order by tourney_date;
```

There are only two recorded matches in the dataset. Hope this is helpful to you.

Thank you for letting me do this project! I have learned a lot about tennis and SQL from this project. Thank you again for trusting me! Hope those results are useful for you and your students.