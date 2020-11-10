# Optimisation des services

De manière à optimiser les opérations faites par notre serveur de monitoring nous devons changer certains paramètres dans des services existants de centOS. Pandora nous affiche une liste de "Warning" nous permettant de savoir quels services doivent être modifiés.

### Optimisation de MariaDB

Lors du diagnostique de Pandora, il nous indique qu'il y des paramètres à changer pour maria-db. Nous modifions donc le fichier `/etc/my.cnf`comme suit :

```text
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
```

### Optimisation de PHP

Lorsque l'on veut effectuer les mises à jour en ligne, Pandora nous signale que : 

{% hint style="danger" %}
Your PHP has set memory limit in 128M. To use Update Manager Online, please set it to 500M. Your PHP has set maximum allowed size for uploaded files limit in 2M. To use Update Manager Online, please set it to 800M 
{% endhint %}

Nous allons donc modifier notre fichier `/etc/php.ini`comme suit :

```text
sed -i 's/memory_limit = 128M/memory_limit = 500M/g' /etc/php.ini
sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 800M/g' /etc/php.ini
service httpd restart
```

