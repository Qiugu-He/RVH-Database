# Design and Implementation of  the RVH Database

## 1. Enhanced Entity Relationship (EER) structure/diagram:
<img src="https://github.com/Qiugu-He/RVH-Database/blob/master/EER.jpg" alt="alt text" width="50%" height="50%">
## 2. Example of creation relations using Oracle SQL:
## 3. Database data:
## 4. SQL statement to met the user need:
- In order to meet the user's request to access the data, appropriate SQL should be implemented
- Performance: to speed up a query, an appropriate index is added to appropriate attribute on each table. For example, un-clustered hash index is using on the attritbute on patient as the patient table it access most frequently. 
An clustered B+ tree index is added on EmployeeID attribute and careCenterId as system requires to list all the employee works at a specific care center.

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
        - 	The SELECT privileges on VIEW DeptInfo 
