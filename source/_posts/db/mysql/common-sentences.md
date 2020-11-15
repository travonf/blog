---
title: mysql常用语句
date: 2009-07-02 08:00:00
updated: 2009-07-02 08:00:00
tags: "mysql"
categories: "Database"
---

# 登陆控制台

```shell
# mysql -u root -p
```

<!-- more -->

# 查看数据库

```sql
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| test               |
+--------------------+
3 rows in set (0.00 sec)
```

# 查看数据表

```sql
mysql> USE mysql;
mysql> SHOW TABLES;
+---------------------------+
| Tables_in_mysql           |
+---------------------------+
| columns_priv              |
| db                        |
| event                     |
| func                      |
| time_zone_transition      |
| time_zone_transition_type |
| user                      |
+---------------------------+
23 rows in set (0.00 sec)
```

# 查看表结构

```sql
1. mysql> show columns from user;
2. mysql> DESCRIBE user;
+-----------------------+-----------------------------------+------+-----+---------+-------+
| Field                 | Type                              | Null | Key | Default | Extra |
+-----------------------+-----------------------------------+------+-----+---------+-------+
| Host                  | char(60)                          | NO   | PRI |         |       |
| User                  | char(16)                          | NO   | PRI |         |       |
| Password              | char(41)                          | NO   |     |         |       |
| Select_priv           | enum('N','Y')                     | NO   |     | N       |       |
| Insert_priv           | enum('N','Y')                     | NO   |     | N       |       |
| Update_priv           | enum('N','Y')                     | NO   |     | N       |       |
| Delete_priv           | enum('N','Y')                     | NO   |     | N       |       |
| max_updates           | int(11) unsigned                  | NO   |     | 0       |       |
| max_connections       | int(11) unsigned                  | NO   |     | 0       |       |
| max_user_connections  | int(11) unsigned                  | NO   |     | 0       |       |
+-----------------------+-----------------------------------+------+-----+---------+-------+
39 rows in set (0.00 sec)
```

# 创建数据库

```sql
mysql> CREATE DATABASE 库名;
```

# 删除数据库

```sql
mysql> DROP DATABASE 库名;
```

# 创建数据库

```sql
mysql> USE 库名;
mysql> CREATE TABLE 表名 (字段名 VARCHAR(20), 字段名 CHAR(1));
```

# 删除数据表

```sql
mysql> DROP TABLE 表名;
```

# 将表中记录清空

```sql
mysql> DELETE FROM 表名;
```

# 查询

```sql
select user,host,password from mysql.user;
+------+-----------+----------+
| user | host      | password |
+------+-----------+----------+
| root | localhost |          |
| root | RHEL6x64  |          |
| root | 127.0.0.1 |          |
|      | localhost |          |
|      | RHEL6x64  |          |
+------+-----------+----------+
5 rows in set (0.00 sec)
```

# 授权

```sql
show grants for 'root'@'localhost';
+---------------------------------------------------------------------+
| Grants for root@localhost                                           |
+---------------------------------------------------------------------+
| GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' WITH GRANT OPTION |
+---------------------------------------------------------------------+
1 row in set (0.00 sec)
```
