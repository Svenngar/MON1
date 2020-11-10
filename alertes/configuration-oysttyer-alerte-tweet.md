# Configuration oysttyer \(alerte tweet\)

Commencer par télécharger le programme et le dezip:

```text
wget https://github.com/oysttyer/oysttyer/archive/master.zip
unzip master.zip
```

Il faut ensuite de placer dans le dossier et lancer le script perl pour la configuration initiale:

```text
cd oysttyer-master
./oysttyer.pl
```

Après avoir visité le site web donné en URL et avoir entré le PIN dans oysttyer nous pouvons tester les tweet:

```text
echo "publishing test tweet" | ./oysttyer.pl
```

![](../.gitbook/assets/image%20%2811%29.png)

Nous pouvons maintenant intégrer notre module twitter à Pandora.

