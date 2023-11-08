# Ex. No: 5 Creating Triggers using PL/SQL
## DATE : 31.08.23
## AIM: To create a Trigger using PL/SQL.

## Steps:
1. Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
2. Create salary_log table with following attributes (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
3. Create a trigger named as log_salary-update.
4. Inside the trigger block, Insert the values into the salary_log table whenever the salary is updated.
5. End the trigger.
6. Update the salary of an employee in employee table.
7. Whenever a salary is updated for the employee it must be logged into the salary_log table with old salary and new salary.
8. Display the employee table, salary_log table.

### NAME : ASHWIN KUMAR.A
### REG.NO :212222100006 
## Program:
### Create employee table
```
CREATE TABLE employee(empid NUMBER,empname VARCHAR(10),dept VARCHAR(10),salary NUMBER);
insert into employee values(1,'joe','HR',55000);
insert into employee values(2,'rose','IT',60000);
insert into employee values(3,'jack','CS',45000);
```
![image](https://github.com/ASHWINKUMAR2903/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119407186/f6a96a8c-07e0-4f9a-bda8-81e5f83a5056)

### Create salary_log table
```
create table salary_log(log_id number generated always as identity, empid number,empname varchar(10),old_salary number,new_salary number,update_date date);
```
lets keep the salary_log table empty so that trigger can be used.
### PLSQL Trigger code
```
SQL> CREATE OR REPLACE TRIGGER log_salary_update
  2  BEFORE UPDATE ON employee
  3  FOR EACH ROW
  4  BEGIN
  5    IF :OLD.salary != :NEW.salary THEN
  6      INSERT INTO salary_log (empid, empname, old_salary, new_salary, update_date)
  7      VALUES (:OLD.empid, :OLD.empname, :OLD.salary, :NEW.salary, SYSDATE);
  8    END IF;
  9  END;
 10  /
```
![image](https://github.com/ASHWINKUMAR2903/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119407186/08302b6b-8748-4c86-b286-1ceaa91b2d7b)
## Output:
now lets update the values in employee table to create a trigger in the log_salary_update to the salary_log table.
```
update employee set salary = 53000 where empid = 2;
```
![image](https://github.com/ASHWINKUMAR2903/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119407186/e1e67d14-0212-4d04-b256-a945d7df42b0)

now lets see the salary_log table.
![image](https://github.com/ASHWINKUMAR2903/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119407186/2594d128-c1fc-41c7-a8ff-770ec6e838e8)

## Result:
The trigger has been created and executed successfully.
