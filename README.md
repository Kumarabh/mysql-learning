## INSTALLATION GUIDE: https://www.cyberciti.biz/faq/how-to-install-docker-on-amazon-linux-2/


---------------------------------------------- Mysql configuration on docker

### Pull mysql image
``` docker pull mysql/mysql-server:latest ```

### Run mysql image
``` docker run -d --name=mysql-container -p 3306:3306 mysql/mysql-server ```

### Copy password 
``` docker logs mysql-container ```

### For EMPTY PASSWORD CONTAINER -> 
``` docker logs mysql-container 2>&1 | grep GENERATED ```

``` docker exec -it mysql-container sh ```

### login to mysql
``` cd var/lib ```
``` mysql -u root -p ```

### Change root password
``` ALTER USER 'root'@'localhost' IDENTIFIED BY '[newpassword]'; ```



## COMMANDS

``` show databases ```
``` use mysql; ```

### mysql info
``` \s ```

### create table
``` create table employee (id int not null primary key auto_increment, name varchar(255), gender varchar(255)); ```

- single insertion
``` insert into employee (id, name, gender) values (null, "John", "Male"); ```

- multiple insertion
``` insert into employee (id, name, gender) values (), (); ```

- update 
``` update employee set gender = "Male"; // updates gender to all rows. ```
``` update employee set gender = "Male" where name = "John"; // updates gender of John ```
``` update employee set gender = "Male", city = "New Delhi" where name "John" // updates multiple columns ```
 
## alter 
### add a column
``` alter table employee add column gender varchar(255); ```

- modify column
``` alter table employee modify column customerName varchar(15); ```

- rename a column
``` alter table employee rename column gender to customerGender; ```

- drop a column
``` alter table employee drop column gender; ```

- order by
``` select * from employee order by name asc | desc; ```

- limit
``` select * from employee order by name asc limit 3; ```

- offset - ignore first n
``` select * from employee order by name asc limit 3 offset 2; ```

- alias
``` select name as employeeName from employee; ```
``` select name "employeeName" from employee; ```


- add a foreign key during the foreign table is being created
``` create table department (id not null primary key auto_increment, deptName varchar(200), cid int, foreign key(cid) references employee(id)); ```

- add a foreign key after the foreign table is created
``` create table department (id not null primary key auto_increment, deptName varchar(200)); ```
``` alter table add column cid int; ```
``` alter table department add constraint fk_employee01 foreign key (cid) references customer(id); OR alter table department add foreign key(cid) references customer(id); ```

- drop foreign key
``` alter table department drop foreign key [constraint_name] ```

- join multiple tables - fetch data from multiple tables

- normal join ( without alias )
``` SELECT employee.name, employee.city, department.name ```
  ```FROM employee, department```
  ```WHERE employee.id = department.eid ```

- normal join ( with alias )
``` SELECT e.name, e.city, d.name ```
 ``` FROM employee e, department d ```
 ``` WHERE e.id = d.eid  ```


## functions
### sum
``` select sum(salary) from employee where city = "New Delhi"; // total salary goes to new delhi employees ```

### avg
### count
``` select count(name) from employee where city = "New Delhi"; // total count of employees from New Delhi location; ```
``` select count(gender) from employee; ```

### string functions
``` length("str") ```
``` concate(str1, str2) ```
``` lcase(str) ```
``` ucase(str) ```
``` substring(str, start, length) ```
``` trim(str) ```

### more functions
``` database() ```
``` version() ```
``` user() ```
``` select DATABASE() "DB", VERSION() "version" USER() "user"; ```

### math functions
``` sin ```
``` cos ```
``` tan ```

- CREATE PROCEDURE
> delimiter //
> create procedure CreateUserTable() 
  begin
  create table if not exists customer( customerId int, customerName varchar(255) );
  insert into customer values (101, "John Doe");
  select * from customer;
  end //
> call CreateUserTable();


---------------------------------------------- NODE JS connection



- For node JS connection, We can create new user 'admin' password 'admin'
> select host, user from user;

> CREATE USER 'admin'@'%' IDENTIFIED BY 'admin';   // Create a new user account with a desired username and password:

> GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%';   // Grant appropriate privileges to the new user account:

> FLUSH PRIVILEGES;   // to apply all changes


// app.ts
import mysql from 'mysql2';

const connectDB = async() => {
  const credentials = {host: 'localhost', user: 'admin', password: 'admin'};
  try {
    const connection = await mysql.createConnection(credentials)
    connection.connect((error: any) => { 
      if(error) throw Error('connection failed.'+ error.message)
      console.log('==> Database connected');
    })
  } catch (error: any) {
    throw Error(error);
  }
}

export {connectDB};












--------------------------------------------------- PRIVILLAGES

Mxl::8AVvn837.?wvh6?J;3*z+nh93Cw

// --------------------- optional
// check the list of users

use mysql;
select user from user;


-- create a user for connection

CREATE USER 'dbeaver'@'%' IDENTIFIED BY 'dbeaver';
GRANT ALL PRIVILEGES ON *.* TO 'dbeaver'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;









## Expanding the ESLint configuration

If you are developing a production application, we recommend updating the configuration to enable type aware lint rules:

- Configure the top-level `parserOptions` property like this:

```js
export default {
  // other rules...
  parserOptions: {
    ecmaVersion: 'latest',
    sourceType: 'module',
    project: ['./tsconfig.json', './tsconfig.node.json'],
    tsconfigRootDir: __dirname,
  },
}
```

