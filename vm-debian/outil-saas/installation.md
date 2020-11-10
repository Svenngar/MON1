# Collecteur Sumo Logic

L'installation est extrêmement simple et rapide, il faut tout d'abord se rendre sur le site web de sumo logic et aller dans le menu suivant:  `Manage Data>Collection>Setup Wizard`

Nous cherchons à monitorer l'état du serveur, il faut donc choisir "Set Up Streaming Data" puis sélectionner la catégorie "Host Metrics" puis "New Collector&gt;Linux"

Une fois que c'est fait nous pouvons voir apparaître un bloc de code, ce bloc de code installe et configure pour vous le collecteur de données de Sumo Logic:

![](../../.gitbook/assets/image%20%2815%29.png)

Il suffit ensuite copier coller cette ligne de code sur un client ssh relié à votre serveur et l'installation débute. Un script se lance et effectue une suite d'actions qui permets d'installer le collecteur, de le configurer pour la tâche souhaitée et de l'activer.

![](../../.gitbook/assets/image%20%289%29.png)

Une fois cette opération effectuée, retournez sur le site web de Sumo Logic, le wizard vous demande de cliquer sur le bouton "Continue":

![](../../.gitbook/assets/image%20%285%29.png)

Le collecteur se met en route et envoie les premières données au site web, une fois que le premier envoi est fait vous pouvez accéder au dashboard contenant l'ensemble des données collectées:

![](../../.gitbook/assets/image%20%2817%29.png)

