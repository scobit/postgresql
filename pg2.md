apt-get update
apt-get install libpq-dev make gcc

wget https://www.pgpool.net/mediawiki/download.php?f=pgpool-II-3.6.6.tar.gz

tar xf 'download.php?f=pgpool-II-3.6.6.tar.gz'

cd pgpool-II-3.6.6/
  
mkdir /etc/pgpool-3.6.6

./configure --prefix=/etc/pgpool-3.6.6


make

make install

ln -s /etc/pgpool-3.6.6/bin/* /usr/sbin/
or
cp /etc/pgpool-3.6.6/bin/* /usr/sbin/
or
mv /etc/pgpool-3.6.6/bin/* /usr/sbin/
