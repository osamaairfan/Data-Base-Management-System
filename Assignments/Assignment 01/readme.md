## Question #2:
1. `SELECT STUDENT.sname  
   FROM STUDENT  
   JOIN ENROLLED ON STUDENT.snum = ENROLLED.snum   
   JOIN CLASS ON ENROLLED.cname = CLASS.cname  
   JOIN FACULTYON CLASS.fid = FACULTY.fid  
   WHERE STUDENT.level = 'JR' AND FACULTY.fname = 'I. Teach';  ` 

2.  `SELECT MAX(STUDENT.age) AS oldest_age   
   FROM STUDENT  
   JOIN Enrolled ON STUDENT.snum = Enrolled.snum  
   JOIN Class ON Enrolled.cname = Class.name  
   JOIN Faculty ON Class.fid = Faculty.fid  
   WHERE Student.major = 'History' OR Faculty.fname = 'I. Teach';  `

3. `SELECT cname FROM ENROLLED  
   JOIN CLASS ON Student.snum = Enrolled.snum  
   WHERE cname = ‘R128’ OR snum >= 5;`  

4. `SELECT s.name FROM Student S  
   JOIN Enrolled E1 ON S.snum = E1.snum  
   JOIN Enrolled E2 ON S.snum = E2.snum  
   JOIN Class C1 ON E1.cname = C1.name  
   JOIN Class C2 ON E2.cname = C2.name    
   WHERE C1.meets_at = C2.meets_at AND E1.cname <> E2.cname; ` 

5. `SELECT F.fname
   FROM Faculty F
   WHERE NOT EXISTS (
       SELECT C1.room
       FROM Class C1
       WHERE NOT EXISTS (
           SELECT 1
           FROM Class C2
           WHERE C2.room = C1.room
           AND C2.fid = F.fid
       )
   );`

6. `SELECT F.fname AS FacultyName
   FROM Faculty F
   JOIN Class C ON F.fid = C.fid
   GROUP BY F.fname
   HAVING COUNT(C.name) < 5;`

7. `SELECT level, AVG(age) AS AVERAGEAGE
   FROM STUDENT
   GROUP BY level;`

8. `SELECT level, AVG(age) AS AVERAGEAGE
   FROM STUDENT
   WHERE level != JR
   GROUP BY level;`

9. `SELECT fname, COUNT(C.fid)
   FROM FACULTY
   JOIN FACULTY ON F.fid = C.fid
   GROUP BY fname
   HAVING C.name = ‘R128’;`

10. `SELECT sname, COUNT(E.cname)
    FROM ENROLLED
    JOIN E.snum = S.snum
    GROUP BY snum
    HAVING MAX(snum);`

11. `SELECT sname, COUNT(E.cname)
    FROM ENROLLED
    JOIN E.snum = E.snum
    GROUP BY snum
    HAVING E.sname = NULL;`

12. `SELECT age, level COUNT(snum)
    FROM STUDENTS
    GROUP BY age
    HAVING MAX(COUNT(snum));`

## Question #3:

1. `SELECT aname
   FROM Aircraft A
   JOIN CERTIFIED ON A.aid = C.aid
   JOIN EMPLOYEES ON C.eid = E.eid
   WHERE E.salary > 80000;`

2. `SELECT MAX(A.crusingrange), AS maxCruisingRange C.eid
   FROM Aircraft A
   JOIN Certified C ON A.aid = C.aid
   GROUP BY C.eid
   HAVING COUNT(A.aid) > 3`

3. `SELECT ename
   FROM Employees E
   WHERE salary < (SELECT MIN






    
      
