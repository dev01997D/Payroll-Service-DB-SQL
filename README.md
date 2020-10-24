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

