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
### update table for field gender
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
     dept_id int not null,
     dept_name varchar(50) not null,
     primary key(dept_id)
     );
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
### Creating employee_department table
```
create table employee_department
(
emp_id int unsigned not null,
dept_id int not null,
foreign key (emp_id)  references employee (emp_id),
foreign key (dept_id) references department (dept_id)
);
```

## UC12 - Ensure All retrieve queries done before
### Adding data into table comapny
```
 insert into company values
    -> (1, 'BridgeLab'),
    -> (2, 'CapGemini'),
    -> (3, 'Dee-Shaw');
```
### Adding data into table Department
```
 insert into department values
    -> (51, 'Sales'),
    -> (52, 'Marketing'),
    -> (53, 'Production');
```
### Adding data into table Employee
```
 insert into employee values
    -> (101, 1, 51, 'Dev', 'Kumar', 'HYD', 7870752948,  'M'),
    -> (102, 2, 52, 'Manoj', 'Harale', 'CHN', 829469847, 'M'),
    -> (103, 3, 53, 'Avantika', 'Pandey', 'HYD', 787456974, 'F');
```
### Adding data into table payroll
```
 insert into payroll values
    -> (101, 1000000.00, 100000.00, 900000.00, 100000.00, 800000.0),
    -> (102, 2000000.00, 150000.00, 1850000.00, 150000.00, 1700000.0),
    -> (103, 3000000.00, 300000.00, 2700000.00, 300000.00, 2400000.0);
```
### Adding data to employee_department table
```
 insert into employee_department values
    -> (101,51),
    -> (101,52),
    -> (102,52),
    -> (103,52),
    -> (103,53);
```
## UC12- 
### Altering payroll table to add start date and insert values
```
ALTER TABLE payroll ADD start DATE
update  payroll set start = '2019-10-12' where emp_id=102;
update  payroll set start = '2018-1-15' where emp_id=101;
update payroll set start = '2018-5-9' where emp_id=103;
SELECT * from payroll where start between CAST('2019-1-1' AS DATE) and DATE(NOW());
```
### Sum of total salary according to gender
```
select e.gender, sum(p.net_pay) as TOTAL_SALARY from employee e left join payroll p using (emp_id) group by e.gender;
```
### Average salary according to gender
```
select e.gender, AVG(p.net_pay) as AVG_SALARY from employee e left join payroll p using (emp_id) group by e.gender;
```
### Minimum salary according to gender
```
select e.gender, MIN(p.net_pay) as MIN_SALARY from employee e left join payroll p using (emp_id) group by e.gender;
```
### Maximum salary according to gender
```
select e.gender, MAX(p.net_pay) MAX_SALARY from employee e left join payroll p using (emp_id) group by e.gender;
```
### Count of employees according to gender
```
select e.gender, COUNT(p.net_pay)  as COUNT from employee e left join payroll p using (emp_id) group by e.gender;