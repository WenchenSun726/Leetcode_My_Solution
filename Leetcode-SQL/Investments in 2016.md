# Investments in 2016

585
####  MySQL
- same **TIV_2015** value as one or more other policyholders
- unique LAT,LON - use () for two values
- SUM(TIV_2016)
```
SELECT SUM(TIV_2016) AS TIV_2016
FROM insurance 
WHERE TIV_2015 in 
	(SELECT TIV_2015 FROM insurance
    GROUP BY TIV_2015
	HAVING COUNT(*) > 1)
and (LAT,LON) in (
    SELECT LAT,LON FROM insurance
	GROUP BY LAT,LON
	HAVING COUNT(*) = 1)
```