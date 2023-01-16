### Exercise SQL Lesson 1
We will be using a database with data about some of Pixar's classic movies for most of our exercises. This first exercise will only involve the Movies table, and the default query below currently shows all the properties of each movie. To continue onto the next lesson, alter the query to find the exact information we need for each task.
1. Find the title of each film
```
SELECT TITLE FROM movies;
```
2. Find the director of each film
```
SELECT director FROM movies;
```
3. Find the title and director of each film
```
SELECT title, director FROM movies;
```
4. Find the title and year of each film
```
SELECT title, year FROM movies;
```
5. Find all the information about each film
```
SELECT * FROM movies;
```

### Exercise SQL Lesson 2
Using the right constraints, find the information we need from the Movies table for each task below.
1. Find the movie with a row id of 6
```
SELECT * FROM movies
  WHERE id = 6;
```
2. Find the movies released in the years between 2000 and 2010
```
SELECT * FROM movies
  WHERE year BETWEEN 2000 and 2010;
```
3. Find the movies not released in the years between 2000 and 2010
```
SELECT * FROM movies
  WHERE year NOT BETWEEN 2000 and 2010;
```
4. Find the first 5 Pixar movies and their release year
```
SELECT * FROM movies
  WHERE year
  LIMIT 5;
```

### Exercise SQL Lesson 3
Here's the definition of a query with a WHERE clause again, go ahead and try and write some queries with the operators above to limit the results to the information we need in the tasks below.
1. Find all the Toy Story movies 
```
SELECT * FROM movies
  WHERE title LIKE "%Toy%";
```
2. Find all the movies directed by John Lasseter
```
SELECT * FROM movies
  WHERE director LIKE "%Jo%";
```
3. Find all the movies (and director) not directed by John Lasseter
```
SELECT * FROM movies
  WHERE director NOT LIKE "%Jo%";
```
4. Find all the WALL-* movies
```
SELECT * FROM movies
  WHERE titleLIKE "%wall-%";
```

### Exercise SQL Lesson 4
There are a few concepts in this lesson, but all are pretty straight-forward to apply. To spice things up, we've gone and scrambled the Movies table for you in the exercise to better mimic what kind of data you might see in real life. Try and use the necessary keywords and clauses introduced above in your queries.
1. List all directors of Pixar movies (alphabetically), without duplicates
```
SELECT DISTINCT director
  FROM movies
  ORDER BY director;
```
2. List the last four Pixar movies released (ordered from most recent to least)
```
SELECT title
  FROM movies
  ORDER BY YEAR DESC
  LIMIT 4;
```
3. List the first five Pixar movies sorted alphabetically
```
SELECT title
  FROM movies
  ORDER BY title ASC
  LIMIT 5;
```
4.List the next five Pixar movies sorted alphabetically
```
SELECT title
FROM movies
ORDER BY title ASC
LIMIT 5
OFFSET 5;
```

### Exercise SQL Lesson 5
In the exercise below, you will be working with a different table. This table instead contains information about a few of the most populous cities of North America[1] including their population and geo-spatial location in the world.
1. List all the Canadian cities and their populations
```
SELECT city, population 
  FROM north_american_cities
  WHERE country = "Canada";
```

2. Order all the cities in the United States by their latitude from north to south
```
SELECT * FROM north_american_cities
  WHERE country="United States"
  ORDER BY latitude DESC;
```
3. List all the cities west of Chicago, ordered from west to east 
```
SELECT city
  FROM north_american_cities
  WHERE longitude < -87.629798
  ORDER BY longitude;
```
4. List the two largest cities in Mexico (by population) 
```
SELECT city 
  FROM north_american_cities
  WHERE country="Mexico"
  ORDER BY population DESC
  LIMIT 2;
```

5. List the third and fourth largest cities (by population) in the United States and their population 
```
SELECT city, population 
 FROM north_american_cities
 WHERE country="United States"
 ORDER BY population DESC
 LIMIT 2
 OFFSET 2;
```
