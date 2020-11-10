# Stress test

Pour effectuer le stress test il faut installer une librairie, ici nous utiliserons "Stress":

```text
sudo apt install stress
```

Une fois que c'est fait nous allons lancer deux commandes en une, une pour stresser le CPU et une pour stresser la mémoire:

```text
su -
stress -c 16 -i 1 -m 1 --vm-bytes 550M -t 1m
```

Le stress test est directement répercuté sur notre dashboard:

![](../../.gitbook/assets/image%20%284%29.png)

Nous pouvons voir 4 pics concernant la mémoire, ce sont 4 tests effectués consécutivement en augmentant à chaque fois la charge. Concernant le CPU nous pouvons voir aussi 4 pics qui correspondes à 2 tests mineurs et 2 majeurs dont 3 lorsque la mémoire n'était pas testée et nous pouvons voir que sur le 4ème, le pic est à peine plus élevé pour une valeur semblable car la mémoire était testée en même temps.

