// server
mysql-ctl cli
exit; quit; \q; CTRL+C;
mysql-ctl stop;

// Navigation
SHOW DATABASES;
SELECT @@hostname; SELECT <database name>;
USE <database name>; // selecting a database to use
SELECT DATABASE(); // shows what is currently in use
SHOW TABLES;
SHOW COLUMNS FROM <tablename>; DESC <tablename>;

// Create
CREATE DATABASE <name>;
CREATE TABLE <tablename> (
    <column name> <data type>, <column name> <data type>
    // name VARCHAR(100), age INT 
    )
    ***Extra properties for data type***
    NOT NULL // you can explicitly state "NULL" as a property
    DEFAULT <default>
    PRIMARY KEY (<CN>); <CN> PRIMARY KEY // unique identifier
    AUTO_INCREMENT
INSERT INTO <tablename>(<CN>,<CN>) VALUES (<CV>, <CV>) // can insert multiple values (with comma)

// READ
SELECT * FROM <tablename>; // * = give me all columns 
    SELECT <CN>,<CN> FROM <tablename>;
    SELECT & FROM <tablename> WHERE <query> // Query asks a question i.e "age=2"
    SELECT <CN> AS <user variable> FROM <tablename> // AS uses an alias, data is not changed, just displayed output
    
// UPDATE
UPDATE <tablename> SET <assignment> WHERE <query>; // select from <CN> all <query> and set to <assignment>

// Delete
DROP DATABASE <database>; // delete database
DROP TABLE <tablename>; // completely destroys the table
DELETE FROM <tablename> WHERE <query>; 
DELETE FROM <tablename>; // clears a whole table but retains the table's properties

// OTHERS
SHOW WARNINGS; // warnings do not persist, must be used upon seeing it
SOURCE <filename.sql>

// STRING FUNCTIONS
SELECT <CN> AS <user variable>, <CN> AS <user variable>, CONCAT(<CN>, ' ', <CN>) AS <user variable>;
SELECT CONCAT_WS(<seperator>, <CN>, <CN>) FROM <tablename>;
SELECT SUBSTRING(<string>, <number>, <number>); 
    // 1 number = ...XXX onwards; 2 numbers = XXXX... between A and B;
    // INDEXES START AT 1 NOT 0 lol;
    // negative indexes go backwards from the end then go forwards;
SELECT REPLACE(<targeted item>, <target>, <replaced item>);
