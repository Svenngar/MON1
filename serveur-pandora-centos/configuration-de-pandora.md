# Configuration de Pandora

### Configuration initiale après l’installation

L’ordre qui doit suivre après l’installation est :

1. Créer la base de données, grâce au wizard d’installation de la console web de Pandora FMS.
2. Modifier la configuration du serveur, comprenant les accréditations d’accès à la base de données générées par l’étape précédente.
3. Démarrer le serveur.
4. Démarrer l’agent local \(si besoin\)
5. Accéder à la console de Pandora FMS pour la première fois pour commencer à utiliser Pandora FMS.

#### Peaufiner la configuration sur CentOS7

CentOS 7 est une bonne distribution de Linux mais a ses petites particularités que nous traiterons brièvement et faciliteront l’installation de Pandora FMS :

CentOS a un pare-feu très agressif et nous avons besoin de le désactiver \(plus tard vous pourrez sécuriser le serveur si besoin\).

```text
systemctl disable firewalld
systemctl stop firewalld
CentOS 7 a aussi SELinux d’activé par défaut. Pour le désactiver :  
setenforce 0
sed -i 's/enforcing/disabled/g' /etc/selinux/config /etc/selinux/config
```

Nous programmons pour le redémarrage aussi bien le serveur WEB que le serveur de base données :

```text
 systemctl start httpd.service
 systemctl enable httpd.service
 systemctl enable mariadb.service
```

Nous enlevons le private tmp du systemd sur Apache

```text
sed -i 's/PrivateTmp=true/PrivateTmp=false/g' /etc/systemd/system/multi-user.target.wants/httpd.service
```

### Configuration initiale de la Console

Nous supposons que vous allez exécuter toutes les composantes \(Base de données, Console, Serveur et Agent\) sur la même machine. Si vous ne l’avez toujours pas fait, démarrez le serveur mysql et établissez un mot de passe d’administrateur \(root\).

```text
service mariadb start
```

Maintenant remontez le serveur Apache à votre serveur :

```text
service httpd start
```

À présent, il devrait être possible d'accéder par le navigateur à l’adresse IP de notre serveur de Pandora FMS et terminer le processus de création de la base de données.

Mettez sur votre navigateur

```text
http://192.168.66.10/pandora_console/install.php
```

À partir de maintenant, vous n’aurez plus qu’à suivre les étapes qui vous seront indiquées pour créer la base de données de Pandora FMS.

Lors de la connexion à la base de donnée pandora, le serveur change le mot de passe de l'utilisateur pandora. Il faut changer ce mot de passe dans le fichier `etc\pandora\pandora_server.conf`

```text
# dbpass: Database password
dbpass [nouveau mot de passe]
```

 Cette étape ne peut pas être scriptée. Une fois cela changé, il faut redémarrer les service pandora :

```text
 service pandora_server restart
 service tentacle_serverd restart
```

