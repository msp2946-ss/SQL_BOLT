**SQLBolt Solutions with Questions – All Lessons <br>
https://sqlbolt.com/ <br>
Last updated: 23 March 2026 <br>
Author: Shreyansh Pratap Mishra**

**Lesson 1: SELECT queries 1**

Question: Select all columns from the movies table
SELECT * FROM movies;

Question: Select the title and director from the movies table
SELECT title, director FROM movies;

Question: Select the title and year from the movies table
SELECT title, year FROM movies;

Question: Select all movies from the year 2000 or later
SELECT * FROM movies WHERE year >= 2000;

Question: Select all movies released before the year 2000
SELECT title FROM movies WHERE year < 2000;  

**Lesson 2: Queries with constraints (Pt. 1)**

Question: Select all movies directed by Wes Anderson
SELECT * FROM movies WHERE director = 'Wes Anderson';

Question: Select all movies from the year 1995
SELECT * FROM movies WHERE year = 1995;

Question: Select all movies after 1999
SELECT * FROM movies WHERE year > 1999;

Question: Select all movies produced by Pixar Animation Studios
SELECT * FROM movies WHERE studio = 'Pixar Animation Studios';

**Lesson 3: Queries with constraints (Pt. 2)**

Question: Select all movies not directed by Wes Anderson
SELECT * FROM movies WHERE director != 'Wes Anderson';

Question: Select movies from years 1985, 1995, or 2005
SELECT * FROM movies WHERE year IN (1985, 1995, 2005);

Question: Select movies released before 1985 or after 2005
SELECT * FROM movies WHERE year < 1985 OR year > 2005;

Question: Select movies with "Toy" in the title
SELECT * FROM movies WHERE title LIKE '%Toy%';

**Lesson 4: Filtering and sorting Query results**

Question: Select all episodes of South Park ordered by season and episode number
SELECT * FROM south_park ORDER BY season, episode_in_season;

Question: Select the first 20 episodes by ID
SELECT * FROM south_park ORDER BY id LIMIT 20;

Question: Select top 10 highest-rated episodes by IMDb rating
SELECT * FROM south_park ORDER BY imdb_rating DESC LIMIT 10;

**Lesson 5: Simple SELECT Queries Review**

Question: Select all North American cities with population over 3,000,000
SELECT * FROM north_american_cities WHERE population > 3000000;

Question: Select all North American cities ordered by population descending
SELECT * FROM north_american_cities ORDER BY population DESC;

Question: Select top 10 most populous North American cities
SELECT * FROM north_american_cities ORDER BY population DESC LIMIT 10;

Question: Select cities in California ordered by population descending
SELECT * FROM north_american_cities WHERE region = 'California' ORDER BY population DESC;

**Lesson 6: Multi-table queries with JOINs**

Question: Select title, domestic sales, and international sales for all movies
SELECT title, domestic_sales, international_sales FROM movies JOIN boxoffice ON movies.id = boxoffice.movie_id;

Question: Select movies where international sales exceed domestic sales
SELECT title, domestic_sales, international_sales FROM movies JOIN boxoffice ON movies.id = boxoffice.movie_id WHERE international_sales > domestic_sales;

Question: Select top 5 movies by total sales (domestic + international)
SELECT title, (domestic_sales + international_sales) AS total_sales FROM movies JOIN boxoffice ON movies.id = boxoffice.movie_id ORDER BY total_sales DESC LIMIT 5;

**Lesson 7: OUTER JOINs**

Question: Select title and rating for all movies including those without box office data
SELECT title, rating FROM movies LEFT JOIN boxoffice ON movies.id = boxoffice.movie_id;

Question: Select movies that have no box office data
SELECT title FROM movies LEFT JOIN boxoffice ON movies.id = boxoffice.movie_id WHERE boxoffice.international_sales IS NULL;

**Lesson 8: A short note on NULLs**

Question: Select movies where rating is NULL
SELECT title FROM movies WHERE rating IS NULL;

Question: Select movies with a rating
SELECT title, rating FROM movies WHERE rating IS NOT NULL;

**Lesson 9: Queries with expressions**

Question: Select the absolute difference between domestic and international sales for each movie
SELECT title, ABS(domestic_sales - international_sales) AS difference FROM movies JOIN boxoffice ON movies.id = boxoffice.movie_id;

Question: Select movies ordered by international sales descending
SELECT title, international_sales FROM movies JOIN boxoffice ON movies.id = boxoffice.movie_id ORDER BY international_sales DESC;

**Lesson 10: Queries with aggregates (Pt. 1)**

Question: Find the total worldwide sales for all movies
SELECT SUM(domestic_sales + international_sales) AS total_worldwide FROM boxoffice;

Question: Count movies released before 2000
SELECT COUNT(*) AS count_pre_2000 FROM movies WHERE year < 2000;

Question: Find the highest international sales
SELECT MAX(international_sales) AS highest_intl FROM boxoffice;

**Lesson 11: Queries with aggregates (Pt. 2)**

Question: Find average domestic sales by director
SELECT director, AVG(domestic_sales) AS avg_domestic FROM movies JOIN boxoffice ON movies.id = boxoffice.movie_id GROUP BY director;

Question: Count movies by director with at least 2 movies
SELECT director, COUNT(*) AS movie_count FROM movies GROUP BY director HAVING COUNT(*) >= 2 ORDER BY movie_count DESC;

**Lesson 12: Order of execution of a Query**

Question: Find directors with average worldwide sales over 500 million, ordered by average sales descending
SELECT director, AVG(domestic_sales + international_sales) AS avg_worldwide FROM movies JOIN boxoffice ON movies.id = boxoffice.movie_id GROUP BY director HAVING AVG(domestic_sales + international_sales) > 500000000 ORDER BY avg_worldwide DESC;

**Lesson 13: Inserting rows**

Question: Insert a new movie
INSERT INTO movies (title, director, year, length_minutes) VALUES ('Monsters, Inc.', 'Pete Docter', 2001, 92);

Question: Insert box office data for the new movie
INSERT INTO boxoffice (movie_id, rating, domestic_sales, international_sales) VALUES (20, 8.1, 289916256, 272900000);

**Lesson 14: Updating rows**

Question: Update the year of Toy Story
UPDATE movies SET year = 1995 WHERE title = 'Toy Story';

Question: Increase rating by 1 for all movies with rating less than 10
UPDATE boxoffice SET rating = rating + 1 WHERE rating < 10;

**Lesson 15: Deleting rows**

Question: Delete movies released before 1990
DELETE FROM movies WHERE year < 1990;

Question: Delete box office records for movies that no longer exist
DELETE FROM boxoffice WHERE movie_id NOT IN (SELECT id FROM movies);

**Lesson 16: Creating tables**

Question: Create a new database table
CREATE TABLE database ( name TEXT PRIMARY KEY, version REAL, download_count INTEGER );

Question: Insert a row into the database table
INSERT INTO database (name, version, download_count) VALUES ('SQLite', 3.45, 12000000);

**Lesson 17: Altering tables**

Question: Add a language column to movies with default 'English'
ALTER TABLE movies ADD COLUMN language TEXT DEFAULT 'English';

**Lesson 18: Dropping tables**

Question: Drop a table (use with extreme caution – irreversible)
DROP TABLE database;
DROP TABLE north_american_cities;
