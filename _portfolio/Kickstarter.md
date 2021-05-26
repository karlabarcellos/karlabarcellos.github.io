![alttext](/images/purpledata.png)

# Kickstarter Challenge 
## **Overview**

The executive team of a small board game company has approached you seeking **assistance with setting up their Kickstarter campaign.** The team has decided that they will need a **minimum of $15,000 USD** to get this project off the ground. However, they have ambitions of expanding the business and would like **to maximize their funding.** They must decide how much money to ask for and determine how many backers they will need to succeed.

### Report

**Context to the problem**

We reviewed the data for 15,000 cases where 11,772 of them established their goals in US Dollars, with a minimum of $1 USD and a maximum of $100,000,000 USD. The average funding that they asked for was $72,361 USD. For the 4,369 successful cases, the average goal was $9,976 USD, when the average goal for the successful projects was $104,449 USD. Within the unsuccessful cases, specifically, the "Failed" cases had an average of $101,653 USD. We can see that there are more projects with goals closed to a round number closer to the thousands of dollars. 

[![alttext](/images/chart_2.png)

The campaign durations are about 1 and 92 days, with a general average of 34 days (32 days in successful cases and 35 in unsuccessful cases). The countries with most of the campaigns were the US, the UK, and Canada (78%, 8%. and 3% of the total cases, respectively). 

[![alttext](/images/chart_1.png)

To be able to analyze the pledged and goal per country and currency we would have to analyze the currencies in a single exchange rate, in this case, convert all the currencies to dollars. However, for a matter of time, we will analyze only the campaigns reported in dollars, in this case, it only applies to the United States and the United Kingdom. For all the campaigns, the average goal was $9,638 USD while the average goal was $69,386 USD. **In the successful campaigns, the average goal was smaller than the pledged, $9,976 USD average goal while $23,117 USD pledged.** 

On the other hand, unsuccessful campaigns asked for an average goal of $104,449 USD, having an average pledged of $1, 683 USD. 

The number of backers that support this kind of campaign is wide, it starts in only 1 and finishes with 105,857 supporters. Of the total of successful cases, 39% of them had more than 100 backers. This means that, of a total of 4,365 campaigns, 1,702 had more than 100 supporters. While the failed and canceled had mostly less than 10 backers (82% of the canceled and 85% of the failed campaigns). 

[![alttext](/images/chart_5.png)

Also, there are 15 different categories. In general, the top three categories with the most backers are first place Film&Video with 2,158 cases, Music with 1,783 cases, and Publishing with 1,291 cases. While in the bottom three are the categories Journalism (94 campaigns), Dance (102 campaigns), and Crafts (271 campaigns). 

The average length of their campaigns was 36 days for the first two places and 34 days for the third place. The average length for the bottom was 36, 33, and 31 days, respectively. 

The top three that raised the most money in the successful campaigns calculated by average pledged were Technology, Games, and Design. While the bottom three were Theater, Crafts, and Dance. The differences between the top and bottom represent the trends in the support for the development of new technologies and entertainment sources such as in games and design. I think that these categories have fewer backers than the top but these backers consider a big amount of money, especially because of their technological requirement that usually needs more funding.

Looking in the general games, they have an average length of 30 days, establishing an average goal of $13,893 USD, with an average pledge of $60,950 USD, this means an average gain of $47,057 USD. We need to consider this number carefully because can be some outliers that higher than the average expected gain. Analyzing the board games, that are part of the subcategory of Tabletop Games, they have an average length of 30 days as well, and an average goal of $10,853 USD, an average pledge of $67,519 USD, with an average gain of $56,666 USD. We can observe how board games established a smaller goal and had a higher pledge than the general games. Also, the board games have a higher number of backers, on average they had 902 in the period analyzed.  

[![alttext](/images/chart_4.png)

The most successful board game company was "Gloomhaven (Second Printing)". It raised $3,999,795 USD in 2017, after 28 days and the support of  40,642 backers. Their goal was only $100,000 USD. The second one was Ghostbusters™: The Board Game, and the third one Shadows of Brimstone. It is important to mention that fourth place was Robot Turtles: The Board Game for Little Programmers. 

[![alttext](/images/chart_3.png)

Finally, in terms of countries, the most successful campaigns in terms of the number of campaigns backed were the US with 4, 365 successful campaigns, then 1 with 847, and then 3 with 137. In the future, it will be necessary to analyze by year and dollars to find important trends in our database. With the present analysis, we can not affirm a relation between the length of the campaign and the raise of the money. 


# Findings & Recommendations

Looking at the general games and the board games, I will recommend a duration between 29 and 33 days, with an optimal of 30 days following the average length in success cases. The company should aim to have a goal between 1 and $25,000 USD. However, we should analyze the probabilities of success in more detail in the future.

My recommendation is to aim at a goal of $25,000 USD maximizing the founding but in line with the average of the successful experiences. In case that the company can work on a good strategy to connect with a big number of backers, I will consider setting the goal is $10,000 USD with the expectation of having a gain of at least fourth times gains. This is considering the tendency of the games and table games aiming small goals and raised so much money at the end of the campaign.

Also, because the board games have a higher number of backers, on average they had 902 in the period analyzed, the company can implement resources to aim at least this 902 backers, with a minimum of $27 USD per backer the company can raise at least the $25,000 USD goal. Also, it is important to analyze the resources used by the big top 20 of most successful board game companies. In terms of countries and currency, I will recommend aim the campaign to the US in USD.

Sources: BrainStation Database.

---

# SQL Queries

**Report**

**Data Dictionary**

- **ID**: unique project ID
- **name**: project name
- **sub_category_id**: what industry/category was the project in?
- **country_id**: id number associated to country of origin
- **currency_id**: what currency funding was given in?
- **launched**: date fundraising began
- **deadline:** when the target amount must be raised by
- **goal**: desired amount of funding
- **pledged**: how much was promised by the backer (whether or not the goal was reached)
- **backers**: how many individuals contributed to the campaign?
- **outcome**: was the project funded or not?

### **Part 1 - Preliminary Data Analysis**

Context to the problem - SQL queries

Familiarizing with the database

```sql
SELECT * FROM campaign;
SELECT * FROM campaign LIMIT 5;
SELECT * FROM category;
SELECT * FROM country;
SELECT * FROM sub_category;
```

Average general goal in dollars:  $69,386.78

```sql
SELECT AVG(goal)
FROM campaign
WHERE currency_id = 2;
```

```sql
- Familiarize with the database
-- Exploring the columns and rows
SELECT * FROM campaign;
SELECT * FROM campaign LIMIT 5;
SELECT * FROM category;
SELECT * FROM country;
SELECT * FROM currency;
SELECT * FROM sub_category;

```

```sql
-- Cleaning data
-- keeping only outcomes as listed: Successful, Canceled, Filed, Live, Undefined, and Suspended
SET SQL_SAFE_UPDATES = 0;
DELETE FROM campaign
WHERE outcome NOT IN ('Successful', 'Canceled', 'Failed', 'Live', 'Undefined', 'Suspended');
-- Counting rows and categories
SELECT COUNT(*) FROM campaign
WHERE outcome = "Successful";
SELECT COUNT(*) FROM campaign
WHERE outcome = "Canceled";
SELECT COUNT(*) FROM campaign
WHERE outcome = "Failed";
SELECT COUNT(*) FROM campaign
WHERE outcome = "Live";
SELECT COUNT(*) FROM campaign
WHERE outcome = "Undefined";
SELECT COUNT(*) FROM campaign
WHERE outcome = "Suspended";

-- Counting rows and categories for currency equal dollars
SELECT COUNT(*) FROM campaign
WHERE currency_id = 2;
SELECT COUNT(*) FROM campaign
WHERE outcome = "Successful" AND currency_id = 2;
SELECT COUNT(*) FROM campaign
WHERE outcome = "Canceled" AND currency_id = 2;
SELECT COUNT(*) FROM campaign
WHERE outcome = "Failed" AND currency_id = 2;
SELECT COUNT(*) FROM campaign
WHERE outcome = "Live" AND currency_id = 2;
SELECT COUNT(*) FROM campaign
WHERE outcome = "Undefined" AND currency_id = 2;
SELECT COUNT(*) FROM campaign
WHERE outcome = "Suspended" AND currency_id = 2;

-- Min, Max, and AVG Dollars Goal per category of Outcome
SELECT MAX(goal), MIN(goal), AVG(goal) FROM campaign
WHERE currency_id = 2;
SELECT MAX(goal), MIN(goal), AVG(goal) FROM campaign
WHERE outcome = "Successful" AND currency_id = 2;
SELECT MAX(goal), MIN(goal), AVG(goal) FROM campaign
WHERE outcome = "Canceled" AND currency_id = 2;
SELECT MAX(goal), MIN(goal), AVG(goal) FROM campaign
WHERE outcome = "Failed" AND currency_id = 2;
SELECT MAX(goal), MIN(goal), AVG(goal) FROM campaign
WHERE outcome = "Live" AND currency_id = 2;
SELECT MAX(goal), MIN(goal), AVG(goal) FROM campaign
WHERE outcome = "Undefined" AND currency_id = 2;
SELECT MAX(goal), MIN(goal), AVG(goal) FROM campaign
WHERE outcome = "Suspended" AND currency_id = 2;
```

```sql
-- Ordering and counting by goal in dollars in successful cases
SELECT goal, count(*) orderCount 
FROM campaign
WHERE currency_id = 2 AND outcome IN ('successful')
GROUP BY goal
ORDER BY goal ASC;
-- Ordering and counting by goal in dollars in no successful cases
SELECT goal, count(*) orderCount 
FROM campaign
WHERE currency_id = 2 AND outcome NOT IN ('successful')
GROUP BY goal
ORDER BY goal ASC;
```

```sql
-- How long do they run for (all cases in dollars)
SELECT TIMESTAMPDIFF(day, launched, deadline) AS duration, id, country_id, goal, pledged, backers, outcome
FROM campaign
WHERE currency_id = 2;
-- How long do they run for (successful cases in dollars)
SELECT TIMESTAMPDIFF(day, launched, deadline) AS duration, id, country_id, goal, pledged, backers, outcome
FROM campaign
WHERE currency_id = 2  AND outcome IN ('successful');
-- How long do they run for (unsuccessful cases in dollars)
SELECT TIMESTAMPDIFF(day, launched, deadline) AS duration, id, country_id, goal, pledged, backers, outcome
FROM campaign
WHERE currency_id = 2  AND outcome NOT IN ('successful');
```

```sql
-- Countries, cases (total cases)
SELECT country_id, count(*) orderCount
FROM campaign
GROUP BY country_id
ORDER BY country_id ASC;
-- Ordering and counting by country in dollars
SELECT country_id, count(*) orderCount
FROM campaign
WHERE currency_id = 2
GROUP BY country_id
ORDER BY country_id ASC;
-- Ordering and counting by country in dollars in successful cases
SELECT country_id, count(*) orderCount
FROM campaign
WHERE currency_id = 2 AND outcome IN ('successful')
GROUP BY country_id
ORDER BY country_id ASC;
-- Ordering and counting by goal in dollars in no successful cases
SELECT country_id, count(*) orderCount
FROM campaign
WHERE currency_id = 2 AND outcome NOT IN ('successful')
GROUP BY country_id
ORDER BY country_id ASC;
```

```sql
- Countries, average of raised money (only usd dollars)
Select avg(goal) from campaign
WHERE currency_id = 2;
```

```sql
- Countries, average of raised money (all cases)
Select country_id, avg(pledged) from campaign group by country_id
```

```sql
- Countries, average of raised money (only usd dollars)
Select country_id, avg(goal) from campaign
WHERE currency_id = 2
group by country_id
```

```sql
-- Countries, average of goal and pledged (only usd dollars in unsuccessful cases)
Select currency_id, avg(pledged), avg(goal) from campaign 
WHERE currency_id = 2 AND outcome NOT IN ('successful')
group by currency_id;

-- Countries, average of goal and pledged (only usd dollars in successful cases)
Select currency_id, avg(pledged), avg(goal) from campaign 
WHERE currency_id = 2 AND outcome IN ('successful')
group by currency_id;
```

```sql
-- number of backers, successful, failed, and canceled

SELECT 
      SUM(CASE WHEN backers <= 25 THEN 1 ELSE 0 END) AS less10,
      SUM(CASE WHEN (backers > 25 AND backers <= 50) THEN 1 ELSE 0 END) AS b10_50,
      SUM(CASE WHEN (backers > 50 AND backers <= 75) THEN 1 ELSE 0 END) AS b50_75,
      SUM(CASE WHEN (backers > 75 AND backers <= 100) THEN 1 ELSE 0 END) AS b75_100,
      SUM(CASE WHEN backers > 100  THEN 1 ELSE 0 END) as higher100,
      COUNT(*) as total, outcome
FROM campaign
WHERE campaign.country_id = 2 
        AND campaign.outcome = 'successful' OR campaign.outcome = 'failed' OR campaign.outcome = 'canceled'
GROUP BY campaign.outcome;
```

```sql
-- Goal and Outcome by ranges 

SELECT
SUM(CASE WHEN goal <= 5000 THEN 1 ELSE 0 END) AS g5K,
SUM(CASE WHEN (goal > 5000 AND goal <= 25000) THEN 1 ELSE 0 END) AS g25K,
SUM(CASE WHEN (goal > 25000 AND goal <= 50000) THEN 1 ELSE 0 END) AS g50K,
SUM(CASE WHEN (goal > 50000 AND goal <= 75000) THEN 1 ELSE 0 END) AS g75K,
SUM(CASE WHEN (goal > 75000 AND goal <= 100000) THEN 1 ELSE 0 END) AS g100K,
SUM(CASE WHEN (goal > 100000 AND goal <= 200000) THEN 1 ELSE 0 END) AS g200K,
SUM(CASE WHEN goal > 200000  THEN 1 ELSE 0 END) as higher200K,
COUNT(*) as total, outcome
FROM campaign
WHERE campaign.country_id = 2
AND campaign.outcome = 'successful' OR campaign.outcome = 'failed' OR campaign.outcome = 'canceled'
GROUP BY campaign.outcome;
```

```sql
-- Most backer by category
SELECT  [category.id](http://category.id/), count([category.id](http://category.id/)) orderCount
FROM campaign c LEFT JOIN sub_category ON c.sub_category_id = sub_category.id
LEFT JOIN category ON sub_category.category_id = [category.id](http://category.id/)
WHERE currency_id = 2
GROUP BY [category.id](http://category.id/)
ORDER BY [category.id](http://category.id/);

-- Most backer by category only in success
SELECT  category.id, count(category.id) orderCount
        FROM campaign c LEFT JOIN sub_category ON c.sub_category_id = sub_category.id
                LEFT JOIN category ON sub_category.category_id = category.id
WHERE currency_id = 2 AND outcome  = 'successful'
GROUP BY category.id
ORDER BY category.id;
```

```sql
— Creating average days
SET SQL_SAFE_UPDATES = 0;
alter table campaign add column average_days tinyint;
update campaign set average_days = TIMESTAMPDIFF(day, launched, deadline);
```

```sql
-- Analysing by category

SELECT  [category.id](http://category.id/),
ROUND(AVG(c.average_days)) as Avgdays,
ROUND(AVG(c.goal)) as Avggoal,
ROUND(AVG(c.pledged)) as Avgpledged,
ROUND(AVG(c.backers)),
COUNT(c.backers),
ROUND(AVG(c.pledged))-ROUND(AVG(c.goal)) as gain
FROM campaign c LEFT JOIN sub_category ON c.sub_category_id = sub_category.id
LEFT JOIN category ON sub_category.category_id = [category.id](http://category.id/)
WHERE currency_id = 2 AND c.outcome = 'successful' AND category_id = 7
GROUP BY [category.id](http://category.id/)
ORDER BY [category.id](http://category.id/);
```

```sql
-- by board games (subcategory 14)
SELECT * FROM campaign WHERE sub_category_id = 14 AND currency_id = 2 LIMIT 0, 10000
```
