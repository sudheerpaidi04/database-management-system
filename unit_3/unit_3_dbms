UNIT-3: JOIN Operations and Set Operations
---------------------------------------------------------------------------------------------

Query 5: JOIN Operations
Query Name: Implementation of Various JOIN Operations
Query Code:
select * from tb1 inner join tb2 on tb1.rno=tb2.rno;
select * from tb1 left outer join tb2 on tb1.rno=tb2.rno;
select * from tb1 right outer join tb2 on tb1.rno=tb2.rno;
select * from tb1 natural join tb2;
select * from tb1 cross join tb2;
select t1.rno, t2.name from tb1 t1, tb1 t2 where t1.rno=t2.rno;
select * from tb1, tb2 where tb1.rno=tb2.rno;
Query Output:
JOIN Results:

INNER JOIN: 4 rows (matching records only)
LEFT OUTER JOIN: 5 rows (all from left + matches)
RIGHT OUTER JOIN: 4 rows (all from right + matches)
NATURAL JOIN: 4 rows (auto-matched on common column)
CROSS JOIN: 20 rows (5 × 4 Cartesian product)
SELF JOIN: 5 rows (table with itself)
EQUI JOIN: 4 rows (equality condition matching)

-----------------------------------------------------------------------------------------------------------

  
Query 6: SET Operations
Query Name: Implementation of Set Operations
Query Code:
select sname from sailors ... where bcolor='Red'
UNION
select sname from sailors ... where bcolor='Green';
-- Also: UNION ALL, INTERSECT, MINUS
Query Output:
SET Operation Results:

UNION (Red OR Green - No duplicates): 4 rows
Dustin, Horatio, Lubber, Ravi

UNION ALL (Red OR Green - With duplicates): 6 rows

INTERSECT (Both Red AND Green): 1 row
Horatio

MINUS (Red but NOT Green): 2 rows
Dustin, Lubber

-------------------------------------------------------------------------------------------------------


Query 7: Nested Subqueries
Query Name: Implementation of Nested and Correlated Subqueries
Query Code:
select s.sname from sailors s where s.sid IN (...);
select s.sname from sailors s where s.sid NOT IN (...);
select s.sid from sailors s where s.rating >= ALL (...);
select s.sid from sailors s where s.rating > ANY (...);
select s.sname from sailors s where EXISTS (...);
select s.sname from sailors s where NOT EXISTS (...);
Query Output:
Nested Query Results:

IN Operator: 3 rows (Dustin, Lubber, Ravi)
NOT IN Operator: 7 rows (Brutus, Andy, Horatio, etc.)
ALL Operator: 3 rows (Highest rating sailors)
ANY Operator: 3 rows (Better than Andy)
EXISTS: 3 rows (Reserved boat 103)
NOT EXISTS: 7 rows (Not reserved boat 103)


---------------------------------------------------------------------------------------------------------------



Query 8: Views Implementation
Query Name: Creating and Managing Database Views
Query Code:
create view my_view as select rollno, name from source_table;
insert into myview values(506, 'prathisha');
select * from myview;
delete from myview where rollno=506;
create view myview1 as select * from st1 with read only;
create view myview2 as select * from st1 where marks<101 with check option;
create or replace view myview as select * from Table1, Table2;
drop view viewname;
Query Output:
View Operations Results:

✓ CREATE VIEW: View created
✓ INSERT: 1 row inserted
✓ SELECT: Data retrieved from view
✓ DELETE: 1 row deleted
✓ READ ONLY VIEW: Prevents modifications
✓ CHECK OPTION VIEW: Validates WHERE clause
✓ ALTER VIEW: Structure modified
✓ DROP VIEW: View removed
