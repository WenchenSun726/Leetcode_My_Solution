# Shortest Distance in a Plane

612
####  MySQL
- outer join - p1.x!=p2.x or p1.y!=p2.y / (p1.x,p1.y) <> (p2.x,p2.y)

```
SELECT ROUND(sqrt(pow(p1.x-p2.x,2)+pow(p1.y-p2.y,2)),2) 
AS shortest
FROM point_2d AS p1, point_2d AS p2
WHERE (p1.x,p1.y) <> (p2.x,p2.y)
ORDER BY shortest 
LIMIT 1;
```