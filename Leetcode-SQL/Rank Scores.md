# Rank Scores

178
####  MySQL
- JOIN
```mysql
SELECT s1.Score, COUNT(DISTINCT s2.Score) AS Rank
FROM Scores AS s1 JOIN Scores AS s2 ON s1.Score <= s2.Score
GROUP BY s1.Id
ORDER BY s1.Score DESC
```
- Correlated Query - external query is the base (how many are larger than base)
```mysql
SELECT Score, 
    (SELECT COUNT(DISTINCT Score) 
    FROM Scores WHERE Score >= s.Score) AS RANK
FROM Scores AS s
ORDER BY Score DESC
```
####  MSSQL
- DENSE_RANK() OVER()
```mssql
SELECT Score, 
	dense_rank() OVER (ORDER BY Score DESC) AS Rank
FROM Scores
```