UNIT-4: Database Normalization and Transaction Management
------------------------------------------------------------------------------------------------------------

Query 4.1: Database Normalization - Denormalized vs Normalized Tables
Query Name: Create University Database and Implement Normalization
Query Code - Part A: Create Denormalized Table
create database university;
use university;

CREATE TABLE univ_denorm (
  StudentID INTEGER, StudentName TEXT, Major TEXT,
  CourseID TEXT, CourseName TEXT, Credits INTEGER,
  EnrollmentDate TEXT,
  InstructorID INTEGER, InstructorName TEXT, Phone TEXT
);
Query Code - Part B: Insert Denormalized Data
INSERT INTO univ_denorm
(StudentID, StudentName, Major, CourseID, CourseName, Credits, EnrollmentDate, InstructorID, InstructorName, Phone)
VALUES
(1, 'Alice Smith', 'Computer Science', 'C101', 'Intro to CS', 3, '2025-09-01', 10, 'Dr. Adams', '555-0100'),
(1, 'Alice Smith', 'Computer Science', 'C101', 'Intro to CS', 3, '2025-09-01', 11, 'Dr. Baker', '555-0111'),
(2, 'Bob Jones', 'Mathematics', 'C101', 'Intro to CS', 3, '2025-09-03', 10, 'Dr. Adams', '555-0100'),
(2, 'Bob Jones', 'Mathematics', 'C101', 'Intro to CS', 3, '2025-09-03', 11, 'Dr. Baker', '555-0111'),
(1, 'Alice Smith', 'Computer Science', 'C102', 'Calculus I', 4, '2025-09-02', 11, 'Dr. Baker', '555-0111'),
(3, 'Carol Lee', 'Physics', 'C103', 'Physics I', 4, '2025-09-04', 12, 'Dr. Clark', '555-0122');
Query Code - Part C: Normalize to 2NF
CREATE TABLE Students AS
  SELECT DISTINCT StudentID, StudentName, Major FROM univ_denorm;

CREATE TABLE Courses AS
  SELECT DISTINCT CourseID, CourseName, Credits FROM univ_denorm;

CREATE TABLE Instructors AS
  SELECT DISTINCT InstructorID, InstructorName, Phone FROM univ_denorm;

CREATE TABLE Enrollments AS
  SELECT DISTINCT StudentID, CourseID, EnrollmentDate FROM univ_denorm;

CREATE TABLE Course_Instructors AS
  SELECT DISTINCT StudentID, CourseID, InstructorID FROM univ_denorm;
Query Code - Part D: Verify 5NF with JOIN
SELECT e.StudentID, s.StudentName, s.Major,
       e.CourseID, c.CourseName, c.Credits, e.EnrollmentDate,
       ci.InstructorID, i.InstructorName, i.Phone
FROM Enrollments e
JOIN Students s ON e.StudentID = s.StudentID
JOIN Courses c ON e.CourseID = c.CourseID
JOIN Course_Instructors ci ON c.CourseID = ci.CourseID
JOIN Instructors i ON ci.InstructorID = i.InstructorID
ORDER BY e.StudentID, e.CourseID, ci.InstructorID;
Query Output - Denormalized Table
StudentID | StudentName    | Major               | CourseID | CourseName  | Credits | EnrollmentDate | InstructorID | InstructorName | Phone
1          | Alice Smith    | Computer Science   | C101     | Intro to CS | 3       | 2025-09-01     | 10           | Dr. Adams      | 555-0100
1          | Alice Smith    | Computer Science   | C101     | Intro to CS | 3       | 2025-09-01     | 11           | Dr. Baker      | 555-0111
2          | Bob Jones      | Mathematics        | C101     | Intro to CS | 3       | 2025-09-03     | 10           | Dr. Adams      | 555-0100
2          | Bob Jones      | Mathematics        | C101     | Intro to CS | 3       | 2025-09-03     | 11           | Dr. Baker      | 555-0111
1          | Alice Smith    | Computer Science   | C102     | Calculus I  | 4       | 2025-09-02     | 11           | Dr. Baker      | 555-0111
3          | Carol Lee      | Physics            | C103     | Physics I   | 4       | 2025-09-04     | 12           | Dr. Clark      | 555-0122
Query Output - Normalized Tables (2NF)
Students Table:
StudentID | StudentName | Major
1         | Alice Smith | Computer Science
2         | Bob Jones   | Mathematics
3         | Carol Lee   | Physics

Courses Table:
CourseID | CourseName  | Credits
C101     | Intro to CS | 3
C102     | Calculus I  | 4
C103     | Physics I   | 4

Instructors Table:
InstructorID | InstructorName | Phone
10           | Dr. Adams      | 555-0100
11           | Dr. Baker      | 555-0111
12           | Dr. Clark      | 555-0122

Enrollments Table:
StudentID | CourseID | EnrollmentDate
1         | C101     | 2025-09-01
2         | C101     | 2025-09-03
1         | C102     | 2025-09-02
3         | C103     | 2025-09-04

-----------------------------------------------------------------------------

Query 4.2A: Data Control Language (DCL) - GRANT and REVOKE
Query Name: Access Control with DCL Commands
Query Code
-- Step 1: DBA creates a user
CREATE USER student_user IDENTIFIED BY password;
GRANT CREATE SESSION TO student_user;

-- Step 2: DBA grants object privileges
GRANT SELECT, INSERT ON Students TO student_user;

-- Step 3: student_user accesses Students table
SELECT * FROM Students;
INSERT INTO Students VALUES (101, 'John', 'CSE');

-- Step 4: DBA revokes privilege
REVOKE INSERT ON Students FROM student_user;
-- Now student_user can SELECT but cannot INSERT
Query Output
Step 1: User Created
Command: CREATE USER student_user IDENTIFIED BY password;
Result: ✓ User created
Command: GRANT CREATE SESSION TO student_user;
Result: ✓ Session permission granted

Step 2: Privileges Granted
Command: GRANT SELECT, INSERT ON Students TO student_user;
Result: ✓ SELECT and INSERT privileges granted

Step 3: User Access Successful
Command: SELECT * FROM Students;
Result: ✓ Retrieved all student records
Command: INSERT INTO Students VALUES (101, 'John', 'CSE');
Result: ✓ 1 row inserted

Step 4: Privilege Revoked
Command: REVOKE INSERT ON Students FROM student_user;
Result: ✓ INSERT privilege revoked
Now: student_user can SELECT but cannot INSERT into Students
Query 4.2B: Transaction Control Language (TCL) - COMMIT, SAVEPOINT, ROLLBACK
Query Name: Transaction Management with TCL Commands
Query Code - Part A: COMMIT
INSERT INTO Students VALUES (101, 'Ravi', 'CSE');
INSERT INTO Students VALUES (102, 'Anita', 'ECE');
COMMIT; -- permanently saves the above two insertions
Query Code - Part B: SAVEPOINT and Partial Rollback
INSERT INTO Students VALUES (103, 'Mahesh', 'IT');
SAVEPOINT sp1;

INSERT INTO Students VALUES (104, 'Sita', 'EEE');
SAVEPOINT sp2;

DELETE FROM Students WHERE StudentID = 101;

-- Rollback to sp1 (undo operations after sp1)
ROLLBACK TO sp1;
Query Code - Part C: Full ROLLBACK
-- Start new transaction
INSERT INTO Students VALUES (105, 'Priya', 'CSE');
INSERT INTO Students VALUES (106, 'Vikram', 'ECE');

-- Undo all uncommitted changes
ROLLBACK;
Query Output
COMMIT Example:
Query: INSERT INTO Students VALUES (101, 'Ravi', 'CSE');
Result: ✓ 1 row inserted
Query: INSERT INTO Students VALUES (102, 'Anita', 'ECE');
Result: ✓ 1 row inserted
Query: COMMIT;
Result: ✓ Committed - Changes are permanent

SAVEPOINT Example:
Query: INSERT INTO Students VALUES (103, 'Mahesh', 'IT');
Result: ✓ 1 row inserted
Query: SAVEPOINT sp1;
Result: ✓ Savepoint created
Query: INSERT INTO Students VALUES (104, 'Sita', 'EEE');
Result: ✓ 1 row inserted
Query: SAVEPOINT sp2;
Result: ✓ Savepoint created
Query: DELETE FROM Students WHERE StudentID = 101;
Result: ✓ 1 row deleted
Query: ROLLBACK TO sp1;
Result: ✓ Rolled back to sp1 (deleted and INSERT of Sita undone)

ROLLBACK Example:
Query: ROLLBACK;
Result: ✓ All uncommitted changes rolled back
Data returned to state before transaction started
