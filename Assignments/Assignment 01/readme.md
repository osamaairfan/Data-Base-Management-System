## Question #2:
1. SELECT STUDENT.sname  
   FROM STUDENT  
   JOIN ENROLLED ON STUDENT.snum = ENROLLED.snum   
   JOIN CLASS ON ENROLLED.cname = CLASS.cname  
   JOIN FACULTYON CLASS.fid = FACULTY.fid  
   WHERE STUDENT.level = 'JR' AND FACULTY.fname = 'I. Teach';   

2.  SELECT MAX(STUDENT.age) AS oldest_age   
   FROM STUDENT  
   JOIN Enrolled ON STUDENT.snum = Enrolled.snum  
   JOIN Class ON Enrolled.cname = Class.name  
   JOIN Faculty ON Class.fid = Faculty.fid  
   WHERE Student.major = 'History' OR Faculty.fname = 'I. Teach';  

3. SELECT cname FROM ENROLLED  
   JOIN CLASS ON Student.snum = Enrolled.snum  
   WHERE cname = ‘R128’ OR snum >= 5  

4. SELECT s.name FROM Student S  
   JOIN Enrolled E1 ON S.snum = E1.snum  
   JOIN Enrolled E2 ON S.snum = E2.snum  
   JOIN Class C1 ON E1.cname = C1.name  
   JOIN Class C2 ON E2.cname = C2.name    
   WHERE C1.meets_at = C2.meets_at AND E1.cname <> E2.cname;  

5. n
