UNIT-2: Data Manipulation Language (DML) Commands
--------------------------------------------------------------------------------------------------------------

Query 3: Students Table DML Operations
Query Name: Students Table Creation with INSERT, SELECT, UPDATE, DELETE
Query Code:
create table students ( rollno varchar2(30), name varchar2(30));
insert into students values('24B11CS234','Bala');
insert into students values('24B11CS381','Kiran');
select * from students;
select name from students;
select * from students where rollno='24B11CS234';
delete from students where rollno='24B11CS381';
update students set name='Bala Raju' where rollno='24B11CS234';
Query Output:
Operation Results:

1. CREATE TABLE: Table Created ✓
2. INSERT: 2 rows inserted ✓
3. SELECT ALL: Returns Bala and Kiran records
4. SELECT SPECIFIC: Returns name column only
5. SELECT WHERE: Returns matching record (Bala)
6. DELETE: 1 row deleted ✓
7. UPDATE: 1 row updated ✓

Final Table: ROLLNO=24B11CS234, NAME=Bala Raju


----------------------------------------------------------------------------------------------

  
Query 4: Aggregate Functions and GROUP BY
Query Name: Implementation of Aggregate Functions (AVG, SUM, MAX, MIN, COUNT)
Query Code:
Select AVG(amount) from company;
Select SUM(amount) from company;
Select Max(amount) from company;
Select Min(amount) from company;
Select Count(*) from company;

select company, sum(amount) from company group by company;
select company, count() from company group by company having count()>1;
select company, sum(amount) from company group by company having sum(amount)>10000;
Query Output:
Aggregate Results:
AVG(amount) = 6800
SUM(amount) = 34000
MAX(amount) = 10000
MIN(amount) = 2000
COUNT(*) = 5

GROUP BY Results:
wipro: SUM=7000, COUNT=2
ibm: SUM=8000, COUNT=1
dell: SUM=19000, COUNT=2

HAVING Results:
COUNT > 1: wipro (2), dell (2)
SUM > 10000: dell (19000)
