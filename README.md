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
## UC7 - Use of Various inbuilt function in SQL

### Find sum, average, min, max and number of male and female employees
```
select gender, sum(salary), count(gender), avg(salary), min(salary), max(salary) from employee_payroll group by gender;
```
## UC8 - Store extra employee info like phone, department and Address
```
 alter table employee_payroll
    -> add column phoneNo long,
    -> add column Address varchar(150) default 'HYD',
    -> add column Department varchar(50) not null;
```
### See the table, employee_payroll
```
 desc employee_payroll;
```
## UC9 - Extend table to have Basic_Pay, deductions, taxable pay, tax and net pay
```
 alter table employee_payroll
    -> add column deductions double not null after Basic_Pay,
    -> add column taxable_pay double not null after deductions,
    -> add column income_tax double not null after taxable_pay,
    -> add column net_pay double not null after income_tax;
```
## UC10.1 Adding Terisa department as sales and marketing by doing double entry
### Entry for department 'Sales'
```
 insert into employee_payroll values
    -> (5, 'Terisa', 'F', 3000000.00, 400000.00, 2600000.00, 400000.00, 2200000.00, '2019-08-13', 9162458745, 'HYD', 'Sales');
```
### Entry for department 'Marketing'
```
 insert into employee_payroll values
    -> (4, 'Terisa', 'F', 3000000.00, 400000.00, 2600000.00, 400000.00, 2200000.00, '2019-08-13', 9162458745, 'HYD', 'Marketing');
```

## UC11 - implementing ER diagram for employee_payroll database
### Adding table company
```
 create table Company
    -> (
    -> company_id int not null,
    -> company_name varchar(50) not null,
    -> primary key(company_id)
    -> );
```
### creating table Department
```
 create table Department (
    -> dept_id int not null,
    -> dept_name varchar(50) not null,
    -> primary key(dept_id)
    -> );
```
### creating table employee
```
 create table employee(
    -> emp_id int unsigned not null auto_increment primary key,
    -> company_id int not null,
    -> dept_id int not null,
    -> firstName varchar(50) not null,
    -> lastName varchar(50) not null,
    -> address varchar(50) not null,
    -> phoneNo long,
    -> gender char(1),
    -> foreign key(company_id) references company(company_id),
    -> foreign key(dept_id) references department(dept_id)
    -> );
```
### creating table payroll
```
 create table payroll
    -> (
    -> emp_id int unsigned not null auto_increment primary key,
    -> basic_pay double not null,
    -> deductions double not null,
    -> taxable_income double not null,
    -> income_tax double not null,
    -> net_pay double not null,
    -> foreign key (emp_id) references employee(emp_id)
    -> );
```


