## Question #2:
1. SELECT STUDENT.sname    
   FROM STUDENT    
   JOIN ENROLLED ON STUDENT.snum = ENROLLED.snum     
   JOIN CLASS ON ENROLLED.cname = CLASS.cname    
   JOIN FACULTYON CLASS.fid = FACULTY.fid    
   WHERE STUDENT.level = 'JR' AND FACULTY.fname = 'I. Teach';    

2. SELECT MAX(STUDENT.age) AS oldest_age   
   FROM STUDENT  
   JOIN Enrolled ON STUDENT.snum = Enrolled.snum  
   JOIN Class ON Enrolled.cname = Class.name  
   JOIN Faculty ON Class.fid = Faculty.fid  
   WHERE Student.major = 'History' OR Faculty.fname = 'I. Teach';  

3. SELECT cname FROM ENROLLED  
   JOIN CLASS ON Student.snum = Enrolled.snum  
   WHERE cname = ‘R128’ OR snum >= 5; 

4. SELECT s.name FROM Student S  
   JOIN Enrolled E1 ON S.snum = E1.snum  
   JOIN Enrolled E2 ON S.snum = E2.snum  
   JOIN Class C1 ON E1.cname = C1.name  
   JOIN Class C2 ON E2.cname = C2.name    
   WHERE C1.meets_at = C2.meets_at AND E1.cname <> E2.cname;  

5. SELECT F.fname  
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
   );  

6. SELECT F.fname AS FacultyName  
   FROM Faculty F  
   JOIN Class C ON F.fid = C.fid  
   GROUP BY F.fname  
   HAVING COUNT(C.name) < 5;  

7. SELECT level, AVG(age) AS AVERAGEAGE  
   FROM STUDENT  
   GROUP BY level;  

8. SELECT level, AVG(age) AS AVERAGEAGE  
   FROM STUDENT  
   WHERE level != JR  
   GROUP BY level;  

9. SELECT fname, COUNT(C.fid)  
   FROM FACULTY  
   JOIN FACULTY ON F.fid = C.fid  
   GROUP BY fname  
   HAVING C.name = ‘R128’;  

10. SELECT sname, COUNT(E.cname)  
    FROM ENROLLED  
    JOIN E.snum = S.snum  
    GROUP BY snum  
    HAVING MAX(snum);  

11. SELECT sname, COUNT(E.cname)  
    FROM ENROLLED  
    JOIN E.snum = E.snum  
    GROUP BY snum  
    HAVING E.sname = NULL;  

12. SELECT age, level COUNT(snum)  
    FROM STUDENTS  
    GROUP BY age  
    HAVING MAX(COUNT(snum));  

## Question #3:  

1. SELECT aname  
   FROM Aircraft A  
   JOIN CERTIFIED ON A.aid = C.aid  
   JOIN EMPLOYEES ON C.eid = E.eid  
   WHERE E.salary > 80000;  

2. SELECT MAX(A.crusingrange), AS maxCruisingRange C.eid  
   FROM Aircraft A  
   JOIN Certified C ON A.aid = C.aid  
   GROUP BY C.eid  
   HAVING COUNT(A.aid) > 3  

3. SELECT ename  
   FROM Employees E  
   WHERE salary < (SELECT MIN(price)  
   FROM Flights   
   WHERE "from" = 'Los Angeles' AND "to" = 'Honolulu');  

4. SELECT ename  
   FROM Employees E  
   JOIN Employees ON Certified.eid = E.eid  
   JOIN Certified ON Aircraft.aid = Certified.aid  
   WHERE Aircraft.aname = 'Boeing%'  

5. SELECT aid  
   FROM Aircraft A  
   JOIN Flights F ON "from" = 'Los Angeles' AND "to" = 'Chicago';  

6. SELECT E.eno, E.ename, F.flno, F.from, F.to  
   FROM Employees E  
   JOIN Certified C ON E.eno = C.eno  
   JOIN Flights F ON C.aid = F.aid  
   WHERE E.salary > 100000  
   GROUP BY E.eno, E.ename, F.flno, F.from, F.to  
   HAVING COUNT(*) = (SELECT COUNT(*)  
   FROM Aircraft);  

7. SELECT DISTINCT  
   F1.flno AS flight1,  
   F1.arrives AS arrival1,  
   F2.flno AS flight2,  
   F2.arrives AS arrival2,  
   F3.flno AS flight3,  
   F3.arrives AS arrival3  
   FROM Flights F1  
   JOIN Flights F2 ON F1.to = F2.from  
   JOIN Flights F3 ON F2.to = F3.from  
   WHERE F1.from = 'Madison' AND F3.to = 'New York' AND F3.arrives <='18:00';  

8. SELECT (  
   SELECT AVG(salary)  
    FROM Employees  
    WHERE ename IN (SELECT ename FROM Certified)  
   )  
   (  
    SELECT AVG(salary)  
    FROM Employees  
   ) AS SalaryDifference;   

9. SELECT ename, salary  
   FROM Employees  
   WHERE salary > (SELECT AVG(salary)  
   FROM Employees  
   WHERE ename IN (SELECT ename FROM Certified));  

10. SELECT E.ename  
    FROM Employees E  
    JOIN Employees ON C.eid = E.eid  
    JOIN CERTIFIED C ON AIRCRAFT.aid = C.aid  
    WHERE AIRCRAFT.crusingrange > 1000  

11. SELECT E.ename  
    FROM Employees E  
    JOIN Certified C ON E.eid = C.eid   
    JOIN Aircraft A1 ON C.aid = A1.aid   
    JOIN Certified C2 ON E.eid = C2.eid   
    JOIN Aircraft A2 ON C2.aid = A2.aid   
    WHERE A1.crusingrange > 1000 AND A1.aid <> A2.aid ;  

12. SELECT E.ename  
    FROM Employees E  
    JOIN Certified C ON E.eid = C.eid     
    JOIN Aircraft A ON C.aid = A.aid   
    WHERE A.cruisingrange > 1000 AND A.aname LIKE '%Boeing%';  

## Question #4:

1. ALTER TABLE Emp   
   ADD CONSTRAINT check_minimum_salary CHECK (salary >= 10000);   

4. DELETE FROM Employees   //part 4
   WHERE salary > (   
       SELECT D.salary   
       FROM Department D  
       WHERE D.did = (  
           SELECT W.did  
           FROM Works W  
           WHERE W.eid = Employees.eid  
       ) AND D.managerid = Emp.eid  
   );  
   DELETE FROM Works  
   WHERE eid NOT IN (SELECT eid FROM Emp);  
   DELETE FROM Emp  
   WHERE eid NOT IN (SELECT eid FROM Works);  
 
      
