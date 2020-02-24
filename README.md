# Design and Implementation for the RVH Database

## 1. Enhanced Entity Relationship (EER) structure/diagram:
<img src="https://github.com/Qiugu-He/RVH-Database/blob/master/EER.jpg" alt="alt text" width="60%" height="60%">

## 2. Some created relations with using Oracle:
<img src="https://github.com/Qiugu-He/RVH-Database/blob/master/Oracle_Sql.jpg" alt="alt text" width="60%" height="60%">

## 3. Database data:
<img src="https://github.com/Qiugu-He/RVH-Database/blob/master/DB_data.png" alt="alt text" width="60%" height="60%">

## 4. SQL statement to meet the user's request:
- In order to access the data for specific user's reuqest, an appropriate SQL is be implemented
- Performance: to speed up a query, an appropriate index is added to appropriate attribute on each table. For example, un-clustered hash index is used on the personeId attritbute of patient relations as the this table is access most frequently. 
An clustered B+ tree index is added on EmployeeID attribute and careCenterId as system requires to show all the employee works at a specific care center.

- System SQL query examples: 
    - View for person (Patient & Employee) info:
        -   CREATE VIEW Persons (pname) 
	        AS SELECT P.pname 
	        FROM Person P
	- View for average salary for each department:
	    -   CREATE VIEW DeptInfo (dept, avgsalary) 
	        AS SELECT DISTINCT E.dept, AVG (E.salary) AS avgsalary
	        FROM Employee E
	        Group by E.dept
    - Privileges granted to user who needs to know only average department salaries for the HR and CS departments
        - The SELECT privileges on VIEW DeptInfo 
