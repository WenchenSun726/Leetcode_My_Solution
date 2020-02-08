# Reported Posts II
1132

- daily percentage of posts that got removed after being reported as spam: count('remove')/count('spam')
- average daily percentage 
- DISTINCT 
####  MySQL
```
SELECT ROUND(AVG(daily_per),2) AS average_daily_percent
FROM
	(SELECT a.action_date, 
	COUNT(Distinct r.post_id)/COUNT(DISTINCT a.post_id)*100  
	AS daily_per
	FROM Actions AS a LEFT JOIN Removals AS r 
	ON a.post_id = r.post_id
	WHERE a.extra = 'spam'
	GROUP BY a.action_date) AS tmp
```