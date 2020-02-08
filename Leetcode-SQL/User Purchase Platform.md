# User Purchase Platform
1127 - hard...

- build the table with all table and platform - base table
- for each user_id: 
	- 1) user_id | date | mobile_amount | desktop_amount 
	- 2) assign platform and amount - user_id | date | platform | amount
 - LEFT JOIN - consider null!
####  MySQL
```
SELECT d.spend_date, d.platform, 
	IFNULL(SUM(o.amount), 0) total_amount, 
	COUNT(o.user_id) total_users
FROM 
	(SELECT DISTINCT spend_date, 
	'mobile' AS platform FROM Spending
	UNION
	SELECT DISTINCT spend_date, 
	'desktop' AS platform FROM Spending
	UNION 
	SELECT DISTINCT spend_date, 
	'both' AS platform FROM Spending) AS d
LEFT JOIN
	(SELECT spend_date, user_id, 
    IF(mobile_amount>0, 
	    if(desktop_amount>0, 'both','mobile'),'desktop') 
	    AS platform,
    (mobile_amount+desktop_amount) AS amount
	FROM 
	(SELECT spend_date, user_id,
    SUM(if(platform = 'mobile', amount, 0)) AS mobile_amount,
    SUM(if(platform = 'desktop', amount, 0)) 
    AS desktop_amount
	FROM Spending GROUP BY spend_date,user_id) AS a) AS o
ON d.spend_date = o.spend_date and d.platform = o.platform
GROUP BY d.spend_date, d.platform

```