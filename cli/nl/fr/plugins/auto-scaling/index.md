---

 

copyright:

  years: 2016

 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Interface de ligne de commande Auto-Scaling
{: #autoscalingcli}

*Dernière mise à jour : 25 février 2016*

Vous pouvez configurer le service {{site.data.keyword.autoscaling}} à l'aide de l'interface de ligne de commande {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}}. L'interface de ligne de commande {{site.data.keyword.autoscaling}} prend en charge Linux64, Win64 et OSX, et fournit des fonctionnalités semblables à celles de l'API RESTful de mise à l'échelle automatique.
{: shortdesc}

Avant de commencer, installez l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}. Voir [Télécharger l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](http://plugins.{DomainName}/ui/home.html){: new_window} pour des instructions.

## Ajout du plug-in d'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}

Une fois l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} installée, vous pouvez ajouter le plug-in de l'interface de ligne de commande {{site.data.keyword.autoscaling}}.

Procédez comme suit pour ajouter le référentiel et installer le plug-in :
1. Pour ajouter le référentiel de plug-in de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}, exécutez la commande suivante :
```
bluemix plugin repo-add bluemix-plugin-repo https://plugins.ng.bluemix.net
```
2. Pour installer le plug-in de l'interface de ligne de commande {{site.data.keyword.autoscaling}}, exécutez la commande suivante :
```
bluemix plugin install auto-scaling -r bluemix-plugin-repo
```

## Association d'une règle de mise à l'échelle automatique

Vous pouvez associer une règle de mise à l'échelle automatique à une application spécifique. Exécutez la commande suivante :

```bx as policy-attach <NOM_APP> -p <fichier_règle>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;NOM_APP&gt;</dt>
<dd class="pd">Nom de l'application à laquelle associer une règle de mise à l'échelle automatique.</dd>
<dt class="pt dlterm">&lt;fichier_règle&gt;</dt>
<dd class="pd">Nom du fichier JSON décrivant la règle de mise à l'échelle automatique. Voir la <a href="https://new-console.{DomainName}/apidocs/48" target="_blank">documentation de l'API RESTful {{site.data.keyword.autoscaling}}</a> pour plus de détails.</dd>
</dl>


## Génération d'une règle de mise à l'échelle automatique

Vous pouvez générer une règle de mise à l'échelle automatique en répondant aux questions dans l'interface de ligne de commande. Selon vos réponses, un fichier JSON contenant la définition de la règle de mise à l'échelle est sauvegardé avec le nom que vous indiquez. Si vous n''entrez pas le nom du fichier, le contenu de la règle est affiché directement sur la ligne de commande sans sauvegarde dans un fichier. Exécutez la commande suivante :

```bx as policy-create```
{: codeblock}


## Affichage d'une règle de mise à l'échelle automatique

Vous pouvez afficher la règle de mise à l'échelle automatique d'une application. Le contenu de la règle est affiché directement sur la ligne de commande. Exécutez la commande suivante :

```bx as policy-show <NOM_APP> [--json]```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;NOM_APP&gt;</dt>
<dd class="pd">Nom de l'application dont vous voulez afficher la règle de mise à l'échelle automatique. Par défaut, la structure JSON est convertie en une série de sorties lisibles par l'utilisateur.</dd>
</dl>

**Astuce :** vous pouvez également utiliser l'option **--json** pour formater automatiquement la réponse JSON originale.


## Retrait d'une règle de mise à l'échelle automatique

Vous pouvez retirer une règle de mise à l'échelle automatique d'une application. Exécutez la commande suivante :

```bx as policy-detach <NOM_APP>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;NOM_APP&gt;</dt>
<dd class="pd">Nom de l'application dont vous voulez retirer la règle de mise à l'échelle automatique.</dd>
</dl>


## Activation ou désactivation d'une règle de mise à l'échelle automatique

Vous pouvez activer ou désactiver la règle de mise à l'échelle automatique d'une application spécifique. Exécutez la commande suivante :

```bx as policy-enable|policy-disable <NOM_APP>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;NOM_APP&gt;</dt>
<dd class="pd">Nom de l'application dont vous voulez activer ou désactiver la règle de mise à l'échelle automatique.</dd>
</dl>


## Affichage de l'historique de mise à l'échelle automatique d'une application

Vous pouvez afficher l'historique d'une activité de mise à l'échelle automatique d'une application spécifique. Un tableau d'enregistrements d'historique de mise à l'échelle automatique s'affiche dans l'interface de ligne de commande.

```bx as history-show <NOM_APP>  [--start-date=<horodatage_début>]  [--end-date=<horodatage_fin>]  [--json]```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;NOM_APP&gt;</dt>
<dd class="pd">Nom de l'application dont vous voulez afficher l'historique de la règle de mise à l'échelle automatique.
<dt class="pt dlterm">&lt;horodatage_début&gt;</dt>
<dd class="pd">Horodatage de début de la plage d'historique. Les formats pris en charge sont `aaaa-MM-jjTHH:mm:ss+/-hhmm, aaaa-MM-jjTHH:mm:ssZ`. Par défaut, l'horodatage est fixé à 50 heures avant l'heure actuelle. Voir <a href="https://www.w3.org/TR/NOTE-datetime" target="_blank">W3C Date and Time Formats</a> pour obtenir des détails sur le format d'horodatage. 
<dt class="pt dlterm">&lt;horodatage_fin&gt;</dt>
<dd class="pd">Horodatage de fin de la plage d'historique. Les formats pris en charge sont `aaaa-MM-jjTHH:mm:ss+/-hhmm, aaaa-MM-jjTHH:mm:ssZ`. Par défaut, l'horodatage est fixé à l'heure actuelle. Voir <a href="https://www.w3.org/TR/NOTE-datetime" target="_blank">W3C Date and Time Formats</a> pour obtenir des détails sur le format d'horodatage. 
</dl>

**Astuce :** vous pouvez également utiliser l'option **--json** pour formater automatiquement la réponse JSON originale.

# rellinks
## general
* [Service {{site.data.keyword.autoscaling}}](../../../services/Auto-Scaling/index.html)
* [Interface de ligne de commande
de {{site.data.keyword.Bluemix_notm}}](http://plugins.{DomainName}/ui/home.html){: new_window}
* [W3C Date and Time Formats](https://www.w3.org/TR/NOTE-datetime){: new_window}


