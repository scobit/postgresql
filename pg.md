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
PGDATA="/data/local/db/data"
```

#### Копируем все исполняемые файлы postgres в один из каталогов переменной PATH 
```
cp /usr/lib/postgresql/9.6/bin/* /usr/sbin/
```

#### Выключаем автоматически запущенный кластер и удаляем его
```
pg_ctl stop

rm -rf /var/lib/postgresql/9.6/main
```


#### Создаём кластер БД (запускаем от имени пользователя postgres)
```
mkdir -p /data/local/db/data

chown -R postgres:postgres /data

pg_ctl -D /data/local/db/data -l /tmp/logfile start
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
cp /data/local/db/data/postgresql.conf /data/local/db/data/postgresql.conf.bak

vim /data/local/db/data/postgresql.conf

listen_addresses = '*'
port = 5433
```

#### Редактируем pg_hba.conf
```
cp /data/local/db/data/pg_hba.conf /data/local/db/data/pg_hba.conf.bak

vim /data/local/db/data/pg_hba.conf

host  replication     replication     192.168.0.172/32          md5
host  replication     replication     192.168.0.173/32          md5
host  all             postgres        192.168.0.0/16            md5
```
### Configuring Primary Server

#### Настраиваем параметры WAL Archiving
```
vim /data/local/db/data/postgresql.conf

wal_level = hot_standby
max_wal_senders = 3
wal_keep_segments = 32
archive_mode    = on
archive_command = 'cp %p /path_to/archive/%f'
```

#### Создаём базу с главного сервера (запускаем на ведомом от пользователя postgres)
```
pg_basebackup -v -D /data/local/db/data -R -P -h 192.168.0.172 -p 5433 -U replication

```

#### Редактируем postgresql.conf на standby ноде
```
vim /data/local/db/data/postgresql.conf

hot_standby = on
hot_standby_feedback = on
```

#### Редактируем recovery.conf для Wal архивации на standby ноде
```
vim $PGDATA/recovery.conf

standby_mode = 'on'
primary_conninfo = 'host=10.1.10.150 port=5433 user=replication password=reppassword'
trigger_file = '$PGDATA/im_master'
restore_command = 'cp /path_to/archive/%f "%p"'

```
#### Запускаем standby
```
pg_ctl -D /data/local/db/data -l /tmp/logfile start
```

#### Проверка репликации
```
#### on primary node

sudo -u postgres psql

CREATE DATABASE replicationtest;

\l

#### on standby node

sudo -u postgres psql

\l

DROP DATABASE replicationtest;

#### on primary node

DROP DATABASE replicationtest;

```


