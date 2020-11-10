# Installation de la Console et du Serveur de Pandora FMS

### Pré-requis minimum de logiciel

| Logiciel | Pré-requis |
| :--- | :---: |
| Système d’exploitation | Windows Server \(2003 ou plus récent\)RedHat Enterprise \(RHEL\) **7.XCentOS 7.X \(Recommandé\)**SLES 11 SP1 ou plus récentOpenSUSE 11.X ou plus récentDebian 5, 6, 7 ou plus récentUbuntu 11 ou plus récent |
| FreeBSD 9.X y 10.XSolaris 10/OpenSolaris | Pandora FMS n’apporte pas de soutien officiel sur ces plates-formes |
| Autorisations | **Server**- Linux : vous devez exécuter le service de Pandora FMS Server comme autorisations de root. L’exécution comme utilisateur non root est possible, se faisant d’une façon différente. Plus d’information sur ce lien.-Windows : vous devez exécuter le service de Pandora FMS Server comme autorisations d’administrateur.**Console**Pour pouvoir utiliser la console depuis n’importe quel navigateur web, Apache doit avoir des autorisations de lecture et d’exécution sur les fichiers de la console.De plus, le fichier config.php doit avoir les autorisations 600 \(lecture et écriture pour administrateur/ root\).Il faut que lui-même ait les autorisations d’écritures dans le répertoire du serveur : /var/spool/pandora/**Agent**-Linux : vous devez exécuter l’Agent Software de Pandora FMS Server comme autorisations de root pour pouvoir compter sur toutes les fonctionnalités de l’agent, bien qu’il soit possible de l’exécuter avec d’autres autorisations.-Windows : vous devez exécuter l’Agent Software de Pandora FMS Server comme autorisations d’administrateur. |
| Console | PHP 7.2 -&gt; Pour des versions de Pandora FMS 729 ou plus récente.PHP 5 -&gt; Pour des versions de Pandora FMS 728 ou moins récente. |
| Navigateurs | Microsoft EdgeOperaChromeFirefox |

### Pré-requis de base de données

| Base de données | Détails |
| :--- | :---: |
| MySQL Standard | Version 5.5 Pour l’installation standard, un utilisateur avec des privilèges de création dans la base de données de Pandora FMS est nécessaire. Dans le cas où vous ne possédez pas d’utilisateur, vous pourrez réaliser une installation manuelle. |
| Percona XTraDB | L’installation de Percona XTraDB est recommandé pour les larges environnements de Pandora FMS où vont se créer plus de 4000 agents.Version 5.5Pour l’installation standard, un utilisateur avec des privilèges de création dans la base de données de Pandora FMS est nécessaire. Dans le cas où vous ne possédez pas d’utilisateur, vous pourrez réaliser une installation manuelle. |

| [![Template warning.png](https://pandorafms.com/docs/images/d/d7/Template_warning.png)](https://pandorafms.com/docs/index.php?title=File:Template_warning.png) | Il faudrait disposer de tout cela AVANT de commencer à installer Pandora FMS. Si vous ignorez comment installer un serveur MySQL, recherchez la documentation sur le processus complet. Nous ne pouvons pas fournir toute cette documentation puisqu’elle varie en fonction du système, la distribution et/ou la version. |  |
| :--- | :--- | :--- |


### Installation de l'OS

#### Matériel

* Mémoire :    4GB
* Processeur : 1
* Disque dur : 40 GB
* Réseau : NAT

#### Logiciel

* Centos 7 Installé
* Hostname : pandora.rct.org
* Login : root/Pa$$w0rd
* Ip fixe : 192.168.66.10/24
* Passerelle : 192.168.66.2
* DNS : 192.168.43.1
* MariaDB login : root/Pa$$w0rd

### Installation de la console et du serveur

Dans un premier temps, il faudra activer certains répertoires officiels de Centos pour réaliser l’installation de dépendances. Les répertoires à activer sont EXTRAS, UPDATES et l’installation additionnelle du répertoire EPEL.

Edite /etc/yum.repos.d/CentOS-Base.repo et laissez les répertoires EXTRAS et UPDATES actifs. En général, ils se présenteront de la façon suivante :

```bash
[updates]
name=CentOS-$releasever - Updates
mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates
gpgcheck=0

[extras]
name=CentOS-$releasever - Extras
mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras
gpgcheck=0
```

Ajouter le dépôt EPEL :

```bash
[EPEL]
Name = EPEL
baseurl = http://dl.fedoraproject.org/pub/epel/$releasever/$basearch/
enabled = 1
gpgcheck = 0
```

Et actualisez l’information de vos répertoires :

```bash
yum makecache
```

#### Installation grâce au répertoire officiel de Pandora FMS

Pour effectuer cette installation, nous aurons besoin de YUM et d'un accès Internet. Tout d'abord, nous créons le dépôt officiel de Pandora FMS pour CentOS 7. Ce référentiel peut également être utilisé dans RHEL7.

```bash
nano /etc/yum.repos.d/pandorafms.repo
```

Ajoutez ce contenu

```bash
[artica_pandorafms]
name=CentOS7 - PandoraFMS official repo
baseurl=http://firefly.artica.es/centos7
gpgcheck=0
enabled=1
```

Rafraîchissez vos répertoires :

```text
yum makecache
```

Il faut encore installer PHP

Nous exécutons cette commande afin de rendre disponible EPEL et Remi `repositories`:

```bash
yum install -y epel-release yum-utils
yum install -y http://rpms.remirepo.net/enterprise/remi-release-7.rpm
```

#### Installation de PHP 7.3 sur CentOS 7

On commence par activer le PHP 7.3 Remi repository:

```text
yum-config-manager --enable remi-php73
```

Puis on installe PHP 7.3

```text
yum install -y php php-common php-opcache php-mcrypt php-cli php-gd php-curl php-mysqlnd
```

Pour terminer on peut contrôler la version :

```text
php -v
```

### 



