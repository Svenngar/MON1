# Ajout du plugin apache

Il faut tout d'abord ajouter le service apache:

```text
sudo apt install apache2
```

Afin de monitorer apache2 nous avons besoin du plugin de Pandora que nous allons télécharger sur le shop des plugins.

Voici le contenu du fichier qui nous intéresse:

```text
module_begin
module_name apache2_Status
module_type generic_data_string
module_exec (if test $(systemctl list-unit-files | grep apache2 | wc -l) -ne 0 ; then systemctl is-active --quiet apache2 && echo active || echo inactive; else echo not installed; fi)
module_str_critical inactive
module_group Application
module_end
```

Nous allons ensuite coller ce plugin tout en bas du fichier `pandora_agent.conf`  où il y a un espace prévu pour la création de petits modules du genre.

Maintenant notre agent remontera l'état du service apache2 du client Debian sous le nom de "apache2\_Status".

