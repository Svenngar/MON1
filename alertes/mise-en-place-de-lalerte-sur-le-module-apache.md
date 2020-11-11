# Mise en place de l'alerte sur le module Apache

Pour recevoir l'alerte nous devons lier la commande de l'alerte twitter ainsi que celle de mail to admin.

Nous avons besoin ensuite de créer une commande spécialisée qui n'aura pas d'influence lorsque le service va s'éteindre mais qui va lancer une commande de bash quand le module se remettra dans son état normal:

```text
ssh debian@10.0.4.5 'sudo systemctl start apache2'
```

![](../.gitbook/assets/image%20%2819%29.png)

L'ajouter à l'action:

![](../.gitbook/assets/image%20%2822%29.png)

Puis ajouter l'action à l'alerte:

![](../.gitbook/assets/image%20%2820%29.png)

{% hint style="warning" %}
Les problèmes qu'engendrent une telle commande sont les suivants:

* Droit de connexion par SSH d'une machine à une autre sans prompt de mot de passe
* Droit d'exécution d'une commande avec sudo sans prompt de mot de passe
{% endhint %}

Nous devons ensuite désactiver le prompt du password pour la commande systemctl sur le client debian pour l'utilisateur debian:

```text
sudo visudo

debian ALL=(ALL:ALL) NOPASSWD: /usr/bin/systemctl
```

Finalement nous devons autoriser notre client à accéder à l'utilisateur debian via ssh sans entrer de password. Il faut générer une clé depuis le serveur Pandora:

```text
ssh-keygen -t rsa
```

Il faut se rendre sur le client debian en tant que debian et dans le directory ~ créer le directory `.ssh`

```text
ssh debian@10.0.4.5
entrer mdp debian
cd ~
mkdir .ssh
exit
```

Et finalement nous copions notre clé dans le fichier `authorized_keys`sur le client debian:

```text
cd ~
cat .ssh/id_rsa.pub | ssh debian@10.0.4.5 'cat >> .ssh/authorized_keys'
```

Le serveur Pandora peut maintenant exécuter le script en remote sans avoir à utiliser de mot de passe.

