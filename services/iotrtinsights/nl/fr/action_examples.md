---

Copyright :
  Années : 2015, 2016

---

{:shortdesc: .shortdesc}

# Exemples d'action

Les actions de type Envoyer un courrier électronique, IFTTT, Node-RED et Webhooks ouvrent tout un univers d'options permettant d'exécuter des tâches, qui évolue au gré de votre imagination et des connecteurs utilisés par les autres outils. Il s'agit par exemple, des actions permettant de publier des messages d'état de périphérique sur Slack, d'envoyer des messages texte au personnel de maintenance, de créer des demandes de maintenance de périphérique, etc.
{: shortdesc}

Tous les exemples suivants illustrent une action qui prévient un technicien de maintenance lorsque la température, représentée par le point de données temp d'un périphérique, dépasse 100 degrés, à l'aide de la condition de règle suivante :
`temp >= 100`


Vous pouvez déclencher un ou plusieurs des types d'action suivants lorsque la condition de règle se produit :   
 - [Envoyer un courrier électronique](#emailex "Envoyer un courrier électronique")
 - [Webhook](#webhookex "Webhook")
 - [Node-RED](#noderedex "Node-RED")
 - [IFTTT](#iftttex "IFTTT")

## Utilisation de l'action Envoyer un courrier électronique{: #emailex}
Dans cet exemple, l'action est configurée pour utiliser la fonction Envoyer un courrier électronique de Real-Time Insights afin d'envoyer un courrier électronique au technicien de maintenance et un message de sauvegarde à son responsable.

Pour créer l'action Envoyer un courrier électronique :
1. Dans Real-Time Insights, accédez à **Analyse > Actions**.
2. Cliquez sur **Ajouter une action**.
3. Sélectionnez le type **Envoyer un courrier électronique**.
4. Entrez le nom d'action `Envoyer un courrier électronique de demande de maintenance`.
5. Entrez la description `Envoyer un courrier électronique au technicien de maintenance et à son responsable`.
6. Dans la zone A, entrez `service.engineer@company.com`.
7. Dans la zone Cc, entrez `service.manager@company.com`.
8. Sur la ligne Objet, entrez `Demande de maintenance`.
9. Choisissez d'ajouter en préfixe "alerte {{site.data.keyword.iotrtinsights_short}}" pour préciser la provenance du courrier électronique.
10. Pour inclure les données de périphérique dans le courrier électronique, désélectionnez la case à cocher **Ne pas inclure les données de périphérique dans le message électronique**.
11. Cliquez sur **OK** pour enregistrer l'action.  




## Utiliser un Webhook pour effectuer une publication sur Slack {: #webhookex}

Dans cet exemple, l'action est configurée pour utiliser un Webhook afin de publier un message sur votre canal Slack #service-requests.

Pour créer l'action de publication sur Slack :
1. Dans Slack, configurez l'intégration de Webhooks entrants pour le canal #service-requests. Notez l'URL des Webhooks. Pour plus d'informations, voir la [documentation Slack](https://api.slack.com/incoming-webhooks).
2. Dans Real-Time Insights, accédez à **Analyse > Actions** et créez une nouvelle action dotée des paramètres suivants :
 - Type - **Webhook**
 - Nom - `Publier une demande de maintenance sur Slack`
 - URL - `URL des Webhooks Slack`
 - Méthode - **POST**
 - Type de contenu - application/json
 - Sélectionnez **Utiliser un corps de message personnalisé**
 - Corps  
 ```{"text":"*Un périphérique nécessite votre attention*\n Heure : {{timestamp}}\n Instance {{site.data.keyword.iotrtinsights_short}} : {{tenantId}}\n Périphérique : {{deviceId}}\n Règle : {{ruleName}}\n Description : {{ruleDescription}}\n Condition : {{ruleCondition}}\n Message de périphérique brut : \n{{message}}"}```
 {: codeblock}  
 **Important :** Le Webhook Slack doit au moins contenir la zone "text". Pour plus d'informations, voir la rubrique [Incoming Webhooks](https://api.slack.com/incoming-webhooks "documentation Slack") dans la documentation Slack. 
11. Cliquez sur **OK** pour enregistrer l'action.

## Utiliser Node-RED pour envoyer un message texte {: #noderedex}

Dans cet exemple, l'action est configurée pour utiliser Node-Red avec un noeud Twilio afin d'envoyer un message texte au technicien de maintenance.

Pour créer l'action Envoyer un message texte :
1. Dans Twilio, localisez ou créez un nouveau service de messagerie à utiliser pour envoyer des messages texte depuis votre compte Twilio. Pour plus d'informations, voir la [documentation Twilio](https://www.twilio.com/help).
1. Dans Bluemix, configurez votre compte Node-RED et connectez-vous à ce compte à l'aide de l'URL Node-RED `http://mynodered.mybluemix.net/red/`. Pour plus d'informations, voir la rubrique [Creating apps with Node-RED Starter](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html) dans la documentation Bluemix.
2. Dans Node-RED, créez un simple flux à deux noeuds, tel que [RTI-alert]->[SMS],
où le premier noeud est un noeud HTTP et le second noeud est un noeud Twilio.
 1. Ajoutez le noeud d'entrée "http" et configurez-le à l'aide des attributs suivants :
  <ul>
  <li>Méthode - POST</li>
  <li>URL - `RTI-alert`</li>
  <li>Nom - Action RTI</li>
  </ul>
  2. Ajoutez un noeud de sortie "http response" et connectez celui-ci au noeud d'entrée "http" en faisant glisser le port de sortie de l'un de ces noeuds vers le port d'entrée de l'autre noeud.
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
3. Dans {{site.data.keyword.iotrtinsights_short}}, accédez à **Analyse > Actions** et créez une action dotée des paramètres suivants :
 - Type - **Node-RED**
 - Nom - `Envoyer un texte à l'aide de Node-RED et Twilio`
 - Description - `Envoyer un message texte d'alerte au technicien de maintenance.`
 - URL - `http://mynodered.mybluemix.net/RTI-alert`
 - CORPS
```{"text":"*Un périphérique nécessite votre attention*\n Heure : {{timestamp}}\n Instance {{site.data.keyword.iotrtinsights_short}} : {{tenantId}}\n Périphérique : {{deviceId}}\n Règle : {{ruleName}}\n Description : {{ruleDescription}}\n Condition : {{ruleCondition}}\n Message de périphérique brut : \n{{message}}"}```
 {: codeblock}
4. Cliquez sur **OK** pour enregistrer l'action.

## Utiliser IFTTT pour publier une carte Trello {: #iftttex}

Dans cet exemple, nous configurons l'action pour qu'elle utilise IFTTT afin de publier une carte dans la liste de demandes de service sur Trello.

Pour créer l'action Publier une carte sur Trello :
1.	Dans IFTTT, connectez-vous au canal Trello.
2.	Dans IFTTT, connectez-vous au canal Maker. Notez la clé IFTTT. Vous avez besoin de cette information pour établir une connexion à IFTTT depuis Real-Time Insights.
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
3. Dans {{site.data.keyword.iotrtinsights_short}}, accédez à **Analyse > Actions** et créez une action dotée des paramètres suivants :
<ul>
<li>Type - **IFTTT**</li>
<li>Nom - `Publier une carte de demande de maintenance`</li>
<li>Description - `Utiliser IFTTT pour publier une carte dans la liste de demandes de maintenance sur Trello.`</li>
<li>Clé - Votre clé IFTTT</li>
<li>Evénement - `post-Trello-card`</li>
<li>Vous pouvez, si vous le souhaitez, ajouter des valeurs pour les valeur 1 à 3. **Astuce :** Vous pouvez utiliser une [substitution de variable](actions.html#variable_substitution) pour inclure les données de périphérique de façon dynamique. </li>
</ul>
4. Cliquez sur **OK** pour enregistrer l'action.
