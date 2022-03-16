# devops-netology
**Sarkisyan Aleksey**

**Домашнее задание - Оркестрация группой Docker контейнеров на примере Docker Compose**


**Задание 1**

```
version: '2.1'

services:
  postgres:
    image: postgres:12.0
    environment:
      POSTGRES_USER: postgres
      POSTGRES_DB: test_db
      POSTGRES_PASSWORD: postgres
	  PGDATA: "/var/lib/postgresql/data/pgdata"
    volumes:
      - .:/var/lib/postgresql/data
    ports:
      - "5432:5432"
```

**Задание 2**


**Итоговый список БД**

```
postgres=# \l
                                 List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges
-----------+----------+----------+------------+------------+-----------------------
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 |
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 test_db   | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =Tc/postgres         +
           |          |          |            |            | postgres=CTc/postgres
(4 rows)
```

**Описание таблиц**

```
postgres=# \c test_db
You are now connected to database "test_db" as user "postgres".
test_db=# \d+ orders
                                                      Table "public.orders"
    Column    |     Type      | Collation | Nullable |              Default               | Storage  | Stats target | Desc
ription
--------------+---------------+-----------+----------+------------------------------------+----------+--------------+-----
--------
 id           | integer       |           | not null | nextval('orders_id_seq'::regclass) | plain    |              |
 наименование | character(30) |           |          |                                    | extended |              |
 цена         | integer       |           |          |                                    | plain    |              |
Indexes:
    "orders_pkey" PRIMARY KEY, btree (id)
Referenced by:
    TABLE "clients" CONSTRAINT "clients_заказ_fkey" FOREIGN KEY ("заказ") REFERENCES orders(id)
Access method: heap

test_db=# \d+ clients
                                                         Table "public.clients"
      Column       |     Type      | Collation | Nullable |               Default               | Storage  | Stats target
| Description
-------------------+---------------+-----------+----------+-------------------------------------+----------+--------------
+-------------
 id                | integer       |           | not null | nextval('clients_id_seq'::regclass) | plain    |
|
 фамилия           | character(30) |           |          |                                     | extended |
|
 страна проживания | character(30) |           |          |                                     | extended |
|
 заказ             | integer       |           |          |                                     | plain    |
|
Indexes:
    "clients_pkey" PRIMARY KEY, btree (id)
Foreign-key constraints:
    "clients_заказ_fkey" FOREIGN KEY ("заказ") REFERENCES orders(id)
Access method: heap
```


**Запрос на пользователей с правами**

```
test_db=# select * from information_schema.table_privileges where table_schema = 'public';
 grantor  |     grantee      | table_catalog | table_schema | table_name | privilege_type | is_grantable | with_hierarchy
----------+------------------+---------------+--------------+------------+----------------+--------------+----------------
 postgres | postgres         | test_db       | public       | orders     | INSERT         | YES          | NO
 postgres | postgres         | test_db       | public       | orders     | SELECT         | YES          | YES
 postgres | postgres         | test_db       | public       | orders     | UPDATE         | YES          | NO
 postgres | postgres         | test_db       | public       | orders     | DELETE         | YES          | NO
 postgres | postgres         | test_db       | public       | orders     | TRUNCATE       | YES          | NO
 postgres | postgres         | test_db       | public       | orders     | REFERENCES     | YES          | NO
 postgres | postgres         | test_db       | public       | orders     | TRIGGER        | YES          | NO
 postgres | test_admin_user  | test_db       | public       | orders     | INSERT         | NO           | NO
 postgres | test_admin_user  | test_db       | public       | orders     | SELECT         | NO           | YES
 postgres | test_admin_user  | test_db       | public       | orders     | UPDATE         | NO           | NO
 postgres | test_admin_user  | test_db       | public       | orders     | DELETE         | NO           | NO
 postgres | test_admin_user  | test_db       | public       | orders     | TRUNCATE       | NO           | NO
 postgres | test_admin_user  | test_db       | public       | orders     | REFERENCES     | NO           | NO
 postgres | test_admin_user  | test_db       | public       | orders     | TRIGGER        | NO           | NO
 postgres | test_simple_user | test_db       | public       | orders     | INSERT         | NO           | NO
 postgres | test_simple_user | test_db       | public       | orders     | SELECT         | NO           | YES
 postgres | test_simple_user | test_db       | public       | orders     | UPDATE         | NO           | NO
 postgres | test_simple_user | test_db       | public       | orders     | DELETE         | NO           | NO
 postgres | postgres         | test_db       | public       | clients    | INSERT         | YES          | NO
 postgres | postgres         | test_db       | public       | clients    | SELECT         | YES          | YES
 postgres | postgres         | test_db       | public       | clients    | UPDATE         | YES          | NO
 postgres | postgres         | test_db       | public       | clients    | DELETE         | YES          | NO
 postgres | postgres         | test_db       | public       | clients    | TRUNCATE       | YES          | NO
 postgres | postgres         | test_db       | public       | clients    | REFERENCES     | YES          | NO
 postgres | postgres         | test_db       | public       | clients    | TRIGGER        | YES          | NO
 postgres | test_admin_user  | test_db       | public       | clients    | INSERT         | NO           | NO
 postgres | test_admin_user  | test_db       | public       | clients    | SELECT         | NO           | YES
 postgres | test_admin_user  | test_db       | public       | clients    | UPDATE         | NO           | NO
 postgres | test_admin_user  | test_db       | public       | clients    | DELETE         | NO           | NO
 postgres | test_admin_user  | test_db       | public       | clients    | TRUNCATE       | NO           | NO
 postgres | test_admin_user  | test_db       | public       | clients    | REFERENCES     | NO           | NO
 postgres | test_admin_user  | test_db       | public       | clients    | TRIGGER        | NO           | NO
 postgres | test_simple_user | test_db       | public       | clients    | INSERT         | NO           | NO
 postgres | test_simple_user | test_db       | public       | clients    | SELECT         | NO           | YES
 postgres | test_simple_user | test_db       | public       | clients    | UPDATE         | NO           | NO
 postgres | test_simple_user | test_db       | public       | clients    | DELETE         | NO           | NO
(36 rows)
```


**Список пользователей с правами на БД**

```
test_db=# \dp
                                          Access privileges
 Schema |      Name      |   Type   |        Access privileges         | Column privileges | Policies
--------+----------------+----------+----------------------------------+-------------------+----------
 public | clients        | table    | postgres=arwdDxt/postgres       +|                   |
        |                |          | test_admin_user=arwdDxt/postgres+|                   |
        |                |          | test_simple_user=arwd/postgres   |                   |
 public | clients_id_seq | sequence |                                  |                   |
 public | orders         | table    | postgres=arwdDxt/postgres       +|                   |
        |                |          | test_admin_user=arwdDxt/postgres+|                   |
        |                |          | test_simple_user=arwd/postgres   |                   |
 public | orders_id_seq  | sequence |                                  |                   |
(4 rows)
```


**Задание 3**

```
test_db=# select count(*) from orders;
 count
-------
     5
(1 row)

test_db=# select count(*) from clients;
 count
-------
     5
(1 row)

test_db=# select * from orders;
 id |          наименование          | цена
----+--------------------------------+------
  1 | Шоколад                        |   10
  2 | Принтер                        | 3000
  3 | Книга                          |  500
  4 | Монитор                        | 7000
  5 | Гитара                         | 4000
(5 rows)

test_db=# select * from clients;
 id |            фамилия             |       страна проживания        | заказ
----+--------------------------------+--------------------------------+-------
  1 | Иванов Иван Иванович           | USA                            |
  2 | Петров Петр Петрович           | Canada                         |
  3 | Иоганн Себастьян Бах           | Japan                          |
  4 | Ронни Джеймс Дио               | Russia                         |
  5 | Ritchie Blackmore              | Russia                         |
(5 rows)
```


**Задание 4**

```
test_db=# update clients set заказ = 3  where фамилия = 'Иванов Иван Иванович';
UPDATE 1
test_db=# update clients set заказ = 4  where фамилия = 'Петров Петр Петрович';
UPDATE 1
test_db=# update clients set заказ = 5  where фамилия = 'Иоганн Себастьян Бах';
UPDATE 1
test_db=# select * from clients;
 id |            фамилия             |       страна проживания        | заказ
----+--------------------------------+--------------------------------+-------
  4 | Ронни Джеймс Дио               | Russia                         |
  5 | Ritchie Blackmore              | Russia                         |
  1 | Иванов Иван Иванович           | USA                            |     3
  2 | Петров Петр Петрович           | Canada                         |     4
  3 | Иоганн Себастьян Бах           | Japan                          |     5
(5 rows)

test_db=# select * from clients where заказ is not null;
 id |            фамилия             |       страна проживания        | заказ
----+--------------------------------+--------------------------------+-------
  1 | Иванов Иван Иванович           | USA                            |     3
  2 | Петров Петр Петрович           | Canada                         |     4
  3 | Иоганн Себастьян Бах           | Japan                          |     5
(3 rows)
```


**Задание 5**

```
test_db=# explain select * from clients where заказ is not null;
                         QUERY PLAN
------------------------------------------------------------
 Seq Scan on clients  (cost=0.00..12.80 rows=279 width=256)
   Filter: ("заказ" IS NOT NULL)
(2 rows)
```

время, которое проходит, прежде чем начнется вывод данных и приблизительная общая стоимость

Ожидаемое число строк, которое должно вывести.

Средний размер строк в байтах.


**Задание 6**

Для бекапа я немного поменял файл докера из первого задания

```
version: '2.1'

services:
  postgres:
    image: postgres:12.0
    environment:
      POSTGRES_USER: postgres
      POSTGRES_DB: test_db
      POSTGRES_PASSWORD: postgres
    volumes:
      - ./pgdata:/var/lib/postgresql/data
      - ./pgbackup:/var/lib/postgresql/backup
    ports:
      - "5432:5432"
```

**делаю бэкап и копирую его в volume**

```
vagrant@server1:~/dz6.1/test$ docker exec -u postgres test-postgres-1 pg_dump -Fc test_db >db.dump
vagrant@server1:~/dz6.1/test$ docker cp db.dump test-postgres-1:/var/lib/postgresql/backup
```

**Останавливаю и удаляю контейнер**

```
vagrant@server1:~/dz6.1/test$ docker-compose down
```

**файл докера для нового контейнера**

```
version: '2.1'

services:
  postgres:
    image: postgres:12.0
    environment:
      POSTGRES_USER: postgres
      POSTGRES_DB: test_db
      POSTGRES_PASSWORD: postgres
    volumes:
      - ./pgdata2:/var/lib/postgresql/data
      - ./pgbackup:/var/lib/postgresql/backup
    ports:
      - "5432:5432"
```

**восстановление бд**

```
vagrant@server1:~/dz6.1/test$ docker exec -i -u postgres test-postgres-1 pg_restore -d test_db < pgbackup/db.dump
```