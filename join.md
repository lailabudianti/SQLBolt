### SQL Lesson 6: Multi-table queries with JOINs
We've added a new table to the Pixar database so that you can try practicing some joins. The BoxOffice table stores information about the ratings and sales of each particular Pixar movie, and the Movie_id column in that table corresponds with the Id column in the Movies table 1-to-1. Try and solve the tasks below using the INNER JOIN introduced above.
1. Find the domestic and international sales for each movie
```
SELECT title, domestic_sales, international_sales
    FROM movies
    INNER JOIN boxoffice ON (movies.id=boxoffice.movie_id)
    ;
```
2. Show the sales numbers for each movie that did better internationally rather than domestically
```
SELECT title, domestic_sales, international_sales
    FROM movies
    INNER JOIN boxoffice ON (movies.id=boxoffice.movie_id)
    WHERE international_sales > domestic_sales
    ;
```
3. List all the movies by their ratings in descending order
```
SELECT *
    FROM movies
    inner join boxoffice on (movies.id=boxoffice.movie_id)
    ORDER BY rating desc;
```
