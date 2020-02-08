# Game Play Analysis IV

550
####  MySQL

- find the first login data AS a2
- check whether this is only 1 day diff
- round()
```
SELECT 
ROUND(SUM(IF(DATEDIFF(a1.event_date, a2.first_day)=1,1,0))
/ COUNT(DISTINCT a1.player_id),2) AS fraction 
FROM Activity AS a1 
JOIN 
(SELECT player_id,MIN(event_date) AS first_day 
FROM Activity GROUP BY 1) AS a2 
on a1.player_id = a2.player_id;
```