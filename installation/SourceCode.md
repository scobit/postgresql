## Install from source code (postgresql-14.6 example)

#### Source code site
http://www.postgresql.org/ftp/source/


#### goto home directory
```
cd ~
```
#### download source code
```
wget https://ftp.postgresql.org/pub/source/v14.6/postgresql-14.6.tar.bz2
```
#### if gz archive
`gunzip postgresql-14.6.tar.gz`

`tar xf postgresql-14.6.tar`

or

`tar xzf postgresql-14.6.tar.gz`

#### if bz2 archive
`bunzip2 postgresql-14.6.tar.bz2`

`tar xf postgresql-14.6.tar`

#### goto source folder
`cd postgresql-14.6/`

#### configure
`./configure`

#### make
`make`

#### clean make
`make distclean`

#### installation 
`sudo make install`

#### add postgres user
`sudo adduser postgres`

#### create data folder
`sudo mkdir -p /usr/local/pgsql/data`

#### change ownership
`sudo chown postgres /usr/local/pgsql/data`

### Under postgres user
#### create system variables
`echo 'export PATH=/usr/local/pgsql/bin:$PATH' >> ~/.profile`

`echo 'export PGDATA=/usr/local/pgsql/data' >> ~/.profile`
#### apply changes
`. ~/.profile`
#### init database
`initdb -k`
#### start database
`pg_ctl start -l logfile`
#### chech database
`psql -c 'select now();'`
##### stop database
`pg_ctl stop -m fast`

### Install extension
### Under general user
#### goto extension folder
`cd ~/postgresql-14.6/contrib/oid2name`
#### make
`make`
#### install
`sudo make install`
