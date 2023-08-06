# Moderate Problems

1. [IMDb Rating](#IMDb-Rating)
2. [Second Highest Salary](#Second-Highest-Salary)


## IMDb Rating
#### From the IMDb dataset, print the title and rating of those movies which have a genre starting with the letter 'C' released in 2014 with a budget higher than 4 Crore(40 million).

```sql
SELECT imdb.title, imdb.rating
FROM imdb
JOIN genre 
	ON genre.movie_id = imdb.movie_id
WHERE genre.genre LIKE 'C%' AND imdb.budget > 40000000 AND imdb.title LIKE '%2014%';
```

| title                                | rating |
|--------------------------------------|--------|
| Gone Girl (2014)                     | 8.1    |
| Kingsman: The Secret Service (2014)  | 7.7    |


## Second Highest Salary
#### Write a SQL query to get the second highest salary from the Employee table.

```
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
For example, given the above Employee table, the query should return 200 as the second highest salary.
If there is no second highest salary, then the query should return null.

+---------------------+
| SecondHighestSalary |
+---------------------+
| 200                 |
+---------------------+
```
```sql
SELECT Salary
FROM Employee
LIMIT 1 OFFSET 1;
```
| Salary |
|--------|
| 200    |
