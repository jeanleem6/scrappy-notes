---
title: Mysql Shell
date: 2016-11-22 09:24:24
tags: [mysql]
---

## Install MySQL

``` bash
    brew install MySQL
```

设置MySql开机启动

``` bash
    mkdir -p ~/Library/LaunchAgents    # 首先确认该目录是否存在，若已经存在不用执行本命令
    ln -sfv /usr/local/opt/mysql/*.plist ~/Library/LaunchAgents
    launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
```

启动MySql服务

``` bash
    mysql.server start
```

<!-- more -->

## Fix Errors

如果在启动过程中出现如下错误：`ERROR! The server quit without updating PID file` ，使用以下方法修复。

``` bash
    sudo chmod -R 755 /usr/local/var/mysql
    rm -Rf /usr/local/var/mysql/Your-Machine-Name.local.err
```

> 注:将Your-Machine-Name替换为机器名称。


---

## Access MySQL

``` bash
    mysql -u root -p
```

## Show DataBase

``` bash
    mysql> show databases;
    +--------------------+
    | Database           |
    +--------------------+
    | information_schema |
    | mysql              |
    | performance_schema |
    | sys                |
    +--------------------+
    4 rows in set (0.00 sec)
```

## Create DataBase

``` bash
    CREATE DATABASE database name;
    # eg:
    CREATE DATABASE myblog
```

``` bash
    mysql> show databases;
    +--------------------+
    | Database           |
    +--------------------+
    | information_schema |
    | myblog             |
    | mysql              |
    | performance_schema |
    | sys                |
    +--------------------+
    5 rows in set (0.00 sec)
```

## Delete DataBase

``` bash
    DROP DATABASE database name;
    # eg:
    DROP DATABASE
```

## Access a Database

``` bash
    USE myblog;
```

### OverView Tables

In the same way that you could check the available databases, you can also see an overview of the tables that the database contains.

``` bash
    SHOW tables;
```

### Create a Table

``` bash
    CREATE TABLE potluck (id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(20),
    food VARCHAR(30),
    confirmed CHAR(1),
    signup_date DATE);
```

This command accomplishes a number of things:

1. It has created a table called potluck within the directory, events.
2. We have set up 5 columns in the table—id, name, food, confirmed, and signup date.
3. The “id” column has a command (INT NOT NULL PRIMARY KEY AUTO_INCREMENT) that automatically numbers each row.
4. The “name” column has been limited by the VARCHAR command to be under 20 characters long.
5. The “food” column designates the food each person will bring. The VARCHAR limits text to be under 30 characters.
6. The “confirmed” column records whether the person has RSVP’d with one letter, Y or N.
7. The “date” column will show when they signed up for the event. MySQL requires that dates be written as yyyy-mm-dd

``` bash
    mysql> SHOW TABLES;
    +------------------+
    | Tables_in_myblog |
    +------------------+
    | potluck          |
    +------------------+
    1 row in set (0.01 sec)
```

### Table’s Organization

``` bash
    DESCRIBE potluck;
```

For example,

``` bash
    mysql>DESCRIBE potluck;
    +-------------+-------------+------+-----+---------+----------------+
    | Field       | Type        | Null | Key | Default | Extra          |
    +-------------+-------------+------+-----+---------+----------------+
    | id          | int(11)     | NO   | PRI | NULL    | auto_increment |
    | name        | varchar(20) | YES  |     | NULL    |                |
    | food        | varchar(30) | YES  |     | NULL    |                |
    | confirmed   | char(1)     | YES  |     | NULL    |                |
    | signup_date | date        | YES  |     | NULL    |                |
    +-------------+-------------+------+-----+---------+----------------+
    5 rows in set (0.01 sec)
```

## Add Information to a Table

``` bash
    INSERT INTO `potluck` (`id`,`name`,`food`,`confirmed`,`signup_date`) VALUES (NULL, "John", "Casserole","Y", '2016-11-22');
```

Once you input that in, you will see the words:

``` bash
    Query OK, 1 row affected (0.00 sec)
```

Let’s add a couple more people to our group:

``` bash
    INSERT INTO `potluck` (`id`,`name`,`food`,`confirmed`,`signup_date`) VALUES (NULL, "Sandy", "Key Lime Tarts","N", '2016-11-22');
    INSERT INTO `potluck` (`id`,`name`,`food`,`confirmed`,`signup_date`) VALUES (NULL, "Tom", "BBQ","Y", '2016-11-18');
    INSERT INTO `potluck` (`id`,`name`,`food`,`confirmed`,`signup_date`) VALUES (NULL, "Tina", "Salad","Y", '2016-11-15');
```

<!--  -->

``` bash
    mysql> SELECT * FROM potluck;
    +----+-------+----------------+-----------+-------------+
    | id | name  | food           | confirmed | signup_date |
    +----+-------+----------------+-----------+-------------+
    |  1 | John  | Casserole      | Y         | 2012-04-11  |
    |  2 | Sandy | Key Lime Tarts | N         | 2012-04-14  |
    |  3 | Tom   | BBQ            | Y         | 2012-04-18  |
    |  4 | Tina  | Salad          | Y         | 2012-04-10  |
    +----+-------+----------------+-----------+-------------+
    4 rows in set (0.00 sec)
```

## Update Information in the Table

``` bash
    UPDATE `potluck`
    SET
    `confirmed` = 'Y'
    WHERE `potluck`.`name` ='Sandy';
```

## Add and Delete a Column

``` bash
    ALTER TABLE potluck ADD email VARCHAR(40);  # Add
    ALTER TABLE potluck ADD email VARCHAR(40) AFTER name;  # Add a Column 'email' after 'name'
    ALTER TABLE potluck DROP email;  # Delete
```

## Delete a Row

``` bash
    DELETE from [table name] where [column name]=[field text];
```

For example,

``` bash
    mysql> DELETE from potluck  where name='Sandy';
    Query OK, 1 row affected (0.00 sec)

    mysql> SELECT * FROM potluck;
    +----+------+-----------+-----------+-------------+
    | id | name | food      | confirmed | signup_date |
    +----+------+-----------+-----------+-------------+
    |  1 | John | Casserole | Y         | 2012-04-11  |
    |  3 | Tom  | BBQ       | Y         | 2012-04-18  |
    |  4 | Tina | Salad     | Y         | 2012-04-10  |
    +----+------+-----------+-----------+-------------+
    3 rows in set (0.00 sec)
```

> Notice that the `id numbers` associated with each person `remain the same`.

