# IMDB (Internet Movie Database)

## Setup MySQL on Cloud 9
Install MySQL database engine on command line:
```
mysql-ctl install
```
The output will be:
```
MySQL 5.5 database added.  Please make note of these credentials:

Root User: username
Database Name: c9
```
No password is set on MySQL, which is rarely an issue in a development
environment. You can setup user authentication if you want.

We will use the MySQL client on the command line to interact with MySQL database
engine:
```
mysql-ctl cli
```

## Import the database
Type the commands after the MySQL command prompt (`mysql>`):

Create an empty database:
```
mysql> create database imbd_small;
Query OK, 1 row affected (0.00 sec)

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| c9                 |
| mysql              |
| performance_schema |
| phpmyadmin         |
| imdb_small         |
+--------------------+
6 rows in set (0.00 sec)
```
Populate the database with data from `rating.sql`:
```
mysql> use imdb_small
Database changed
mysql> source imdb_small.sql
```
Note: the last command assumes that `imdb_small.sql` is in the directory where you
run `mysql-ctl cli`. You can always exit by typing `exit` and restart the MySQL
client in another directory.

Run a test query:
```
mysql> show tables;
+----------------------+
| Tables_in_imdb_small |
+----------------------+
| actors               |
| actors2              |
| directors            |
| directors_genres     |
| movies               |
| movies_directors     |
| movies_genres        |
| roles                |
+----------------------+
8 rows in set (0.00 sec)

mysql> desc actors;
+------------+--------------+------+-----+---------+-------+
| Field      | Type         | Null | Key | Default | Extra |
+------------+--------------+------+-----+---------+-------+
| id         | int(11)      | NO   | PRI | 0       |       |
| first_name | varchar(100) | YES  |     | NULL    |       |
| last_name  | varchar(100) | YES  |     | NULL    |       |
| gender     | char(1)      | YES  |     | NULL    |       |
| film_count | int(11)      | YES  |     | 0       |       |
+------------+--------------+------+-----+---------+-------+
5 rows in set (0.00 sec)

mysql> desc movies_directors;
+-------------+---------+------+-----+---------+-------+
| Field       | Type    | Null | Key | Default | Extra |
+-------------+---------+------+-----+---------+-------+
| director_id | int(11) | YES  | MUL | NULL    |       |
| movie_id    | int(11) | YES  | MUL | NULL    |       |
+-------------+---------+------+-----+---------+-------+
2 rows in set (0.00 sec)

mysql> select count(*) from actors;
+----------+
| count(*) |
+----------+
|     1907 |
+----------+
1 row in set (0.00 sec)
```
## Explore the database
Write some queries to explore the content of the database.

## Exercise problems
Write queries to answer the following questions. You can
test your queries on a larger database stored in (imdb.sql).
You will need to download the database script file using the following command:
```
wget http://www.webstepbook.com/supplements-2ed/databases/imdb.sql
```
Then, create another database (e.g. imdb) in your mysql and import the data as you did for `imbd_small`.
```
mysql> select count(*) from actors;
+----------+
| count(*) |
+----------+
|   817718 |
+----------+
1 row in set (0.00 sec)
```
1. Find the actors who have "mick" in their first names.
1. Find the number of genres each movie is in.
1. What are the names of all movies released in 1995?
1. How many people played a part in the movie "Lost in Translation"?
1. What are the names of all the people who played a part in the movie "Lost in Translation"?
1. Who directed the movie "Fight Club"?
1. How many movies has Clint Eastwood directed?
1. What are the names of all directors who have
  directed at least one horror movie?
1. What are the names of every actor who has appeared
  in a movie directed by Christopher Nolan?
1. Consider all actors that had five or more roles in a movie in 2010. List each such actor's name, the movie name, and the roles he/she played. Your answer should have one tuple for each combination of (actor, movie, role) - so if an actor has 10 roles in a given movie, there should be 10 tuples for that actor and movie.
1. For each year, count the number of movies in that year that had only female actors. A movie without any actors is also a movie with only female actors (since there are no male actors in such a movie!).
1. For each year, report the percentage of movies with only female actors made that year, and also the total number of movies made that year.
1. Find the movie(s) with the largest cast. Return the movie title and the size of the cast. By "cast size" we mean the number of distinct actors that played in that movie: if an actor played multiple roles, or if the actor is simply listed more than once, we still count her/him only once. You may not assume that only one film has the largest cast.
1. A decade is a sequence of 10 consecutive years. For example 1965, 1966, ..., 1974 is a decade, and so is 1967, 1968, ..., 1976. Find the decade with the largest number of movies.
1. (optional) The Bacon number of an actor is the length of the shortest path between the actor and Kevin Bacon in the "co-acting" graph. That is, Kevin Bacon has Bacon number 0; all actors who acted in the same film as KB have Bacon number 1; all actors who acted in the same film as some actor with Bacon number 1 (but not with Bacon himself) have Bacon number 2, etc. Count how many actors have Bacon number is 2.
* https://oracleofbacon.org
* https://oracleofbacon.org/onecenter.php?who=Kevin+Bacon



