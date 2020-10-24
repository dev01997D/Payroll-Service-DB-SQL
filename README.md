# Payroll-Service-DB-SQL

## UC1 - Create database for payroll_service
```
create database payroll_service;
```

### see the DB created using show database query
```
show databases;
```

### Go to the database created 
```
use payroll_service;
```
## UC2 - Create employee_payroll table in payroll_service database
```
create table employee_payroll( 
id int unsigned not null auto_increment,
 name varchar(50) not null, 
salary double not null, 
start date not null, 
primary key(id)
);
```
## UC3 - Insert employee data into payroll_service
### select current database
```
  select database();
```
### Insert employee data into payroll table
```
insert into employee_payroll (name, salary, start) values
    ('Dev', 5000000.0, '2020-05-08'),
    ('Kavya', 74000.6, '2013-08-15');
```
## UC4 - Retrieve all data from payroll_service database
### select current database
```
  select database();
```
### Retrieve all the employee data from employee_payroll table
```
select * from employee_payroll;
```
## UC5 -Retrieve employee data for particular name or joined date
### select employee for name 'Dev'
```
SELECT salary FROM employee_payroll
    WHERE name ='Dev';
```
### select employee who has joined after '2019-06-18'
```
SELECT name, start, salary FROM employee_payroll
     where start between cast('2019-06-18' as date) and date(now());
```
## UC6 - Alter table and update table
### Alter table to add gender as field
```
alter table employee_payroll add gender char(1) after name;
```
### Update table for field gender
```
update employee_payroll set gender='M' where name='Dev' or name='Manoj';
update employee_payroll set gender='F' where name='Kavya';
```




