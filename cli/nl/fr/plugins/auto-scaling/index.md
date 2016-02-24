{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Interface de ligne de commande Auto-Scaling
{: #autoscalingcli}

*Dernière mise à jour : 20 janvier 2015*

Vous pouvez configurer le service {{site.data.keyword.autoscaling}} à l'aide de l'interface de ligne de commande {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}}. L'interface de ligne de commande {{site.data.keyword.autoscaling}} prend en charge Linux64, Win64 et OSX, et fournit des fonctionnalités semblables à celles de l'API RESTful {{site.data.keyword.autoscaling}}.
{: shortdesc}

Avant de commencer, installez l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}. Voir [Télécharger l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](http://plugins.{DomainName}/ui/home.html){: new_window} pour obtenir des instructions.

## Ajout du plug-in de l'interface de ligne de commande Auto-Scaling

Une fois l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} installée, vous pouvez ajouter le plug-in de l'interface de ligne de commande {{site.data.keyword.autoscaling}}.

Pour ajouter le référentiel et installer le plug-in, procédez comme suit :
1. Pour ajouter le référentiel de plug-in de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}, exécutez la commande suivante :
```
bluemix plugin repo-add bluemix-plugin-repo https://plugins.stage1.ng.bluemix.net
```
2. Pour installer le plug-in de l'interface de ligne de commande {{site.data.keyword.autoscaling}}, exécutez la commande suivante :
```
bluemix plugin install auto-scaling -r bluemix-plugin-repo
```

## Association d'une règle de mise à l'échelle automatique

Vous pouvez associer une règle de mise à l'échelle automatique (Auto-Scaling policy) à une application spécifique. Exécutez la commande suivante :

```bx as policy-attach <APP_NAME> -p <policy_file>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Nom de l'application à laquelle vous voulez associer une règle de mise à l'échelle automatique.</dd>
<dt class="pt dlterm">&lt;policy_file&gt;</dt>
<dd class="pd">Nom du fichier JSON décrivant la règle de mise à l'échelle automatique. Pour plus d'informations, voir la [documentation de l'API RESTful {{site.data.keyword.autoscaling}}](https://www.{DomainName}/docs/api/content/api/auto-scaling/index.html).</dd>
</dl>


## Génération d'une règle de mise à l'échelle automatique

Vous pouvez générer une règle de mise à l'échelle automatique en répondant aux questions sur l'interface de ligne de commande. Selon ce que vous avez saisi, un fichier JSON contenant la définition de cette règle est sauvegardé avec le nom que vous avez indiqué. Si vous n'avez pas entré le nom du fichier, le contenu de la règle s'imprime directement sur la ligne de commande sans sauvegarde dans un fichier. Exécutez la commande suivante :

```bx as policy-create```
{: codeblock}


## Affichage d'une règle de mise à l'échelle automatique

Vous pouvez afficher la règle de mise à l'échelle automatique d'une application. Le contenu de la règle s'imprime directement sur la ligne de commande. Exécutez la commande suivante :

```bx as policy-show <APP_NAME> [--json]```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Nom de l'application dont vous voulez afficher la règle de mise à l'échelle automatique. Par défaut, la structure JSON est convertie en une série de sorties lisibles par l'utilisateur.</dd>
</dl>

**Astuce :** Vous pouvez également utiliser l'option **--json** pour imprimer automatiquement la réponse JSON originale.


## Retrait d'une règle de mise à l'échelle automatique

Vous pouvez retirer une règle de mise à l'échelle automatique d'une application. Exécutez la commande suivante :

```bx as policy-detach <APP_NAME>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Nom de l'application dont vous voulez retirer la règle de mise à l'échelle automatique.</dd>
</dl>


## Activation ou désactivation d'une règle de mise à l'échelle automatique

Vous pouvez activer ou désactiver la règle de mise à l'échelle automatique d'une application spécifique. Exécutez la commande suivante :

```bx as policy-enable|policy-disable <APP_NAME>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Nom de l'application dont vous voulez activer ou désactiver la règle de mise à l'échelle automatique.</dd>
</dl>


## Affichage de l'historique de mise à l'échelle automatique d'une application

Vous pouvez afficher l'historique d'une activité de mise à l'échelle automatique d'une application spécifique. Un tableau d'enregistrements d'historique de mise à l'échelle automatique s'affiche dans l'interface de ligne de commande.

```bx as history-show <APP_NAME>  [--start-date=<start_timestamp>]  [--end-date=<end_timestamp>]  [--json]```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Nom de l'application dont vous voulez afficher l'historique de la règle de mise à l'échelle automatique.
<dt class="pt dlterm">&lt;start_timestamp&gt;</dt>
<dd class="pd">Horodatage de début de la plage d'historique. Les formats pris en charge sont `yyyy-MM-ddTHH:mm:ss+/-hhmm, yyyy-MM-ddTHH:mm:ssZ`. Par défaut, l'horodatage est fixé à 50 heures avant l'heure actuelle. Voir le site [W3C Date and Time Formats](https://www.w3.org/TR/NOTE-datetime){: new_window} pour obtenir des détails sur le format d'horodatage.
<dt class="pt dlterm">&lt;end_timestamp&gt;</dt>
<dd class="pd">Horodatage de fin de la plage d'historique. Les formats pris en charge sont `yyyy-MM-ddTHH:mm:ss+/-hhmm, yyyy-MM-ddTHH:mm:ssZ`. Par défaut, l'horodatage est fixé à l'heure actuelle. Voir le site [W3C Date and Time Formats](https://www.w3.org/TR/NOTE-datetime){: new_window} pour obtenir des détails sur le format d'horodatage.
</dl>

**Astuce :** Vous pouvez également utiliser l'option **--json** pour imprimer automatiquement la réponse JSON originale.

# rellinks
## general
* [Service {{site.data.keyword.autoscaling}}](../../services/Auto-Scaling/index.html)
* [Interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](http://plugins.{DomainName}/ui/home.html){: new_window}
* [W3C Date and Time Formats](https://www.w3.org/TR/NOTE-datetime){: new_window}


