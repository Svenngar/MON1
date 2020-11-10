# Installation de l'agent Debian

Le client Pandora est téléchargeable à cette adresse :

[https://sourceforge.net/projects/pandora/files/Pandora FMS 7.0NG/745/Debian\_Ubuntu/pandorafms.agent\_unix\_7.0NG.745.deb/download](https://sourceforge.net/projects/pandora/files/Pandora%20FMS%207.0NG/745/Debian_Ubuntu/pandorafms.agent_unix_7.0NG.745.deb/download)

Pour installer l'agent ainsi que ses dépendances, exécutez tout simplement ces commandes :

```text
dpkg -i pandorafms_agent_unix-7.0NG-1.noarch.deb
apt install libyaml-tiny-perl
```

Si le référentiel Debian est activé, vous pouvez installer l'agent directement via cette exécution :

```text
apt-get install pandorafms_agent_unix
```

Une fois installé, il faut modifier le fichier de configuration /etc/pandora/pandora.conf comme suit de manière à ce que l'agent s'enregistre auprès du serveur puis remonte les informations de monitoring :

```bash
server_ip       192.168.66.10
group            Servers
agent_alias     DEBIAN9
```

