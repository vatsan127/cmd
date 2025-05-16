# PostgreSQL Cheat Sheet

## Database Operations

### Creating a Database
```sql
CREATE DATABASE database_name;
```

### Dropping a Database
```sql
DROP DATABASE [IF EXISTS] database_name;
```

### Connect to Database
```sql
\c database_name
```

## DDL (Data Definition Language)

### Table Operations

#### Create Table
```sql
CREATE TABLE table_name (
    column1 datatype1 [constraints],
    column2 datatype2 [constraints],
    ...
    [table_constraints]
);
```

#### Common Data Types
- `INTEGER` or `INT`: Whole numbers
- `BIGINT`: Large whole numbers
- `SMALLINT`: Small whole numbers
- `DECIMAL(p,s)` or `NUMERIC(p,s)`: Exact decimal numbers with precision p and scale s
- `REAL`, `FLOAT`: Floating point numbers
- `BOOLEAN`: true/false values
- `CHAR(n)`: Fixed-length character string
- `VARCHAR(n)`: Variable-length character string with limit
- `TEXT`: Variable unlimited length text
- `DATE`: Date (YYYY-MM-DD)
- `TIME`: Time (HH:MM:SS)
- `TIMESTAMP`: Date and time
- `TIMESTAMPTZ`: Date and time with timezone
- `INTERVAL`: Time interval
- `JSON`, `JSONB`: JSON data
- `UUID`: Universally unique identifier
- `BYTEA`: Binary data
- `ARRAY`: Array of values

#### Common Constraints
- `PRIMARY KEY`: Uniquely identifies each record
- `FOREIGN KEY`: Links to another table
- `UNIQUE`: Ensures values in a column are unique
- `NOT NULL`: Column cannot have NULL value
- `CHECK`: Ensures values meet specific conditions
- `DEFAULT`: Provides default value if none specified

#### Create Table with Constraints
```sql
CREATE TABLE employees (
    emp_id SERIAL PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    hire_date DATE DEFAULT CURRENT_DATE,
    salary DECIMAL(10,2) CHECK (salary > 0),
    department_id INT REFERENCES departments(dept_id)
);
```

#### Create Table from Another Table
```sql
CREATE TABLE new_table AS 
SELECT column1, column2 FROM existing_table
[WHERE condition];
```

#### Alter Table

Add Column:
```sql
ALTER TABLE table_name ADD COLUMN column_name datatype [constraints];
```

Drop Column:
```sql
ALTER TABLE table_name DROP COLUMN column_name;
```

Rename Column:
```sql
ALTER TABLE table_name RENAME COLUMN old_name TO new_name;
```

Change Column Data Type:
```sql
ALTER TABLE table_name ALTER COLUMN column_name TYPE new_datatype;
```

Add Constraint:
```sql
ALTER TABLE table_name ADD CONSTRAINT constraint_name constraint_definition;
```

Drop Constraint:
```sql
ALTER TABLE table_name DROP CONSTRAINT constraint_name;
```

Rename Table:
```sql
ALTER TABLE table_name RENAME TO new_table_name;
```

#### Drop Table
```sql
DROP TABLE [IF EXISTS] table_name [CASCADE | RESTRICT];
```

#### Truncate Table (Delete all rows without logging)
```sql
TRUNCATE TABLE table_name [CASCADE | RESTRICT];
```

### Index Management

#### Create Index
```sql
CREATE INDEX index_name ON table_name (column1, column2, ...);
```

#### Create Unique Index
```sql
CREATE UNIQUE INDEX index_name ON table_name (column1, column2, ...);
```

#### Create Partial Index
```sql
CREATE INDEX index_name ON table_name (column) WHERE condition;
```

#### Create B-tree Index (default)
```sql
CREATE INDEX index_name ON table_name USING BTREE (column);
```

#### Create Hash Index
```sql
CREATE INDEX index_name ON table_name USING HASH (column);
```

#### Create GIN Index (for arrays and JSON)
```sql
CREATE INDEX index_name ON table_name USING GIN (column);
```

#### Create GIST Index (for geometric data and full-text search)
```sql
CREATE INDEX index_name ON table_name USING GIST (column);
```

#### Drop Index
```sql
DROP INDEX [IF EXISTS] index_name;
```

### View Management

#### Create View
```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

#### Create Materialized View (stored physically)
```sql
CREATE MATERIALIZED VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

#### Refresh Materialized View
```sql
REFRESH MATERIALIZED VIEW view_name;
```

#### Drop View
```sql
DROP VIEW [IF EXISTS] view_name;
```

### Schema Management

#### Create Schema
```sql
CREATE SCHEMA schema_name;
```

#### Drop Schema
```sql
DROP SCHEMA [IF EXISTS] schema_name [CASCADE | RESTRICT];
```

### Sequence Management

#### Create Sequence
```sql
CREATE SEQUENCE sequence_name
[INCREMENT BY n]
[START WITH n]
[MINVALUE n | NO MINVALUE]
[MAXVALUE n | NO MAXVALUE]
[CACHE n]
[CYCLE | NO CYCLE];
```

#### Using Sequence
```sql
SELECT nextval('sequence_name');
SELECT currval('sequence_name');
SELECT setval('sequence_name', value);
```

#### Drop Sequence
```sql
DROP SEQUENCE [IF EXISTS] sequence_name;
```

## DML (Data Manipulation Language)

### SELECT Statement

#### Basic Select
```sql
SELECT column1, column2, ...
FROM table_name;
```

#### Select All Columns
```sql
SELECT * FROM table_name;
```

#### Select with Condition
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

#### Select with Distinct Values
```sql
SELECT DISTINCT column1, column2, ...
FROM table_name;
```

#### Sorting Results
```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column1 [ASC | DESC], column2 [ASC | DESC], ...;
```

#### Filtering Groups
```sql
SELECT column1, aggregate_function(column2)
FROM table_name
GROUP BY column1
HAVING condition;
```

#### Limit and Offset
```sql
SELECT column1, column2, ...
FROM table_name
LIMIT n OFFSET m;
```

#### Select with Joins

INNER JOIN:
```sql
SELECT t1.column1, t2.column2, ...
FROM table1 t1
INNER JOIN table2 t2 ON t1.common_field = t2.common_field;
```

LEFT JOIN:
```sql
SELECT t1.column1, t2.column2, ...
FROM table1 t1
LEFT JOIN table2 t2 ON t1.common_field = t2.common_field;
```

RIGHT JOIN:
```sql
SELECT t1.column1, t2.column2, ...
FROM table1 t1
RIGHT JOIN table2 t2 ON t1.common_field = t2.common_field;
```

FULL OUTER JOIN:
```sql
SELECT t1.column1, t2.column2, ...
FROM table1 t1
FULL OUTER JOIN table2 t2 ON t1.common_field = t2.common_field;
```

CROSS JOIN:
```sql
SELECT t1.column1, t2.column2, ...
FROM table1 t1
CROSS JOIN table2 t2;
```

SELF JOIN:
```sql
SELECT a.column1, b.column2, ...
FROM table_name a, table_name b
WHERE condition;
```

#### Subqueries
```sql
SELECT column1, column2, ...
FROM table_name
WHERE column_name IN (SELECT column_name FROM table_name WHERE condition);
```

#### Common Table Expressions (CTE)
```sql
WITH cte_name AS (
    SELECT column1, column2, ...
    FROM table_name
    WHERE condition
)
SELECT * FROM cte_name;
```

#### Recursive CTE
```sql
WITH RECURSIVE cte_name AS (
    -- Base case
    SELECT column1, column2, ... FROM table_name WHERE condition1
    UNION ALL
    -- Recursive case
    SELECT t.column1, t.column2, ... FROM table_name t
    INNER JOIN cte_name c ON t.column = c.column
    WHERE condition2
)
SELECT * FROM cte_name;
```

#### Window Functions
```sql
SELECT column1,
       aggregate_function(column2) OVER (
           PARTITION BY column3
           ORDER BY column4
           ROWS BETWEEN frame_start AND frame_end
       ) AS window_result
FROM table_name;
```

Common window functions:
- `ROW_NUMBER()`: Unique row number
- `RANK()`: Rank with gaps
- `DENSE_RANK()`: Rank without gaps
- `NTILE(n)`: Divide into n buckets
- `LEAD(column, offset, default)`: Access value from following row
- `LAG(column, offset, default)`: Access value from previous row
- `FIRST_VALUE(column)`: First value in window
- `LAST_VALUE(column)`: Last value in window

### INSERT Statement

#### Insert Single Row
```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```

#### Insert Multiple Rows
```sql
INSERT INTO table_name (column1, column2, ...)
VALUES 
    (value1, value2, ...),
    (value1, value2, ...),
    ...;
```

#### Insert from Select
```sql
INSERT INTO table_name (column1, column2, ...)
SELECT column1, column2, ... FROM source_table
[WHERE condition];
```

#### Insert with RETURNING
```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...)
RETURNING column1, column2, ...;
```

### UPDATE Statement

#### Basic Update
```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

#### Update with Subquery
```sql
UPDATE table_name
SET column1 = (SELECT column_x FROM another_table WHERE condition)
WHERE condition;
```

#### Update Multiple Tables (using FROM)
```sql
UPDATE table1
SET column1 = table2.column2
FROM table2
WHERE table1.common_column = table2.common_column;
```

#### Update with RETURNING
```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition
RETURNING column1, column2, ...;
```

### DELETE Statement

#### Basic Delete
```sql
DELETE FROM table_name
WHERE condition;
```

#### Delete with Subquery
```sql
DELETE FROM table_name
WHERE column_name IN (SELECT column_name FROM another_table WHERE condition);
```

#### Delete All Rows
```sql
DELETE FROM table_name;
```

#### Delete with RETURNING
```sql
DELETE FROM table_name
WHERE condition
RETURNING column1, column2, ...;
```

### UPSERT Statement (INSERT ... ON CONFLICT)

```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...)
ON CONFLICT (conflict_column)
DO UPDATE SET column1 = EXCLUDED.column1, ...;
```

#### Do Nothing on Conflict
```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...)
ON CONFLICT (conflict_column)
DO NOTHING;
```

## Transaction Control

### Begin a Transaction
```sql
BEGIN;
-- or
BEGIN TRANSACTION;
```

### Commit a Transaction
```sql
COMMIT;
-- or
END TRANSACTION;
```

### Rollback a Transaction
```sql
ROLLBACK;
```

### Save Point in a Transaction
```sql
SAVEPOINT savepoint_name;
```

### Rollback to a Save Point
```sql
ROLLBACK TO SAVEPOINT savepoint_name;
```

### Set Transaction Isolation Level
```sql
SET TRANSACTION ISOLATION LEVEL 
    { SERIALIZABLE | REPEATABLE READ | READ COMMITTED | READ UNCOMMITTED };
```

## Advanced Features

### Full-Text Search

#### Create Text Search Configuration
```sql
CREATE TEXT SEARCH CONFIGURATION config_name (
    PARSER = parser_name
);
```

#### Text Search with to_tsvector and to_tsquery
```sql
SELECT *
FROM table_name
WHERE to_tsvector('english', text_column) @@ to_tsquery('english', 'search_term');
```

#### Create GIN Index for Full-Text Search
```sql
CREATE INDEX idx_name ON table_name 
USING GIN (to_tsvector('english', text_column));
```

### JSON Operations

#### Query JSON Data
```sql
SELECT json_column->'key' FROM table_name;  -- returns JSON
SELECT json_column->>'key' FROM table_name; -- returns TEXT
```

#### JSON Array Elements
```sql
SELECT jsonb_array_elements(json_column) FROM table_name;
```

#### JSON Object Fields
```sql
SELECT jsonb_object_keys(json_column) FROM table_name;
```

### Hierarchical/Tree Queries

#### Recursive Query Example for Tree Structure
```sql
WITH RECURSIVE tree AS (
    -- Base case: get root node(s)
    SELECT id, name, parent_id, 0 AS level
    FROM nodes
    WHERE parent_id IS NULL
    
    UNION ALL
    
    -- Recursive case: get children
    SELECT n.id, n.name, n.parent_id, t.level + 1
    FROM nodes n
    JOIN tree t ON n.parent_id = t.id
)
SELECT * FROM tree ORDER BY level, id;
```

### Common Aggregate Functions

```sql
SELECT 
    COUNT(*),
    COUNT(column),
    SUM(column),
    AVG(column),
    MAX(column),
    MIN(column),
    STRING_AGG(column, delimiter),
    ARRAY_AGG(column),
    JSON_AGG(column),
    JSONB_AGG(column),
    PERCENTILE_CONT(fraction) WITHIN GROUP (ORDER BY column),
    PERCENTILE_DISC(fraction) WITHIN GROUP (ORDER BY column),
    STDDEV(column),
    VARIANCE(column)
FROM table_name
GROUP BY grouping_column;
```

### Conditional Expressions

#### CASE Expression
```sql
SELECT 
    column1,
    CASE 
        WHEN condition1 THEN result1
        WHEN condition2 THEN result2
        ...
        ELSE result_else
    END AS derived_column
FROM table_name;
```

#### COALESCE Function
```sql
SELECT COALESCE(column1, column2, ..., default_value) FROM table_name;
```

#### NULLIF Function
```sql
SELECT NULLIF(expression1, expression2) FROM table_name;
```

#### GREATEST and LEAST Functions
```sql
SELECT GREATEST(value1, value2, ...) FROM table_name;
SELECT LEAST(value1, value2, ...) FROM table_name;
```

## Role and Privilege Management

### Create Role/User
```sql
CREATE ROLE role_name [WITH options];
CREATE USER user_name [WITH options];
```

Options include:
- `SUPERUSER | NOSUPERUSER`
- `CREATEDB | NOCREATEDB`
- `CREATEROLE | NOCREATEROLE`
- `LOGIN | NOLOGIN`
- `PASSWORD 'password'`
- `VALID UNTIL 'timestamp'`

### Grant Privileges
```sql
GRANT privilege [, ...] 
ON object_name
TO role_name;
```

Privileges include:
- `SELECT`
- `INSERT`
- `UPDATE`
- `DELETE`
- `TRUNCATE`
- `REFERENCES`
- `TRIGGER`
- `CREATE`
- `CONNECT`
- `TEMPORARY`
- `EXECUTE`
- `USAGE`
- `ALL PRIVILEGES`

### Revoke Privileges
```sql
REVOKE privilege [, ...] 
ON object_name
FROM role_name;
```

### Alter Role/User
```sql
ALTER ROLE role_name WITH options;
```

### Drop Role/User
```sql
DROP ROLE [IF EXISTS] role_name;
```
