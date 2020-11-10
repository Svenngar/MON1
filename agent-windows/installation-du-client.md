# Installation de l'agent Windows

Le client Windows est téléchargeable à cette adresse :

[https://sourceforge.net/projects/pandora/files/Pandora FMS 7.0NG/745/Windows/Pandora FMS Windows Agent v7.0NG.745\_x86\_64.exe/download](https://sourceforge.net/projects/pandora/files/Pandora%20FMS%207.0NG/745/Windows/Pandora%20FMS%20Windows%20Agent%20v7.0NG.745_x86_64.exe/download)

#### Installation de l'agent Windows sans surveillance

À partir de la « 'VERSION 5.1' » de l'agent, le programme d'installation prend en charge le mode sans assistance. Pour effectuer l'installation, vous devez simplement exécuter les tâches suivantes :

```text
"Pandora FMS Windows Agent v7.0NG.VERSION-BUILD_ARCH.exe" /S
```

Dans le cas où vous souhaitez installer l'agent sur une chemin différente de ce par défaut :

```text
"Pandora FMS Windows Agent v7.0NG.VERSION-BUILD_ARCH.exe" /S /D=C:\Agent_Pandora
```

Vous pouvez également transmettre certains paramètres à écrire dans le fichier de configuration de l'agent à créer. Grâce à ces options, le déploiement des agents Pandora FMS est beaucoup plus personnalisable. Les options par ligne de commande prises en charge sont les suivantes :

* « '--ip' » : Cela correspond au token « server\_ip. »
* « '--group' » : Cela correspond au token « group. »
* « '--alias' » : Cela correspond au token « agent\_alias. »

Par exemple, si vous souhaitez créer un agent appartenant au groupe « Serveurs », nommé « WINCORE1 » et pointant vers le serveur avec l'adresse IP « 192.168.66.10 », la commande est la suivante :

```text
"Pandora FMS Windows Agent v7.0NG.VERSION-BUILD_ARCH.exe" /S  --ip 192.168.66.10 --group Serveurs --alias WINCORE1
```



