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
### Exercise SQL Lesson 6
#### Multi-table queries with JOINs
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
    INNER JOIN boxoffice ON (movies.id=boxoffice.movie_id)
    ORDER BY rating DESC;
```

### Exercise SQL Lesson 7
#### OUTER JOINs
In this exercise, you are going to be working with a new table which stores fictional data about Employees in the film studio and their assigned office Buildings. Some of the buildings are new, so they don't have any employees in them yet, but we need to find some information about them regardless.

Since our browser SQL database is somewhat limited, only the LEFT JOIN is supported in the exercise below.
1. Find the list of all buildings that have employees
```
SELECT DISTINCT building FROM employees;
```
2. Find the list of all buildings and their capacity
```
SELECT * FROM buildings;
```
3. List all buildings and the distinct employee roles in each building (including empty buildings)
```
SELECT distinct building_name,  role 
    FROM buildings
    LEFT OUTER JOIN employees ON (employees.building=buildings.building_name);
```

### Exercise SQL Lesson 8
#### A short note on NULLs
This exercise will be a sort of review of the last few lessons. We're using the same Employees and Buildings table from the last lesson, but we've hired a few more people, who haven't yet been assigned a building.
1. Find the name and role of all employees who have not been assigned to a building
```
SELECT * FROM employees
  WHERE building IS NULL;
```
2. Find the names of the buildings that hold no employees
```
SELECT DISTINCT building_name, role 
    FROM buildings
    LEFT OUTER JOIN employees ON (employees.building=buildings.building_name)
    WHERE building IS NULL;
```

### Exercise SQL Lesson 9
#### Queries with expressions
You are going to have to use expressions to transform the BoxOffice data into something easier to understand for the tasks below.
1. List all movies and their combined sales in millions of dollars 
```
SELECT DISTINCT title, (domestic_sales+international_sales) / 1000000 AS sales
FROM movies
INNER JOIN boxoffice ON movies.id=boxoffice.movie_id
;
```
2. List all movies and their ratings in percent
```
SELECT DISTINCT title, rating*10 AS rate_percent
FROM movies
INNER JOIN boxoffice ON movies.id=boxoffice.movie_id
;
```
3. List all movies that were released on even number years
```
SELECT DISTINCT title, year
FROM movies
INNER JOIN boxoffice ON movies.id=boxoffice.movie_id
WHERE year % 2 = 0
;
```

### Exercise SQL Lesson 10
#### Queries with aggregates (Pt. 1)
For this exercise, we are going to work with our Employees table. Notice how the rows in this table have shared data, which will give us an opportunity to use aggregate functions to summarize some high-level metrics about the teams. Go ahead and give it a shot.
1. Find the longest time that an employee has been at the studio
```
SELECT MAX(years_employed) FROM employee;
```
2. For each role, find the average number of years employed by employees in that role
```
SELECT role, AVG(years_employed) 
    FROM employees
    GROUP BY role;
```
3. Find the total number of employee years worked in each building
```
SELECT building, SUM(years_employed)
  FROM employees
  GROUP BY building;
```












