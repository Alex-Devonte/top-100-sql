# Easy Problems

1. [IMDb Metacritic Rating](#IMDb-Metacritic-Rating)
2. [IMDb Max Weighted Rating](#IMDb-Max-Weighted-Rating)
3. [Students DB](#Students-DB)
4. [Big Countries](#Big-Countries)
5. [Sales Executive](#Sales-Executive)
6. [Director's Actor](#Director's-Actor)
7. [Combine Two Tables](#Combine-Two-Tables)



## IMdb Metacritic Rating
#### Print the title and the ratings of the movies released in 2012 whose Metacritic rating is more than 60 and domestic collections exceed 10 Crores(100 Million).

```sql
SELECT imdb.title, imdb.rating
FROM imdb
JOIN earning 
	ON imdb.movie_id = earning.movie_id
WHERE imdb.title LIKE '%2012%' AND imdb.metacritic > 60 AND earning.domestic > 100000000;
```

| title                     | rating |
|---------------------------|--------|
| Argo (2012)               | 7.7    |
| Django Unchained (2012)   | 8.4    |
| Les Misérables (2012)     | 7.6    |
| Silver Linings Playbook (2012) | 7.8 |
| Skyfall (2012)            | 7.8    |
| The Avengers (2012)       | 8.1    |
| The Dark Knight Rises (2012) | 8.4 |
| Wreck-It Ralph (2012)     | 7.7    |


## IMDb Max Weighted Rating
#### Print the genre and the maximum net profit among all the movies of that genre that released in 2012 per genre.

```sql
SELECT genre.genre, MAX((earning.domestic + earning.worldwide) - imdb.budget) AS net_profit
FROM genre
JOIN earning 
	ON genre.movie_id = earning.movie_id
JOIN imdb 
	ON earning.movie_id = imdb.movie_id
WHERE genre.genre IS NOT NULL AND imdb.title like '%2012%' 
GROUP BY genre.genre;
```
| genre       | net_profit    |
|-------------|---------------|
| Romance     | 529,619,540   |
| Musical     | 529,619,540   |
| Fantasy     | 1,144,107,136 |
| Drama       | 529,619,540   |
| Biography   | 323,851,006   |
| Action      | 1,922,170,898 |
| Thriller    | 1,283,078,198 |
| Sci-Fi      | 1,922,170,898 |
| Western     | 488,173,672   |
| Comedy      | 495,645,778   |
| Adventure   | 1,212,921,290 |
| Animation   | 495,645,778   |
| Crime       | 82,129,755    |


## Students DB
#### Insert below student details in students table and print all data of table

	| ID | Name   | Gender |
	-------------------------
	| 3  | Kim    | F      |
	| 4  | Molina | F      |
	| 5  | Dev    | M      |

 ```sql
INSERT INTO students
VALUES 
	(3, 'Kim', 'F'),
 	(4, 'Molina', 'F'),
 	(5, 'Dev', 'M');

SELECT * FROM students;
```

| id | name    | gender |
|----|---------|--------|
| 1  | Ryan    | M      |
| 2  | Joanna  | F      |
| 3  | Kim     | F      |
| 4  | Molina  | F      |
| 5  | Dev     | M      |


## Big Countries
#### A country is big if it has an area of bigger than 3 million square km or a population of more than 25 million. Write a SQL solution to output big countries' name, population, and area.

```sql
SELECT world."name", world.population, world.area
FROM world 
WHERE world.area > 3000000 OR world.population > 25000000;
```
| name        | population   | area       |
|-------------|--------------|------------|
| Afghanistan | 25,500,100   | 652,230    |
| Algeria     | 37,100,000   | 2,381,741  |


## Sales
#### Given three tables: salesperson, company, orders. Output all the names in the table salesperson, who didn't have sale to company 'RED'

```sql
SELECT salesperson.name 
FROM salesperson
WHERE salesperson.sales_id NOT IN
(SELECT orders.sales_id FROM orders LEFT JOIN company ON orders.com_id = company.com_id WHERE company.name = 'RED');
```
| name |
|------|
| Amy  |
| Mark |
| Alex |

## Director's Actor
#### Write a SQL query for a report that provides the pairs (actor_id, director_id) where the actor have co-worked with the director at least 3 times. 

```sql
SELECT actor_id, director_id FROM actordirector GROUP BY actor_id, director_id HAVING count(*) >= 3;
```
| actor_id | director_id |
|----------|-------------|
|    1     |     1       |

## Combine Two Tables
#### Table: Person
```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| PersonId    | int     |
| FirstName   | varchar |
| LastName    | varchar |
+-------------+---------+
PersonId is the primary key column for this table.
```
#### Table: Address
```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| AddressId   | int     |
| PersonId    | int     |
| City        | varchar |
| State       | varchar |
+-------------+---------+
AddressId is the primary key column for this table.
```
#### Write a SQL query for a report that provides the following information for each person in the Person table, regardless if there is an address for each of those people: FirstName, LastName, City, State

```sql
SELECT Person.FirstName, Person.LastName, Address.City, Address.State
FROM Person
LEFT JOIN Address
    ON Person.PersonID = Address.PersonID;
```
| firstname | lastname | city | state |
|-----------|----------|------|-------|
| Allen     | Wang     |      |       |
