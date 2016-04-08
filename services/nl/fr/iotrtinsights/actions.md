---

Copyright :
  Années : 2015, 2016

---

{:shortdesc: .shortdesc}

# Types d'action{: #actions}

Outre l'affichage d'alertes dans le tableau de bord des alertes, {{site.data.keyword.iotrtinsights_short}} prend en charge plusieurs types d'actions déclenchées par des règles, tels que l'envoi de courriers électroniques et l'envoi de webhooks.
{: shortdesc}

## Création d'actions{: #shared}
Vous pouvez [créer les actions directement à partir de l'éditeur de règles](rules.html "créer des règles") ou vous pouvez créer les actions dans le panneau Actions, puis sélectionner les actions lorsque vous créez vos règles. 

Pour créer une action à partir du panneau Actions :
1. Dans la console {{site.data.keyword.iotrtinsights_short}}, accédez à **Analyse > Actions**.
2. Cliquez sur **Ajouter une action**, sélectionnez un type d'action, attribuez un nom à l'action et indiquez une description.
3. Définissez les paramètres obligatoires pour le type d'action que vous créez.
Types d'action :  
 - [Envoyer un courrier électronique](#email "Envoyer un courrier électronique")
 - [Webhook](#webhook "Webhook")
 - [Node-RED](#nodered "Node-RED")
 - [IFTTT](#ifttt "IFTTT")
4. Cliquez sur **OK** pour créer la nouvelle action.

Cette action est maintenant disponible dans l'[éditeur de règles](rules.html#rules "éditeur de règles").



## Envoyer un courrier électronique {: #email}
Utilisez l'action Envoyer un courrier électronique pour envoyer un courrier électronique à un ou plusieurs destinataires lorsqu'une règle est déclenchée.

Exemple : [Envoyer un courrier électronique](action_examples.html#emailex).

Les paramètres suivants sont utilisés pour configurer l'action Envoyer un courrier électronique :

Paramètre | Description
---|---
Nom | Nom de l'action qui est utilisée dans le tableau de bord des alertes.
Description | Courte description de l'action.
A | Une ou plusieurs adresses électroniques, séparées par des virgules.
Cc | Une ou plusieurs adresses électroniques, séparées par des virgules.
Objet | Ligne d'objet du courrier électronique. Vous pouvez, si vous le souhaitez, faire commencer automatiquement l'objet par "IoT Real-Time Insight alert".
Le corps du courrier électronique est créé automatiquement à partir du message du périphérique au moment de la règle est déclenchée.  
**Important :** Si les données de périphérique contiennent des informations sensibles, vous pouvez choisir de ne pas les inclure dans le message électronique et de les afficher uniquement dans le panneau des alertes. 


## Webhook {: #webhook}
Utilisez l'action Webhook pour envoyer une demande HTTP au service Web activé par Webhook lorsqu'une alerte est déclenchée. Par exemple, un Webhook peut être utilisé afin d'ouvrir une demande de service pour un actif si un détecteur présent dans le périphérique signale une lecture incorrecte. 

Example: [Utiliser un Webhook pour effectuer une publication sur Slack](action_examples.html#webhookex).

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
Type de contenu | Type de contenu du corps : JSON, XML, texte codé d'URL de formulaire WWW ou texte en clair. Disponible pour les méthodes OPTIONS, PATCH, PUT, POST et DELETE.
Corps | Corps de l'appel Webhook. Disponible pour les méthodes OPTIONS, PATCH, PUT, POST et DELETE. Par défaut, le corps du texte est prérempli avec toutes les variables répertoriées dans la [substitution de variable](#variable_substitution). Sélectionnez **Utiliser un corps de message personnalisé** pour éditer le contenu du corps du texte. **Important :** Le serveur Webhook peut nécessiter que certaines zones soient inclues dans le corps. Par exemple, un Webhook Slack doit contenir la zone "text".    



## Node-RED{: #nodered}
Utilisez l'action Node-RED pour vous connecter à une application Node-RED lorsqu'une règle est déclenchée. Pour plus d'informations sur l'utilisation de Node-RED, voir [Création d'applications avec l'application Internet of Things Starter](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html#iot500).

Exemple : [Utiliser Node-RED pour envoyer un message texte](action_examples.html#noderedex).

Les paramètres suivants sont utilisés pour configurer une action Node-RED :

Paramètre | Description
---|---
Nom | Nom de l'action qui est utilisée dans le tableau de bord des alertes.
Description | Courte description de l'action.
URL | URL du noeud d'entrée HTTP Node-RED cible.
Nom d'utilisateur | A ajouter si cela est requis par le service Node-RED.
Mot de passe | A ajouter si cela est requis par le service Node-RED. **Important :** Le mot de passe est envoyé dans un texte en clair.
Corps | Par défaut, le corps du texte est prérempli avec toutes les variables répertoriées dans la [substitution de variable](#variable_substitution). Sélectionnez **Utiliser un corps de message personnalisé** pour éditer le contenu du corps du texte.

## IFTTT {: #ifttt}
Utilisez l'action IFTTT pour déclencher une recette IFTTT lorsqu'une règle est déclenchée. Pour plus d'informations sur le déclenchement d'actions Real-Time Insights, telles que les recettes IFTTT, voir l'article [Maker Channel](https://ifttt.com/maker) sur le site IFTTT. 

Exemple : [Utiliser IFTTT pour publier une carte Trello](action_examples.html#iftttex).

Les paramètres suivants sont utilisés pour configurer une action IFTTT :

Paramètre | Description
---|---
Nom | Nom de l'action qui est utilisée dans le tableau de bord des alertes.
Description | Courte description de l'action.
Clé | Clé Maker Channel à utiliser pour déclencher l'événement.
Evénement | Nom de l'événement que vous avez configuré comme déclencheur pour Maker Event. Vous pouvez créer plusieurs recettes avec différents déclencheurs, chacune portant un nom distinct.
Valeur 1-3 | Vous pouvez spécifier n'importe quel contenu dans ces paramètres, qui sont transmis à l'action dans votre règle IFTTT.. **Astuce :** Vous pouvez utiliser une [substitution de variable](#variable_substitution) pour ajouter dynamiquement des données supplémentaires dans l'en-tête.

## Substitution de variable{: #variable_substitution}
Ajoutez les substitutions de variable ci-après pour ajouter dynamiquement des données de périphérique. La variable doit être placée entre accolades. 

Variable | Description
---|---
**URL, en-tête et corps** |
`{{timestamp}}` | Horodatage du message
`{{tenantId}}` | ID du service Real-Time Insights
`{{deviceId}}` | ID du périphérique
`{{ruleName}}` | Nom de la règle qui inclut l'action **Corps uniquement** |
`{{ruleDescription}}`| Description de la règle qui contient l'action
`{{ruleCondition}}` | Condition de règle qui a déclenché l'action
`{{message}}` | Message brut du périphérique contenant la valeur de point de données qui a déclenché la règle
