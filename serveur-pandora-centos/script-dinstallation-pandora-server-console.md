# Script complet Pandora\_server & Pandora\_console

```text
echo off
# Ajout du dépot EPEL dans /etc/yum.repos.d/CentOS-Base.repo

echo "Ajout du dépot EPEL"
echo "*******************"
echo
echo "[EPEL]" >> /etc/yum.repos.d/CentOS-Base.repo
echo "Name = EPEL" >> /etc/yum.repos.d/CentOS-Base.repo
echo "baseurl = http://dl.fedoraproject.org/pub/epel/\$releasever/\$basearch/"  >> /etc/yum.repos.d/CentOS-Base.repo
echo "enabled = 1" >> /etc/yum.repos.d/CentOS-Base.repo
echo "gpgcheck = 0" >> /etc/yum.repos.d/CentOS-Base.repo
yum makecache


echo
echo "Ajout du dépot officiel de Pandora FMS"
echo "**************************************"
echo
echo "[artica_pandorafms]" >> /etc/yum.repos.d/pandorafms.repo
echo "name=CentOS7 - PandoraFMS official repo" >> /etc/yum.repos.d/pandorafms.repo
echo "baseurl=http://firefly.artica.es/centos7" >> /etc/yum.repos.d/pandorafms.repo
echo "gpgcheck=0" >> /etc/yum.repos.d/pandorafms.repo
echo "enabled=1" >> /etc/yum.repos.d/pandorafms.repo
yum makecache

echo
echo "Mise à disposition des dépots EPEL et REMI"
echo "******************************************"
yum install -y epel-release yum-utils
yum install -y http://rpms.remirepo.net/enterprise/remi-release-7.rpm

echo
echo "Installation de PHP version 7.3"
echo "*******************************"
echo
yum-config-manager --enable remi-php73
yum install -y php php-common php-opcache php-mcrypt php-cli php-gd php-curl php-mysqlnd
php -v

echo
echo "Installation de Pandora FMS front et back end et de MariaDB"
echo "*************************************************************"
echo
yum install -y pandorafms_console pandorafms_server mariadb-server

echo
echo "Installation des dependances"
echo "****************************"
echo
yum install -y php php-gd graphviz php-mysql php-pear-DB php-zip php-mbstring php-ldap \
php-snmp php-ldap php-common make perl-CPAN perl-HTML-Tree perl-DBI perl-DBD-mysql \
perl-libwww-perl perl-XML-Simple perl-XML-Twig perl-XML-SAX perl-NetAddr-IP \
net-snmp perl-SNMP net-tools perl-IO-Socket-INET6 perl-Socket6 nmap sudo xprobe2 \
perl-Encode-Locale

echo
echo "Configuration intiale"
echo "*********************"
echo
echo "Disable Firewall"
echo
systemctl disable firewalld
systemctl stop firewalld

echo "Disable SElinux"
echo
setenforce 0
sed -i 's/enforcing/disabled/g' /etc/selinux/config /etc/selinux/config

echo "Demarrage des services WEB et DB"
echo
systemctl start httpd.service
systemctl enable httpd.service
systemctl enable mariadb.service
sed -i 's/PrivateTmp=true/PrivateTmp=false/g' /etc/systemd/system/multi-user.target.wants/httpd.service

echo
echo "Configuration initiale du Front-END"
echo "***********************************"
service mariadb start
service httpd start

echo 
echo "Configuration de la base de donnée pandora"
echo "******************************************"
echo
echo "dbUser : pandora"
echo "dnName: pandora"
echo "dbpsw : pandora"
echo
mysql -uroot -e "CREATE DATABASE IF NOT EXISTS pandora;"
mysql -uroot -e "CREATE USER 'pandora'@'localhost' IDENTIFIED BY 'pandora';"
mysql -uroot -e "GRANT ALL ON *.* TO 'pandora'@'localhost' IDENTIFIED BY 'pandora';"
mysql -uroot -e "FLUSH PRIVILEGES;"

echo "Optimisation de MariaDB"
echo "*************************************************************"
sed -i "11i\# Pandora settings\n" /etc/my.cnf
sed -i "12i\max_allowed_packet = 64M\n" /etc/my.cnf
sed -i "13i\innodb_buffer_pool_size = 800M\n" /etc/my.cnf
sed -i "14i\innodb_lock_wait_timeout = 90\n" /etc/my.cnf
sed -i "15i\innodb_file_per_table = ON\n" /etc/my.cnf
sed -i "16i\innodb_flush_log_at_trx_commit = 2\n" /etc/my.cnf
sed -i "17i\innodb_flush_method = O_DIRECT\n" /etc/my.cnf
sed -i "19i\innodb_io_capacity = 100\n" /etc/my.cnf
sed -i "20i\thread_cache_size = 8\n" /etc/my.cnf
sed -i "21i\thread_stack = 256K\n" /etc/my.cnf
sed -i "22i\max_connections = 100\n" /etc/my.cnf
sed -i "23i\key_buffer_size=4M\n" /etc/my.cnf
sed -i "24i\read_buffer_size=128K\n" /etc/my.cnf
sed -i "25i\read_rnd_buffer_size=128K\n" /etc/my.cnf
sed -i "26i\sort_buffer_size=128K\n" /etc/my.cnf
sed -i "27i\join_buffer_size=4M\n" /etc/my.cnf
sed -i "28i\query_cache_type = 1\n" /etc/my.cnf
sed -i "29i\query_cache_size = 64M\n" /etc/my.cnf
sed -i "30i\query_cache_min_res_unit = 2k\n" /etc/my.cnf
sed -i "31i\query_cache_limit = 8M\n" /etc/my.cnf

echo "Optimisation de PHP"
echo "*************************************************************"
sed -i 's/memory_limit = 128M/memory_limit = 500M/g' /etc/php.ini
sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 800M/g' /etc/php.ini
service httpd restart
```



