PostgreSQL - это свободно распространяемая объектно-реляционная СУБД (ORDBMS)
Поддержка ANSI SQL (1992...2011), а также NoSQL (key-value, JSON, JSONB)

https://www.postgresql.org/

Лицензия: BSD, MIT-like

Сайт где обладатель малоизвестной архитектуры железа или ОС, может зарегестрироваться со своей системой, спец софт автоматически будет коплировать устновку бд, проводить регрессионые тесты и убеждаться что будет работать. Также на сайте списко провенных платформ.
https://buildfarm.postgresql.org/

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
