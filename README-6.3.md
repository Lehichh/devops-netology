# devops-netology
**Sarkisyan Aleksey**

**Домашнее задание - Оркестрация группой Docker контейнеров на примере Docker Compose**


**Задание 1**

```
vagrant@server1:~/dz62$ docker run --name mysql -v dbfile:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root -d mysql:8

vagrant@server1:~/dz62$ cat test_dump.sql | docker exec -i mysql /usr/bin/mysql -u root --password=root testdb

mysql> \s
--------------
mysql  Ver 8.0.28 for Linux on x86_64 (MySQL Community Server - GPL)

Connection id:          17
Current database:       testdb
Current user:           root@localhost
SSL:                    Not in use
Current pager:          stdout
Using outfile:          ''
Using delimiter:        ;
Server version:         8.0.28 MySQL Community Server - GPL
Protocol version:       10
Connection:             Localhost via UNIX socket
Server characterset:    utf8mb4
Db     characterset:    utf8mb4
Client characterset:    latin1
Conn.  characterset:    latin1
UNIX socket:            /var/run/mysqld/mysqld.sock
Binary data as:         Hexadecimal
Uptime:                 3 days 10 hours 37 min 36 sec

Threads: 2  Questions: 91  Slow queries: 0  Opens: 165  Flush tables: 3  Open tables: 82  Queries per second avg: 0.000
--------------


mysql> select * from orders where price>300;
+----+----------------+-------+
| id | title          | price |
+----+----------------+-------+
|  2 | My little pony |   500 |
+----+----------------+-------+
1 row in set (0.00 sec)
```

**Задание 2**

```
mysql> greate user ''test'@'localhost' identified by 'test-pass';
mysql> SET GLOBAL default_password_lifetime = 180;
mysql> alter user 'test'@'localhost' FAILED_LOGIN_ATTEMPTS 3 PASSWORD_LOCK_TIME UNBOUNDED;
mysql> alter user 'test'@'localhost' PASSWORD EXPIRE DEFAULT;
mysql> alter user 'test'@'localhost' WITH MAX_QUERIES_PER_HOUR 100;
mysql> FLUSH PRIVILEGES;
mysql> select * from INFORMATION_SCHEMA.USER_ATTRIBUTES where user='test';
+------+-----------+---------------------------------------+
| USER | HOST      | ATTRIBUTE                             |
+------+-----------+---------------------------------------+
| test | localhost | {"fname": "Pretty", "lname": "James"} |
+------+-----------+---------------------------------------+
1 row in set (0.00 sec)

```



**Задание 3**

```
mysql> SHOW TABLE STATUS FROM mysql LIKE 'plugin'\G;
*************************** 1. row ***************************
           Name: plugin
         Engine: InnoDB
        Version: 10
     Row_format: Dynamic
           Rows: 0
 Avg_row_length: 0
    Data_length: 16384
Max_data_length: 0
   Index_length: 0
      Data_free: 4194304
 Auto_increment: NULL
    Create_time: 2022-03-02 08:56:47
    Update_time: NULL
     Check_time: NULL
      Collation: utf8_general_ci
       Checksum: NULL
 Create_options: row_format=DYNAMIC stats_persistent=0
        Comment: MySQL plugins
1 row in set (0.02 sec)


mysql> SHOW PROFILES;
+----------+------------+--------------------------------------------+
| Query_ID | Duration   | Query                                      |
+----------+------------+--------------------------------------------+
|        1 | 0.00124800 | SHOW ENGINES                               |
|        2 | 0.02589150 | SHOW TABLE STATUS FROM mysql LIKE 'plugin' |
|        3 | 0.00074500 | ALTER TABLE orders ENGINE = MyISAM         |
|        4 | 0.00015175 | testdb
ALTER TABLE orders ENGINE = MyISAM  |
|        5 | 0.00376700 | show databases                             |
|        6 | 0.00024225 | SELECT DATABASE()                          |
|        7 | 0.00040800 | show databases                             |
|        8 | 0.00093175 | show tables                                |
|        9 | 0.00073350 | show tables                                |
|       10 | 0.03432300 | ALTER TABLE orders ENGINE = MyISAM         |
|       11 | 0.03479225 | ALTER TABLE orders ENGINE = InnoDB         |
+----------+------------+--------------------------------------------+
11 rows in set, 1 warning (0.00 sec)
```


**Задание 4**

```
[mysqld]
pid-file        = /var/run/mysqld/mysqld.pid
socket          = /var/run/mysqld/mysqld.sock
datadir         = /var/lib/mysql
secure-file-priv = NULL
innodb_log_file_size = 100M
innodb_buffer_pool_size = 4.8G
innodb_log_buffer_size = 1M
innodb_file_per_table = ON
innodb_file_format=Barracuda
innodb_flush_log_at_trx_commit = 0
```
