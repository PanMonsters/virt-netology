# Домашнее задание к занятию "6.2. SQL"

---
## Задача 1

<details><summary>.</summary>

Используя docker поднимите инстанс PostgreSQL (версию 12) c 2 volume, 
в который будут складываться данные БД и бэкапы.

Приведите получившуюся команду или docker-compose манифест.
    
</details>

## Решение 1

```
vagrant@ubuntu-16:~$ docker pull postgres:12  

vagrant@ubuntu-16:~$ docker volume create vol1  
vol1  

vagrant@ubuntu-16:~$ docker volume create vol2  
vol2  

root@ubuntu-16:/var/lib/docker/volumes/vol2/_data/data# docker run --network host --name postgres_test -e POSTGRES_PASSWORD=postgres -ti -d -v vol1:/var/lib/postgresql/data -v vol2:/var/lib/postgresql/backup postgres:12  

vagrant@ubuntu-16:~$ docker exec -it 6fc86b69589c psql -h localhost -p 5432 -U postgres

postgres=# \l  
```
![image](https://github.com/PanMonsters/virt-netology/blob/306dc89bbfd8357b91d2e58ae6fd0be1c6974b52/image/SQL1.png)
---
## Задача 2

<details><summary>.</summary>

В БД из задачи 1: 
- создайте пользователя test-admin-user и БД test_db
- в БД test_db создайте таблицу orders и clients (спeцификация таблиц ниже)
- предоставьте привилегии на все операции пользователю test-admin-user на таблицы БД test_db
- создайте пользователя test-simple-user  
- предоставьте пользователю test-simple-user права на SELECT/INSERT/UPDATE/DELETE данных таблиц БД test_db

Таблица orders:
- id (serial primary key)
- наименование (string)
- цена (integer)

Таблица clients:
- id (serial primary key)
- фамилия (string)
- страна проживания (string, index)
- заказ (foreign key orders)

Приведите:
- итоговый список БД после выполнения пунктов выше,
- описание таблиц (describe)
- SQL-запрос для выдачи списка пользователей с правами над таблицами test_db
- список пользователей с правами над таблицами test_db
    
</details>
    
## Решение 2

```
# Создаю пользователя test-admin-user с паролем Street123
postgres=# CREATE USER "test-admin-user" WITH ENCRYPTED PASSWORD 'Street123';

Создаю пользователя test-simple-user с паролем Street123
test_db=# CREATE USER "test-simple-user" WITH ENCRYPTED PASSWORD 'Street123';

# Создаю базу данных test_db
postgres=# CREATE DATABASE test_db;	

postgres-# \connect test_db 

# Создаю таблицу orders
test_db=# CREATE TABLE orders (id INT PRIMARY KEY, title VARCHAR(50), price INT NOT NULL);

# Создаю таблицу clients
test_db=# CREATE TABLE clients (id INT PRIMARY KEY, second_name VARCHAR(50), сountry_residence VARCHAR(50), booking INT REFERENCES orders(id) ON DELETE CASCADE);

#Создаю индекс для сountry_residence
test_db=# CREATE INDEX indx_сountry_residence ON clients (сountry_residence);

#Разрешаю подключение пользователя test-admin-user к базе данных test_db
test_db=# GRANT CONNECT ON DATABASE test_db to "test-admin-user";

#Выдаю права на все таблица в схеме public для test-admin-user
test_db=# GRANT ALL ON ALL TABLES IN SCHEMA public to "test-admin-user";

#Разрешаю подключение пользователя test-simple-user к базе данных test_db
test_db=# GRANT CONNECT ON DATABASE test_db to "test-simple-user";

 #Выдаю необходимые права на все таблица в схеме public для test-simple-user";
test_db=# GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public to "test-simple-user";
```
- итоговый список БД после выполнения пунктов выше  
![image](https://github.com/PanMonsters/virt-netology/blob/306dc89bbfd8357b91d2e58ae6fd0be1c6974b52/image/SQL2.png)

- описание таблиц (describe)  
![image](https://github.com/PanMonsters/virt-netology/blob/306dc89bbfd8357b91d2e58ae6fd0be1c6974b52/image/SQL3.png)

- SQL-запрос для выдачи списка пользователей с правами над таблицами test_db
```
test_db=# SELECT * FROM information_schema.table_privileges WHERE table_catalog = 'test_db' AND grantee LIKE 'test%';
```

- список пользователей с правами над таблицами test_db
![image](https://github.com/PanMonsters/virt-netology/blob/306dc89bbfd8357b91d2e58ae6fd0be1c6974b52/image/SQL4.png)



---
## Задача 3

<details><summary>.</summary>

Используя SQL синтаксис - наполните таблицы следующими тестовыми данными:

Таблица orders

|Наименование|цена|
|------------|----|
|Шоколад| 10 |
|Принтер| 3000 |
|Книга| 500 |
|Монитор| 7000|
|Гитара| 4000|

Таблица clients

|ФИО|Страна проживания|
|------------|----|
|Иванов Иван Иванович| USA |
|Петров Петр Петрович| Canada |
|Иоганн Себастьян Бах| Japan |
|Ронни Джеймс Дио| Russia|
|Ritchie Blackmore| Russia|

Используя SQL синтаксис:
- вычислите количество записей для каждой таблицы 
- приведите в ответе:
    - запросы 
    - результаты их выполнения.
    
</details>

## Решение 3

```
#Наполняю таблицу orders  
test_db=# INSERT INTO orders (id, title, price) VALUES (1, 'chocolate', 10), (2, 'printer', 3000), (3, 'book', 500), (4, 'monitor', 7000), (5, 'guitar', 4000);

#Наполняю таблицу clients  
test_db=# INSERT INTO clients (id, second_name, сountry_residence) VALUES (1, 'Иванов Иван Иванович', 'USA'), (2, 'Петров Петр Петрович', 'Canada'), (3, 'Иоганн Себастьян Бах', 'Japan'), (4, 'Ронни Джеймс Дио', 'Russia'), (5, 'Ritchie Blackmore', 'Russia');  
```
![image](https://github.com/PanMonsters/virt-netology/blob/306dc89bbfd8357b91d2e58ae6fd0be1c6974b52/image/SQL5.png)

Используя SQL синтаксис:
- вычислите количество записей для каждой таблицы 
- приведите в ответе:
    - запросы 
    - результаты их выполнения.
        
```
test_db=# select count(*) from orders;

test_db=# select count(*) from clients;
```

![image](https://github.com/PanMonsters/virt-netology/blob/306dc89bbfd8357b91d2e58ae6fd0be1c6974b52/image/SQL6.png)

---
## Задача 4

<details><summary>.</summary>
    
Часть пользователей из таблицы clients решили оформить заказы из таблицы orders.

Используя foreign keys свяжите записи из таблиц, согласно таблице:

|ФИО|Заказ|
|------------|----|
|Иванов Иван Иванович| Книга |
|Петров Петр Петрович| Монитор |
|Иоганн Себастьян Бах| Гитара |

Приведите SQL-запросы для выполнения данных операций.

Приведите SQL-запрос для выдачи всех пользователей, которые совершили заказ, а также вывод данного запроса.
 
Подсказк - используйте директиву `UPDATE`.

</details>

## Решение 4

Приведите SQL-запросы для выполнения данных операций.

```
test_db=# update clients set booking = (select id from orders where title = 'book') where second_name = 'Иванов Иван Иванович';

test_db=# update clients set booking = (select id from orders where title = 'monitor') where second_name = 'Петров Петр Петрович';

test_db=# update clients set booking = (select id from orders where title = 'guitar') where second_name = 'Иоганн Себастьян Бах';

select c.* from clients c join orders o on c.booking = o.id;
```

![image](https://github.com/PanMonsters/virt-netology/blob/306dc89bbfd8357b91d2e58ae6fd0be1c6974b52/image/SQL7.png)

---
## Задача 5

<details><summary>.</summary>

Получите полную информацию по выполнению запроса выдачи всех пользователей из задачи 4 
(используя директиву EXPLAIN).

Приведите получившийся результат и объясните что значат полученные значения.
    
</details>

## Решение 5

```
test_db=# explain select c.* from clients c join orders o on c.booking = o.id;
```

![image](https://github.com/PanMonsters/virt-netology/blob/306dc89bbfd8357b91d2e58ae6fd0be1c6974b52/image/SQL8.png)

- Чтение таблицы orders
- Создание хеша для поля id
- Сканирование таблицы clients
- Для каждой строки по полю booking будет проверено, соответствует ли она чему-то в кеше orders
- При налии соответствий формируется вывод
- Так же указано примерное количество строк, вес и стоимость.

---
## Задача 6

<details><summary>.</summary>

Создайте бэкап БД test_db и поместите его в volume, предназначенный для бэкапов (см. Задачу 1).

Остановите контейнер с PostgreSQL (но не удаляйте volumes).

Поднимите новый пустой контейнер с PostgreSQL.

Восстановите БД test_db в новом контейнере.

Приведите список операций, который вы применяли для бэкапа данных и восстановления. 
    
</details>

## Решение 6

```
# Подключаюсь к контейнеру
vagrant@ubuntu-16:/var/lib$ docker exec -it postgres_test bash

# Создание бекапа на нужный volume
root@ubuntu-16:/var/lib/postgresql/backup# pg_dump -U postgres -W test_db > /var/lib/postgresql/backup/test_db.sql

# Останваливаю старый контейнер
vagrant@ubuntu-16:~$ docker stop postgres_test

# Поднимаю новый контейнер и монтирую volume с бекапом
vagrant@ubuntu-16:~$ docker run --network host --name postgres_test2 -e POSTGRES_PASSWORD=postgres -ti -d -v vol2:/var/lib/postgresql/backup postgres:12

# Подключаюсь к новому контейнеру
vagrant@ubuntu-16:~$ docker exec -it postgres_test2 bash

# Востановление из бекапа необходимой базы
root@ubuntu-16:/# psql -U postgres -W test_db < /var/lib/postgresql/backup/test_db.sql
```
Проверяю наличие базы и таблиц

![image](https://github.com/PanMonsters/virt-netology/blob/306dc89bbfd8357b91d2e58ae6fd0be1c6974b52/image/SQL9.png)


