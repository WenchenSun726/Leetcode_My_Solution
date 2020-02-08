# Delete Duplicate Emails

196
####  MySQL

- DELETE
```
DELETE FROM Person
WHERE id not in (
    SELECT * FROM(
        SELECT Min(id)
        FROM Person p
        GROUP BY Email) AS a)
# cannot refer Person if UPDATE, DELETE
```

```
DELETE P2
FROM Person as P1 join Person as P2
WHERE (P1.id < P2.id) and (P1.Email = P2.Email);
# DELETE records of P2 for certain conditions 
```