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
##UC2 - Create employee_payroll table in payroll_service database
```
create table employee_payroll( 
id int unsigned not null auto_increment,
 name varchar(50) not null, 
salary double not null, 
start date not null, 
primary key(id)
);
```
