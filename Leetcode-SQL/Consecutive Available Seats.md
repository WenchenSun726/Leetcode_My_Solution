# Consecutive Available Seats

603
####  MySQL
- consecutive: should consider both seat_id - 1 and seat_id + 1
- free = 1 
- DISTINCT 
```
SELECT DISTINCT c1.seat_id 
FROM cinema AS c1, cinema AS c2 
WHERE (c1.free = 1 and c2.free = 1) 
and 
(c1.seat_id = c2.seat_id + 1 or c1.seat_id = c2.seat_id - 1)
ORDER BY c1.seat_id
```