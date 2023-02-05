#### Установка специфической версии PostgreSQL, используя репозиторий Development Group maintained repo.
#### For Ubuntu 18.04 Добавляем адрес репозитория (focal для ubuntu 20)
```
vim /etc/apt/sources.list.d/pgdg.list
deb http://apt.postgresql.org/pub/repos/apt/ bionic-pgdg main
```

#### Импортируем ключ подписи 
```
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
```

#### Обновляем список пакетов
```
apt-get update
```

#### Устанавливаем необходимые версии пакетов, для примера postgresql-10
```
apt install postgresql-9.6
apt install postgresql-9.6-pgpool2
```
#### Добавляем в переменные окружения PGDATA
```
vim /etc/environment
PGDATA="/var/lib/postgresql/9.6/main"
```

#### Копируем все исполняемые файлы postgres в один из каталогов переменной PATH 
```
cp /usr/lib/postgresql/9.6/bin/* /usr/sbin/
```

#### Команда запуска БД (запускаем от имени пользователя postgres)
```
/usr/lib/postgresql/9.6/bin/pg_ctl -D /var/lib/postgresql/9.6/main -l /tmp/logfile start
```

#### Меняем пароль пользователя postgres в БД
```
sudo -u postgres psql
ALTER USER postgres WITH PASSWORD 'xE%23465';
\q
```

#### Меняем пароль пользователя postgres в операционной системе (Aa123456)
```
passwd postgres
```


#### Создаем пользователя для выполнения репликации
```
CREATE ROLE replication WITH REPLICATION PASSWORD 'Qweasd123' LOGIN;
```

#### Создаем файл аутентификации
```
vim /var/lib/postgresql/.pgpass

*:*:*:replication:reppassword
```

#### Файл аутентификации требует определённых прав
```
chown postgres:postgres /var/lib/postgresql/.pgpass

chmod 0600 /var/lib/postgresql/.pgpass
```

#### Редактируем файл postgresql.conf
```
cp /etc/postgresql/9.6/main/postgresql.conf /var/lib/postgresql/9.6/main/postgresql.conf

chown postgres:postgres /var/lib/postgresql/9.6/main/postgresql.conf

vim /var/lib/postgresql/9.6/main/postgresql.conf

listen_addresses = '*'
port = 5433
```

#### Редактируем pg_hba.conf
```
cp /etc/postgresql/9.6/main/pg_hba.conf /var/lib/postgresql/9.6/main/pg_hba.conf

chown postgres:postgres /var/lib/postgresql/9.6/main/pg_hba.conf

vim /var/lib/postgresql/9.6/main/pg_hba.conf

host  replication     replication     192.168.0.172/32          md5
host  replication     replication     192.168.0.173/32          md5
host  all             postgres        192.168.0.0/16            md5
```
### Configuring Primary Server

#### Настраиваем параметры WAL Archiving
```
vim /var/lib/postgresql/9.6/main/postgresql.conf

wal_level = hot_standby
max_wal_senders = 3
wal_keep_segments = 32
archive_mode    = on
archive_command = 'cp %p /path_to/archive/%f'
```



