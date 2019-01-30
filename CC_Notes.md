# Intro to MySQL II

## INTRO

does everybody feel comfortable with RDBMS?

---

## 1 - STUDENT - BANK DB - 10 MIN

<details><summary>Instructions</summary>


* Create a new database called `Second_International_Bank` using MySQL Workbench

  * Within this new database, create a table called `Customers` with six columns that are capable of holding the following values...

    * `ID`: An integer that will be used as the primary key for the table and automatically increments

    * `FirstName`: A string which will hold a customer's first name

    * `LastName`: A string which will hold a customer's last name

    * `Loan`: A boolean which will let users know if the customer has any unpaid loans

    * `Checking`: A decimal value which will let users know how much money a customer has in their checking account

    * `Savings`: A decimal values which will let users know how much money a customer has in their savings account

* Create five new rows of data to fill up the `Customers` table with some data

 Bonus

* Look into the [decimal](https://dev.mysql.com/doc/refman/5.7/en/precision-math-decimal-characteristics.html) datatype in MySQL and convert the `Checkings` and `Savings` columns so that they can only hold values with two or less numbers after a decimal point
</details>


<details><summary>Solution</summary>

```SQL
CREATE DATABASE Second_International_Bank;

USE Second_International_Bank;

CREATE TABLE Customers (
    ID int(50) AUTO_INCREMENT,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Loan BOOLEAN,
    Checking DECIMAL(20,2),
    Savings DECIMAL(20,2),
    primary KEY(ID)
);

INSERT INTO Customers(FirstName,LastName,Loan,Checking,Savings)
VALUES ("Richard", "Rich", TRUE, 1000.00, 20000.50),
("Bob", "Someone", TRUE, 10.75, 2.05),
("Shelly", "RichRich", FALSE, 1000000.00, 50000025.00),
("Ryan", "Middleman", FALSE, 250.00, 10000.00),
("Ryan", "Middleman", FALSE, 250.00, 10000.00),
("Shannon", "Waffles", TRUE, 1000.00, 20000.50);

SELECT * FROM Customers;
```

</details>

---

## 2 - INSTRUCTOR - Import Wizard - 5 MIN

<details><summary>Instructions</summary>
<p>

>Create a new database called `Miscellaneous_db'
```SQL
CREATE DATABASE Miscellaneous_db;
```

>Import the birdsong.csv file into a new table

Explain the screen that allows you to select/deselect columns and edit datatypes

>Query new table
```SQL
SELECT * FROM birdsong;
```

>Explain what a Primary Key is and alter table to add one

Right-click on the table and select `Alter Table` and then select PK next to the `file_id` column

>Reupload the birdsong.csv file demonstrating that it overwrites the data rather than appending to it
</p>
</details>

---

## 3 - INSTRUCTOR - Intro to Queries - 15 MIN

Use this exercise to show how you can edit values in the GUI

<details><summary>Instructions</summary>
<p>

>Still using the `birdsong` table, explain how to use `WHERE` to filter your response

```SQL 
SELECT * FROM birdsong WHERE genus = "Acanthis";
```
>Explain how to use AND/OR
```SQL 
# AND
SELECT * FROM birdsong WHERE genus = "Acanthis" AND country="Netherlands";

# OR
SELECT * FROM birdsong WHERE genus = "Acanthis" OR country="Netherlands";

# IN
SELECT * FROM birdsong WHERE genus IN ("Acanthis","Fulica");

# NOT
SELECT * FROM birdsong WHERE NOT (genus = "Acanthis" AND country = "Netherlands");
```

</p> 
</details>

---

## 4 - STUDENT - WordAssociation / Hide and Go Seek? - 15 MIN

<details><summary>Instructions</summary>
<p>

* Start by using the Table Import Wizard to create a new table called `wordassociation` with the data stored within `WordAssociation-AC.csv`.

* Come up with a means to add a new column to this table that will act as an "ID" column. This column should act as the primary key and auto-increment. By doing this, each row will now have a unique ID.

* Import the values stored within `WordAssociation-BC.csv` and `WordAssociation-CC.csv` into the table created. This can take some time, so look through the CSV files or read through some [MySQL tutorials](https://www.w3schools.com/sql/) whilst waiting.

  * Create a query that collects all of the rows whose "source" is "AC"

  * Create a query that collects all of the rows whose "source" is "BC"

  * Create a query that collects all of the rows whose "source" is "CC"

  * Create a query that collects all of the rows whose author is within the range of 0-20

  * Create a query that searches for any rows that have "pie" in their "word1" or "word2" columns

>Bonus

* There are some functions in MySQL that allow users to perform simple calculations like `MIN()`, `MAX()`, `COUNT()`, `AVG()`, and `SUM()`. Look some of these functions up and then perform the following calculations...

* Find the lowest "ID" for those rows with a "source" of "CC"

* Count how many rows have an "author" of 12


</p>
</details>

<details><summary>Solution</summary>
<p>

```SQL
-- Alter imported table to add an id
ALTER TABLE wordassociation
ADD COLUMN id INT AUTO_INCREMENT PRIMARY KEY FIRST;

-- Select all with the source of AC
SELECT * FROM wordassociation
WHERE source = "AC";

-- Select all with the source of BC
SELECT * FROM wordassociation
WHERE source = "BC";

-- Select all with the source of CC
SELECT * FROM wordassociation
WHERE source = "CC";

-- Select all where the author is greater than 0 and less than 20
SELECT * FROM wordassociation
WHERE author >= 0 AND author <= 20;

-- Select all where either word is pie
SELECT * FROM wordassociation
WHERE word1 = "pie" OR word2 = "pie";

-- Find the lowest id whose source is CC
SELECT MIN(id) FROM wordassociation
WHERE source = "CC";

-- Find how many rows have an author of 12
SELECT COUNT(author)  FROM wordassociation
WHERE author = 12;
```

</p>
</details>

---

## 5 - STUDENT - Seek, Create, Update, Destroy - 20 MIN

Explain that this exercise may take some googling.

<details><summary>Instructions</summary>
<p>

* Import the `GlobalFirePower.csv` into a new table within a localhost database.

  * Add a primary key to the table.

  * Find all of those rows that have a "ReservePersonnel" of 0 and then remove these rows from the dataset. **Note** MySQL often adds a safety measure to avoid deleting data. Check [Stack Overflow](https://stackoverflow.com/questions/11448068/mysql-error-code-1175-during-update-in-mysql-workbench) for help.

  * Every country in the world at least deserves one "FighterAircraft". Only seems fair. Lets add one to each nation that has none.

  * Oh no! By updating this column, the values within "TotalAircraftStrength" column are now off for those nations! We've got to [add one](https://stackoverflow.com/a/2680352) to the original number.

  * Find the [Averages](https://www.w3schools.com/sql/sql_count_avg_sum.asp) for `TotalMilitaryPersonnel`, `TotalAircraftStrength`, `TotalHelicopterStrength` and `TotalPopulation`. Record these averages.

  * A new nation has been founded and you are declared its leader! Congratulations! Unfortunately for you, every other nation is now looking to take over your land. Insert a new country with the average values you have just calculated.

> Bonus

* After creating your new nation and some parts of your military strategies, go through each column in the newly created row and update their values in any way that you desire!


</p>
</details>

<details><summary>Solution</summary>
<p>

```SQL
-- Add primary key
ALTER TABLE globalfirepower
ADD COLUMN id INT AUTO_INCREMENT PRIMARY KEY FIRST;

-- Turn off safe updates
SET SQL_SAFE_UPDATES = 0;

-- Delete and update data
DELETE FROM globalfirepower
WHERE ReservePersonnel = 0;

UPDATE globalfirepower
SET FighterAircraft = 1
WHERE FighterAircraft = 0;

UPDATE globalfirepower
SET TotalAircraftStrength = TotalAircraftStrength + 1
WHERE FighterAircraft = 1;

--  Turn safe updates on
SET SQL_SAFE_UPDATES = 1;

-- Select Averages
SELECT AVG(TotalMilitaryPersonnel),
	AVG(TotalAircraftStrength),
	AVG(TotalHelicopterStrength),
	AVG(TotalPopulation)
FROM globalfirepower;

-- Insert new data
INSERT INTO globalfirepower(Country, TotalPopulation, TotalMilitaryPersonnel, TotalAircraftStrength, TotalHelicopterStrength)
VALUES ("GlobalLand", 60069024, 524358, 457, 183);

SELECT * FROM globalfirepower;
```

</p>
</details>

---

## 6 - INSTRUCTOR - Joins - 10 MIN

<details><summary>Instructions</summary>
<p>

Use the `Joins.xlsx` file to demonstrate how joins work again
<center><img src="./MySQL_joins.png" width="50%"></img></center>

> Players Query
```SQL
SELECT * FROM players;
```

> Matches Query
```SQL
SELECT * FROM matches;
SELECT loser_id, loser_name, loser_rank, winner_id, winner_name, winner_rank, tourney_name FROM matches;
```

> INNER JOIN Query
```SQL
SELECT matches.winner_id, matches.winner_name, matches.winner_rank, matches.tourney_name, players.country_code as "Winner Country"
FROM matches INNER JOIN players ON players.player_id = matches.winner_id
WHERE matches.tourney_name = "Australian Open";
```

> LEFT OUTER JOIN Query
```SQL
DELETE FROM players
WHERE player_id = '200001';

SELECT players.player_id, matches.winner_name, matches.winner_rank, matches.tourney_name, players.country_code as "Winner Country"
FROM matches LEFT JOIN players ON players.player_id = matches.winner_id 
WHERE matches.tourney_name = "Australian Open";
```

> RIGHT OUTER JOIN Query
```SQL
SELECT players.player_id, matches.winner_name, matches.winner_rank, matches.tourney_name, players.country_code as "Winner Country"
FROM matches RIGHT JOIN players ON players.player_id = matches.winner_id LIMIT 25000;
```
</p>
</details>

---

## 7 - STUDENT - NBA Joins - 20 MIN

<details><summary>Instructions</summary>
<p>

* Using tables made from `Players.csv` and `Seasons_Stats.csv`, perform joins that will create the following tables:

  * Basic Information Table:

    ![Basic Info](./Images/08-JoiningNBA_BasicInfo.png)

  * Percent Stats:

    ![Percent Stats](./Images/08-JoiningNBA_PercentStats.png)

</p>
</details>

<details><summary>Solution</summary>
<p>

Explain that joining by ID won't work. Ask somebody why that is.
Use `player = "Ralph Beard"` as an example.

>Join players with seasons_stats
```SQL
SELECT players.player, players.height, players.weight, players.college, players.born, seasons_stats.pos, seasons_stats.tm
FROM players
INNER JOIN seasons_stats ON
players.player = seasons_stats.player;
```

>Join seasons_stats with players
```SQL
SELECT seasons_stats.player, players.college, seasons_stats.year, seasons_stats.pos, seasons_stats.`2P%`,
seasons_stats.`FG%`, seasons_stats.`FT%`, seasons_stats.`TS%`
FROM seasons_stats
INNER JOIN players ON
players.player = seasons_stats.player;
```

</p>
</details>

---

## 8 - PARTNERS - Witchcraft - 30 MIN

<details><summary>Instructions</summary>
<p>

* Open up the zipped folder provided and look through the CSV files contained within. As you are examining these files, take note of how they reference each other using different ID columns.

  * While you are performing your investigation on one computers, start importing these CSV files into a MySQL database using another.

  * Once all of the files have been imported, begin to create joins between the tables that would allow users to view more detailed information per witchcraft trial.

  * As you are creating joins, attempt to create new permanent tables that contains the data collected by your joins. You can use this [Stack Overflow response](https://stackoverflow.com/a/6595301) as a good starting point to how this can be accomplished.

  * Attempt to create as comprehensive a table as possible. At the end of this activity, partners will share what their final tables look like and explain why they chose to make them this way.

</p>
</details>

<details><summary>Solution</summary>
<p>

```SQL
SELECT c.caseref, d.devil_text, d.devil_type, a.accusedref
FROM wdb_accused AS a
INNER JOIN wdb_case AS c ON a.accusedref = c.accusedref
INNER JOIN wdb_devilappearance AS d ON d.caseref = c.caseref
WHERE d.devil_text > ' ';
```

</p>
</details>