# Moderate Problems

1. [IMDb Rating](#IMDb-Rating)
2. [Second Highest Salary](#Second-Highest-Salary)
3. [Recyclable and Low Fat Products](#Recyclable-and-Low-Fat-Products)


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

## Recyclable and Low Fat Products 
```
Table: Products

+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| product_id  | int     |
| low_fats    | enum    |
| recyclable  | enum    |
+-------------+---------+
product_id is the primary key for this table.
low_fats is an ENUM of type ('Y', 'N') where 'Y' means this product is low fat and 'N' means it is not.
recyclable is an ENUM of types ('Y', 'N') where 'Y' means this product is recyclable and 'N' means it is not.

Products table:
+-------------+----------+------------+
| product_id  | low_fats | recyclable |
+-------------+----------+------------+
| 0           | Y        | N          |
| 1           | Y        | Y          |
| 2           | N        | Y          |
| 3           | Y        | Y          |
| 4           | N        | N          |
+-------------+----------+------------+

Only products 1 and 3 are both low fat and recyclable.
```
#### Write an SQL query to find the ids of products that are both low fat and recyclable.

```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y' AND recyclable = 'Y';
```

| product_id |
|------------|
|      1     |
|      3     |
