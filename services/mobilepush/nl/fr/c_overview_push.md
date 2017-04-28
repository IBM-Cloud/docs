---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Service de notification push
{: #overview-push}
Dernière mise à jour : 31 mars 2017
{: .last-updated}

IBM {{site.data.keyword.mobilepushshort}} est un service que vous pouvez utiliser pour envoyer des notifications à des appareils et des plateformes. Les notifications peuvent être ciblées vers tous les utilisateurs d'application ou vers un ensemble spécifique d'utilisateurs et d'appareils à l'aide de balises. Vous pouvez administrer les appareils, les balises et les abonnements.  

Vous pouvez utiliser l'une des options suivantes pour créer un service lié ou non lié :

- En créant une application Bluemix à l'aide du conteneur boilerplate de MobileFirst Services Starter du catalogue. Ceci crée un service Push
Notifications lié à une application dorsale Bluemix.
- En créant directement depuis le catalogue Mobile un service Push Notifications non lié. Vous pouvez le lier par la suite à une
application ou même opter de l'utiliser comme service non lié. 
- En utilisant le [Tableau de bord Mobile ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.ng.bluemix.net/docs/mobile/services.html){: new_window}.

Notez que l'onglet de surveillance {{site.data.keyword.mobilepushshort}} n'affiche pas de données d'analyse.

Le service {{site.data.keyword.mobilepushshort}}  est maintenant activé pour OpenWhisk. Pour plus d'informations, voir [OpenWhisk](/docs/openwhisk/index.html).


## Processus du service de notification push
{: #overview_push_process}

Les clients mobiles et de navigateurs Web et les applications et extensions Google Chrome peuvent souscrire au service {{site.data.keyword.mobilepushshort}} et s'y enregistrer. Au démarrage, les applications client s'inscrivent et s'abonnent elles-mêmes au service {{site.data.keyword.mobilepushshort}}. Les notifications sont réparties sur le serveur APNS (Apple Push Notification service) ou FCM (Firebase Cloud Messaging)/Google Cloud Messaging (GCM) puis envoyées aux clients de navigateur ou appareils mobiles enregistrés.

![Présentation de Push](images/overview.jpg)


### Applications mobiles et applications de navigateur
{: #mobile-applications}

Au démarrage, les applications client s'inscrivent et s'abonnent elles-mêmes au service {{site.data.keyword.mobilepushshort}} pour recevoir des notifications.

### Applications de back end
{: #backend-applications}

Les applications de back end peuvent se trouver sur site ou dans un cloud public. Elles utilisent le service {{site.data.keyword.mobilepushshort}} pour envoyer des notifications qui dépendent du contexte aux utilisateurs d'applications mobiles et d'applications de navigateur. Elles n'ont pas besoin d'assurer la maintenance et la gestion des appareils mobiles, des agents de navigateur et des informations utilisateur pour l'envoi des notifications push. Au lieu de cela, les applications peuvent utiliser le service {{site.data.keyword.mobilepushshort}} qui se chargera des ces opérations.

### Propriétaire de l'application de back end
{: #app-backend-owner}

Le propriétaire de l'application de back end crée l'application de back end qui comporte une instance du service {{site.data.keyword.mobilepushshort}}. Il configure et paramètre aussi le service {{site.data.keyword.mobilepushshort}} pour l'adapter aux applications de back end en l'utilisant en même temps que les applications mobiles et les applications de navigateur définies comme cible pour {{site.data.keyword.mobilepushshort}}.

### Service de notification push
{: #push-notification-service}

Le service {{site.data.keyword.mobilepushshort}} gère les informations relatives aux appareils mobiles et aux clients de navigateur Web qui sont enregistrés pour les notifications. Avec ce service, les détails de la technologie permettant d'envoyer des notifications à ces plateformes mobiles et de navigateur Web hétérogènes restent transparents pour les applications.

### Passerelles
{: #gateways}

Il s'agit de services de cloud de notifications push spécifiques aux plateformes, comme FCM/GCM ou APNS (Apple Push Notification service), qui sont utilisés par le service IBM {{site.data.keyword.mobilepushshort}} pour envoyer des notifications aux applications mobiles et aux applications de navigateur.

### Sécurité push
{: #push-security}

Les API {{site.data.keyword.mobilepushshort}} sont sécurisées par deux types de valeur confidentielle :

- **appSecret** : `appSecret` protège les API qui sont généralement appelées par des applications de back end (telles que l'API d'envoi de {{site.data.keyword.mobilepushshort}}  et l'API de configuration des paramètres).
- **clientSecret** : `clientSecret` protège les API généralement appelées par des applications de client mobile. Il n'y a qu'une seule API relative à l'enregistrement d'un appareil avec un ID utilisateur associé qui nécessite cette valeur confidentielle `clientSecret`. Aucune des autres API invoquées depuis les clients mobiles n'ont besoin de `clientSecret`. 

Les valeurs `appSecret` et `clientSecret` sont allouées à chaque instance de service au moment de la liaison d'une application au service {{site.data.keyword.mobilepushshort}}. Reportez-vous à la documentation des [API REST ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://mobile.{DomainName}/imfpush/) pour plus d'informations sur la transmission des valeurs confidentielles et pour quelles API.

**Remarque** : Les applications plus anciennes ne devaient transmettre le clientSecret que lors de l'enregistrement ou de la mise à jour
d'appareils avec la zone userId. Toutes les autres interfaces API invoquées par des clients mobiles et de navigateur n'avaient pas besoin de clientSecret. Toutes ces anciennes applications peuvent continuer à se servir facultativement de clientSecret pour les enregistrements d'appareil ou la mise à jour des appels. Il est toutefois vivement conseillé d'appliquer une vérification clientSecret pour tous les appels d'API client. Pour mettre en oeuvre ce processus dans les applications existantes, une nouvelle API, `verifyClientSecret`, a été publiée. Pour les nouvelles applications, la vérification clientSecret sera mise en oeuvre sur tous les appels d'API client et ce comportement ne peut être modifié avec l'API `verfiyClientSecret`.

Par défaut, la vérification de la valeur confidentielle n'est appliquée que dans les nouvelles applications, mais aussi bien les applications existantes que les applications nouvelles sont autorisées à activer ou désactiver cette vérification en utilisant l'API REST verifyClientSecret. Il est conseillé d'imposer la vérification de la valeur confidentielle pour éviter d'exposer des appareils à des utilisateurs qui pourraient avoir connaissance des valeurs applicationId et deviceId.

Prenez soin de préserver la confidentialité de clientSecret `clientSecret` et ne procédez jamais à un codage en dur dans l'application mobile. Il existe différents modèles d'initialisation d'application qui peuvent être utilisés pour extraire dynamiquement la valeur confidentielle `clientSecret` durant l'exécution de l'application. Le diagramme de séquence décrit ce modèle possible.
![Enable_Push](images/init_client_secret.jpg) 

## Types de notification push
{: #overview-push-types}

### Diffusion
{: #broadcast}

Quand une application client s'enregistre auprès du service {{site.data.keyword.mobilepushshort}}, elle peut commencer à recevoir des diffusions. Les notifications de diffusion sont des messages ciblés vers toutes les instances d'une application installée sur des appareils mobiles et des navigateurs ou implémentée en tant qu'application ou instance d'application Chrome et configurée pour le service {{site.data.keyword.mobilepushshort}} ; elles sont activées par défaut dans toute application activée pour {{site.data.keyword.mobilepushshort}}. Les applications activées pour le service {{site.data.keyword.mobilepushshort}} possèdent un abonnement prédéfini à la balise Push.ALL, qui est utilisé par le serveur pour diffuser des messages de notification de diffusion à tous les appareils. Pour envoyer une notification de diffusion qui utilise l'API REST Push, assurez-vous que la "cible" est un fichier JSON vide lors de l'envoi à la ressource de message.

### Notifications basées sur les balises
{: #tag-based-notifications}

Les notifications basées sur les balises sont des messages qui sont ciblés vers tous les appareils abonnés à une balise particulière. Elles permettent la segmentation des notifications en fonction de domaines ou de rubriques. Les destinataires des notifications peuvent choisir de ne recevoir les notifications que si elles concernent un sujet ou une rubrique qui les intéresse. Par conséquent, les notifications en fonction d'une balise constituent un moyen de segmenter les destinataires. Cette fonction permet de définir des balises, puis d'envoyer et de recevoir des messages en fonction des balises. Un message n'est ciblé que vers les instances d'application client (sur un appareil mobile, un navigateur ou une extension) qui sont abonnées à la balise. Vous devez d'abord créer des balises pour l'application, configurer les abonnements aux balises puis initier les notifications basées sur une balise. Pour envoyer une notification basée sur une balise qui utilise l'API REST, vérifiez que les éléments "tagNames" sont fournis lors de l'envoi à la ressource de message.

### Notifications Unicast
{: #unicast-notifications}

Les notifications Unicast sont des messages qui sont envoyés à un appareil ou utilisateur spécifique. Elles ne requièrent pas de configuration supplémentaire et sont activées par défaut quand l'application est activée pour {{site.data.keyword.mobilepushshort}}.

Toutefois, les notifications Unicast ciblées vers des utilisateurs nécessitent l'association d'un ID utilisateur à un appareil au moment de l'enregistrement de l'appareil mobile client, du navigateur Web ou des applications et extensions Chrome pour {{site.data.keyword.mobilepushshort}}.   

En général, une application client exécute d'abord un cycle d'authentification au cours duquel l'utilisateur d'application mobile est authentifié auprès d'un service d'authentification comme [Mobile Client Access](docs/services/mobileaccess/index.html). Si l'authentification aboutit, l'ID de l'utilisateur authentifié est transféré vers l'API d'enregistrement d'appareil Push. 
Pour envoyer une notifications Unicast via une API REST, veillez à ce que les ID d'appareil ou d'utilisateur soient fournis lors de l'envoi à une ressource de message.

### Notifications en fonction de la plateforme
{: #platform-based-notifications}

Les notifications peuvent être ciblées afin de viser une plateforme d'appareil particulière. Ainsi, une notification peut être envoyée uniquement aux utilisateurs Android ou aux utilisateurs Google Chrome. Pour envoyer une notification en fonction de la plateforme qui utilise l'API REST, veillez à ce que les plateformes ciblées soient fournies lors de l'envoi à une ressource de message. Spécifiez les plateformes dans un tableau. Les plateformes prises en charge sont les suivantes :
* A (Apple)
* G (Google)
* WEB_CHROME (Web Push navigateur Google Chrome)
* WEB_FIREFOX (Web Push navigateur Mozilla Firefox)
* WEB_SAFARI (Web Push navigateur Safari)
* APPEXT_CHROME (Applications et extensions Google Chrome)

## Taille des messages de notification push
{: #push-message-size}

La taille d'un message de type {{site.data.keyword.mobilepushshort}} dépend des contraintes imposées par les passerelles (FCM/GCM, APNS) et les plateformes client. 

### iOS et Safari
{: #ios-message-size}

Pour iOS 8 et ultérieur, la taille maximale autorisée est de 2 kilo-octets. Le service des notifications push d'Apple n'envoie pas les notifications qui dépassent cette limite.

### Android, navigateur Firefox, navigateur Chrome et Applications et extensions Chrome
{: #android-message-size}

La taille de la charge maximale autorisée pour les messages est de 4 kilo-octets.  
