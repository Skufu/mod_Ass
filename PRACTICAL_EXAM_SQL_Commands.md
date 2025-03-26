# SQL Commands for PRACTICAL_EXAM

## Task 1: Create database file

```sql
-- 1. Create database file PRACTICAL_EXAM_Lastname
CREATE DATABASE PRACTICAL_EXAM_Lastname;
GO
USE PRACTICAL_EXAM_Lastname;
GO
```

## Task 2: Create Tables 1.0, 2.0, 3.0, and 4.0

```sql
-- Create Table 1.0 (AUTHOR)
CREATE TABLE AUTHOR (
    au_id VARCHAR(11) PRIMARY KEY,
    au_lname VARCHAR(20) NOT NULL,
    au_fname VARCHAR(20) NOT NULL,
    address VARCHAR(40),
    city VARCHAR(20),
    state CHAR(2)
);
GO

-- Create Table 2.0 (TITLE)
CREATE TABLE TITLE (
    title_id VARCHAR(6) PRIMARY KEY,
    title VARCHAR(80) NOT NULL,
    type VARCHAR(12),
    price MONEY,
    pub_id INT
);
GO

-- Create Table 3.0 (PUBLISHER)
CREATE TABLE PUBLISHER (
    pub_id INT PRIMARY KEY,
    pub_name VARCHAR(40) NOT NULL,
    city VARCHAR(20)
);
GO

-- Create Table 4.0 (AUTHOR_TITLE)
CREATE TABLE AUTHOR_TITLE (
    au_id VARCHAR(11),
    title_id VARCHAR(6),
    PRIMARY KEY (au_id, title_id),
    FOREIGN KEY (au_id) REFERENCES AUTHOR(au_id),
    FOREIGN KEY (title_id) REFERENCES TITLE(title_id)
);
GO
```

## Sample Data Insertion

```sql
-- Insert data into AUTHOR table
INSERT INTO AUTHOR VALUES('172-32-1176', 'White', 'Johnson', '10932 Bigge Rd.', 'Menlo Park', 'CA');
INSERT INTO AUTHOR VALUES('213-46-8915', 'Green', 'Marjorie', '309 63rd St. #411', 'Oakland', 'CA');
INSERT INTO AUTHOR VALUES('238-95-7766', 'Carson', 'Cheryl', '589 Darwin Ln.', 'Berkeley', 'CA');
INSERT INTO AUTHOR VALUES('267-41-2394', 'O''Leary', 'Michael', '22 Cleveland Av. #14', 'San Jose', 'CA');
INSERT INTO AUTHOR VALUES('274-80-9391', 'Straight', 'Dean', '5420 College Av.', 'Oakland', 'CA');
INSERT INTO AUTHOR VALUES('341-22-1782', 'Smith', 'Meander', '10 Mississippi Dr.', 'Lawrence', 'KS');
INSERT INTO AUTHOR VALUES('409-56-7008', 'Bennet', 'Abraham', '6223 Bateman St.', 'Berkeley', 'CA');
INSERT INTO AUTHOR VALUES('427-17-2319', 'Dull', 'Ann', '3410 Blonde St.', 'Palo Alto', 'CA');
INSERT INTO AUTHOR VALUES('472-27-2349', 'Gringlesby', 'Burt', 'PO Box 792', 'Covelo', 'CA');
INSERT INTO AUTHOR VALUES('486-29-1786', 'Locksley', 'Charlene', '18 Broadway Av.', 'San Francisco', 'CA');
GO

-- Insert data into PUBLISHER table
INSERT INTO PUBLISHER VALUES(736, 'New Moon Books', 'Boston');
INSERT INTO PUBLISHER VALUES(877, 'Binnet & Hardley', 'Washington');
INSERT INTO PUBLISHER VALUES(1389, 'Algodata Infosystems', 'Berkeley');
INSERT INTO PUBLISHER VALUES(1622, 'Five Lakes Publishing', 'Chicago');
INSERT INTO PUBLISHER VALUES(1756, 'Ramona Publishers', 'Dallas');
INSERT INTO PUBLISHER VALUES(9901, 'GGG&G', 'München');
INSERT INTO PUBLISHER VALUES(9952, 'Scootney Books', 'New York');
INSERT INTO PUBLISHER VALUES(9999, 'Lucerne Publishing', 'Paris');
GO

-- Insert data into TITLE table
INSERT INTO TITLE VALUES('BU1032', 'The Busy Executive''s Database Guide', 'business', 19.99, 1389);
INSERT INTO TITLE VALUES('BU1111', 'Cooking with Computers', 'business', 11.95, 1389);
INSERT INTO TITLE VALUES('BU2075', 'You Can Combat Computer Stress!', 'business', 2.99, 736);
INSERT INTO TITLE VALUES('BU7832', 'Straight Talk About Computers', 'business', 19.99, 1389);
INSERT INTO TITLE VALUES('MC2222', 'Silicon Valley Gastronomic Treats', 'mod_cook', 19.99, 877);
INSERT INTO TITLE VALUES('MC3021', 'The Gourmet Microwave', 'mod_cook', 2.99, 877);
INSERT INTO TITLE VALUES('MC3026', 'The Psychology of Computer Cooking', 'UNDECIDED', NULL, 877);
INSERT INTO TITLE VALUES('PC1035', 'But Is It User Friendly?', 'popular_comp', 22.95, 1389);
INSERT INTO TITLE VALUES('PC8888', 'Secrets of Silicon Valley', 'popular_comp', 20.00, 1389);
INSERT INTO TITLE VALUES('PC9999', 'Net Etiquette', 'popular_comp', NULL, 1389);
INSERT INTO TITLE VALUES('PS2091', 'Is Anger the Enemy?', 'psychology', 10.95, 736);
INSERT INTO TITLE VALUES('MC3027', 'The Psychology of Computer Cooking', 'UNDECIDED', NULL, 877);
GO

-- Insert data into AUTHOR_TITLE table
INSERT INTO AUTHOR_TITLE VALUES('172-32-1176', 'PS2091');
INSERT INTO AUTHOR_TITLE VALUES('213-46-8915', 'BU1032');
INSERT INTO AUTHOR_TITLE VALUES('213-46-8915', 'BU2075');
INSERT INTO AUTHOR_TITLE VALUES('238-95-7766', 'PC1035');
INSERT INTO AUTHOR_TITLE VALUES('267-41-2394', 'BU1111');
INSERT INTO AUTHOR_TITLE VALUES('267-41-2394', 'TC7777');
INSERT INTO AUTHOR_TITLE VALUES('274-80-9391', 'BU7832');
INSERT INTO AUTHOR_TITLE VALUES('409-56-7008', 'BU1032');
INSERT INTO AUTHOR_TITLE VALUES('427-17-2319', 'PC8888');
INSERT INTO AUTHOR_TITLE VALUES('472-27-2349', 'TC7777');
GO
```

## Task 3: Perform the following queries

### a. Display all Book IDs, Book Titles and Book Prices
```sql
SELECT title_id AS 'Book ID', title AS 'Book Title', price AS 'Book Price'
FROM TITLE;
```

### b. Display the Address, City and State of Mr. Abraham Bennet
```sql
SELECT address AS 'Address', city AS 'City', state AS 'State'
FROM AUTHOR
WHERE au_fname = 'Abraham' AND au_lname = 'Bennet';
```

### c. Display the book's price of "The Busy Executive's Database Guide"
```sql
SELECT price AS 'Book Price'
FROM TITLE
WHERE title = 'The Busy Executive''s Database Guide';
```

### d. Display all Publisher's IDs and Publisher's Names living at Boston, New York or Paris
```sql
SELECT p.pub_id AS 'Publisher ID', p.pub_name AS 'Publisher Name'
FROM PUBLISHER p
WHERE p.city IN ('Boston', 'New York', 'Paris');
```

### e. Display the Book Titles written by Author's ID "213-46-8915"
```sql
SELECT t.title AS 'Book Title'
FROM TITLE t
JOIN AUTHOR_TITLE at ON t.title_id = at.title_id
WHERE at.au_id = '213-46-8915';
```

### f. Determine the number of authors living in the state of CA
```sql
SELECT COUNT(*) AS 'Number of Authors in CA'
FROM AUTHOR
WHERE state = 'CA';
```

### g. Display the Book Title of Meander Smith
```sql
SELECT t.title AS 'Book Title'
FROM TITLE t
JOIN AUTHOR_TITLE at ON t.title_id = at.title_id
JOIN AUTHOR a ON at.au_id = a.au_id
WHERE a.au_fname = 'Meander' AND a.au_lname = 'Smith';
```

### h. Display the Book Title of the most expensive book published by Algodata Infosystems
```sql
SELECT TOP 1 t.title AS 'Most Expensive Book'
FROM TITLE t
JOIN PUBLISHER p ON t.pub_id = p.pub_id
WHERE p.pub_name = 'Algodata Infosystems'
ORDER BY t.price DESC;
```

### i. Display author's name who did not publish anything
```sql
SELECT a.au_fname + ' ' + a.au_lname AS 'Author Name'
FROM AUTHOR a
LEFT JOIN AUTHOR_TITLE at ON a.au_id = at.au_id
WHERE at.au_id IS NULL;
```

### j. Determine the number of books marked as Undecided under Type
```sql
SELECT COUNT(*) AS 'Number of Undecided Books'
FROM TITLE
WHERE type = 'UNDECIDED';
```

## Task 4: Add the following data into Autor_Title table
```sql
INSERT INTO AUTHOR_TITLE VALUES('111-11-1111', 'MC3027');
```

## Task 5: Change the city of Publisher Id 9999, from Paris to Cabuyao
```sql
UPDATE PUBLISHER
SET city = 'Cabuyao'
WHERE pub_id = 9999;
```

## Task 6: Remove all data of Title table permanently
```sql
DELETE FROM AUTHOR_TITLE;
DELETE FROM TITLE;
```

## Task 7: Remove permanently Johnson White from your database file
```sql
DELETE FROM AUTHOR_TITLE
WHERE au_id = '172-32-1176';
DELETE FROM AUTHOR
WHERE au_id = '172-32-1176';
```

## Task 8: Remove Publisher Table permanently
```sql
DROP TABLE AUTHOR_TITLE;
DROP TABLE TITLE;
DROP TABLE PUBLISHER;
```

## Task 9: Modify the field size of Author's Lastname to 30
```sql
ALTER TABLE AUTHOR
ALTER COLUMN au_lname VARCHAR(30);
```

## Task 10: Remove Author's state field permanently from Author table
```sql
ALTER TABLE AUTHOR
DROP COLUMN state;
``` 