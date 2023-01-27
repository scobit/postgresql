#### Запуск
```
psql
```

#### Справка
```
psql --help
```
```
man psql
```


#### Создать базу данных
createdb MyDbName


### Команды psql в БД

#### Список комманд psql
```
\?
```

#### Список комманд SQL
```
\h[elp] 
```

#### синтаксис команды SQL
```
\h command
```

#### Выход из psql
```
\q
```

#### Параметры подключения

База данных: -d database или $PGDATABASE по умолчанию совпадает с именем пользователя

Имя сервера: -h host или $PGHOST по умолчанию локальное соединение

Порт: -p port или $PGPORT по умолчанию можно задать при сборке, обычно 5432

Имя пользователя: -U username или $PGUSER по умолчанию совпадает с именем пользователя ОС

#### Подключение (или указать параметры в переменных окружения)
```
psql -d database -h host -p port -U username
```

#### Информация о подключении 
```
\conninfo
```

#### Отобразить список баз
```
\l
```

#### Информация о подключении 
```
\c[onnect]
```

#### Подключение к другой базе
```
\c[onnect] database username host port
```



#### Параметры \c должны идти в указанном порядке, но их можно заменять на дефис. Например, чтобы cменить пользователя в текущей БД
```
\c - username
```

#### При запуске выполняются скрипты (общий системный файл), находится в каталоге $PGDATA
```
psqlrc
```

#### пользовательский файл
```
~/.psqlrc
```

#### Пользовательский файл через переменную окружения
```
$PSQLRC
```

#### История команд
```
~/.psql_history
```

#### История команд через переменную
```
$PSQL_HISTORY
```
или
```
HISTFILE
```

#### Отображение конфигурационного каталога
```
pg_config --sysconfdir
```

#### Создать БД
```
psql -c "CREATE DATABASE TypeDbName OWNER TypeOwnerName;"
```


#### для каждой команды печатается время ее выполнения, повторном запуске эта настройка сохраняется.
```
echo '\timing on' >> ~/.psqlrc
```

#### Пример выполнения SELECT
SELECT schemaname, tablename, tableowner FROM pg_tables LIMIT 10;


#### Команда SQL может занимать и несколько строк,точка с запятой завершает ее.
```
SELECT schemaname, tablename, tableowner 
FROM pg_tables LIMIT 10;
```


#### Если вывод команды SQL не помещется на экран, для его отображения можно использовать специальную программу $PAGER.
#### Использование можно включать или выключать с помощью 
```
\pset pager on|off
```

#### Для управления выводом используется команда \pset в разных вариациях.
#### Например, можно включить отображение полей "в столбик":
```
\pset expanded on|off
```
или просто 
```
\x
```
```
\pset expanded on  
select schemaname, tablename, tableowner from pg_tables limit 2;     
\pset expanded off  
```

#### Если вывод предстоит разбирать программно, то можно:
#### убрать выравнивание полей
```
\pset format unaligned
```
#### убрать вывод заголовка таблицы
```
\pset tuples_only on
```
#### заменить разделитель
```
\pset fieldsep ' '
```

#### Проверка
```
select schemaname, tablename, tableowner from pg_tables limit 10;
```

#### Возвращаем исходные значения
``` 
\pset format aligned
```
```
\pset tuples_only off
```


#### Можно включить формат вывода HTML:
```
\pset format html
``` 
#### Проверка
```
select schemaname, tablename, tableowner from pg_tables limit 1;
```
#### Возвращаем исходное значение
```
\pset format aligned
```

#### Выполнить shell комманду:
```
\! ls | head -n 10
```
```
\! pwd
```

#### Для изменения текущего (для psql) каталога есть специальная команда:
```
\! pwd
       
\cd ..

\! pwd
  
\cd /tpm
```

#### Установить переменную окружения:
```
\! echo $TEST
        
\setenv TEST Hello

\! echo $TEST
```


#### Можно записать вывод команды в файл с помощью \o[ut]:
```
\o dba1_log

\select schemaname, tablename, tableowner from pg_tables limit 5;
```

#### На экран ничего не попало. Посмотрим в файле:
```
\! cat dba1_log
```        

#### Вернем вывод на экран:
```
\o
```

#### Запишем в файл команды SQL.
```
\a
```
```
\t
```
```
\pset fieldsep ' '
```
```
\o dba1_log
```
```
select 'select count(*) from', tablename, ';' from pg_tables limit 3;
```
```
\o
```
```
\t
```
```
\a
```

#### Вот что получилось в файле:
```
\! cat dba1_log
```

#### И выполним теперь эти команды с помощью \i[nclude]:
```
\i dba1_log
```

#### Другие способы выполнить команды из файла:
```
psql < filename
psql -f filename
psql -c command (работает только для одной команды)
```

#### Файл также можно отредактировать, не выходя из psql, при этом используется редактор $PSQL_EDITOR (или $EDITOR, или $VISUAL)
```
\e[dit] filename
```

