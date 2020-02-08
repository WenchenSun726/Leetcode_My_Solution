# Unpopular Books
1098

- LEFT JOIN to consider all books
- maybe some null values - coalesce
####  MySQL
```
SELECT b.book_id, b.name
FROM Books as b LEFT JOIN Orders as o ON b.book_id = o.book_id and o.dispatch_date BETWEEN '2018-06-23' AND '2019-06-23'
WHERE datediff('2019-06-23', b.available_from) > 30 
GROUP BY b.book_id
HAVING coalesce(SUM(o.quantity),0) < 10
```