---

 

copyright:

  years: 2015，2016
lastupdated: "2016-11-02"  
 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Initiation au service {{site.data.keyword.autoscaling}}
{: #autoscaling}
Dernière mise à jour : 2 novembre 2016
{: .last-updated}

Dans {{site.data.keyword.Bluemix_notm}}, vous pouvez gérer automatiquement la capacité de vos applications. Utilisez le service {{site.data.keyword.autoscaling}} pour augmenter ou diminuer automatiquement la capacité de calcul de votre application. Le nombre d'instances d'application est ajusté dynamiquement en fonction de la règle {{site.data.keyword.autoscaling}} que vous définissez.
{:shortdesc} 

## Contenu
  * [Utilisation du service {{site.data.keyword.autoscaling}} dans {{site.data.keyword.Bluemix_notm}}](#as-service)
  * [Configuration des applications Node.js avec le service {{site.data.keyword.autoscaling}}](#node-asagent)
  * [Gestion du service {{site.data.keyword.autoscaling}} via une API RESTful](#RESTAPI)
  * [Gestion du service {{site.data.keyword.autoscaling}} via l'interface de ligne de commande {{site.data.keyword.autoscaling}}](#CLI)
  * [Zones de règle pour le service {{site.data.keyword.autoscaling}}](#policy_fields)
  * [Messages d'erreur](#err_msg)

## Utilisation du service {{site.data.keyword.autoscaling}} dans {{site.data.keyword.Bluemix_notm}}
{: #as-service}

Pour utiliser le service {{site.data.keyword.autoscaling}}, procédez comme suit :

1. Dans le tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur *Ajouter un service ou une API*, puis sélectionnez le service {{site.data.keyword.autoscaling}} dans la section DevOps du catalogue de service. Une nouvelle fenêtre s'ouvre et présente le service
{{site.data.keyword.autoscaling}}.
2. Sélectionnez l'application à laquelle lier le service {{site.data.keyword.autoscaling}} et cliquez sur *Créer*. <br/>
*Rappel :* Vous ne pouvez lier qu'UN SEUL service {{site.data.keyword.autoscaling}} à une application. Si l'application est déjà liée à un autre service {{site.data.keyword.autoscaling}}, ne la sélectionnez pas à cette étape. Autrement, vous obtiendrez l'erreur CWSCV2004E.<br/>La fenêtre Reconstitution de l'application s'affiche.
3. Dans la fenêtre Reconstitution de l'application, cliquez sur *Reconstituer* pour reconstituer votre application avant l'utilisation du nouveau service {{site.data.keyword.autoscaling}} que vous venez d'ajouter. <br/><ul><li>Pour l'application Liberty, le service {{site.data.keyword.autoscaling}} est configuré automatiquement et prêt à être utilisé après la reconstitution de l'application.</li> <li>Pour les applications Node.js, vous devez mettre à jour votre code d'application pour activer le service {{site.data.keyword.autoscaling}} avant d'envoyer l'application par commande push vers {{site.data.keyword.Bluemix_notm}}. Voir [Configuration des applications Node.js avec le service {{site.data.keyword.autoscaling}}](index.html#node_asagent) pour plus de détails.</ul><br/>
Une fois la reconstitution de l'application terminée, vous pouvez commencer à configurer le service {{site.data.keyword.autoscaling}} pour votre application.
4. Afin de configurer {{site.data.keyword.autoscaling}} pour une application, accédez à l'interface utilisateur {{site.data.keyword.Bluemix_notm}} et cliquez sur l'application à laquelle le service {{site.data.keyword.autoscaling}} est lié.
5. Dans la section des services du tableau de bord, cliquez sur l'icône *Auto-Scaling*.
6. Si vous ne l'avez pas encore fait, définissez la règle {{site.data.keyword.autoscaling}} pour l'application en cliquant sur *Créer une règle {{site.data.keyword.autoscaling}}*.

A présent, vous pouvez configurer la règle {{site.data.keyword.autoscaling}}, afficher les statistiques des mesures, ou afficher l'historique de mise à l'échelle pour l'application.
<dl>
<dt>Configuration de la règle</dt>
<dd>Utilisez cette section pour créer ou éditer les règles de mise à l'échelle afin de spécifier les conditions de déclenchement de certaines activités de mise à l'échelle.<ul>
<li> Pour les applications Liberty for Java™, vous pouvez définir des règles de mise à l'échelle pour le segment de mémoire, la mémoire, le temps de réponse et le débit.
  
<li> Pour les applications Node.js, vous pouvez définir des règles de mise à l'échelle pour le segment de mémoire, la mémoire et le débit.
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


## Configuration des applications Node.js avec le service {{site.data.keyword.autoscaling}}
{: #node-asagent}

Pour activer le service {{site.data.keyword.autoscaling}} dans vos applications Node.js, en plus des étapes de mise à disposition et de liaison du service, effectuez les étapes suivantes avant d'envoyer l'application par commande push vers {{site.data.keyword.Bluemix_notm}}.

1. Mettez à jour le fichier package.json en procédant comme suit : <ol><li>Créez une entrée de dépendance pour `blumix-autoscaling-agent`, `"bluemix-autoscaling-agent": "*"`.<br/>, par exemple.<li>(Facultatif) Définissez la limite de segment de mémoire au sein de la section `scripts`, basée sur la mémoire que vous allouez pour votre application, `"start": "node --max-old-space-size=600 app.js"`, par exemple. .<br/>*Remarque :* définissez une valeur pour `max-old-space-size` si vous voulez déclencher la mise à l'échelle des instances en fonction de l'utilisation du segment mémoire. Si la valeur n'est pas définie quand vous démarrez votre application, la limite de segment mémoire Node.js par défaut de 1,4 Go est utilisée quel que soit le volume de mémoire alloué à votre application, ce qui peut entraîner des décisions de mise à l'échelle automatique incorrectes.<br/>
```
{
	"name": "NodejsStarterApp",
	"version": "0.0.1",
	"description": "A sample nodejs app for Bluemix",
	"scripts": {
		"start": "node --max-old-space-size=600 app.js"
	},
	"dependencies": {
		"bluemix-autoscaling-agent": "*"
	},
	"repository": {},
	"engines": {
		"node": "0.12.x"
	} 
}
```
</ol>
2. Mettez à jour votre fichier principal pour ajouter la déclaration d'agent `var as_agent = require('bluemix-autoscaling-agent');`. Le fragment de code montre un fichier js d'entrée complet avec la déclaration d'agent de mise à l'échelle automatique.<br/>
```
var agent = require('bluemix-autoscaling-agent');
var http = require('http');
var server = http.createServer(function handler(req, res) {
	console.log("Hello!");
	
	}).listen(process.env.PORT || 3000);
console.log('App is listening on port 3000');
```

## Gestion du service {{site.data.keyword.autoscaling}}  via une API RESTful 
{: #RESTAPI}

L'API RESTful de service {{site.data.keyword.autoscaling}} fournit une autre façon de gérer le service {{site.data.keyword.autoscaling}} à côté de l'interface utilisateur Bluemix, et elle prend aussi en charge l'extraction et l'analyse des données de mise à l'échelle. Elle propose des fonctions similaires, comme la création d'une règle et l'obtention d'un historique de mise à l'échelle, comme dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}} avec API .

Pour utiliser l'API RESTful {{site.data.keyword.autoscaling}} pour gérer le service {{site.data.keyword.autoscaling}}, effectuez les prérequis suivants : liez le service {{site.data.keyword.autoscaling}}  à votre service application comme spécifié dans la section précédente, procurez-vous le jeton `AccessToken`, l'URL du serveur d'API {{site.data.keyword.autoscaling}} et l'ID `ID_app` de l'application dont vous voulez augmenter ou réduire la capacité de traitement :

1. Pour répondre à des objectifs de sécurité, dans chaque en-tête de demande de l'API RESTful {{site.data.keyword.autoscaling}}, un jeton `AccessToken` correct obtenu via la procédure UAA CloudFoundry doit être fourni dans l'en-tête `Autorisation` pour indiquer la validation requise de la demande. En cas de non respect de l'obligation relative à `AccessToken`, une réponse Non autorisé (401) est émise. Deux méthodes sont à votre disposition pour obtenir ce jeton `AccessToken` après avoir installé l'outil de ligne de commande Cloud Foundry et vous être connecté à {{site.data.keyword.Bluemix_notm}} :<ul><li>Vous pouvez obtenir ce jeton via la commande `cf oauth-token` :
   ```
   > cf oauth-token
   Getting OAuth token...
   OK

     bearer eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiJhNjIzMGE1YS1mNzE3LTQ0YjItOWM3Yi1kNGJkYThhZGU0NjkiLCJzdWIiOiI4OGViNjM2My1hMjkzLTRlZTItYWQ1MS0yOGVkMTZmZjMwNzQiLCJzY29wZSI6WyJjbG91ZF9jb250cm9sbGVyLnJlYWQiLCJwYXNzd29yZC53cml0ZSIsImNsb3VkX2NvbnRyb2xsZXIud3JpdGUiLCJvcGVuaWQiXSwiY2xpZW50X2lkIjoiY2YiLCJjaWQiOiJjZiIsImF6cCI6ImNmIiwiZ3JhbnRfdHlwZSI6InBhc3N3b3JkIiwidXNlcl9pZCI6Ijg4ZWI2MzYzLWEyOTMtNGVlMi1hZDUxLTI4ZWQxNmZmMzA3NCIsIm9yaWdpbiI6InVhYSIsInVzZXJfbmFtZSI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJlbWFpbCI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJyZXZfc2lnIjoiZDhlNGY0MDIiLCJpYXQiOjE0NTU2MDc1NDUsImV4cCI6MTQ1NTY1MDc0NSwiaXNzIjoiaHR0cHM6Ly91YWEuc3RhZ2UxLm5nLmJsdWVtaXgubmV0L29hdXRoL3Rva2VuIiwiemlkIjoidWFhIiwiYXVkIjpbImNsb3VkX2NvbnRyb2xsZXIiLCJwYXNzd29yZCIsImNmIiwib3BlbmlkIl19.nrzsEAZmGXNOWjX8r5Xf7U8Hj5-CE1rtHg8_C-jZKSk
   ```
 La chaîne longue retournée qui commence par “bearer” correspond au jeton AccessToken qui peut être utilisé dans la demande de l'API RESTful {{site.data.keyword.autoscaling}}. Si vous rencontrez des erreurs de type “Commande introuvable”, vous pouvez mettre votre outil de ligne de commande Cloud Foundry au niveau de la dernière version disponible.</li><li>Vous pouvez aussi trouver ce jeton AccessToken dans le répertoire de base. Une fois que vous vous êtes connecté à {{site.data.keyword.Bluemix_notm}} depuis l'interface de ligne de commande, un dossier `.cf` est créé dans votre répertoire de base, dans lequel vous pouvez trouver un fichier JSON intitulé `config.json` qui contient une liste des informations d'environnement de votre consignation actuelle (organisation, espace, noeud final d'authentification et version, par exemple). Vous pouvez localiser une entrée `AccessToken` dans le fichier, comme ci-dessous : 
    ```
   >cat ~/.cf/config.json
 {
  "ConfigVersion": 3,
  "Target": "https://api.ng.bluemix.net",
  "ApiVersion": "2.40.0",
  "AuthorizationEndpoint": "https://login.ng.bluemix.net/UAALoginServerWAR",
  "LoggregatorEndPoint": "wss://loggregator.ng.bluemix.net:443",
  "DopplerEndPoint": "wss://doppler.ng.bluemix.net:443",
  "UaaEndpoint": "https://uaa.ng.bluemix.net",
  "RoutingApiEndpoint": "https://api.ng.bluemix.net/routing",
  "AccessToken": "bearer eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiJhNjIzMGE1YS1mNzE3LTQ0YjItOWM3Yi1kNGJkYThhZGU0NjkiLCJzdWIiOiI4OGViNjM2My1hMjkzLTRlZTItYWQ1MS0yOGVkMTZmZjMwNzQiLCJzY29wZSI6WyJjbG91ZF9jb250cm9sbGVyLnJlYWQiLCJwYXNzd29yZC53cml0ZSIsImNsb3VkX2NvbnRyb2xsZXIud3JpdGUiLCJvcGVuaWQiXSwiY2xpZW50X2lkIjoiY2YiLCJjaWQiOiJjZiIsImF6cCI6ImNmIiwiZ3JhbnRfdHlwZSI6InBhc3N3b3JkIiwidXNlcl9pZCI6Ijg4ZWI2MzYzLWEyOTMtNGVlMi1hZDUxLTI4ZWQxNmZmMzA3NCIsIm9yaWdpbiI6InVhYSIsInVzZXJfbmFtZSI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJlbWFpbCI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJyZXZfc2lnIjoiZDhlNGY0MDIiLCJpYXQiOjE0NTU2MDc1NDUsImV4cCI6MTQ1NTY1MDc0NSwiaXNzIjoiaHR0cHM6Ly91YWEuc3RhZ2UxLm5nLmJsdWVtaXgubmV0L29hdXRoL3Rva2VuIiwiemlkIjoidWFhIiwiYXVkIjpbImNsb3VkX2NvbnRyb2xsZXIiLCJwYXNzd29yZCIsImNmIiwib3BlbmlkIl19.nrzsEAZmGXNOWjX8r5Xf7U8Hj5-CE1rtHg8_C-jZKSk",
  "SSHOAuthClient": "ssh-proxy",
 .....
 }
   ```
Le jeton `AccessToken` du fichier `config.json` n'est valide que pendant une période de temps précise. Si vous obtenez une erreur 401 de réponse non autorisée pour la demande d'API REST, vous devrez vous reconnecter de nouveau depuis l'interface de ligne de commande pour actualiser le fichier et obtenir le nouveau jeton `AcessToken`. </li></ul>
 
2.  Vous pouvez obtenir l'URL du serveur d'{{site.data.keyword.autoscaling}}API en contrôlant la variable d'environnement `VCAP_SERVICE` après liaison de votre application au service {{site.data.keyword.autoscaling}}. Dans `VCAP_SERVICE`, localisez la section relative au service {{site.data.keyword.autoscaling}} ; l'URL `url_api` est l'URL du serveur d'API avec lequel votre application est liée. Vous avez besoin de cette URL de serveur d'API pour vous connecter au service d'API RESTful {{site.data.keyword.autoscaling}} :
   ```
    {
      "Auto-Scaling": [
      {
         "name": "Auto-Scaling-iw",
         "label": "Auto-Scaling",
         "plan": "free",
         "credentials": {
            "agentUsername": "agent",
            "api_url": "https://ScalingAPI.ng.bluemix.net",
            "service_id": "3f42b7ff-d939-4ff2-9a55-cb09cef9ab9e",
            "app_id": "2287f442-a7f3-4799-8919-d3908c386fa3",
            "url": "https://Scaling3.ng.bluemix.net",
            "agentPassword": "0cddf80b-37e1-4cfd-b648-83a6c8wee69f"
         }
      }
     ]
   }
   ``` 
  Notez que cette URL peut aussi être trouvée via la commande `cf env APPNAME` :
   ```
   > cf env Hello
   Getting env variables for app Hello in org OE_Runtimes_SVT / space RT_SVT as Alice...
   OK

   System-Provided:
   {
     "VCAP_SERVICES": {
     "Auto-Scaling": [
     {
      "credentials": {
       "agentPassword": "b626b064-7d26-417a-b954-41c6d3cb5200",
       "agentUsername": "agent",
       "api_url": "https://ScalingAPI.ng.bluemix.net",
       "app_id": "aa8d19b6-eceb-4b6e-b034-926a87e98a51",
       "service_id": "8f482f78-58d8-493c-829b-635e4cbfd817",
       "url": "https://Scaling.ng.bluemix.net"
      },
      "label": "Auto-Scaling",
      "name": "ScalingService",
      "plan": "free",
      "tags": [
       "bluemix_extensions",
       "ibm_created",
       "dev_ops"
      ]
     }
   ...
   ```  
3.  Vous pouvez obtenir cet ID `ID_app` depuis la variable d'environnement `VCAP_SERVICES` ou simplement exécuter la commande `cf app APPNAME --guid` :

   ```
   > cf app Hello --guid
   aa8d19b6-eceb-4b6e-b034-926a87e98a51
   > 
   ```

Avec tous les prérequis ci-dessus, vous pouvez maintenant effectuer la demande d'API REST en utilisant le module complémentaire RestClient dans le navigateur ou via un outil de type `curl`. 

Avec le module complémentaire client REST, comme celui de Firefox ou de Chrome, vous pouvez déclencher une demande REST vers le serveur d'API {{site.data.keyword.autoscaling}} pour exécuter votre commande. Vous fournissez simplement ces modules complémentaires avec l'URL d'API REST, les méthodes et en-têtes qui sont requis par cette API REST et les paramètres de la partie corps. Pour plus de détails sur chaque API, voir [API REST d'IBM {{site.data.keyword.autoscaling}} pour {{site.data.keyword.Bluemix_notm}}](https://new-console.ng.bluemix.net/apidocs/48){:new_window}.

Avec des outils comme `curl`, vous pouvez gérer le service {{site.data.keyword.autoscaling}} au sein d'un script comme suit :    
```
    cf login -a http://api.ng.bluemix.net -u Alice -p pa55w0rd --skip-ssl-validation
    accessToken=$(cf oauth-token | grep bearer | sed -e s/bearer/Bearer/g)
    API_url=$(cf env Hello | grep "api_url" | awk '{print $2}' | cut -d "," -f1 | cut -d "\"" -f2 )
    policyJson="./policy.json"
    appId=$(cf app Hello --guid)

    echo  -e "\nCreate scaling policy using API :"
    createPolicyUrl="${API_url}/v1/autoscaler/apps/${appId}/policy"
    curl_cmd="curl $createPolicyUrl -X 'PUT' -H 'Content-Type:application/json'  -H 'Accept:application/json' -H 'Authorization:$accessToken' --data-binary @${policyJson} -s -o response.txt -w '%{http_code}\n'"
    eval status_code=$($curl_cmd)
    if [[ $status_code -eq 201 ]]; then
         echo "looks good"
    else
         echo "error happens"
         exit 255
    fi
  ```

## Gestion du service {{site.data.keyword.autoscaling}} via l'interface de ligne de commande {{site.data.keyword.autoscaling}} 
{: #CLI}

L'interface de ligne de commande {{site.data.keyword.autoscaling}} fournit des fonctionnalités similaires à l'API RESTful {{site.data.keyword.autoscaling}} mais plus conviviales pour configurer le service {{site.data.keyword.autoscaling}}. Avec l'interface de ligne de commande {{site.data.keyword.autoscaling}}, vous n'avez pas besoin de vous préoccuper des détails de l'API RESTful {{site.data.keyword.autoscaling}}, comme le jeton `AccessToken` ou l'URL du serveur d'API. La seule chose que vous ayez à faire est de suivre pas à pas les instructions fournies par l'interface. Pour plus de détails sur la façon d'installer et d'utiliser l'interface de ligne de commande {{site.data.keyword.autoscaling}}, voir [Interface de ligne de commande {{site.data.keyword.autoscaling}}](../../cli/plugins/auto-scaling/index.html){:new_window}



## Zones de règle pour le service {{site.data.keyword.autoscaling}}
{: #policy_fields}

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
| *Segment de mémoire* |	Pourcentage d'utilisation du segment de mémoire.	| Liberty for Java, SDK Node.js |
| *Mémoire*   |	Pourcentage d'utilisation de la mémoire.	|  Tout |
| *Débit* | Nombre de demandes traitées par seconde.| Liberty for Java, SDK Node.js |
| *Temps de réponse* |	Temps de réponse des demandes traitées.	| Liberty for Java |

Tableau 2. Noms de mesure pris en charge

*Remarque :* Pour collecter les données de mesures de mise à l'échelle, votre application doit être déployée en tant qu'application Web Liberty pour que les mesures de requêtes HTTP/HTTPS soient traitées via un conteneur Web Liberty.
Par exemple, si vous exécutez une application Spring Boot en tant qu'appli "Main-Class", le pack de construction Liberty ne vous fournit qu'un environnement Java et l'appli s'exécute en fait dans le conteneur Tomcat intégré Spring. Par conséquent, aucune mesure ne sera collectée par le service Auto-Scaling. Vous devez exécuter votre appli en tant que fichier WAR Liberty pour qu'elle fonctionne avec le service Auto-Scaling.

## Messages d'erreur
{: #err_msg}
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
{: #rellinks}

## samples
{: #samples}

* [Tutoriel : Make your application elastic on {{site.data.keyword.Bluemix_notm}}](http://www.ibm.com/developerworks/cloud/library/cl-autoscale-app/index.html){:new_window}
* [Cloud Foundry Architecture Labs](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/){:new_window}

## sdk
{: #sdk}

* [API REST d'IBM {{site.data.keyword.autoscaling}} pour {{site.data.keyword.Bluemix_notm}}](https://new-console.{DomainName}/apidocs/48){:new_window}

## general
{: #general}

* [Conteneurs de mise à l'échelle](https://www.{DomainName}/docs/containers/container_creating_ov.html#container_group_ov){:new_window}
* [Serveurs virtuels de mise à l'échelle](https://www.{DomainName}/docs/virtualmachines/vm_index.html#vm_manage_instances){:new_window}
* [Interface de ligne de commande {{site.data.keyword.autoscaling}}](../../cli/plugins/auto-scaling/index.html){:new_window}
* Agent [{{site.data.keyword.autoscaling}} pour Node.js](https://www.npmjs.com/package/bluemix-autoscaling-agent){:new_window}

