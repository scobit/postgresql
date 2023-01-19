
psql 

#### Вывести список баз
psql -l 
                      
#### Информация о базах данных
SELECT datname, datistemplate, datallowconn, datconnlimit FROM pg_database;
     
где:
 - datistemplate - является ли база данных шаблоном;
 - datallowconn  - разрешены ли соединения с базой данных;
 - datconnlimit  - максимальное количество соединений (-1 = без ограничений).

При необходимости флаги можно изменить с помощью обычного update.

#### Подключиться к базе template1 и установить расширение pgcrypto.Дальше мы увидим, что новые БД будут создаваться уже с этим расширением.

\c template1

create extension pgcrypto;

Если бы расширение pgcrypto не было установлено с помощью make install, мы получили бы ошибку "ERROR: could not open extension control file..."

#### функции, входящие в расширение pgcrypto.Например, можно вычислить MD5-дайджест:

SELECT digest('Hello, world!', 'md5');
      
#### Чтобы шаблон можно было использовать для создания базы, к нему не должно быть активных подключений, поэтому отключимся от базы template1.
\c postgres

#### Создать базу данных
create database test;

#### Подключиться к базе данных test
\c test

#### Создание БД из shell
createdb test


#### По умолчанию при создании используется шаблон template1. Убедимся, что в новой базе доступно расширение pgcrypto:


#### Созать базу данных из шаблона template0 с максимальным количеством соединений = 20
create database test0 template template0 connection limit 20;

#### Подключиться к БД
\c test0
        
#### Проверить, что функции digest не существует        
select digest('Hello, world!', 'md5');


#### Вычислить размер БД
select pg_database_size('test0');
        
#### Вычислить размер БД в читаемом виде
select pg_size_pretty(pg_database_size('test0'));


#### Создадим таблицу и индекс:

create table t(n numeric);

create index t_idx on t(n);

insert into t select * from generate_series(1, 10000);

#### вывести размер, занимаемый таблицей:
select pg_size_pretty(pg_table_size('t'));

#### размер индексов таблицы:
select pg_size_pretty(pg_indexes_size('t'));

#### размер таблицы вместе с индексами:
select pg_size_pretty(pg_total_relation_size('t'));

#### Созданную базу данных можно переименовать:

alter database test rename to db;



#### Изменить количество соединений:
alter database db connection limit 10;
        

Базу данных можно удалить (если к ней нет активных подключений).

#### 
\conninfo

####
drop database db;

####
\c postgres

####
drop database test0;
    
Если база данных не существует, команда DROP DATABASE будет ругаться:

        => drop database db;
        ERROR:  database "db" does not exist

asdasdasdasd

        => asdasdasdasdasdasd
       
       
asdasdasdasd

        qwe
        

`asdasdagsfgsfgs`

Поэтому можно воспользоваться другой формой (она применима и к удалению других объектов): if nott exist тоже существует

        => drop database if exists db;
        NOTICE:  database "db" does not exist, skipping
        DROP DATABASE

        => \q
