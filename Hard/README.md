# Hard Problems

1. [IMDb Genre](#IMDb-Genre)
2. [Rising Temperature](#Rising-Temperature)
3. [Consecutive Numbers](#Consecutive-Numbers)
4. [Top Travellers](#Top-Travellers)



## IMDb Genre
#### Print the genre and the maximum weighted rating among all the movies of that genre released in 2014 per genre. 
#### Do not print any row where either genre or the weighted rating is empty/null.
#### weighted_rating = average of (rating + metacritic/10.0)
#### Keep the name of the columns as 'genre' and 'weighted_rating'.
#### The genres should be printed in alphabetical order.

```sql
SELECT genre.genre, max((imdb.rating + imdb.metacritic / 10.0) / 2) AS weighted_rating
FROM genre
JOIN imdb 
	ON genre.movie_id = imdb.movie_id
	WHERE genre.genre IS NOT NULL AND imdb.title LIKE '%2014%'
GROUP BY genre.genre
ORDER BY genre.genre;
```

| genre      | weighted_rating |
|------------|-----------------|
| Action     | 8.05 |
| Adventure  | 8.45 |
| Animation  | 8.05|
| Biography  | 7.85|
| Comedy     | 8.45 |
| Crime      | 8.0 |
| Drama      | 8.95 |
| Horror     | 7.6 |
| Music      | 8.65|
| Mystery    | 8.0 |
| Romance    | 7.45 |
| Sci-Fi     | 8.0|
| Thriller   | 7.75 |
| War        | 7.0 |


## Rising Temperature
```
Table: Weather

+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| id            | int     |
| recordDate    | date    |
| temperature   | int     |
+---------------+---------+
id is the primary key for this table.
This table contains information about the temperature in a certain day.
```

#### Write an SQL query to find all dates' id with higher temperature compared to its previous dates (yesterday).
#### Return the result table in any order.

```
The query result format is in the following example:

Weather
+----+------------+-------------+
| id | recordDate | Temperature |
+----+------------+-------------+
| 1  | 2015-01-01 | 10          |
| 2  | 2015-01-02 | 25          |
| 3  | 2015-01-03 | 20          |
| 4  | 2015-01-04 | 30          |
+----+------------+-------------+

Result table:
+----+
| Id |
+----+
| 2  |
| 4  |

In 2015-01-02, temperature was higher than the previous day (10 -> 25).
In 2015-01-04, temperature was higher than the previous day (20 -> 30).
```
```sql
SELECT w1.id AS "Id"
FROM Weather AS w1
JOIN Weather AS w2
 ON w1.recordDate = w2.recordDate + INTERVAL '1 day'
WHERE w1.Temperature > w2.Temperature;
```
| Id |
|----|
|  2 |
|  4 |


## Consecutive Numbers
```
Table: Logs

+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| id          | int     |
| num         | varchar |
+-------------+---------+
id is the primary key for this table.
```
#### Write an SQL query to find all numbers that appear at least three times consecutively.

```
The query result format is in the following example:

 Logs table:
+----+-----+
| Id | Num |
+----+-----+
| 1  | 1   |
| 2  | 1   |
| 3  | 1   |
| 4  | 2   |
| 5  | 1   |
| 6  | 2   |
| 7  | 2   |
+----+-----+

 Result table:
+-----------------+
| ConsecutiveNums |
+-----------------+
| 1               |
+-----------------+
  1 is the only number that appears consecutively for at least three times.
```
```sql
SELECT DISTINCT Num AS ConsecutiveNums
FROM (
  SELECT Num,
         LEAD(Num) OVER (ORDER BY Id) AS next_number,
         LAG(Num) OVER (ORDER BY Id) AS prev_number
  FROM Logs
) AS sub
WHERE Num = next_num AND Num = prev_num;
```
|consecutivenums |
|----------------|
|      1         |


## Top Travellers
```
Users table:
+------+-----------+
| id   | name      |
+------+-----------+
| 1    | Alice     |
| 2    | Bob       |
| 3    | Alex      |
| 4    | Donald    |
| 7    | Lee       |
| 13   | Jonathan  |
| 19   | Elvis     |
+------+-----------+

Rides table:
+------+----------+----------+
| id   | user_id  | distance |
+------+----------+----------+
| 1    | 1        | 120      |
| 2    | 2        | 317      |
| 3    | 3        | 222      |
| 4    | 7        | 100      |
| 5    | 13       | 312      |
| 6    | 19       | 50       |
| 7    | 7        | 120      |
| 8    | 19       | 400      |
| 9    | 7        | 230      |
+------+----------+----------+

Result table:
+----------+--------------------+
| name     | travelled_distance |
+----------+--------------------+
| Elvis    | 450                |
| Lee      | 450                |
| Bob      | 317                |
| Jonathan | 312                |
| Alex     | 222                |
| Alice    | 120                |
| Donald   | 0                  |
+----------+--------------------+
```
#### Write an SQL query to report the distance travelled by each user. Return the result table ordered by travelled_distance in descending order, if two or more users travelled the same distance, order them by their name in ascending order.

```sql
SELECT users.name, COALESCE(SUM(rides.distance), 0) as travelled_distance
FROM rides
RIGHT JOIN users
    ON rides.user_id = users.id
GROUP BY users.name
ORDER BY travelled_distance DESC, users.name;
```

|    name    |  travelled_distance  |
|------------|----------------------|
|  Elvis     |                450  |
|  Lee       |                450  |
|  Bob       |                317  |
|  Jonathan  |                312  |
|  Alex      |                222  |
|  Alice     |                120  |
|  Donald    |                  0  |

