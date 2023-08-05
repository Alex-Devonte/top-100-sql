# Easy Problems

1. [IMDb Metacritic Rating](#IMDb-Metacritic-Rating)
2. [IMDb Max Weighted Rating](#IMDb-Max-Weighted-Rating)
3. [Students DB](#Students-DB)



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
