# MySQL-Learning

1. Create a Movies Database with a table similar to the excel screenshot above

CREATE TABLE IF NOT EXISTS Movies(
-> MovieID INT UNSIGNED NOT NULL AUTO_INCREMENT,
-> Title VARCHAR(50) NOT NULL DEFAULT '',
-> Runtime INT UNSIGNED NOT NULL DEFAULT 0,
-> Genre VARCHAR (50) NOT NULL DEFAULT '',
-> IMDB_Score DECIMAL(7,2) NOT NULL DEFAULT 99999.99,
-> Rating VARCHAR(5) NOT NULL DEFAULT '',
-> PRIMARY KEY (MovieID)
-> );
    
INSERT INTO Movies VALUES
-> (NULL,'Howard the Duck',110,'Sci-Fi',4.6,'PG'),
-> (NULL,'Lavalantula',83,'Horror',4.7,'TV-14'),
-> (NULL,'Starship Troopers',129,'Sci-Fi',7.2,'PG-13'),
-> (NULL,'Waltz With Bashir',90,'Documentary',8,'R'),
-> (NULL,'Spaceballs', 96,'Comedy',7.1,'PG'),
-> (NULL,'Monsters Inc.',92,'Animation',8.1,'G');


2. Add a few more movies of your choosing.

INSERT INTO movies VALUES
-> ('Dumbo',95,'Comedy',3.9,'R'),
-> ('IT',193,'Horror',1.3,'PG');


3. Create a query to find all movies in the Sci-Fi genre.
    
select * FROM movies WHERE Genre = 'Sci-Fi';


4. Create a query to find all films that scored at least a 6.5 on IMDB

select * FROM movies WHERE IMDB_Score >= 6.5;
 
 
5. For parents who have young kids, but who don't want to sit through long children's movies, create a query to find all of the movies rated G or PG that are less than 100 minutes long.

select * FROM movies WHERE Rating = 'G' OR Rating = 'PG'
-> AND Runtime <=100;
    
    
6. Create a query to show the average runtimes of movies rated below a 7.5, grouped by their respective genres.

SELECT AVG(Runtime) FROM movies WHERE IMDB_Score <= 7.5
-> GROUP BY Genre;
    
    
7. There's been a data entry mistake; Starship Troopers is actually rated R, not PG-13. Create a query that finds the movie by its title and changes its rating to R.

UPDATE Movies  SET Rating = 'R' WHERE Title = 'Starship Troopers';


8.  Show the ID number and rating of all of the Horror and Documentary movies in the database. Do this in only one query.

SELECT MovieID, Rating FROM Movies WHERE Genre IN('Horror','Documentary');


9.  This time let's find the average, maximum, and minimum IMDB score for movies of each rating.

SELECT Rating, AVG(IMDB_Score),MAX(IMDB_Score),MIN(IMDB_Score) FROM Movies GROUP BY Rating;


10. That last query isn't very informative for ratings that only have 1 entry. use a HAVING COUNT(*) > 1 clause to only show ratings with multiple movies showing.

SELECT Rating, AVG(IMDB_Score),MAX(IMDB_Score),MIN(IMDB_Score) FROM Movies GROUP BY Rating HAVING COUNT(*) > 1;


11. Let's make our movie list more child-friendly. Delete all entries that have a rating of R.

DELETE FROM Movies WHERE Rating = 'R';


