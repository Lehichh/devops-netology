# devops-netology
**Sarkisyan Aleksey**

**Домашнее задание - 6.4. PostgreSQL**


**Задание 1**

```
vagrant@server1:~/dz64$ docker run --name dz64-postgres -e POSTGRES_PASSWORD=root -d postgres:13
vagrant@server1:~/dz64$ docker exec -ti dz64-postgres psql -U postgres
```

**вывода списка БД -** \l

**подключения к БД -** \c *dbname*

**вывода списка таблиц -** \dt

**вывода описания содержимого таблиц -** \dp

**выхода из psql -** \q




**Задание 2**

```
postgres=# CREATE DATABASE test_database;
vagrant@server1:~/dz64$ wget https://raw.githubusercontent.com/netology-code/virt-homeworks/master/06-db-04-postgresql/test_data/test_dump.sql
vagrant@server1:~/dz64$ docker exec -i -u postgres dz64-postgres psql test_database < ./test_dump.sql
vagrant@server1:~/dz64$ docker exec -ti dz64-postgres psql -U postgres
postgres=# \c test_database
test_database=# analyze orders;
test_database=# select max(avg_width) from pg_stats where tablename= 'orders';
```



**Задание 3**


**"ручное" разбиение**

```
test_database=# create table orders_1 as select * from orders where price > 499;
test_database=# create table orders_2 as select * from orders where price <= 499;
```

**исключить "ручное" разбиение можно**

```
test_database=# create table orders_1 (check (price > 499)) inherits (orders);
test_database=# create table orders_2 (check (price <= 499)) inherits (orders);
test_database=# create rule for_orders_1 as on insert to orders where (price>499) do instead insert into orders_1 values (new.*);
test_database=# create rule for_orders_2 as on insert to orders where (price<=499) do instead insert into orders_2 values (new.*);
```


**Задание 4**

```
vagrant@server1:~/dz64$ docker exec -u postgres dz64-postgres pg_dump -d test_database > db.sql

CREATE TABLE public.orders (
    id integer NOT NULL,
    title character varying(80) NOT NULL,
    price integer DEFAULT 0
	UNIQUE (title)
);
```
