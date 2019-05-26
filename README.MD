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
    FOREIGN KEY(<CN>) REFERENCES <TN>(<CN>) // creates a parent relation to this child
    ON DELETE CASCADE // specifies if the parent is deleted, delete this child too
    UNIQUE // every column in the same row must be unique
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
SELECT REVERSE(<target>); // hello becomes olleh
SELECT CHAR_LENGTH(<target>); // counts the number of chars in a string
SELECT UPPER(<target>); // converts to all caps
SELECT LOWER(<target>); // converts to all lowercase

// SEARCH REFINEMENT
SELECT DISTINCT * FROM <tablename>; // omits similiar value
SELECT * FROM <tablename> ORDER BY <CN>; // sorts by CN
    // ascending by default
    ** Extra properties for Order By**
    ORDER BY <CN> DESC; // descending, ASC for ascending
    ORDER BY <number> // number selects the order based on queue
    ORDER BY <CN>,<CN> // sorts by first CN then by second CN
SELECT * FROM <tablename> LIMIT <number>; // 2 numbers = 1st start row, 2nd how far to go (NOT A-B)
    // 0 is the starting array number lol
    // to take all rows select a gigantic 2nd number lol
SELECT * FROM <tablename> WHERE <CN> LIKE '<search query>'; // case insensitive
    ** Extra properties for Like **
    WHERE <CN> LIKE '%<search query>%'; // % = wildcards, anything before or after query
    WHERE <CN> LIKE '____'; // _ = exactly 1 character long
    WHERE <CN> LIKE '%\%%'; // \<query> = ESCAPE CHARACTER, will not use its innate ability
    WHERE <subquery> // refer to subquery section
    
// AGGREGATE FUNCTIONS
SELECT COUNT(*) FROM <tablename>; // counts the number of cn or * for everything
    // SELECT <CN>, COUNT(*) FROM <database> GROUP BY <CN>; // counts the objects created from GROUP BY query
SELECT * FROM <tablename> GROUP BY <tablename>; "summarizes or aggregates identical  data into single rows"
SELECT MIN/MAX(<CN>) FROM <tablename>;
SELECT SUM(<CN>) FROM <tablename>;
SELECT AVG(<CN>) FROM <tablename>;
ROUND(<values>,<what decimal place>);

// SUBQUERY
SELECT * FROM <tablename> WHERE <CN> = (<query>) // "SELECT MIN(<CN>) FROM books"

// DATATYPES
VARCHAR(<INT value>); // up to INT value number of characters
CHAR(<INT value>); // exactly, too much = truncated, too little = added spaces
INT;
DECIMAL(<INT value>, <INT value>); // arg 1 = max number of digits, arg 2 = max decimal
    // too large of a number will give the max value NOT truncate
    // the decimal place are always there
    // decimals are rounded up or down
    // best precision, most memory
DOUBLE // precision issues up to 15 digits, medium memory
FLOAT // precision issues up to 7 digits, smallest memory
DATE // 'YYYY-MM-DD' Format // no time stored
TIME // 'HH:MM:SS' Format // no date stored
DATETIME // 'YYYY-MM-DD HH:MM:SS'
CURDATE() // gives current date
CURTIME() // gives current time
NOW() // gives current date time
DAY() // retrieves day i.e DAY('1983-10-15') = 15
DAYNAME() //retrieves day name i.e DAYNAME('1983-10-15') = Saturday
DAYOFWEEK() // retrieves day number in week i.e DAYOFWEEK('1983-10-15') = 7 (Sunday = 1)
DAYOFYEAR() // retrieves day number in year i.e DAYOFYEAR('1983-10-15') = 288
MONTH()
MONTHNAME()
YEAR(4)
HOUR() MINUTE() SECOND()
DATE_FORMAT(<date>, <format specifiers>) // check documentation for specifiers i.e %m 
DATEDIFF() // result will be in days only, need to converts
DATE_ADD or SUB(<date>, INTERVAL <interval amount>) // INTERVAL 1 SECOND/DAY/MONTH
+/- sign
TIMESTAMP // range is 1970 - 2038 vs DATETIME which goes 1000 - 9999
    // very useful current time property = changed_at TIMESTAMP DEFAULT NOW() ON UPDATE NOW();

// LOGICAL OPERATORS
=; // equal
!=; // not equal
WHERE NOT LIKE '<condition>';
WHERE LIKE '<condition>';
>; // greater than
<; // lesser than
>=; // greater than or equal to
<=; // lesser than or equal to
AND or &&; // combining queries, must be both true
OR or || // combinging queries, either can be true
BETWEEN <condition 1> AND <condition 2> 
    or <condition 1> >= <condition 2> AND <condition 1> <= <condition 3>; 
    // searches between
    // for dates, use CAST() to convert datatype to be the same i.e DATETIME vs TIMESTAMP
NOT BETWEEN; // basically above but opposite
CAST(<values> AS <datatype>); // converts value input into another datatype
WHERE <value> IN (<value>, <value>, <value> etc); // check multiple ORs in one go
NOT IN; // basically multiple ANDs not equal to
MODULO or %; // divides and returns the remainder i.e 20%3 = (6x3) + 2
IFNULL(<query>, <true statement>) // checks if query is null and returns a default
WHERE <CN> IS NULL // cant use WHERE <CN> = NULL / 'NULL' because null is a cunt

// CASE STATEMENTS
CASE WHEN <query> THEN <if true> WHEN <query> THEN <if true> ELSE <if all false> END; // basically case statements
    // NO COMMA between WHEN statements (as comma is process in SELECT)




// MySQL relationships

One to one // not common
One to many // most common
Many to many // relatively common
PRIMARY KEY + AUTO_INCREMENT = special ID
FOREIGN KEY = to specify that the id references another special id
    // put as a seperate line declaration after declaring the <CN>


// JOINS
SELECT * FROM <TN>, <TN>; // Cross join, not very used
SELECT * FROM <TN>, <TN> WHERE <TN>.<CN> = <CN>; // i.e customers.id = orders.customer_id
    // AKA implicit inner join, used often
    
// INNER JOINS
SELECT * FROM <TN> JOIN <TN> ON <query>; // functions same as above
    // Technically called INNER JOIN, JOIN by itself assumes INNER type
    // AKA explicit inner join, used the most
    // Between A and B, finds and outputs the common grounds i.e overlapping cirlce


// LEFT JOINS
SELECT * FROM <TN> LEFT JOIN <TN> ON <query>; //
    // Between A and B, finds and outputs everything from A with any common grounds from B i.e A + overlapping B circle

// RIGHT JOINS
SELECT * FROM <TN> RIGHT JOIN <TN> ON <query>; //
    // Literally the same as Left join but on right lol, you can just swap B and A on left join to achieve the same results
    // The data is the same but the displayed data is different i.e left side and right side

// DATABASE TRIGGERS

SHOW TRIGGERS;
DROP TRIGGER <trigger_name>;


DELIMITER $$

CREATE TRIGGER trigger_name
    trigger_time trigger_event ON table_name FOR EACH ROW
    BEING
        IF <query>
        THEN
            SIGNAL SQLSTATE '<error code>'
                SET MESSAGE_TEXT = '<text>'
        END IF;
    END;
$$

DELIMITER ;

trigger_time = BEFORE, AFTER
trigger_event = INSERT, UPDATE, DELETE
table_name = <TN>
NEW.<cn> = refers to the expected inserting data, data provided to sql // IF NEW.age < 18
SIGNAL SQLSTATE '<error code>' = numeric error code (mysql's error)+ five character SQLSTATE values (refer to mysql docs) // 45000 unhandled user defined exception
SET MESSAGE_TEXT = custom text to describe error
DELIMITER <identifiers> = to tell sql to change the end of code logic, basically end code at identifiers not semicolon // example above resets delimiter to semicolon


// EXTRA EXTRA
SELECT <CN> FROM <TN> UNION SELECT <CN> FROM <TN> // selects two tables' column and find distinct stuff then merge them together
SELECT * FROM <TN> GROUP BY <CN> HAVING <aggregate function>; // SELECT userId, AVG(duration)from sessions GROUP BY userId HAVING COUNT(userId)>1
    // same as WHERE except can be used with aggregate functions
IS NOT NULL
IS
NOT IN
 // SELECT name FROM employees WHERE id NOT IN(SELECT managerId FROM employees WHERE managerid IS NOT null);






