{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Initiation au service {{site.data.keyword.autoscaling}}
{: #autoscaling}

*Dernière mise à jour : 18 janvier 2015*

Dans {{site.data.keyword.Bluemix_notm}}, vous pouvez gérer automatiquement la capacité de vos applications. Utilisez le service {{site.data.keyword.autoscalingfull}} pour augmenter ou diminuer automatiquement la capacité de calcul de votre application. Le nombre d'instances d'application est ajusté dynamiquement en fonction de la règle {{site.data.keyword.autoscaling}} que vous définissez.
{:shortdesc} 

## Utilisation du service {{site.data.keyword.autoscaling}} dans {{site.data.keyword.Bluemix_notm}}
{: #as-service}

Pour utiliser le service {{site.data.keyword.autoscaling}}, procédez comme suit :

1. Dans le tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur *Ajouter un service ou une API*, puis sélectionnez le service {{site.data.keyword.autoscaling}} dans la section DevOps du catalogue de service. Une nouvelle fenêtre s'ouvre et présente le service
{{site.data.keyword.autoscaling}}.
2. Sélectionnez l'application à laquelle lier le service {{site.data.keyword.autoscaling}} et cliquez sur *Créer*. <br/>
*Rappel :* Vous ne pouvez lier qu'un seul service {{site.data.keyword.autoscaling}} à une application. Si l'application est déjà liée à un autre service {{site.data.keyword.autoscaling}}, ne la sélectionnez pas à cette étape. Autrement, vous obtiendrez l'erreur CWSCV2004E.<br/>La fenêtre Reconstitution de l'application s'affiche.
3. Dans la fenêtre Reconstitution de l'application, cliquez sur *Reconstituer* pour reconstituer votre application avant l'utilisation du nouveau service {{site.data.keyword.autoscaling}} que vous venez d'ajouter. Une fois la reconstitution de l'application terminée, vous pouvez commencer à configurer le service {{site.data.keyword.autoscaling}} pour votre application.
4. Afin de configurer {{site.data.keyword.autoscaling}} pour une application, accédez à l'interface utilisateur {{site.data.keyword.Bluemix_notm}} et cliquez sur l'application à laquelle le service {{site.data.keyword.autoscaling}} est lié.
5. Dans la section des services du tableau de bord, cliquez sur l'icône *Auto-Scaling*.
6. Si vous ne l'avez pas encore fait, définissez la règle {{site.data.keyword.autoscaling}} pour l'application en cliquant sur *Créer une règle {{site.data.keyword.autoscaling}}*.

A présent, vous pouvez configurer la règle {{site.data.keyword.autoscaling}}, afficher les statistiques des mesures, ou afficher l'historique de mise à l'échelle pour l'application.
<dl>
<dt>Configuration de la règle</dt>
<dd>Utilisez cette section pour créer ou éditer les règles de mise à l'échelle afin de spécifier les conditions de déclenchement de certaines activités de mise à l'échelle.<ul>
<li> Pour les applications Liberty for Java™, vous pouvez définir des règles de mise à l'échelle pour le segment de mémoire de la machine virtuelle Java, la mémoire et le débit.<li> Pour les applications Node.js, vous pouvez définir des règles de mise à l'échelle pour la mémoire.
<li> Pour les applications Ruby, vous pouvez définir des règles de mise à l'échelle pour la mémoire.</ul>
*Remarque :* Vous pouvez définir plusieurs règles de mise à l'échelle pour plusieurs types de mesure. Toutefois, le service {{site.data.keyword.autoscaling}} ne détecte pas les conflits entre les règles de mise à l'échelle. Lorsque vous définissez la règle de mise à l'échelle, vous devez vous assurer qu'elle n'entre pas en conflit avec d'autres règles du même type. Autrement, vous pourrez voir fluctuer le nombre total d'instances car l'application est réduite en 1 minute et augmentée la minute qui suit.<br/><br/>
Si la charge de travail de votre application change considérablement au cours des heures pleines et des heures creuses, vous pouvez créer une planification de mise à l'échelle afin de traiter les différentes exigences de mise à l'échelle pour différentes périodes. Utilisez le paramètre Nombre minimal d'instances indiqué dans une planification pour définir le nombre d'instances d'application de référence, alors que les règles de mise à l'échelle dynamiques s'appliquent toujours à la planification pour déclencher des actions de mise à l'échelle (réduction/extension).</dd>
<dt>Statistiques des mesures</dt>
<dd>Affiche les statistiques des mesures pour les instances de votre application. Vous pouvez afficher les statistiques moyennes et sélectionner une
instance spécifique pour consulter la statistique qui la concerne.</dd>
<dt>Historique de mise à l'échelle</dt>
<dd>Affiche l'historique de mise à l'échelle de vos applications.<ul>
<li> Semaine dernière : affiche l'historique de mise à l'échelle pour la semaine précédente.
<li> Mois dernier : affiche l'historique de mise à l'échelle pour le mois précédent.
<li> Plage personnalisée : vous pouvez définir la plage de temps.</ul>
*Remarque :* Vous pouvez filtrer l'enregistrement d'historique en sélectionnant l'option Statut de mise à l'échelle ou Réduction/Extension.</dd>
</dl>


## Zones de règle pour le service {{site.data.keyword.autoscaling}}
{: #policyfields}

| Nom de zone  | Description |
|-------------|----------------------|
|*Nombre maximal d'instances autorisé* |	Nombre maximal d'instances d'application pouvant être démarrées. Si le nombre en cours d'instances d'application est égal à cette valeur, le service {{site.data.keyword.autoscaling}} n'augmente plus la capacité de traitement de l'application. Nombre d'instances minimum par défaut - Nombre minimal d'instances d'applications pouvant être démarrées. Si le nombre d'instances est égal à cette valeur, le service {{site.data.keyword.autoscaling}} ne réduit plus la capacité de traitement de l'application. |
| *Type de mesure*	| 	Types de mesure pris en charge pouvant être surveillés. Pour plus d'informations, voir le tableau 2. |
| *Extension* | 	Spécifie le seuil qui déclenche une action d'extension et le nombre d'instances qui sont augmentées lorsque l'action d'extension est déclenchée. |
| *Réduction* |	Spécifie le seuil qui déclenche une action de réduction et le nombre d'instances qui sont réduites lorsque l'action de réduction est déclenchée. |
| *Fenêtre des statistiques* |	Durée de la dernière période au cours de laquelle les valeurs de mesure reçues ont été reconnues comme valides. Les valeurs de mesure ne sont valides que si les horodatages sont compris dans cette période. L'unité du paramètre Fenêtre des statistiques est la seconde. |
| *Durée de la violation*	| Durée de la dernière période au cours de laquelle une action de mise à l'échelle peut être déclenchée. Une action de mise à l'échelle est déclenchée lorsque des valeurs de mesure collectées dépassent le seuil supérieur ou se trouvent en dessous du seuil inférieur pendant plus longtemps que la durée spécifiée. L'unité de la durée de violation est la seconde. |
| *Délai pour la réduction des instances* | Après une action de réduction, les autres demandes de mise à l'échelle sont ignorées pendant la durée spécifiée par le paramètre Délai pour la réduction des instances. L'unité de ce paramètre est la seconde. |
| *Délai pour l'extension des instances*	| Après une action d'extension, les autres demandes de mise à l'échelle sont ignorées pendant la durée spécifiée par le paramètre Délai pour l'extension des instances. L'unité de ce paramètre est la seconde. |
| *Fuseau horaire*	| Fuseau horaire de la planification. |
| *Heure de début*  |	Heure de début d'une planification récurrente. |
| *Heure de fin*    |	Heure de fin d'une planification récurrente.	|
| *Répétition*	|	Jour dans la semaine d'application d'une planification récurrente. |
| *Nombre minimal d'instances* |	Nombre minimal d'instances pouvant être démarrées pour l'application au cours de la période spécifiée dans la planification. |
| *Date & heure de début* |	Date et heure de début de la planification configurée pour une date spécifique. |
| *Date & heure de fin* |	Date et heure de fin de la planification configurée pour une date spécifique.	|

Tableau 1. Zones de règle dans la règle de mise à l'échelle

| Nom de mesure | Description | Type d'application pris en charge |
|-------------|----------------------| ------------------- |
| *Segment de mémoire de JVM* |	Pourcentage d'utilisation du segment de mémoire de la machine virtuelle Java.	| Liberty for Java |
| *Mémoire*   |	Pourcentage d'utilisation de la mémoire.	|  Liberty for Java<br/> Node.js <br/> Ruby <br/> |
| *Débit* | Nombre de demandes traitées par seconde.| Liberty for Java |
| *Temps de réponse* |	Temps de réponse des demandes traitées.	| Liberty for Java |

Tableau 2. Noms de mesure pris en charge

## Messages d'erreur
{: #errmsgs}
Cette section dresse la liste des messages d'erreur et d'avertissement générés par le service {{site.data.keyword.autoscaling}}.
 
### CWSCV2004E Un autre service {{site.data.keyword.autoscaling}} est déjà lié à l'application.
**Vous ne pouvez lier qu'un seul service {{site.data.keyword.autoscaling}} à une application. Cette erreur se produit lorsque vous voulez lier le service {{site.data.keyword.autoscaling}} à une application déjà liée à un autre service {{site.data.keyword.autoscaling}}.**

Sélectionnez une autre application à laquelle aucun service {{site.data.keyword.autoscaling}} n'est lié et liez le service {{site.data.keyword.autoscaling}} cible à cette application.
Si vous rencontrez cette erreur dans d'autres cas, contactez le support IBM.

### CWSCV6001E Le serveur d'API ne peut pas analyser syntaxiquement les chaînes JSON d'entrée pour l'API : {0}.
**Un problème est survenu lors de l'analyse syntaxique des chaînes JSON d'entrée.**

Vérifiez le JSON d'entrée avec le document d'API et corrigez l'erreur.

### CWSCV6002E Le serveur d'API ne peut pas analyser syntaxiquement les chaînes JSON de sortie pour l'API : {0}.
**Un problème est survenu lors de l'analyse syntaxique des chaînes JSON d'entrée.**

Prenez contact avec l'administrateur cloud pour plus d'informations.

### CWSCV6003E Erreur de format des chaînes JSON d'entrée {0} dans le JSON d'entrée pour l'API : {1}.
**Erreur de format détectée lors de l'analyse syntaxique des chaînes JSON d'entrée.**

Vérifiez le JSON d'entrée avec le document d'API et corrigez l'erreur.

### CWSCV6004E Erreur de format des chaînes JSON de sortie {0} dans le JSON de sortie l'API : {1}.
**Erreur de format détectée lors de l'analyse syntaxique des chaînes JSON de sortie.**

Prenez contact avec l'administrateur cloud pour plus d'informations.

### CWSCV6005E Une erreur de serveur interne est survenue au cours de l'opération suivante : {0}.
**Une erreur de serveur interne est survenue lors du traitement de la demande.**

Prenez contact avec l'administrateur cloud pour plus d'informations.

### CWSCV6006E L'appel des API CloudFoundry a échoué : {0}
**Une erreur est survenue lors de l'appel des API CloudFoundry.**

Prenez contact avec l'administrateur cloud pour plus d'informations.

### CWSCV6007E L'application est introuvable : {0}
**L'application est introuvable.**

Vérifiez les informations sur l'application pour plus d'informations.

### CWSCV6008E L'erreur suivante est survenue lors de l'extraction des informations pour l'application {0} : {1}
**L'extraction des informations sur l'application a échoué avec des erreurs.**

Vérifiez les informations sur l'application pour plus d'informations.

### CWSCV6009E Le service {0} pour l'application {1} est introuvable.
**Le service pour cette application est introuvable.**

Vérifiez la liaison de service pour cette application pour plus d'informations.

### CWSCV6010E La règle pour l'application {0} est introuvable.
**La règle pour cette application est introuvable.**

Vérifiez la configuration de l'application pour plus d'informations.

### CWSCV6011E L'authentification interne a échoué au cours de l'opération suivante : {0}
**L'authentification interne a échoué.**

Prenez contact avec l'administrateur cloud pour plus d'informations.


# rellinks
## samples
* [Tutoriel : Make your application elastic on {{site.data.keyword.Bluemix_notm}}](http://www.ibm.com/developerworks/cloud/library/cl-autoscale-app/index.html){:new_window}
* [Cloud Foundry Architecture Labs](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/){:new_window}

## sdk
* [API REST d'IBM {{site.data.keyword.autoscaling}} pour {{site.data.keyword.Bluemix_notm}}](https://www.{DomainName}/docs/api/content/api/auto-scaling/index.html){:new_window}

## general
* [Fiche des prix {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/pricing/){:new_window}
* [{{site.data.keyword.Bluemix_notm}}  Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs){:new_window}
* [Interface de ligne de commande {{site.data.keyword.autoscaling}}](../../cli/plugins/auto-scaling/index.html){:new_window}

