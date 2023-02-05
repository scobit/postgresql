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
/usr/lib/postgresql/9.6/bin/pg_ctl -D /var/lib/postgresql/9.6/main -l logfile start
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














