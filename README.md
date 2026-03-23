-- SQLBolt Solutions – All Lessons <br>
-- https://sqlbolt.com/ <br>
-- Last updated: 23 March 2025 

-- Lesson 1: SELECT queries 1

SELECT * FROM movies;

SELECT title, director FROM movies;

SELECT title, year FROM movies;

SELECT * FROM movies
WHERE year >= 2000;

SELECT title FROM movies
WHERE year < 2000;


-- Lesson 2: Queries with constraints (Pt. 1)

SELECT * FROM movies
WHERE director = 'Wes Anderson';

SELECT * FROM movies
WHERE year = 1995;

SELECT * FROM movies
WHERE year > 1999;

SELECT * FROM movies
WHERE studio = 'Pixar Animation Studios';


-- Lesson 3: Queries with constraints (Pt. 2)

SELECT * FROM movies
WHERE director != 'Wes Anderson';

SELECT * FROM movies
WHERE year IN (1985, 1995, 2005);

SELECT * FROM movies
WHERE year < 1985 OR year > 2005;

SELECT * FROM movies
WHERE title LIKE '%Toy%';


-- Lesson 4: Filtering and sorting Query results

SELECT * FROM south_park
ORDER BY season, episode_in_season;

SELECT * FROM south_park
ORDER BY id
LIMIT 20;

SELECT * FROM south_park
ORDER BY imdb_rating DESC
LIMIT 10;


-- Lesson 5: Simple SELECT Queries Review

SELECT * FROM north_american_cities
WHERE population > 3000000;

SELECT * FROM north_american_cities
ORDER BY population DESC;

SELECT * FROM north_american_cities
ORDER BY population DESC
LIMIT 10;

SELECT * FROM north_american_cities
WHERE region = 'California'
ORDER BY population DESC;


-- Lesson 6: Multi-table queries with JOINs

SELECT title, domestic_sales, international_sales
FROM movies
JOIN boxoffice ON movies.id = boxoffice.movie_id;

SELECT title, domestic_sales, international_sales
FROM movies
JOIN boxoffice ON movies.id = boxoffice.movie_id
WHERE international_sales > domestic_sales;

SELECT title, (domestic_sales + international_sales) AS total_sales
FROM movies
JOIN boxoffice ON movies.id = boxoffice.movie_id
ORDER BY total_sales DESC
LIMIT 5;


-- Lesson 7: OUTER JOINs

SELECT title, rating
FROM movies
LEFT JOIN boxoffice ON movies.id = boxoffice.movie_id;

SELECT title
FROM movies
LEFT JOIN boxoffice ON movies.id = boxoffice.movie_id
WHERE boxoffice.international_sales IS NULL;


-- Lesson 8: A short note on NULLs

SELECT title
FROM movies
WHERE rating IS NULL;

SELECT title, rating
FROM movies
WHERE rating IS NOT NULL;


-- Lesson 9: Queries with expressions

SELECT title, ABS(domestic_sales - international_sales) AS difference
FROM movies
JOIN boxoffice ON movies.id = boxoffice.movie_id;

SELECT title, international_sales
FROM movies
JOIN boxoffice ON movies.id = boxoffice.movie_id
ORDER BY international_sales DESC;


-- Lesson 10: Queries with aggregates (Pt. 1)

SELECT SUM(domestic_sales + international_sales) AS total_worldwide
FROM boxoffice;

SELECT COUNT(*) AS count_pre_2000
FROM movies
WHERE year < 2000;

SELECT MAX(international_sales) AS highest_intl
FROM boxoffice;


-- Lesson 11: Queries with aggregates (Pt. 2)

SELECT director, AVG(domestic_sales) AS avg_domestic
FROM movies
JOIN boxoffice ON movies.id = boxoffice.movie_id
GROUP BY director;

SELECT director, COUNT(*) AS movie_count
FROM movies
GROUP BY director
HAVING COUNT(*) >= 2
ORDER BY movie_count DESC;


-- Lesson 12: Order of execution of a Query

SELECT director, AVG(domestic_sales + international_sales) AS avg_worldwide
FROM movies
JOIN boxoffice ON movies.id = boxoffice.movie_id
GROUP BY director
HAVING AVG(domestic_sales + international_sales) > 500000000
ORDER BY avg_worldwide DESC;


-- Lesson 13: Inserting rows

INSERT INTO movies (title, director, year, length_minutes)
VALUES ('Monsters, Inc.', 'Pete Docter', 2001, 92);

INSERT INTO boxoffice (movie_id, rating, domestic_sales, international_sales)
VALUES (20, 8.1, 289916256, 272900000);


-- Lesson 14: Updating rows

UPDATE movies
SET year = 1995
WHERE title = 'Toy Story';

UPDATE boxoffice
SET rating = rating + 1
WHERE rating < 10;


-- Lesson 15: Deleting rows

DELETE FROM movies
WHERE year < 1990;

DELETE FROM boxoffice
WHERE movie_id NOT IN (SELECT id FROM movies);


-- Lesson 16: Creating tables

CREATE TABLE database (
    name TEXT PRIMARY KEY,
    version REAL,
    download_count INTEGER
);

INSERT INTO database (name, version, download_count)
VALUES ('SQLite', 3.45, 12000000);


-- Lesson 17: Altering tables

ALTER TABLE movies
ADD COLUMN language TEXT DEFAULT 'English';


-- Lesson 18: Dropping tables

-- DROP TABLE database;
-- DROP TABLE north_american_cities;
-- (use with extreme caution – irreversible) <br>


**Thanks** <br>
**SHREYANSH PRATAP MISHRA**
