# MySQL

[Getting Started with MySQL Quickly](https://www.mysqltutorial.org/getting-started-with-mysql/)

## install on mac

https://flaviocopes.com/mysql-how-to-install/

```sh
# install, start and secure
$ brew install mysql
$ brew services start mysql
$ mysql_secure_installation
...
$ brew services stop mysql

# start NOT in daemon mode (auto re-start it at reboo)
mysql.server start
mysql server stop
```



## Connect to server

```sh
$ mysql -u root -p
```

`-u root` means that you connect to the MySQL Server using the user account `root`.

`-p` instructs mysql to prompt for a password.



## Load a database

```
mysql> source c:\temp\mysqlsampledatabase.sql
```



## Basics

### SELECT...FROM

```mysql
SELECT 
    lastName, 
    firstName, 
    jobTitle
FROM
    employees;
```

```
+-----------+-----------+----------------------+
| lastname  | firstname | jobtitle             |
+-----------+-----------+----------------------+
| Murphy    | Diane     | President            |
| Patterson | Mary      | VP Sales             |
| Firrelli  | Jeff      | VP Marketing         |
| Patterson | William   | Sales Manager (APAC) |
| Bondur    | Gerard    | Sale Manager (EMEA)  |
```



select all columns

```
SELECT * 
FROM employees;
```



### ORDER BY

```mysql
SELECT 
   select_list
FROM 
   table_name
ORDER BY 
   column1 [ASC|DESC], 
   column2 [ASC|DESC],
   ...;
```

- First, sort the result set by the values in the `column1` in ascending order.
- Then, sort the sorted result set by the values in the `column2` in descending order. Note that **the order of values in the `column1` will not change in this step, only the order of values in the `column2` changes.**
- `ASC` is **default**

e.g.

```mysql
SELECT
	contactLastname,
	contactFirstname
FROM
	customers
ORDER BY
	contactLastname;
```

```
+-----------------+------------------+
| contactLastname | contactFirstname |
+-----------------+------------------+
| Accorti         | Paolo            |
| Altagar,G M     | Raanan           |
| Andersen        | Mel              |
| Anton           | Carmen           |
| Ashworth        | Rachel           |
| Barajas         | Miguel           |
| Benitez         | Violeta          |
| Bennett         | Helen            |
| Berglund        | Christina        |
| Bergulfsen      | Jonas            |
| Bertrand        | Marie            |
| Brown           | Julie            |
| Brown           | Ann              |
| Brown           | William          |
| Calaghan        | Ben              |
| Camino          | Alejandra        |
```



### sort data using FIELD()

The `FIELD()` function has the following syntax:

```sql
FIELD(str, str1, str2, ...);
```

The `FIELD()` function returns the position of the str in the str1, str2, … list. If the str is not in the list, the `FIELD()` function returns 0. For example, the following query returns 1 because the position of the string ‘A’ is the first position on the list `'A'`, `'B'`, and `'C'`:

```mysql
SELECT FIELD('A', 'A', 'B','C');
```

Output:

```
+--------------------------+
| FIELD('A', 'A', 'B','C') |
+--------------------------+
|                        1 |
+--------------------------+
1 row in set (0.00 sec)
```

e.g.

```sql
SELECT 
    orderNumber, status
FROM
    orders
ORDER BY FIELD(status,
        'In Process',
        'On Hold',
        'Cancelled',
        'Resolved',
        'Disputed',
        'Shipped');
```

Output:

```
+-------------+------------+
| orderNumber | status     |
+-------------+------------+
|       10425 | In Process |
|       10421 | In Process |
|       10422 | In Process |
|       10420 | In Process |
|       10424 | In Process |
|       10423 | In Process |
|       10414 | On Hold    |
|       10401 | On Hold    |
|       10334 | On Hold    |
|       10407 | On Hold    |
...
```

