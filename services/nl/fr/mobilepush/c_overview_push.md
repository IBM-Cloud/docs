---

copyright:
 years: 2015, 2016

---

# A propos de {{site.data.keyword.mobilepushshort}}
{: #overview-push}
Dernière mise à jour : 16 août 2016
{: .last-updated}

IBM {{site.data.keyword.mobilepushshort}} est un service que vous pouvez utiliser pour envoyer des notifications vers des périphériques iOS et Android. Les notifications peuvent être ciblées vers tous les utilisateurs d'application ou vers un ensemble spécifique d'utilisateurs et de périphériques à l'aide de balises. Vous pouvez administrer les périphériques, les
balises et les abonnements. Vous pouvez aussi utiliser un logiciel SDK (kit de développement de logiciels) et des API REST (K) pour développer davantage vos
applications client. 

{{site.data.keyword.mobilepushshort}} est aussi disponible en tant que service Bluemix dédié. Pour plus d'informations sur le service dédié {{site.data.keyword.mobilepushshort}}, voir [Services dédiés](../../dedicated/index.html). Notez que l'onglet de surveillance {{site.data.keyword.mobilepushshort}} n'affiche pas de données d'analyse.

Le service {{site.data.keyword.mobilepushshort}}  est maintenant activé pour OpenWhisk. Pour plus d'informations, voir [OpenWhisk](../../openwhisk/index.html).


## Processus du service {{site.data.keyword.mobilepushshort}}
{: #overview_push_process}

Les clients mobiles peuvent s'abonner et s'inscrire au service {{site.data.keyword.mobilepushshort}}. Au démarrage, les applications mobiles s'inscrivent et s'abonnent elles-mêmes au service {{site.data.keyword.mobilepushshort}}. Les
notifications sont réparties sur le serveur du service de notifications Push Apple (APNs) ou Google Cloud Messaging, puis envoyées aux clients
mobiles inscrits.

![Présentation de Push](images/overview.jpg)


###Applications mobiles
{: mobile-applications}

Au démarrage, les applications mobiles s'inscrivent et s'abonnent elles-mêmes au service {{site.data.keyword.mobilepushshort}} pour
recevoir des notifications.

###Applications de back end
{: backend-applications}

Les applications de back end peuvent se trouver sur site ou dans un cloud public. Elles utilisent le service {{site.data.keyword.mobilepushshort}} pour envoyer des notifications qui dépendent du contexte aux utilisateurs mobiles. Elles n'ont pas besoin d'assurer la maintenance et la gestion des périphériques mobiles et des informations utilisateur pour l'envoi des notifications push. Au lieu de cela, les applications peuvent utiliser le service {{site.data.keyword.mobilepushshort}}.

###Propriétaire de l'application de back end
{: app-backend-owner}

Le propriétaire de l'application de back end crée l'application de back end qui comporte une instance du service {{site.data.keyword.mobilepushshort}}. Il configure et paramètre aussi le service {{site.data.keyword.mobilepushshort}} pour l'adapter aux applications de back end en l'utilisant en même temps que les applications mobiles qui sont la cible pour {{site.data.keyword.mobilepushshort}}.

###Service {{site.data.keyword.mobilepushshort}}
{: push-notification-service}

Le service {{site.data.keyword.mobilepushshort}} gère les informations relatives aux périphériques qui sont enregistrés pour les notifications. Avec ce service, les détails de la technologie permettant d'envoyer des notifications à ces
plateformes mobiles hétérogènes restent transparents pour les applications.

###Passerelles
{: gateways}

Il s'agit de services de cloud propres à une plateforme de périphérique mobile, comme CGM (Google Cloud Messaging (GCM) ou APNS (Apple Push Notification Service) utilisés par le service {{site.data.keyword.mobilepushshort}} pour envoyer des notifications aux applications mobiles.

###Sécurité Push
{: push-security}

Les interfaces API {{site.data.keyword.mobilepushshort}} sont sécurisées par deux types de valeurs confidentielles : i) appSecret ii) clientSecret. La valeur appSecret protège les interfaces API qui sont typiquement invoquées par des applications de backend (API d'envoi de {{site.data.keyword.mobilepushshort}}, API de configuration de paramètres, par exemple). La valeur clientSecret protège les API qui sont généralement invoquées par des applications client mobiles. A l'heure actuelle, il n'existe qu'une seule API relative à l'enregistrement d'un périphérique dotée d'un ID utilisateur associé qui requiert cette valeur confidentielle clientSecret. Toutes les autres interfaces API invoquées depuis des clients mobiles n'ont pas besoin de clientSecret. Les valeurs appSecret et clientSecret sont allouées à chaque instance de service au moment de la liaison d'une application au service {{site.data.keyword.mobilepushshort}}. Référez-vous à la documentation de l'API ReST pour plus d'informations sur la façon dont les valeurs confidentielles sont passées et pour quelles API.

## Types {{site.data.keyword.mobilepushshort}}
{: #overview-push-types}

###Diffusion
{: broadcast}

Quand une application mobile s'enregistre auprès du service {{site.data.keyword.mobilepushshort}}, elle peut commencer à recevoir des diffusions. Les notifications de diffusion sont des messages ciblés vers tous les périphériques qui ont une application installée et configurée pour le service {{site.data.keyword.mobilepushshort}} ; elles sont activées par défaut dans toute application activée pour {{site.data.keyword.mobilepushshort}}. Les applications activées pour le service {{site.data.keyword.mobilepushshort}} possèdent un abonnement prédéfini à la balise Push.ALL, qui est utilisé par le serveur pour diffuser des messages de notification de diffusion à tous les périphériques. Pour envoyer une notification de diffusion qui utilise l'API REST Push, assurez-vous que la "cible" est un fichier
JSON vide lors de l'envoi à la ressource de message.

###Notifications basées sur les balises
{: tag-based-notifications}

Les notifications basées sur les balises sont des messages qui sont ciblés vers tous les périphériques abonnés à une balise
particulière. Elles permettent la segmentation des notifications en fonction de domaines ou de rubriques. Les destinataires des notifications peuvent
choisir de ne recevoir les notifications que si elles concernent un sujet ou une rubrique qui les intéresse. Par conséquent, les notifications en fonction d'une balise constituent un moyen de segmenter les destinataires. Cette fonction permet de définir des
balises, puis d'envoyer et de recevoir des messages en fonction des balises. Un message est ciblé pour les périphériques qui sont
abonnés à une balise particulière. Vous devez d'abord créer des balises pour l'application, configurer les abonnements aux balises puis initier les
notifications basées sur une balise. Pour envoyer une notification basée sur une balise qui utilise l'API REST, vérifiez que les éléments
"tagNames" sont fournis lors de l'envoi à la ressource de message.

###Notifications Unicast
{: unicast-notifications}

Les notifications Unicast sont des messages qui sont envoyés à un périphérique ou utilisateur spécifique. Elles ne requièrent pas de configuration supplémentaire et sont activées par défaut quand l'application est activée pour {{site.data.keyword.mobilepushshort}}.

Toutefois, les notifications Unicast ciblées vers des utilisateurs nécessitent les opérations suivantes :

- L'association d'un ID utilisateur à un périphérique au moment de l'enregistrement du périphérique mobile pour les notifications push.  

- L'autorisation de l'enregistrement de cet ID utilisateur en passant une valeur confidentielle clientSecret qui est allouée lors de la liaison d'une application de back end au service {{site.data.keyword.mobilepushshort}}. 

En général, une application mobile exécutera d'abord un cycle d'authentification au cours duquel l'utilisateur d'application mobile est authentifié auprès d'un service d'authentification comme [Mobile Client Access](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html). Si l'authentification aboutit, l'ID de l'utilisateur authentifié est transféré vers l'API d'enregistrement de périphérique Push en même temps qu'une valeur confidentielle clientSecret. La présence de cette valeur a pour effet que seules les associations autorisées entre les ID utilisateur et les enregistrements de périphériques mobiles sont appliquées.
Pour envoyer une notifications Unicast via une API REST, veillez à ce que les ID de périphérique ou d'utilisateur soient fournis lors de l'envoi à une ressource de message.

###Notifications en fonction de la plateforme
{: platform-based-notifications}

Les notifications peuvent être ciblées afin de viser une plateforme de périphérique
particulière. Par exemple, une notification peut être envoyée aux utilisateurs Android seulement. Pour envoyer une notification en fonction de la
plateforme qui utilise l'API REST, veillez à ce que les plateformes ciblées soient fournies lors de l'envoi à une ressource de message. Spécifiez les plateformes dans un tableau. Les plateformes prises en charge sont les suivantes :
* A (Apple)
* G (Google)

## Taille des messages de type {{site.data.keyword.mobilepushshort}}
{: #push-message-size}

La taille d'un message de type {{site.data.keyword.mobilepushshort}} dépend des médiateurs. 

###iOS
{: ios-message-size}

Pour iOS 8 et ultérieur, la taille maximale autorisée est de 2 kilo-octets. Le service des notifications push d'Apple n'envoie pas les notifications qui dépassent cette limite.

###Android
{: android-message-size}

La plateforme Android n'impose aucune limite.
