# Utilisation des logs

Les logs concernant le serveur Pandora se trouvent dans le répertoire /var/log/Pandora. On y trouve deux fichiers:

* pandora\_server.error 
* pandora\_server.log

### Pandora\_server.error

Ce fichier est utile pour toute erreur critique qui impacterait le fonctionne du serveur, par exemple si l'on change le mot de passe du compte qui a accès à la DB uniquement dans MariaDB sans le changer dans le fichier de conf de pandora alors le serveur s'arrête et affiche une erreur au démarrage. Cette erreur est directement documentée dans le fichier pandora\_server.error car elle empêche le serveur de redémarrer.

### Pandora\_server.log

Nous y retrouvons les warnings relatifs au serveur Pandora mais qui ne provoquent pas d'interruption de service. Il est toutefois bon de régler au plus vite ces warnings de manière à ce qu'ils ne se transforment pas en une erreur qui pourrait potentiellement arrêter notre infrastructure de monitoring. Mais il y a aussi la trace écrite des tâches effectuées, par exemple si l'on démarre un scan SNMP la ligne suivante apparaît:

```text
2020-05-27 10:49:42 Base: localhost.localdomain [V3] [Recon task 1] [1/6] Scanning the network...
```

### Verbosité

Niveau de détail pour les journaux du serveur. Les valeurs possibles vont de 0 \(désactivé\) à 10 \(niveau de détail maximum\). Avec la valeur 10, le journal affiche toutes les exécutions effectuées par le serveur, y compris les modules, les plug-ins et les alertes.

