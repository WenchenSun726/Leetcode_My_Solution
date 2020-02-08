# Exchange Seats
626

- change id to change name
####  MySQL
```
SELECT (
    CASE WHEN id%2 = 1 and id = (select count(*) from seat) THEN id
        WHEN id%2=1 then id+1
        WHEN id%2=0 then id-1
end) AS id, student
FROM seat
ORDER BY id
```