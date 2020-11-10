# Mise en place de l'alerte twitter

Nous devons créer une commande qui pourra être utilisée par une alerte:

![](../.gitbook/assets/image%20%282%29.png)

Nous créons ensuite l'action qui permettra d'utiliser la commande sur le groupe Servers:

![](../.gitbook/assets/image%20%287%29.png)

Et finalement nous créons l'alerte sur l'agent en question en liant l'action que nous venons de créer:

![](../.gitbook/assets/image%20%286%29.png)

Nous avons maintenant une alerte sur le groupe Servers qui déclenchera un tweet lorsque la charge d'un des CPU monitoré sera en dehors de l'état "normal" ce qui nous indiquera qu'une de nos machines est surchargée.

{% hint style="warning" %}
Après avoir suivi rigoureusement la documentation officielle, l'alerte le lance pas de tweet alors que la ligne configurée et envoyée par CMD produit bien un tweet. Aucun log ne rapporte de problème concernant notre ligne\([https://pandorafms.com/blog/twitter-alerts/](https://pandorafms.com/blog/twitter-alerts/)\)
{% endhint %}

