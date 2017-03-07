---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Cloud Analytics
{: #cloud_analytics}

En utilisant {{site.data.keyword.iot_short}} Cloud Analytics, vous spécifiez des conditions de règle qui sont basées sur les données de terminal en temps réel et qui déclenchent des alertes et des actions facultatives lorsqu'elles sont réunies.    
{: shortdesc}

Par exemple, vous pouvez créer une règle garantissant que lorsque le terminal est supprimé ou que la température du terminal augmente, une alerte est envoyée au tableau de bord du terminal de l'utilisateur et un courrier électronique est envoyé à l'administrateur.

## Avant de commencer
{: #byb}
Assurez-vous que les propriétés de terminal que vous souhaitez utiliser comme conditions dans vos règles ont été mappées à des schémas. Pour plus d'informations, voir [Connexion de terminaux](iotplatform_task.html) et [Création de schémas](im_schemas.html).

En outre, consultez la recette [Using Rules and Actions with {{site.data.keyword.iot_short}} Cloud Analytics ![](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/){: new_window} pour comprendre les règles et les actions utilisées dans Cloud Analytics.

## Gestion des règles et des actions  
{: #managing_rules}

Utilisez le tableau de bord **Règles** pour créer et gérer des règles et des actions pour votre organisation.

Pour obtenir une présentation des règles et des alertes qui ont été déclenchées pour vos terminaux, utilisez les tableaux suivants :

 |Nom de tableau | Description |  
 |:---|:---|  
  |Analyse centrée sur la règle | Affiche les règles de votre organisation. Des cartes supplémentaires recensent les alertes déclenchées, les terminaux associés, les propriétés de terminal et les informations d'alerte. |  
 |Analyse centrée sur le terminal | Affiche les terminaux qui sont connectés à votre organisation. Des cartes supplémentaires affichent des alertes pour un terminal sélectionné, des informations relatives à un terminal sélectionné, et des informations d'alerte. |

 Pour plus d'informations sur les cartes d'analyse par défaut, voir [Visualisation des données en temps réel à l'aide de tableaux et de cartes](data_visualization.html#default_boards).


## Création de règles
{: #rules}

Les règles sont des points de décision basés sur une condition qui correspondent aux données de terminal en temps réel avec des valeurs de seuil prédéfinies ou d'autres données de propriété afin de déclencher une alerte si une condition est remplie. Outre l'alerte qui s'affiche dans le tableau de bord {{site.data.keyword.iot_short}}, vous pouvez ajouter une ou plusieurs actions afin d'exécuter une logique métier lorsqu'une règle est déclenchée.

**Important :** Avant de pouvoir créer des règles pour un type de terminal, vous devez créer un schéma pour le type de terminal. Pour plus d'informations, voir [Créer des schémas de type de terminal](im_schemas.html).

Pour créer une règle :
1. Dans le tableau de bord {{site.data.keyword.iot_short}}, accédez à **Règles**.
2. Cliquez sur **Créer une règle**, attribuez un nom à la règle, fournissez une description, sélectionnez un type de terminal auquel s'applique la règle, puis cliquez sur **Suivant**.  
3. Pour configurer la logique de règle, ajoutez une ou plusieurs conditions IF à utiliser en tant que déclencheurs pour la règle.  
Vous pouvez ajouter des conditions sur des lignes parallèles afin de les appliquer en tant que conditions OR ou vous pouvez ajouter des conditions dans des colonnes séquentielles afin de les appliquer en tant que conditions AND.  
**Important :** Pour déclencher une condition qui compare deux propriétés ou pour déclencher au moins deux conditions de propriété combinées de manière séquentielle à l'aide de l'opérateur AND, les points de données de déclenchement doivent être inclus dans le même message de terminal. Si les données sont reçues dans plusieurs messages, la condition ou les conditions séquentielles ne se déclenchent pas.  
**Exemples :**   
Une règle simple peut déclencher une alerte si une valeur de paramètre est supérieure à une valeur spécifiée :
Condition = `temp_cpu>80`  
Une règle plus complexe peut être déclenchée lorsqu'une combinaison de seuils est atteinte :
Condition = `temp_cpu>60 AND cpu_load>90`   

4. Configurez les exigences de déclenchement conditionnel pour votre règle.  
Pour contrôler le nombre d'alertes qui sont déclenchées pour une règle pendant une période donnée, vous pouvez configurer des exigences de déclenchement conditionnel pour votre règle.  
**Important :** Le déclenchement conditionnel agit sur n'importe quelle condition dans la règle. Par exemple, si cinq conditions parallèles différentes sont définies sur une règle à l'aide de l'opérateur OR, chaque condition qui est remplie est décomptée du nombre de déclenchements conditionnels.
Pour définir un déclenchement conditionnel pour une règle :
 1. Dans l'éditeur de règles, cliquez sur le lien par défaut **Déclencher chaque fois que les conditions sont remplies** pour ouvrir la boîte de dialogue Définir une exigence de fréquence.
 2. Sélectionnez et configurez le déclencheur conditionnel que vous souhaitez utiliser dans la règle.
 <ul>
 <li>Déclencher chaque fois que les conditions sont remplies</li>
 <li>Déclencher si des conditions sont remplies N fois en M *unité de temps*</li>
 </ul>  
 Pour obtenir une description plus détaillée des déclencheurs conditionnels, voir [Déclenchement de règle conditionnel](#conditional "Vue d'ensemble du déclenchement conditionnel").
5. Créez ou sélectionnez une ou plusieurs actions qui se déclenchent si les conditions de règle sont remplies.  
Pour plus d'informations sur les actions, voir [Utilisation d'actions avec vos règles](#shared "Créer des actions").   
 Par exemple, une action peut être utilisée pour envoyer un courrier électronique ou poster un webhook.
3. **Facultatif :** Sélectionnez une priorité d'alerte pour la règle.  
 La priorité est utilisée pour classifier les alertes qui s'affichent dans le tableau **Analyse basée sur les règles**. La priorité par défaut est Low (faible).
6. Lorsque la règle vous convient, cliquez sur **Sauvegarder** pour sauvegarder la règle sans l'activer ou cliquez sur **Activer** pour sauvegarder la règle et l'activer.

Votre règle est créée. Si vous activez la règle, lorsque les conditions de la règle sont remplies, une alerte est ajoutée au tableau **Tableaux > Analyse basée sur des règles**, et toute action associée à la règle est exécutée.

## Déclenchement de règle conditionnel
{: #conditional}

Pour contrôler le nombre d'alertes qui sont déclenchées pour une règle pendant une période donnée, vous pouvez configurer des exigences de déclenchement conditionnel pour votre règle.

Selon la fréquence de message et les conditions de règle, une règle peut se déclencher de nombreuses fois dès lors qu'une condition de déclenchement est remplie. Par exemple, si la condition est `temp >= 90` et que la température augmente et se stabilise à 91, la règle se déclenche à chaque message entrant. Selon la fréquence des messages de terminal et les actions associées à la règle, votre boîte de réception de messagerie électronique peut se remplir rapidement d'alertes ou un flux Twitter peut être inondé de messages qui n'apportent rien de plus.

**Important :** Le déclenchement conditionnel agit sur n'importe quelle condition dans la règle. Par exemple, si cinq conditions parallèles différentes sont définies sur une règle à l'aide de l'opérateur OR, chaque condition qui est remplie est décomptée du nombre de déclenchements conditionnels.

Condition | Description
------------- | -------------
Déclencher chaque fois que les conditions sont remplies | La règle est déclenchée chaque fois que les conditions qui lui sont associées sont remplies.
Déclencher si des conditions sont remplies *N* fois en *M* *jours/heures/minutes/personnalisé* | La règle est déclenchée lorsque les conditions sont remplies *N* fois au cours de l'intervalle de temps sélectionné, puis elle n'est pas redéclenchée tant que le délai configuré n'est pas dépassé. </br>Exemple : Exigence de déclenchement conditionnel =`Déclencher une fois si les conditions sont remplies 4 fois en 30 minutes`. Le terminal envoie un nouveau message toutes les cinq minutes. A midi, la température dépasse 90 degrés et remplit ainsi la condition. Le compteur associé au déclenchement conditionnel est démarré mais la règle n'est pas encore déclenchée.  Au bout de 15 minutes et la réception de plus de trois messages indiquant `temp > 90`, la règle est déclenchée. Ensuite, la règle n'est pas déclenchée au cours des 15 minutes suivantes, quelle que soit la température.
Déclencher uniquement la première fois que les conditions sont remplies et réinitialiser lorsque les conditions ne sont plus remplies. | La règle est déclenchée lorsque les conditions sont remplies mais elle n'est pas déclenchée pour les messages consécutifs qui remplissent également les conditions. Les critères de déclenchement sont réinitialisés par le premier message qui ne remplit pas les conditions de règle.
Déclencher si les conditions persistent pour *M* *jours/heures/minutes/personnalisé*. | La règle est déclenchée après l'intervalle de temps sélectionné si tous les points de données reçus pendant l'intervalle de temps répondent aux conditions ou si aucun point de données supplémentaire n'est reçu. L'intervalle de temps commence lorsque les conditions sont initialement remplies.



## Utilisation d'actions dans vos règles
{: #shared}

Outre l'affichage d'alertes dans le tableau de bord des alertes, {{site.data.keyword.iot_short}} prend en charge plusieurs types d'actions déclenchées par des règles, tels que l'envoi de courriers électroniques et la publication de webhooks.

Vous pouvez créer des actions directement dans l'éditeur de règles ou vous pouvez créer les actions dans l'onglet Actions, puis sélectionner les actions lorsque vous créez vos règles.

Pour créer une action à partir de l'onglet Actions :
1. Dans le tableau de bord {{site.data.keyword.iot_short}}, accédez à **Règles**.
2. Dans le tableau de bord Règles, sélectionnez l'onglet **Actions**.
2. Cliquez sur **Créer une action**, attribuez un nom et une description à l'action et sélectionnez un type d'action, puis cliquez sur **Suivant**.
3. Définissez les paramètres obligatoires pour le type d'action que vous créez.  
Types d'action :  
 - [Envoyer un courrier électronique](#email "Envoyer un courrier électronique")
 - [IFTTT](#ifttt "IFTTT")
 - [Node-RED](#nodered "Node-RED")
 - [Webhook](#webhook "Webhook")
4. Cliquez sur **OK** pour créer la nouvelle action.

L'action est maintenant disponible dans l'éditeur de règles.

**Remarque :** Les exemples qui suivent représentent tous une action qui prévient un technicien de maintenance lorsque la température, représentée par la propriété `temp_cpu` d'un terminal, dépasse 80 degrés, à l'aide de la condition de règle suivante : `temp_cpu >= 80`

### Envoyer un courrier électronique  
{: #email}
Utilisez l'action Envoyer un courrier électronique pour envoyer un courrier électronique à un ou plusieurs destinataires lorsqu'une règle est déclenchée.

Exemple : [Envoyer un courrier électronique](#emailex).

Les paramètres suivants sont utilisés pour configurer l'action Envoyer un courrier électronique :

Paramètre | Description
---|---
Nom | Nom de l'action qui est utilisée dans le tableau de bord des alertes.
Description | Courte description de l'action.
Objet | Ligne d'objet du courrier électronique. La ligne objet par défaut est "IBM Watson IoT Alert: Mail action".
A | Vous pouvez choisir d'envoyer l'alerte à vous même uniquement ou à une liste d'adresses électroniques séparées par des virgules. Si vous choisissez d'envoyer l'alerte à vous même, le courrier électronique est envoyé à l'adresse électronique de l'instance {{site.data.keyword.iot_short}} à laquelle vous êtes connecté.
Cc | Néant, ou une  liste d'adresses électroniques séparées par des virgules.
Le corps du courrier électronique est créé automatiquement à partir du message du terminal au moment où la règle est déclenchée.  
**Important :** Par défaut, les courriers électroniques n'incluent pas de données de terminal susceptibles de contenir des informations sensibles. Modifiez le paramètre **Inclure des données** de manière à inclure des données de terminal.

#### Exemple : Utilisation de l'action Envoyer un courrier électronique
{: #emailex}

Dans cet exemple, l'action est configurée pour utiliser la fonction Envoyer un courrier électronique afin d'envoyer un courrier électronique au technicien de maintenance et un message de sauvegarde à son responsable.

Pour créer l'action Envoyer un courrier électronique :
1. Dans le tableau de bord {{site.data.keyword.iot_short}}, accédez à **Règles**.
2. Cliquez sur **Créer une action**.
4. Entrez le nom d'action `Envoyer un courrier électronique de demande de maintenance`.
5. Entrez la description `Envoyer un courrier électronique au technicien de maintenance et à son responsable`.
3. Sélectionnez le type **Courrier électronique**.
6. Dans la zone A, sélectionnez **Des personnes spécifiques** et entrez `service.engineer@company.com`.
7. Dans la zone Cc, sélectionnez **Des personnes spécifiques** et entrez `service.manager@company.com`.
8. Sur la ligne Objet, entrez `Demande de maintenance`.
10. Sélectionnez **Inclure des données** pour inclure les données de terminal dans le courrier électronique.
11. Cliquez sur **Terminer** pour sauvegarder l'action.  


### IFTTT  
{: #ifttt}

Utilisez l'action IFTTT pour déclencher une recette IFTTT lorsqu'une règle est déclenchée. Pour plus d'informations sur le déclenchement d'actions, telles que les recettes IFTTT, voir l'article [Maker Channel ![](../../icons/launch-glyph.svg)](https://ifttt.com/maker){: new_window} sur le site IFTTT. 

Exemple : [Utiliser IFTTT pour publier une carte Trello](#iftttex).

Les paramètres suivants sont utilisés pour configurer une action IFTTT :

Paramètre | Description
---|---
Nom | Nom de l'action qui est utilisée dans le tableau de bord des alertes.
Description | Courte description de l'action.
Clé | Clé Maker Channel à utiliser pour déclencher l'événement.
Evénement | Nom de l'événement que vous avez configuré comme déclencheur pour Maker Event. Vous pouvez créer plusieurs recettes avec différents déclencheurs, chacune portant un nom distinct.
Valeur 1-3 | Vous pouvez spécifier n'importe quel contenu dans ces paramètres, qui sont transmis à l'action dans votre recette IFTTT. **Astuce :** Vous pouvez utiliser une [substitution de variable](#variable_substitution) pour ajouter dynamiquement des données supplémentaires dans l'en-tête.

#### Exemple : Utilisation de IFTTT pour publier une carte Trello {: #iftttex}

Dans cet exemple, l'action est configurée pour utiliser un IFTTT afin de publier une carte sur votre liste de demandes de service sur Trello.

Pour créer l'action Publier une carte sur Trello :
1.	Dans IFTTT, connectez-vous au canal Trello.
2.	Dans IFTTT, connectez-vous au canal Maker. Notez la clé IFTTT. Vous avez besoin de cette information pour établir une connexion à IFTTT depuis {{site.data.keyword.iot_short_notm}}.
5.	Dans IFTTT, créez une recette :
 1. Cliquez sur **THIS**.
 2. Sélectionnez le canal **Maker**.  
 2. Cliquez sur **Recevoir une demande Web**.
 3. Entrez le nom d'événement `post-Trello-card`.
 4. Cliquez sur **THAT**.
 5. Sélectionnez le canal **Trello**.
 6. Sélectionnez la carte mère Trello dans laquelle créer la carte.
 7. Entrez le nom de la liste à laquelle ajouter les cartes.
 8. Editez le titre et la description.
 9. Affectez les membres @service.engineer et @service.manager.
 8. Cliquez sur **Créer une action**.   
3. Dans le tableau de bord {{site.data.keyword.iot_short}}, accédez à **Règles > Actions** et créez une nouvelle action dotée des paramètres suivants :
<ul>
<li>Type - **IFTTT**</li>
<li>Nom - `Publier une carte de demande de maintenance`</li>
<li>Description - `Utiliser IFTTT pour publier une carte dans la liste de demandes de maintenance sur Trello.`</li>
<li>Clé - Votre clé IFTTT</li>
<li>Evénement - `post-Trello-card`</li>
<li>Eventuellement, ajoutez des valeurs pour Value 1-3. **Astuce :** Vous pouvez utiliser une [substitution de variable](#variable_substitution) pour inclure dynamiquement des données de terminal.</li>
</ul>
4. Cliquez sur **OK** pour enregistrer l'action.


### Node-RED
{: #nodered}

Utilisez l'action Node-RED pour vous connecter à une application Node-RED lorsqu'une règle est déclenchée. Pour plus d'informations sur l'utilisation de Node-RED, voir [Création d'applications avec l'application Internet of Things Starter](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html).

Exemple : [Utiliser Node-RED pour envoyer un message texte](#noderedex).

Les paramètres suivants sont utilisés pour configurer une action Node-RED :

Paramètre | Description
---|---
Nom | Nom de l'action qui est utilisée dans le tableau de bord des alertes.
Description | Courte description de l'action.
URL | URL du noeud d'entrée HTTP Node-RED cible.
Nom d'utilisateur | A ajouter si cela est requis par le service Node-RED.
Mot de passe | A ajouter si cela est requis par le service Node-RED. **Important :** Le mot de passe est envoyé dans un texte en clair.
Corps | Par défaut, le corps du texte est prérempli avec toutes les variables répertoriées dans la [substitution de variable](#variable_substitution).

#### Exemple : Utilisation de Node-RED pour envoyer un message texte
{: #noderedex}

Dans cet exemple, l'action est configurée pour utiliser Node-Red avec un noeud Twilio afin d'envoyer un message texte au technicien de maintenance.

Pour créer l'action Envoyer un message texte :
1. Dans Twilio, localisez ou créez un nouveau service de messagerie à utiliser pour envoyer des messages texte depuis votre compte Twilio. Pour plus d'informations, voir la [documentation Twilio![](../../icons/launch-glyph.svg)](https://www.twilio.com/help){: new_window}.
2. Dans Bluemix, configurez votre compte Node-RED et connectez-vous à ce compte à l'aide de l'URL Node-RED `http://mynodered.mybluemix.net/red/`. Pour plus d'informations, voir la rubrique [Creating apps with Node-RED Starter](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html) dans la documentation Bluemix.
3. Dans Node-RED, créez un simple flux à deux noeuds, tel que [RTI-alert]->[SMS],  
où le premier noeud est un noeud HTTP et le second noeud est un noeud Twilio.
 1. Ajoutez le noeud d'entrée "http" et configurez-le à l'aide des attributs suivants :
  <ul>
  <li>Méthode - POST</li>
  <li>URL - `RTI-alert`</li>
  <li>Nom - Action RTI</li>
  </ul>
  2. Ajoutez un noeud de sortie "http response" et connectez celui-ci aux noeuds d'entrée "http" en faisant glisser le port de sortie de l'un de ces noeuds vers le port d'entrée de l'autre noeud.
  3. Ajoutez un noeud de sortie "twilio" et configurez-le à l'aide des attributs suivants :
  <ul>
  <li>Service - **Service externe**</li>
  <li>Twilio - Ajouter un nouvel élément twilio-api</li>
  <li>Envoyer un SMS à - `Numéro de téléphone du technicien de maintenance`</li>
  <li>Nom - **SMS**</li>
  </ul>
  4. Connectez les noeuds entre eux  
  Connectez les noeuds http et twilio entre eux en faisant glisser le port de sortie de l'un des noeuds vers le port d'entrée de l'autre noeud.
  5. Cliquez sur le bouton **Déployer** pour déployer le flux sur le serveur.
4. Dans le tableau de bord {{site.data.keyword.iot_short}}, accédez à **Règles > Actions** et créez une nouvelle action dotée des paramètres suivants :
 - Type - **Node-RED**
 - Nom - `Envoyer un texte à l'aide de Node-RED et Twilio`
 - Description - `Envoyer un message texte d'alerte au technicien de maintenance.`
 - URL - `http://mynodered.mybluemix.net/RTI-alert`
 - CORPS   
 ```json
 {"text":"*Un terminal nécessite votre attention*\n Heure : {{timestamp}}\n {{site.data.keyword.iot_short}} instance : {{tenantId}}\n Terminal : {{deviceId}}\n Règle : {{ruleName}}\n Description : {{ruleDescription}}\n Condition : {{ruleCondition}}\n Message de terminal brut : \n{{message}}"}
 ```  
5. Cliquez sur **Terminer** pour sauvegarder l'action.



### Webhook
{: #webhook}

Utilisez l'action Webhook pour envoyer une demande HTTP au service Web activé par Webhook lorsqu'une alerte est déclenchée. Par exemple, un Webhook peut être utilisé afin d'ouvrir une demande de service pour un actif si un détecteur présent dans le terminal signale une lecture incorrecte.

Example: [Utilisation d'un Webhook pour effectuer une publication sur Slack](#webhookex).

Les paramètres suivants sont utilisés pour configurer une action Webhook :

Paramètre | Description
---|---
Nom | Nom de l'action qui est utilisée dans le tableau de bord des alertes.
Description | Courte description de l'action.
URL | URL du serveur activé par un Webhook cible. **Astuce :** Vous pouvez utiliser une [substitution de variable](#variable_substitution) pour ajouter dynamiquement des données supplémentaires dans l'URL.
Méthode | Type d'appel Webhook à exécuter. Sélectionnez l'un des types suivants : GET, HEAD, OPTIONS, PATCH, PUT, POST ou DELETE.
Nom d'utilisateur | A ajouter si cela est requis par le service Web.
Mot de passe | A ajouter si cela est requis par le service Web. **Important :** Le mot de passe est envoyé dans un texte en clair.
En-tête | Les en-têtes se composent de paires de clés-valeurs. **Astuce :** Vous pouvez utiliser une [substitution de variable](#variable_substitution) pour ajouter dynamiquement des données supplémentaires dans l'en-tête.
Type de contenu | Type de contenu du corps : JSON, XML, texte codé d'URL de formulaire WWW ou texte en clair.  Disponible pour les méthodes OPTIONS, PATCH, PUT, POST et DELETE.
Corps | Corps de l'appel Webhook.  Disponible pour les méthodes OPTIONS, PATCH, PUT, POST et DELETE. Par défaut, le corps du texte est prérempli avec toutes les variables répertoriées dans la [substitution de variable](#variable_substitution). **Important :** Le serveur Webhook peut nécessiter que certaines zones soient inclues dans le corps. Par exemple, un Webhook Slack doit contenir la zone "text".   

#### Exemple : Utilisation d'un Webhook pour effectuer une publication sur Slack
{: #webhookex}

Dans cet exemple, l'action est configurée pour utiliser un Webhook afin de publier un message sur le canal Slack #service-requests.

Pour créer l'action de publication sur Slack :
1. Dans Slack, configurez l'intégration de Webhooks entrants pour le canal #service-requests. Notez l'URL des Webhooks. Pour plus d'informations, voir la [documentation Slack![](../../icons/launch-glyph.svg)](https://api.slack.com/incoming-webhooks){: new_window}.
2. Dans le tableau de bord {{site.data.keyword.iot_short}}, accédez à **Règles > Actions** et créez une nouvelle action dotée des paramètres suivants :
 - Nom - `Publier une demande de maintenance sur Slack`
 - Type - **Webhook**
 - URL - `URL des Webhooks Slack`
 - Méthode - **POST**
 - Type de contenu - `application/json`
 - Corps   
 ```json
 {"text":"*Un terminal nécessite votre attention*\n Heure : {{timestamp}}\n {{site.data.keyword.iot_short}} instance : {{tenantId}}\n Terminal : {{deviceId}}\n Règle : {{ruleName}}\n Description : {{ruleDescription}}\n Condition : {{ruleCondition}}\n Message de terminal brut : \n{{message}}"}
 ```  
  **Important :** Le Webhook Slack doit au moins contenir la zone "text". Pour plus d'informations, voir la rubrique [Incoming Webhooks ![](../icons/launch-glyph.svg)](https://api.slack.com/incoming-webhooks){: new_window} dans la documentation Slack.
11. Cliquez sur **Terminer** pour sauvegarder l'action.


### Substitution de variable  
{: #variable_substitution}

Ajoutez les substitutions de variable ci-après pour ajouter dynamiquement des données de terminal. La variable doit être placée entre accolades.

Variable | Description
---|---
**URL, en-tête et corps** |
`{{timestamp}}` | Horodatage du message.
`{{orgId}}` | Id organisation du service {{site.data.keyword.iot_short_notm}}.
`{{tenantId}}` | Obsolète : ID du service {{site.data.keyword.iotrtinsights_full}}.
`{{deviceId}}` | ID du terminal.
`{{ruleName}}` | Nom de la règle qui inclut l'action.
`{{ruleID}}` | ID de la règle qui inclut l'action.
**Corps uniquement** |
`{{ruleDescription}}`| Description de la règle qui inclut l'action.
`{{ruleCondition}}` | Condition de règle qui a déclenché l'action.
`{{message}}` | Message brut du terminal qui contenait la valeur de point de données ayant déclenché la règle.

## Recettes relatives à Cloud Analytics

Les recettes suivantes expliquent comment utiliser les fonctions Cloud Analytics pour différents scénarios d'utilisation :

- [Real Time Data Analysis Using IBM Watson™ IoT Platform Analytics ![](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/real-time-data-analysis-using-ibm-watson-iot-platform-analytics/){: new_window}

- [Predictive Analytics on IOT Sample Data ![](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/predictive-analytics-on-iot-sample-data/){: new_window}

- [Device List Card SIMPLIFIES Real Time Device Monitoring on WIoTP Dashboard ![](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/device-list-card-simplifies-real-time-device-monitoring-on-wiotp-dashboard/){: new_window}

- [Perform Actions in IBM Watson IoT Platform Cloud Analytics ![](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/perform-actions-in-ibm-watson-iot-platform-cloud-analytics/){: new_window}

- [Use IBM Data Science Experience to detect time series anomalies ![](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/use-ibm-data-science-experience-to-detect-time-series-anomalies/){: new_window}
