PostgreSQL - это свободно распространяемая объектно-реляционная СУБД (ORDBMS)
Поддержка ANSI SQL (1992...2011), а также NoSQL (key-value, JSON, JSONB)

https://www.postgresql.org/

Лицензия: BSD, MIT-like

Сайт где обладатель малоизвестной архитектуры железа или ОС, может зарегестрироваться со своей системой, спец софт автоматически будет коплировать устновку бд, проводить регрессионые тесты и убеждаться что будет работать. Также на сайте списко провенных платформ.
https://buildfarm.postgresql.org/



#### PostgreSQL wiki
https://wiki.postgresql.org/

#### PostgreSQL guide
https://www.postgresguide.com

#### PostgreSQL subscriptions
https://lists.postgresql.org/

#### psql
https://www.postgresql.org/docs/11/app-psql.html

#### pgctl
https://www.postgresql.org/docs/11/app-pg-ctl.html

#### Tutorial administration
https://www.postgresqltutorial.com/postgresql-administration/

#### Tutorial psql
https://www.postgresqltutorial.com/

#### Tutorial getting started
https://www.postgresqltutorial.com/postgresql-getting-started

if the database server machine is a remote machine, you will need to set the PGHOST environment variable to the name of the database server machine. The environment variable PGPORT might also have to be set. 

The PostgreSQL version. You can run the command SELECT version(); to find out the version of the server you are connected to. Most executable programs also support a --version option; at least postgres --version and psql --version should work.

Typically, a separate database is used for each project or for each user.

#### home dir for postgres user
/var/lib/pgsql


su - postgres
mkdir /home/postgres/.ssh
ssh-keygen -b 2048 -t rsa -N '' -f /home/postgres/.ssh/id_rsa



pgpool-II version 3.6.6 (subaruboshi)
pgpool-II version 4.1.4 (karasukiboshi)


https://www.pgpool.net/mediawiki/index.php/Old_releases




EnvironmentFile=-/etc/sysconfig/pgpool-II-96
ExecStart=/usr/pgpool-9.6/bin/pgpool -f /etc/pgpool-II-96/pgpool.conf $OPTS 
ExecStop=/usr/pgpool-9.6/bin/pgpool -f /etc/pgpool-II-96/pgpool.conf -m fast stop
ExecReload=/bin/kill -HUP $MAINPID



yum install libpqxx-devel
