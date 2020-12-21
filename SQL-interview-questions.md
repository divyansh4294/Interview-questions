# Interview Questions on SQL for Data Scientist

### Q: What is best for data science Normalised data or Denormalised data?  
A: Normalised:  
      1. Normalization is used to remove redundant data from the database and to store non-redundant and consistent data into it.  
      2. Normalization mainly focuses on clearing the database from unused data and to reduce the data redundancy and inconsistency.  
      3. During Normalization as data is reduced so a number of tables are deleted from the database hence tables are lesser in number.  
      4. Normalization uses optimized memory and hence faster in performance.  
      5. Normalization maintains data integrity i.e. any addition or deletion of data from the table will not create any mismatch in the relationship of the tables.  
      6. Normalization is generally used where number of insert/update/delete operations are performed and joins of those tables are not expensive.  

   Denormalised:  
      1. Denormalization is used to combine multiple table data into one so that it can be queried quickly.  
      2. Focus on to achieve the faster execution of the queries through introducing redundancy.  
      3. During Denormalization data is integrated into the same database and hence a number of tables to store that data increases in number.  
      4. Denormalization introduces some sort of wastage of memory.  
      5. Denormalization does not maintain any data integrity.  
      6. Denormalization is used where joins are expensive and frequent query is executed on the tables.  
      
###  Q: Difference between CHAR and VARCHAR2 datatype in SQL?  
 A: Both Char and Varchar2 are used for characters datatype but varchar2 is used for character strings of variable length whereas Char is used for strings of fixed length.  
    For example, char(10) can only store 10 characters and will not be able to store a string of any other length whereas varchar2(10) can store any length i.e 6,8,2 in this variable.  
 
###  Q: What are constraints?  
 A: Constraints are used to specify the limit on the data type of the table. It can be specified while creating or altering the table statement. The sample of constraints are:  
    1. Not null 2. check 3. defeault 4. unique 5. primary key 6. foreign key. 
    
###  Q: What is ACID property in Database?  
 A: It is used to ensure that the data transactions are processed reliably in a database system.  
    1. Atomicity: Atomicity refers to the transactions that are completely done or failed where transaction refers to a single logical operation of a data.  
                  It means if one part of any transaction fails, the entire transaction fails and the database state is left unchanged.  
    2. Consistency: Consistency ensures that the data must meet all the validation rules.  
    In simple words, you can say that your transaction never leaves the database without completing its state.  
    3. Isolation: The main goal of isolation is concurrency control.  
    4. Durability: Durability means that if a transaction has been committed, it will occur whatever may come in between such as power loss, crash or any sort of error.  

###  Q: What is the correct order of occurrence in a typical SQL statement?  
A: select, where, group by, having. 

###  Q: What are the commands related to transaction control in SQL?  
A: 1. Rollback  2. Commit  3. Savepoint

###  Q: What is the difference between primary key and unique key?  
A: You can create a date variable as a primary key in table. In relational schema, you can have only one primary key and there may be multiple unique key present in table.  
Unique key can take null values.

###  Q: What UPDATE command can do in SQL?  
A: 1. You can update only a single table using UPDATE command.  2. You must list what columns to update with their new values (separated by commas).  
3. To update multiple targeted records, you need to specify UPDATE command using the WHERE clause.  4. But You can't update multiple tables using UPDATE command.  

###  Q: What TRUNCATE command can do in SQL?  
A: TRUNCATE is faster than delete because truncate is a ddl command so it does not produce any rollback information   and the storage space is released while the delete command is a dml command and it produces rollback information too and space is not deallocated using delete command.


###  Q: Write the query to find the employee record with the highest the salary.    
A: Select * from table_name where salary = (select max(salary) from table_name);

###  Q: write the query to find the 2nd highest salary in the employee table?   
A: There are multiple ways to write query for this:  
1. Select max (salary) from employee where salary not in (select max(salary) from employee).  
Here, we are first selecting the employee with max salary in nested query and then finding max salary in data except already selected which is 1st high  
2. Select Salary from employee where salary in (select salary from employee where level = &topnth connect by prior Salary > Salary group by level).  
 If you run the above query it will ask for entering the value of topnth, if you enter 2 it will show the result for 2 and if you enter 3 it will give the result for 3 likewise this query is generic.  
3. Select salary from employee where salary in (select salary from (select unique salary from employee order by salary desc) group by rownum, salary having rownum = &topnth).  
Execute as same as 2nd query execute.  

###  Q: write the query to find the 2nd lowest salary in the employee table?   
A: There are multiple ways to write query for this:  
1. Select min (salary) from employee where salary not in (select min(salary) from employee).  
2. Select Salary from employee where salary in (select salary from employee where level = &lownth connect by prior Salary < Salary group by level).  
If you run the above query it will ask for entering the value of lownth, if you entering 2 it will show the result for 2 and if you enter 3 it will give the result for 3 likewise this query is generic.  

###  Q: what is the difference between NVL and NVL2 functions?  
A: Both the function is used to convert a NULL value to an actual value   
NVL (EXPR1, EXPR2)  
EXPR1: Is the source value or expression that may contain NULL.  
EXPR2: Is the target value for converting NULL.  
Note: If EXPR1 is character data then EXPR2 may any data type.  
For example: select NVL (100,200) from dual  
Output: 100  
Select NVL(null,200) from dual;  
Output: 200  

NVL2(expr1,expr2,expr3)  
If expr1 is not null, NVL2 returns expr2. If expr1 is null then, NVL2 returns expr3.  
The data type of the return value is always the same as the data type of expr2 unless expr2 is character data.  
Example: select nvl2(100,200,300) from dual;  
Output: 200  
Select nvl2 (null,200,300) from dual;  
Output: 300  

###  Q: write the query to find the distinct domain from email column  
A: Select distinct (substr (Email, Instr (Email,’@’,1,1))) from tablename;  

### Q: Write the query to find the duplicate name and its frequency in the table  
A: Select Name, count(1) as frequency from Employee Group by Name having count(1) > 1  

### Q: Write the query to remove the duplicates from a table without using a temporary table?  
A: 1. Delete from Employee where name in (Select name from employee group by age, salary having count(*) > 1);  
Explanation: In nested quesry, [Select name from employee group by age, salary having count(*) > 1)]  
Selecting those name from table where age and salary count is > 1  
and Delete those name from table.  
2. DELETE FROM tablename where empid NOT IN (Select min(empid) from tablename GROUP BY Col1, COl2,...)  

###  Q: Write the Query to find odd and even records from the table?  
A:  For even number: Select * from employee where empno in (select empno from employee group by empno, rownum having mod(rownum,2) = 0);  
For odd number: Select * from employee where empno in (select empno from employee group by empno, rownum having mod(rownum,2) != 0);  

###  Q: Write a SQL query to create a new table with data and structure copied from another table, create an empty table with the same structure as some other table?  
A: *create a new table with data and structure copied from another table*  
Select * into new table from an existing table;  
*Create an empty table with the same structure as some other table*  
Select * into new_table from existing_table where 1=2;  


Best way to practice SQL: [Click Here] (Hackerrank https://www.hackerrank.com/domains/sql)
