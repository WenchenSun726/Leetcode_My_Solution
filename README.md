# Leetcode Solutions

My solutions for Leetcode SQL and Algorithms. 

## SQL

####  some tips for review
- JOIN
1. explicit join - inner join on;
 implicity join - where column a = column b
2. Types of Join - 1) Inner Join 2) Outer Join [left, right, full] 3) Cross Join
> **Note:** 
> 1) resturn all records that at least one match in both tables - default type 
> 2) return all records from left table and matched rows from right table - right join is opposite; full join: return all records which there is a match is either of tables = union (left + right join)
> 3) return all Cartesian product of records from joined tables - two kind syntax: cross join/list two tables without where clause
self join can be equal to above types
- DATABASE DESIGN
1. Denormalized vs Normalized 

	Denormalized: **optimize read time** - store redundant data, can avoid costly joins;
  
	Normalized: **minimize redundacy** - store data once, but some times require expensive joins
2. Process:
	1) handle ambiguity
	2) define core objects in a table
	3) analyze relations: one-to-many, many-to-many...
	4) investigate actions	
3. DDL, DQL, DMI

	DDL (Data Definition Language) - to define data structures
  
	DQL (Data Query Language) - select
  
	DML (Data Manipulation Language) - insert, update, delete, merge

## Algorithms

Python only
