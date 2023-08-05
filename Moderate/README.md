# Moderate Problems

1. [IMDb Rating](#IMDb-Rating)


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
