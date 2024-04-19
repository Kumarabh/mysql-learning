## INSTALLATION GUIDE: https://www.cyberciti.biz/faq/how-to-install-docker-on-amazon-linux-2/


#### Mysql configuration on docker

#### PULL MYSQL IMAGE
```sql  
docker pull mysql/mysql-server:latest
```

#### RUN IMAGE
```sql
docker run -d --name=mysql-container -p 3306:3306 mysql/mysql-server
```

#### COPY DEFAULT PASSWORD
```sql
docker logs mysql-container
 ```

#### IF NO PASSWORD FOUND
```sql 
docker logs mysql-container 2>&1 | grep GENERATED
```

#### EXECUTE THE CONTAINER
```sql  
docker exec -it mysql-container sh
```

#### LOGIN
```sql
cd var/lib
mysql -u root -p
```

#### CHANGE ROOT USER PASSWORD
```sql 
ALTER USER 'root'@'localhost' IDENTIFIED BY '[newpassword]';
```

#### SQL COMMANDS

```sql 
show databases
use mysql;
\s // MYSQL INFORMATION
```

#### CREATE TABLE
```sql 
create table employee (id int not null primary key auto_increment, name varchar(255), gender varchar(255));
```

#### INSERT SINGLE RECORD
```sql 
insert into employee (id, name, gender) values (null, "John", "Male");
```

#### INSERT MULTIPLE RECORDS
```sql 
insert into employee (id, name, gender) values (), ();
```

#### UPDATE RECORD 
```sql 
update employee set gender = "Male"; // updates gender to all rows.
update employee set gender = "Male" where name = "John"; // updates gender of John
update employee set gender = "Male", city = "New Delhi" where name "John" // updates multiple columns
```
 
#### ALTER TABLE
#### ADD COLUMN
```sql 
alter table employee add column gender varchar(255);
```

#### MODIFY COLUMN
```sql 
alter table employee modify column customerName varchar(15);
```

#### RENAME COLUMN
```sql
alter table employee rename column gender to customerGender; 
```

#### DROP COLUMN
```sql 
alter table employee drop column gender;
```

#### ORDER BY
```sql 
select * from employee order by name asc | desc;
 ```

#### LIMIT
```sql 
select * from employee order by name asc limit 3;
```

#### OFFSET - ignore first n
```sql 
select * from employee order by name asc limit 3 offset 2;
 ```

#### ALIAS
```sql 
select name as employeeName from employee;
select name "employeeName" from employee;
```


#### CREATE FOREIGN KEY
during table creation
```sql 
create table department (id not null primary key auto_increment, deptName varchar(200), cid int,
foreign key(cid) references employee(id));
```

#### CREATE FOREIGN KEY
after table is created
```sql 
create table department (id not null primary key auto_increment, deptName varchar(200)); 
alter table add column cid int;
OR 
```
with constraint
```sql
alter table department add constraint fk_employee01 foreign key (cid) references customer(id);
```

without constraint
```sql
alter table department add foreign key(cid) references customer(id); 
```

#### Drop foreign key
```sql 
alter table department drop foreign key [constraint_name]
 ```

#### JOIN TABLES 
fetch data from multiple tables

#### Normal join
without alias
```sql
SELECT employee.name, employee.city, department.name
FROM employee, department
WHERE employee.id = department.eid
```

with alias
```sql  
SELECT e.name, e.city, d.name
FROM employee e, department d
WHERE e.id = d.eid
```


#### Functions
#### Sum
```sql 
select sum(salary) from employee where city = "New Delhi"; // total salary goes to new delhi employees
```

#### Avg
#### Count
```sql 
select count(name) from employee where city = "New Delhi"; // total count of employees from New Delhi location;
```
```sql 
select count(gender) from employee;
```

#### String functions
```sql 
length("str")
concate(str1, str2)
lcase(str)
ucase(str)
substring(str, start, length)
trim(str)
```

#### More functions
```sql 
database()
version()
user()
select DATABASE() "DB", VERSION() "version" USER() "user";
```

#### Math functions
``` sin ```
``` cos ```
``` tan ```

#### CREATE PROCEDURE
```sql 
delimiter //
```

```sql 
create procedure CreateUserTable()
  begin
  create table if not exists customer( customerId int, customerName varchar(255) );
  insert into customer values (101, "John Doe");
  select * from customer;
  end // 
 call CreateUserTable();
```



#### Create User 'admin' password 'admin'
````sql
select host, user from user;

CREATE USER 'admin'@'%' IDENTIFIED BY 'admin';   // Create a new user account with a desired username and password: 

GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%';   // Grant appropriate privileges to the new user account:

FLUSH PRIVILEGES;   // to apply all changes

````

#### NODE JS connection

```js
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
```





#### PRIVILLAGES
Mxl::8AVvn837.?wvh6?J;3*z+nh93Cw

#### Optional
Check the list of users

```
use mysql; 
select user from user;
```

#### Create a user for connection

```
CREATE USER 'dbeaver'@'%' IDENTIFIED BY 'dbeaver';
GRANT ALL PRIVILEGES ON *.* TO 'dbeaver'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```





#### Expanding the ESLint configuration

If you are developing a production application, we recommend updating the configuration to enable type aware lint rules:

#### Configure the top-level `parserOptions` property like this:

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

