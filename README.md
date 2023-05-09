# DBMS
CREATE database dbms;
USE dbms;

CREATE TABLE department(Dno int(11) NOT NULL, Dname varchar(50) DEFAULT NULL, Location varchar(50) DEFAULT NULL, PRIMARY KEY(Dno));

INSERT INTO department VALUES(10,'Accounting','New York'),(20,'Research','Dallas'), (30,'Sales','Chicago'), (40,'Operation','Boston'),(50,'Marketing','New Delhi');

CREATE TABLE employee(Eno char(3) NOT NULL, Ename varchar(50) NOT NULL,
Job_type varchar(50) NOT NULL, Manager char(3) DEFAULT NULL, Hire_date date NOT NULL,
Dno int(11) DEFAULT NULL, Commission decimal(10,2) DEFAULT NULL, Salary decimal(7,2) NOT NULL, PRIMARY KEY (Eno), CONSTRAINT Dno FOREIGN KEY (Dno) REFERENCES department(Dno), CONSTRAINT Manager FOREIGN KEY (Manager) REFERENCES employee (Eno))

INSERT INTO employee VALUES ('736','Smith','Clerk','790','1981-12-17',20,0.00,1000.00),
('749','Allan','Sales_man','769','1981-02-20',30,300.00,2000.00),
('752','Ward','Sales_man','769','1981-02-22',30,500.00,1300.00),
('756','Jones','Manager','783','1981-04-02',20,0.00,2300.00),
('765','Martin','Sales_man','784','1981-04-22',30,1400.00,1250.00),
('769','Blake','Manager','783','1981-05-01',30,0.00,2870.00),
('778','Clark','Manager','783','1981-06-09',10,0.00,2900.00),
('783','King','President',NULL,'1981-11-17',10,0.00,2950.00),
('784','Turner','Sales_man','769','1981-09-08',30,0.00,1450.00),
('787','Adams','Clerk','778','1983-01-12',20,0.00,1150.00),
('788','Scott','Analyst','756','1982-12-09',20,0.00,2850.00),
('790','James','Clerk','769','1981-12-03',30,0.00,950.00),
('792','Ford','Analyst','756','1981-12-03',20,0.00,2600.00),
('793','Miller','Clerk','788','1982-01-23',40,0.00,1300.00);

Queries

1. Query to display Employee Name, Job, Hire Date, Employee Number; for each employee with the Employee Number appearing first.
---------SELECT Eno, Ename, Job_type, Hire_date FROM employee;

2. Query to display unique Jobs from the Employee Table.
---------SELECT DISTINCT Job_type FROM employee;

3. Query to display the Employee Name concatenated by a Job separated by a comma.
---------SELECT CONCAT(Ename, ',', Job_type) AS Name_Job FROM employee;

4. Query to display all the data from the Employee Table. Separate each Column by a comma and name the said column as THE_OUTPUT.
---------SELECT CONCAT(Eno , ', ', Ename, ',', Job_type, ', ',Manager, ',' ,Hire_date, ',' ,Dno, ',' ,Commission, ',' ,Salary) AS THE_OUTPUT FROM employee;

5. Query to display the Employee Name and Salary of all the employees earning more than $2850.
---------SELECT Ename, Salary FROM employee WHERE ( Salary + Commission ) > 2850;

6. Query to display Employee Name and Department Number for the Employee No= 790.
---------SELECT Ename,Dno FROM employee WHERE Eno='790';

7. Query to display Employee Name and Salary for all employees whose salary is not in the range of $1500 and $2850.
---------SELECT Ename,Salary FROM employee WHERE Salary NOT BETWEEN 1500 AND 2850;

8. Query to display Employee Name and Department No. Of all the employees in Dept 10 and Dept 30 in the alphabetical order by name.
---------SELECT Ename,Dno FROM employee WHERE Dno=10 OR DNO=30 ORDER BY Ename;

9. Query to display Name and Hire Date of every Employee who was hired in 1981.
---------SELECT Ename,Hire_date FROM EMPLOYEE WHERE Hire_date LIKE '1981%';

10. Query to display Name and Job of all employees who don’t have a current Manager.
---------SELECT Ename,Job_type FROM employee WHERE Manager IS NULL;

11. Query to display the Name, Salary and Commission for all the employees who earn commission. Sort the data in descending order of Salary and Commission.
---------SELECT Ename,Salary,Commission FROM employee WHERE Commission > 0.00 ORDER BY Salary DESC,Commission DESC;

12. Query to display Name of all the employees where the third letter of their name is ‘A’.
---------SELECT Ename FROM employee WHERE Ename LIKE '__A%';

13. Query to display Name of all employees either have two ‘R’s or have two ‘A’s in their name and are either in Dept No = 30 or their Manger’s Employee No = 778.
---------SELECT Ename,Dno,Manager FROM employee WHERE Ename LIKE '%A%A%' OR Ename LIKE '%R%R%' AND Dno=30 OR Manager='778';

14. Query to display Name, Salary and Commission for all employees whose Commission Amount is greater than their Salary increased by 5%.
-------SELECT Ename,Salary,Commission FROM employee WHERE Commission > (Salary+Salary*0.05);

15. Query to display the Current Date.
-------SELECT CURDATE();

16. Query to display Name, Hire Date and Salary Review Date which is the 1st Monday after six months of employment.
-----------SELECT Ename,Hire_date,date_add(date_add(Hire_date,INTERVAL 6 MONTH),INTERVAL (7-WEEKDAY(date_add(Hire_date,INTERVAL 6 MONTH))) DAY) AS REVIEW_DATE FROM employee;

17. Query to display Name and calculate the number of months between today and the date each employee was hired.
----------SELECT Ename,12 *  (YEAR(curdate())-YEAR(Hire_date)) + (MONTH(CURDATE())-MONTH(Hire_date)) AS MONTHS FROM employee;

18. Query to display the following for each employee:- <E-Name> earns < Salary> monthly but wants < 3 * Current Salary >. Label the Column as Dream Salary.
---------SELECT CONCAT(Ename,' earns ',Salary,' monthly but wants ',3*Salary) AS DREAMY_SALARY FROM employee;
  
19. Query to display Name with the 1st letter capitalized and all other letter lower case and length of their name of all the employees whose name starts with ‘J’, ’A’ and ‘M’.
--------SELECT CONCAT( UPPER(SUBSTRING(Ename,1,1)) , LOWER(SUBSTRING(Ename,2,50))) AS NAME,LENGTH(Ename) AS LENGTH  FROM employee WHERE Ename LIKE 'J%' OR Ename LIKE 'A%' OR Ename LIKE 'M%';

20. Query to display Name, Hire Date and Day of the week on which the employee started.
---------SELECT Ename, Hire_date, DAYNAME(Hire_date) AS WEEK_DAY FROM employee;

21. Query to display Name, Department Name and Department No for all the employees.
---------SELECT e.Ename,d.Dname,e.Dno FROM employee AS e,department AS d WHERE e.Dno=d.Dno;
  
22. Query to display Unique Listing of all Jobs that are in Department # 30.
---------SELECT DISTINCT Job_type FROM employee WHERE Dno=30;
  
23. Query to display Name, Dept Name of all employees who have an ‘A’ in their name.
----------SELECT e.Ename,d.Dname FROM employee AS e,department as d WHERE e.Ename LIKE '%A%' AND e.Dno=d.Dno;
  
24. Query to display Name, Job, Department No. And Department Name for all the employees working at the Dallas location.
----------SELECT e.Ename,e.Job_type,e.Dno,d.Dname FROM employee AS e,department as d WHERE e.Dno=d.Dno AND d.Location='Dallas';
  
25. Query to display Name and Employee no. Along with their Manger’s Name and the Manager’s employee no; along with the Employees’ Name who do not have a Manager.
-----------SELECT e.Ename,e.Eno,d.Ename,d.Eno FROM employee AS e LEFT OUTER JOIN employee as d ON e.Eno=d.Manager;

26. Query to display Name, Dept No. And Salary of any employee whose department No. And salary matches both the department no. And the salary of any employee who earns a commission.
----------SELECT Ename,Dno,Salary FROM employee WHERE (Dno,Salary) IN (SELECT Dno,Salary FROM employee WHERE Commission>0);
  
27. Query to display Name and Salaries represented by asterisks, where each asterisk (*) signifies $100.
----------SELECT Ename,REPEAT ('*',(Salary/100)) AS SALARY_IN_STAR FROM employee;
  
28. Query to display the Highest, Lowest, Sum and Average Salaries of all the employees
----------SELECT MAX(Salary),MIN(Salary),SUM(Salary),AVG(Salary) FROM employee;
  
29. Query to display the number of employees performing the same Job type functions.
----------SELECT job_type,COUNT(*) FROM employee GROUP BY Job_type;
  
30. Query to display the no. Of managers without listing their names.
----------SELECT COUNT(DISTINCT Manager) FROM employee;
  
31. Query to display the Department Name, Location Name, No. Of Employees and the average salary for all employees in that department.
----------SELECT d.Dname,d.Location,AVG(e.Salary),COUNT(*) FROM employee AS e,department AS d WHERE d.Dno=e.Dno GROUP BY d.Dname;
  
32. Query to display Name and Hire Date for all employees in the same dept. As Blake.
----------SELECT Ename,Hire_date FROM employee WHERE Dno=(SELECT Dno FROM employee WHERE Ename='Blake');  
  
33. Query to display the Employee No. And Name for all employees who earn more than the average salary.
----------SELECT Eno,Ename FROM employee WHERE Salary > (Select AVG(Salary) FROM employee);
  
34. Query to display Employee Number and Name for all employees who work in a department with any employee whose name contains a ‘T’.
----------SELECT e.Eno,e.Ename FROM employee AS e ,employee as d WHERE e.Manager=d.Eno AND d.Ename LIKE '%T%';
  
35. Query to display the names and salaries of all employees who report to King.
----------SELECT Ename,Salary FROM employee WHERE Manager=(SELECT Eno FROM employee WHERE Ename='King');
  
36. Query to display the department no, name and job for all employees in the Sales department.
---------SELECT e.Dno,e.Ename,e.Job_type FROM employee AS e,department as d WHERE d.Dno=e.Dno AND d.Dname='Sales';
  
37. Display names of employees along with their department name who have more than 20 years experience.
-------select e.ename, d.dname from employee e,department d where e.dno-d.dno and timestampdiff(year,hire_ date, curdate())>20;
  
38. Find the department name in which at least 20 employees work in. 
------select dname from department where dno in (select dno from employee group by dno having count(*)>5);
  
39. Query to find the employee’ name who is not supervisor and name of supervisor supervising more than 5 employees. 
---------select ename from employee where eno in (select supervisoneno from employee where supervisoneno is not null group by supervisoneno having count(*)>3) or eno not in (select supervisoneno from employee where supervisoneno is not null group by supervisoneno);
  
40. Query to display the job type with maximum and minimum employees 
---------select job_type from employee group by job_type having count(*) = (select max(mycount) from (select count(*) as mycount from employee group by job_type) a) or count(*)=(select min (mycount) from (select count(*) as mycount from employee group by job_type)a);
