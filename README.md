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
        -   *CREATE VIEW Persons (pname) 
	        AS SELECT P.pname 
	        FROM Person P;*
     - View for number of nurses holding an RN certificate, as well as their total and average salary
     	-  *CREATE VIEW "NURSE_SUMMARY" ("D", "C", "TOTAL_S", "AVERAGE_S")
            <br>AS SELECT Care.cid AS D, COUNT(care_centre_id) C,  
            SUM(Nur.salary) AS TOTAL_S, AVG(Nur.salary) AS AVERAGE_S 
            <br>FROM Care_centres Care 
            <br>INNER JOIN Nurses Nur 
            <br>ON Care.cid = Nur.care_centre_id 
            <br>WHERE certificate_type = 'RN' 
            <br>GROUP BY Care.cid*

    - Privileges granted to user who needs to know only average department salaries for the HR and CS departments
        - *The SELECT privileges on VIEW DeptInfo;*
	
     - Authorize admin_1 to read and modify database (Patient relation and Employee relation)
        - *GRANT SELECT, INSERT, UPDATE ON Employees TO Joe WITH GRANT OPTION
	    <br>GRANT SELECT, INSERT,UPDATE ON EmployeeNames To Joe WITH GRANT OPTION*
