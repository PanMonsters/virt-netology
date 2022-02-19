# Домашнее задание к занятию "6.3. MySQL"

---
## Задача 1

<details><summary>.</summary>

Используя docker поднимите инстанс MySQL (версию 8). Данные БД сохраните в volume.

Изучите [бэкап БД](https://github.com/netology-code/virt-homeworks/tree/master/06-db-03-mysql/test_data) и 
восстановитесь из него.

Перейдите в управляющую консоль `mysql` внутри контейнера.

Используя команду `\h` получите список управляющих команд.

Найдите команду для выдачи статуса БД и **приведите в ответе** из ее вывода версию сервера БД.

Подключитесь к восстановленной БД и получите список таблиц из этой БД.

**Приведите в ответе** количество записей с `price` > 300.

В следующих заданиях мы будем продолжать работу с данным контейнером.
    
</details>

## Решение 1

```
# Подготавливаю образ
docker pull mysql:8.0

# Cоздаю volume
docker volume create vol1
docker volume create vol2

# Поднимаю контейнер
docker run --name test_mysql --network host -e MYSQL_ROOT_PASSWORD=mysql -ti -d -v vol1:/etc/mysql/ -v vol2:/etc/mysql/backup mysql:8.0

# Копирую бекап в контейнер
docker cp test_dump.sql test_mysql:/etc/mysql/backup

# Создаю базу test_db
exec -it test_mysql mysql -u root --password=mysql -h localhost -P 3306
CREATE DATABASE test_db;

# Востанавливаю бд из бекапа
docker exec -it test_mysql bash
mysql -u root -p test_db < test_dump.sql

# Выбираю необходимую бд
use test_db
```
![image](https://github.com/PanMonsters/virt-netology/blob/b8831331e2988cdd62caac757b90934ec506a65e/image/MySQL1.png)

---
## Задача 2
    
<details><summary>.</summary>

Создайте пользователя test в БД c паролем test-pass, используя:
- плагин авторизации mysql_native_password
- срок истечения пароля - 180 дней 
- количество попыток авторизации - 3 
- максимальное количество запросов в час - 100
- аттрибуты пользователя:
    - Фамилия "Pretty"
    - Имя "James"

Предоставьте привелегии пользователю `test` на операции SELECT базы `test_db`.
    
Используя таблицу INFORMATION_SCHEMA.USER_ATTRIBUTES получите данные по пользователю `test` и 
**приведите в ответе к задаче**.
    
</details>

## Решение 2

```
# Создаю пользователя с паролем test_pass
CREATE USER 'test'@'localhost' IDENTIFIED BY 'test-pass';

# Задаю атрибуты имя и фамилию
ALTER USER 'test'@'localhost' ATTRIBUTE '{"fname":"James", "lname":"Pretty"}';


# максимальное количество запросов в час – 100
# срок истечения пароля - 180 дней
# количество попыток авторизации - 3
ALTER USER 'test'@'localhost'
    -> IDENTIFIED BY 'test-pass'
    -> WITH
    -> MAX_QUERIES_PER_HOUR 100
    -> PASSWORD EXPIRE INTERVAL 180 DAY
    -> FAILED_LOGIN_ATTEMPTS 3 PASSWORD_LOCK_TIME 2;
```
- Используя таблицу INFORMATION_SCHEMA.USER_ATTRIBUTES получите данные по пользователю test и приведите в ответе к задаче.

```
SELECT * FROM INFORMATION_SCHEMA.USER_ATTRIBUTES WHERE USER='test';
```
![image](https://github.com/PanMonsters/virt-netology/blob/b8831331e2988cdd62caac757b90934ec506a65e/image/MySQL2.png)

---
## Задача 3
    
<details><summary>.</summary>

Установите профилирование `SET profiling = 1`.
Изучите вывод профилирования команд `SHOW PROFILES;`.

Исследуйте, какой `engine` используется в таблице БД `test_db` и **приведите в ответе**.

Измените `engine` и **приведите время выполнения и запрос на изменения из профайлера в ответе**:
- на `MyISAM`
- на `InnoDB`
    
</details>

## Решение 3

```
# Устанавливаю профилирование
set profiling=1;

# С помощью запроса узнаю движок
mysql> SELECT TABLE_NAME,ENGINE,ROW_FORMAT FROM information_schema.TABLES WHERE table_name = 'orders' and  TABLE_SCHEMA = 'test_db' ORDER BY ENGINE asc;
```
![image](https://github.com/PanMonsters/virt-netology/blob/b8831331e2988cdd62caac757b90934ec506a65e/image/MySQL3.png)

- По умолчанию движок в таблице используется InnoDB

```
mysql> alter table orders engine = 'MyISAM';
Query OK, 5 rows affected (0.84 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> alter table orders engine = 'InnoDB';
Query OK, 5 rows affected (0.17 sec)
Records: 5  Duplicates: 0  Warnings: 0
```
- Смена на движок MyISAM занимает в разы больше времени чем смена в обратную сторону.

---
## Задача 4 
    
<details><summary>.</summary>

Изучите файл `my.cnf` в директории /etc/mysql.

Измените его согласно ТЗ (движок InnoDB):
- Скорость IO важнее сохранности данных
- Нужна компрессия таблиц для экономии места на диске
- Размер буффера с незакомиченными транзакциями 1 Мб
- Буффер кеширования 30% от ОЗУ
- Размер файла логов операций 100 Мб

Приведите в ответе измененный файл `my.cnf`.
    
 </details>
 
 ## Решение 4
 
- Скорость IO важнее сохранности данных

```
# 0 - скорость
# 1 - сохранность
# 2 - универсальный параметр
innodb_flush_log_at_trx_commit = 0 
```
- Нужна компрессия таблиц для экономии места на диске

```
# Barracuda - формат файла с сжатием путем увеличения нагрузки на цпу
innodb_file_format=Barracuda
```
- Размер буффера с незакомиченными транзакциями 1 Мб
```
innodb_log_buffer_size	= 1M
```
- Буффер кеширования 30% от ОЗУ
```
key_buffer_size = 300М
```
- Размер файла логов операций 100 Мб
```
max_binlog_size	= 100M
```

