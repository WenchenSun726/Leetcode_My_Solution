# Tree Node

603
####  MySQL
- types: 1) root - no parent
			  2) leaf - have parent node but no child
			  3) inner - have parent & child
- ** If there is null value in subquery, the outerquery will be empty list.**
```
SELECT id, 
    (CASE WHEN p_id is null THEN "Root"
	WHEN id in (SELECT distinct p_id FROM tree) THEN "Inner"
	ELSE "Leaf" 
	END) AS Type
FROM tree
ORDER BY id;
```