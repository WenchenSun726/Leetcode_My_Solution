# Market Analysis II
1159 *** 

#### MSSQL
- find second sold item for each user - rank = 2
- user LEFT JOIN CTE table
- CASE WHEN - this can also identify null (return false)
```
WITH rank AS(
SELECT o.seller_id, i.item_brand, 
	row_number() OVER(PARTITION BY o.seller_id 
		ORDER BY o.order_date ASC) AS rnk
FROM Orders AS o JOIN Items AS i ON o.item_id = i.item_id),

second AS (
SELECT *
FROM rank
WHERE rnk=2)

SELECT u.user_id AS seller_id, 
    (CASE WHEN u.favorite_brand = s.item_brand THEN 'yes'
     ELSE 'no'
    END) AS "2nd_item_fav_brand"
FROM Users AS u LEFT JOIN second AS s ON u.user_id = s.seller_id
```