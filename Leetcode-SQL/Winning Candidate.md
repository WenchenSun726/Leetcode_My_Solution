# Winning Candidate

574
####  MySQL
- ORDER BY + Aggregation 
```
SELECT Name
FROM Candidate
WHERE Id =
    (SELECT CandidateId 
    FROM Vote Group BY CandidateId 
    ORDER BY COUNT(*) DESC LIMIT 1)
```

```
SELECT c.Name
FROM Vote v JOIN Candidate c ON v.CandidateId = c.Id
GROUP BY v.CandidateId 
ORDER BY COUNT(v.Id) DESC
LIMIT 1
```