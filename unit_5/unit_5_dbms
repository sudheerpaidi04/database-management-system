UNIT-5: Indexing and Query Optimization
-------------------------------------------------------------------------------------------------------------

Query 5.1: Creating Primary and Secondary Indexes
Query Name: Index Creation and Management
Query Code - Part A: Create Table with Primary Index
CREATE TABLE employees (
  emp_id INT,
  first_name VARCHAR(50),
  last_name VARCHAR(50),
  dept VARCHAR(50),
  salary INT,
  hired_date DATE,
  PRIMARY KEY (emp_id)
) ENGINE=InnoDB;
Query Code - Part B: Create Secondary Indexes
-- Create non-unique secondary index on last_name
CREATE INDEX idx_lastname ON employees (last_name);

-- Create composite secondary index on (dept, salary)
CREATE INDEX idx_dept_salary ON employees(dept, salary);

-- List all indexes on table
SHOW INDEX FROM employees;
Query Output
Part A: Primary Index Created
Query: CREATE TABLE employees (...)
Result: Query OK, 1 row affected (0.01 sec)
Note: PRIMARY KEY (emp_id) creates clustered primary index

Part B: Secondary Indexes Created
Query: CREATE INDEX idx_lastname ON employees (last_name);
Result: Query OK, 0 rows affected (0.01 sec)

Query: CREATE INDEX idx_dept_salary ON employees(dept, salary);
Result: Query OK, 0 rows affected (0.01 sec)

Indexes on employees table:
Table      | Non_unique | Key_name       | Column_name
employees  | 0          | PRIMARY        | emp_id
employees  | 1          | idx_lastname   | last_name
employees  | 1          | idx_dept_salary| dept
employees  | 1          | idx_dept_salary| salary

------------------------------------------------------------------------------------------------------------

Query 5.2: Retrieve Data Using Indexes with EXPLAIN
Query Name: Index-Based Query Retrieval and Query Plan Analysis
Query Code - Insert Sample Data
INSERT INTO employees (first_name, last_name, dept, salary, hired_date) VALUES
('Alice','Kumar','R&D',80000,'2020-03-15'),
('Bob','Sharma','Sales',60000,'2019-08-01'),
('Carol','Kumar','R&D',85000,'2021-02-10'),
('Dave','Patel','Marketing',55000,'2018-11-20'),
('Eve','Sharma','Sales',62000,'2022-01-05');
Query Code - Query with Index Analysis
-- Analyze query plan
EXPLAIN SELECT * FROM employees WHERE last_name = 'Sharma';

-- Execute query
SELECT * FROM employees WHERE last_name = 'Sharma';
Query Output - EXPLAIN Analysis
EXPLAIN Output:
id  select_type  table       partitions  type  possible_keys   key          key_len  ref    rows  filtered  Extra
1   SIMPLE       employees   NULL        ref   idx_lastname    idx_lastname 203      const  2     100.00    NULL

Analysis:
- key = idx_lastname (confirms index was used)
- type = ref (index lookup returning matching rows)
- rows = 2 (MySQL estimates 2 matching rows)
- filtered = 100.00 (all rows matched the WHERE condition)
Query Output - SELECT Result
emp_id | first_name | last_name | dept  | salary | hired_date
2      | Bob        | Sharma    | Sales | 60000  | 2019-08-01
5      | Eve        | Sharma    | Sales | 62000  | 2022-01-05

----------------------------------------------------------------------------------------------------------------

Query 5.3: INSERT, UPDATE and Index Impact
Query Name: Data Modification and Index Maintenance
Query Code - Part A: INSERT and Index Impact
INSERT INTO employees (first_name, last_name, dept, salary, hired_date)
VALUES ('Frank','Kumar','R&D',78000,'2024-07-01');
Query Code - Part B: UPDATE Non-Indexed Column
UPDATE employees SET salary = salary + 2000 WHERE last_name = 'Sharma';
Query Code - Part C: UPDATE Indexed Column
UPDATE employees SET last_name = 'Sharma-Old' WHERE emp_id = 2;
Query Output
Part A: INSERT with Index Impact
Query: INSERT INTO employees VALUES (6, 'Frank', 'Kumar', ...)
Result: Query OK, 1 row affected (0.01 sec)

What happens:
✓ Row inserted into clustered table (via emp_id PRIMARY KEY)
✓ Secondary index entries automatically updated
✓ idx_lastname now includes entry for 'Kumar' pointing to Frank
✓ idx_dept_salary includes entry for ('R&D', 78000) pointing to Frank

Part B: UPDATE Non-Indexed Column
Query: UPDATE employees SET salary = salary + 2000 WHERE last_name = 'Sharma';
Result: Query OK, 2 rows affected (0.01 sec)
Rows matched: 2  Changed: 2

What happens:
- idx_lastname used to find rows with last_name='Sharma' (2 rows found)
- Table rows updated (salary + 2000)
- Secondary indexes remain unchanged (salary column not indexed alone)
- Minimal index impact

Part C: UPDATE Indexed Column
Query: UPDATE employees SET last_name = 'Sharma-Old' WHERE emp_id = 2;
Result: Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1

What happens:
- Primary index locates row (emp_id = 2)
- Old index entry deleted: idx_lastname entry for 'Sharma'
- Row updated in table
- New index entry inserted: idx_lastname entry for 'Sharma-Old'
- More I/O than updating non-indexed column

---------------------------------------------------------------------------------------------------------

Query 5.4: DELETE and Index Impact
Query Name: Data Deletion and Index Maintenance
Query Code - Part A: DELETE Row
DELETE FROM employees WHERE emp_id = 4; -- delete Dave
Query Code - Part B: DROP and Rebuild Indexes
-- Drop secondary index
DROP INDEX idx_lastname ON employees;

-- Recreate if needed
CREATE INDEX idx_lastname ON employees(last_name);

-- Force rebuild all indexes on table
ALTER TABLE employees ENGINE=InnoDB;
Query Output
Part A: DELETE Row
Query: DELETE FROM employees WHERE emp_id = 4;
Result: Query OK, 1 row affected (0.01 sec)

What happens:
✓ Row removed from clustered storage (PRIMARY index)
✓ All secondary index entries (idx_lastname, idx_dept_salary) automatically removed
✓ Cardinality and statistics updated

After DELETE - Remaining Rows:
emp_id | first_name | last_name      | dept      | salary | hired_date
1      | Alice      | Kumar          | R&D       | 80000  | 2020-03-15
2      | Bob        | Sharma-Old     | Sales     | 60000  | 2019-08-01
3      | Carol      | Kumar          | R&D       | 85000  | 2021-02-10
5      | Eve        | Sharma         | Sales     | 62000  | 2022-01-05
6      | Frank      | Kumar          | R&D       | 78000  | 2024-07-01

Note: Dave (emp_id=4) is deleted

Part B: Drop and Rebuild Indexes
Query: DROP INDEX idx_lastname ON employees;
Result: Query OK, 0 rows affected (0.01 sec)

Query: CREATE INDEX idx_lastname ON employees(last_name);
Result: Query OK, 0 rows affected (0.01 sec)

Query: ALTER TABLE employees ENGINE=InnoDB;
Result: Query OK, 0 rows affected (0.05 sec)
Result: ✓ All indexes rebuilt and optimized
