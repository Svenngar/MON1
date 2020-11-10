# Installation et configuration de la VM

### Configuration de la VM

| **Composant** | **Caractéristique** |
| :--- | :--- |
| RAM | 2Go |
| Processeur | 1 |
| HDD | 20Go |
| Réseau | NAT |

### Installation de l'OS Debian Stretch 9.12.0

Installation standard:

| **Champ** | **Valeur** |
| :--- | :--- |
| Langue | fr-CH-RO |
| Miroir | ETHZ |
| Partitionnement | Automatique avec home séparé |
| Services de base | Aucun |
| Grub | /dev/sda |
| Compte root | root root |
| Compte user | cpnv cpnv |

Il faut tout d'abord ajouter le package sudo et ssh puis ajouter "cpnv" aux sudoers en se connectant en tant que root:

```text
apt update
apt install sudo
apt install ssh
adduser cpnv sudo
```

Nous pouvons maintenant utiliser `sudo` depuis l'utilisateur "cpnv".

Il faut ensuite lui attribuer une adresse IP fixe ainsi qu'un DNS et une gateway:

```text
sudo nano /etc/network/interfaces

auto ens33
iface ens33 inet static
        address 192.168.3.3
        netmask 255.255.255.0
        gateway 192.168.3.2
        dns-nameservers 192.168.3.2
```

Le serveur est maintenant prêt à être administré à distance.

