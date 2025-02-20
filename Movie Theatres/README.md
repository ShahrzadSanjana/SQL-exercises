-- https://en.wikibooks.org/wiki/SQL_Exercises/Movie_theatres

**Data Engineering**

Creating the database, its' tables, and populating them with data in order to darry out database analysis. 

```sql CREATE DATABASE "movie_theatres";

CREATE TABLE "Movies" ("Code" INT PRIMARY KEY NOT NULL, "Title" VARCHAR(255) NOT NULL, "Rating" VARCHAR(255));

CREATE TABLE "MovieTheaters" ("Code" INT PRIMARY KEY, "Name" VARCHAR(255) NOT NULL, "Movie" INT FOREIGN KEY (Movie) REFERENCES Movies(Code)) ;

INSERT INTO Movies VALUES 
(1,'Citizen Kane','PG'),
(2,'Singin'' in the Rain','G'),
(3,'The Wizard of Oz','G'),
(4,'The Quiet Man',NULL),
(5,'North by Northwest',NULL),	
(6,'The Last Tango in Paris','NC-17'),
(7,'Some Like it Hot','PG-13'),
(8,'A Night at the Opera',NULL);

INSERT INTO MovieTheaters(Code,Name,Movie) VALUES(1,'Odeon',5);
 INSERT INTO MovieTheaters(Code,Name,Movie) VALUES(2,'Imperial',1);
 INSERT INTO MovieTheaters(Code,Name,Movie) VALUES(3,'Majestic',NULL);
 INSERT INTO MovieTheaters(Code,Name,Movie) VALUES(4,'Royale',6);
 INSERT INTO MovieTheaters(Code,Name,Movie) VALUES(5,'Paraiso',3);
 INSERT INTO MovieTheaters(Code,Name,Movie) VALUES(6,'Nickelodeon',NULL);
```



**Data Analysis - Questions**

```sql
-- 1) Select the title of all movies.

SELECT Title FROM Movies;


-- 2) Show all the distinct ratings in the database.

SELECT DISTINCT(Rating) FROM Movies
WHERE Rating IS NOT NULL;


-- 3) Show all unrated movies.

SELECT * FROM Movies
WHERE Rating IS NULL;


-- 4) Select all movie theaters that are not currently showing a movie.

SELECT * FROM MovieTheaters
WHERE Movie IS NULL;


-- 5) Select all data from all movie theaters and, additionally, the data from the movie that is being shown in the theater (if one is being shown).

SELECT * FROM Movies
JOIN MovieTheaters
ON Movies.Code=MovieTheaters.Movie;


-- 6) Select all data from all movies and, if that movie is being shown in a theater, show the data from the theater.

SELECT * FROM Movies
RIGHT JOIN MovieTheaters
ON Movies.Code=MovieTheaters.Movie;


-- 7) Show the titles of movies not currently being shown in any theaters.

SELECT Title FROM MovieTheaters
RIGHT JOIN Movies
ON Movies.Code=MovieTheaters.Movie
WHERE MovieTheaters.Movie IS NULL; 

-- OR, you could try the following query

SELECT Title FROM Movies
WHERE Code NOT IN (SELECT Movie FROM MovieTheaters WHERE MOVIE IS NOT NULL);


-- 8) Add the unrated movie "One, Two, Three".

INSERT INTO Movies VALUES ('9', 'One,Two,Three', NULL);
SELECT * FROM movies; 


-- 9) Set the rating of all unrated movies to "G".

UPDATE "Movies"
SET Rating = 'G'
WHERE Rating IS NULL;


-- 10) Remove movie theaters projecting movies rated "NC-17"

DELETE FROM Movies
WHERE Rating = 'NC-17';
