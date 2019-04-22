# SQL Homework

The local cinema are having a Marvel Movie Marathon! They have asked you to help maintain their database of movies with times and attendees.

## To access the database:

First, create a database called 'marvel'

```
# terminal
createdb marvel
```

Next, run the provided SQL script to populate your database:

```
# terminal
psql -d marvel -f marvel.sql
```

Use the supplied data as the source of data to answer the questions. Copy the SQL command you have used to get the answer, and paste it below the question, along with the result they gave.

## Questions

1.  Return ALL the data in the 'movies' table.

SELECT * FROM movies;

id |                title                | year | show_time
----+-------------------------------------+------+-----------
 1 | Iron Man                            | 2008 | 19:45
 2 | The Incredible Hulk                 | 2008 | 23:20
 3 | Iron Man 2                          | 2010 | 18:10
 4 | Thor                                | 2011 | 22:35
 5 | Captain America: The First Avenger  | 2011 | 22:30
 6 | Avengers Assemble                   | 2012 | 21:55
 7 | Iron Man 3                          | 2013 | 15:00
 8 | Thor: The Dark World                | 2013 | 12:35
 9 | Batman Begins                       | 2005 | 16:50
10 | Captain America: The Winter Soldier | 2014 | 20:35
11 | Guardians of the Galaxy             | 2014 | 14:25
12 | Avengers: Age of Ultron             | 2015 | 14:10
13 | Ant-Man                             | 2015 | 17:10
14 | Captain America: Civil War          | 2016 | 23:30
15 | Doctor Strange                      | 2016 | 16:15
16 | Guardians of the Galaxy 2           | 2017 | 19:15
17 | Spider-Man: Homecoming              | 2017 | 18:45
18 | Thor: Ragnarok                      | 2017 | 13:35
19 | Black Panther                       | 2018 | 22:05
(19 rows)

2.  Return ONLY the name column from the 'people' table

SELECT name FROM people;

name       
-----------------
James Berry
Kris Brough
Matthew Beeston
Reka Forgacs
Euan Gilmour
Pawel Gorny
Hamish King
Roderick King
Ben Sharp
Donald Trump
Ros Ulldemolins
(11 rows)

3.  Oops! Someone at CodeClan spelled Rose's name wrong! Change it to reflect the proper spelling ('Rose' not 'Ros').

UPDATE people
SET name = 'Rose Ulldemolins'
WHERE name = 'Ros Ulldemolins';

SELECT name FROM people;

name       
------------------
James Berry
Kris Brough
Matthew Beeston
Reka Forgacs
Euan Gilmour
Pawel Gorny
Hamish King
Roderick King
Ben Sharp
Donald Trump
Rose Ulldemolins
(11 rows)

4.  Return ONLY your name from the 'people' table.

SELECT name FROM people
WHERE name LIKE 'Matt%';

name       
-----------------
Matthew Beeston
(1 row)

5.  The cinema is showing 'Batman Begins', but Batman is DC, not Marvel! Delete the entry from the 'movies' table.

DELETE FROM movies
WHERE id = 9;
SELECT * FROM movies;

DELETE 1
 id |                title                | year | show_time
----+-------------------------------------+------+-----------
  1 | Iron Man                            | 2008 | 19:45
  2 | The Incredible Hulk                 | 2008 | 23:20
  3 | Iron Man 2                          | 2010 | 18:10
  4 | Thor                                | 2011 | 22:35
  5 | Captain America: The First Avenger  | 2011 | 22:30
  6 | Avengers Assemble                   | 2012 | 21:55
  7 | Iron Man 3                          | 2013 | 15:00
  8 | Thor: The Dark World                | 2013 | 12:35
 10 | Captain America: The Winter Soldier | 2014 | 20:35
 11 | Guardians of the Galaxy             | 2014 | 14:25
 12 | Avengers: Age of Ultron             | 2015 | 14:10
 13 | Ant-Man                             | 2015 | 17:10
 14 | Captain America: Civil War          | 2016 | 23:30
 15 | Doctor Strange                      | 2016 | 16:15
 16 | Guardians of the Galaxy 2           | 2017 | 19:15
 17 | Spider-Man: Homecoming              | 2017 | 18:45
 18 | Thor: Ragnarok                      | 2017 | 13:35
 19 | Black Panther                       | 2018 | 22:05
(18 rows)


6.  Create a new entry in the 'people' table with the name of one of the instructors.

INSERT INTO people (name) VALUES ('Keith Douglas');
SELECT name FROM people
WHERE name LIKE 'Keith%';

name      
---------------
Keith Douglas
(1 row)



7.  Donald Trump has decided to hijack our movie evening, Remove him from the table of people.

DELETE FROM people
WHERE name LIKE 'Donald%';
SELECT * FROM people;

DELETE 1
 id |      name       
----+-----------------
  1 | James Berry
  2 | Kris Brough
  3 | Matthew Beeston
  4 | Reka Forgacs
  5 | Euan Gilmour
  6 | Pawel Gorny
  7 | Hamish King
  8 | Roderick King
  9 | Ben Sharp
 11 | Ros Ulldemolins
(10 rows)

8.  The cinema has just heard that they will be holding an exclusive midnight showing of 'Avengers: Infinity War'!! Create a new entry in the 'movies' table to reflect this.

SELECT COUNT(*) FROM movies;
INSERT INTO movies (title, year, show_time) VALUES ('Avengers: Infinity War', 2018, '00:00');
SELECT COUNT(*) FROM movies;

count
-------
   19
(1 row)

INSERT 0 1
count
-------
   20
(1 row)



9.  The cinema would also like to make the Guardians movies a back to back feature. Find out the show time of "Guardians of the Galaxy" and set the show time of "Guardians of the Galaxy 2" to start two hours later.

SELECT movies FROM movies
WHERE title LIKE 'Guardian%';
SELECT show_time FROM movies
WHERE id = 11;
UPDATE movies
SET show_time = 16.25
WHERE id = 16;
SELECT movies FROM movies
WHERE title LIKE 'Guardian%';

movies                    
---------------------------------------------
(11,"Guardians of the Galaxy",2014,14:25)
(16,"Guardians of the Galaxy 2",2017,19:15)
(2 rows)

show_time
-----------
14:25
(1 row)

UPDATE 1
movies                    
---------------------------------------------
(11,"Guardians of the Galaxy",2014,14:25)
(16,"Guardians of the Galaxy 2",2017,16.25)
(2 rows)

## Extension

1.  Research how to delete multiple entries from your table in a single command.

The most obvious way to do this appears to be the use of a WHERE clause that matches several records. Eg:

SELECT COUNT(*) FROM movies;
DELETE FROM movies
WHERE title LIKE 'Guardian%';
SELECT COUNT(*) FROM movies;

count
-------
   19
(1 row)

DELETE 2
count
-------
   17
(1 row)


Alternatively specify a single value that matches several records:

SELECT COUNT(*) FROM movies;
DELETE FROM movies
WHERE year = 2017;
SELECT COUNT(*) FROM movies;

count
-------
   19
(1 row)

DELETE 3
count
-------
   16
(1 row)
