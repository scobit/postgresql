### Назначение
Терминальный клиент для работы с PostgreSQL
Поставляется вместе с СУБД
Используется администраторами и разработчиками для
интерактивной работы и выполнения скриптов

#### справка
psql --help
man psql



#### create database
createdb mydb

createdb: command not found
then PostgreSQL was not installed properly. Either it was not installed at all or your shell's search path was not set to include it. # Try calling the command with an absolute path instead: The path at your site might be different
/usr/local/pgsql/bin/createdb mydb

### Команды psql в БД

#### Список комманд psql
\?

#### Список комманд 
\h[elp] SQL

#### синтаксис команды SQL
\h command

#### Выход из psql
\q

#### Параметры подключения

База данных: -d database или $PGDATABASE
по умолчанию совпадает с именем пользователя
Имя сервера: -h host или $PGHOST
по умолчанию локальное соединение
Порт: -p port или $PGPORT
по умолчанию можно задать при сборке, обычно 5432
Имя пользователя: -U username или $PGUSER
по умолчанию совпадает с именем пользователя

#### Подключение (или указать параметры в переменных окружения)
psql -d database -h host -p port -U username

#### Информация о подключении 
\conninfo

#### Отобразить список баз
\l

#### Информация о подключении 
\c[onnect]

#### Подключение к другой базе
\c[onnect] database username host port

Параметры \c должны идти в указанном порядке, но их можно
заменять на дефис. Например, чтобы 

#### Cменить пользователя в текущей БД
\c - username

#### При запуске выполняются скрипты (общий системный файл)
psqlrc

#### пользовательский файл
~/.psqlrc

#### Пользовательский файл через переменную окружения
$PSQLRC

#### История команд
~/.psql_history

#### История команд через переменную
или $PSQL_HISTORY, или HISTFILE


#### Отображение конфигурационного каталога
pg_config --sysconfdir

#### Создать БД
psql -c "CREATE DATABASE TypeDbName OWNER TypeOwnerName;"


### Справка, запуск и выход

$ psql --help
$ man psql
$ psql
postgres=# \? список команд psql
postgres=# \h[elp] список команд SQL
postgres=# \h command синтаксис команды SQL
postgres=# \q

### Параметры подключения

База данных: -d database или $PGDATABASE
по умолчанию совпадает с именем пользователя

Имя сервера: -h host или $PGHOST
по умолчанию локальное соединение

Порт: -p port или $PGPORT
по умолчанию можно задать при сборке, обычно 5432

Имя пользователя: -U username или $PGUSER
по умолчанию совпадает с именем пользователя


### Подключение
Из командной строки:
$ psql -d database -h host -p port -U username
или указать параметры в переменных окружения


Из psql:
postgres=# \conninfo
postgres=# \l
postgres=# \c[onnect] database username host port


Параметры \c должны идти в указанном порядке, но их можно
заменять на дефис. Например, чтобы сменить пользователя в той
же БД:
\c - username

При запуске выполняются скрипты:
psqlrc общий системный файл
(pg_config --sysconfdir)

~/.psqlrc пользовательский файл
или $PSQLRC

История команд сохраняется в файле:
~/.psql_history
или $PSQL_HISTORY, или HISTFILE



1. Вывести список доступных БД
2. Подключиться к БД template1 под пользователем postgres
3. Вывести все строки таблицы pg_class
4. Выйти из psql
5*. Настроить psql так, чтобы для каждой команды
печаталось время ее выполнения. Убедиться, что при
повторном запуске эта настройка сохраняется.

Решения задач с 1 по 4
$ psql
postgres=# \l
postgres=# \c template1 postgres
postgres=# select * from pg_class;
postgres=# \q
Решение задачи 5
$ echo '\timing on' >> ~/.psqlrc







