---

copyright:
 years: 2015, 2016

---

# A propos de Push Notifications
{: #overview-push}

Push Notifications est un service que vous pouvez utiliser pour envoyer des notifications à des périphériques iOS ou Android. Les notifications peuvent être ciblées vers tous les utilisateurs d'application ou vers un ensemble spécifique d'utilisateurs et de périphériques à l'aide de balises. Vous pouvez administrer les périphériques, les
balises et les abonnements. Vous pouvez aussi utiliser un logiciel SDK (kit de développement de logiciels) et des API REST (K) pour développer davantage vos
applications client. Pour plus d'informations sur le service dédié Push, voir [Services dédiés](../../dedicated/index.html). 


## Processus du service Push Notifications
{: #overview_push_process}

Les clients mobiles peuvent s'abonner et s'inscrire au service Push Notifications. Au démarrage, les applications mobiles s'inscrivent et
s'abonnent elles-mêmes au service Push Notifications. Les
notifications sont réparties sur le serveur du service de notifications Push Apple (APNs) ou Google Cloud Messaging, puis envoyées aux clients
mobiles inscrits.

![Présentation de Push](images/overview.jpg)


###Applications mobiles

Au démarrage, les applications mobiles s'inscrivent et s'abonnent elles-mêmes au service Push Notifications pour
recevoir des notifications.

###Applications de back end

Les applications de back end peuvent être sur site ou dans un cloud public. Les
applications de back end utilisent le service Push Notifications pour envoyer des
notifications qui dépendent
du contexte aux utilisateurs mobiles. Elles n'ont pas besoin d'assurer la maintenance et la gestion des périphériques mobiles et des
informations utilisateur pour l'envoi des notifications push. A la place, elle peuvent utiliser le service Push Notifications.

###Propriétaire d'application de back end

Il s'agit du rôle qui a créé l'application de back end mobile comportant une instance du service Push Notifications. Cette personne configure et définit le service Push Notifications pour
l'adapter aux applications de back end qui exploitent le service Push Notifications et
aux applications mobiles ciblées par les notifications push.

###Service Push Notification

Le service Push Notification gère toutes les informations liées aux périphériques qui s'enregistrent pour recevoir des notifications. Avec ce service, les détails de la technologie permettant d'envoyer des notifications à ces
plateformes mobiles hétérogènes restent transparents pour les applications.

###Passerelles

Il s'agit de services de cloud propres à une plateforme de périphérique mobile, comme Google Cloud Messaging (GCM) ou le service de notifications Push
Apple (APNs) que le service Push Notifications utilise pour envoyer des notifications aux applications mobiles.

## Types de notification Push
{: #overview-push-types}

###Diffusion

Lorsqu'une application mobile s'enregistre elle-même auprès du service Push Notifications, elle peut commencer à recevoir des diffusions. Les notifications de diffusion sont des messages de notification envoyés à tous les périphériques sur lesquels l'application est installée
et configurée pour le service Push Notifications. Les notifications de diffusion sont activées par défaut dans toute application activée pour les notifications push. Les applications activées pour le service Push Notifications possèdent un abonnement prédéfini à la balise Push.ALL qui est utilisée par le serveur pour diffuser des messages de notification à tous les périphériques. Pour envoyer une notification de diffusion qui utilise l'API REST Push, assurez-vous que la "cible" est un fichier
JSON vide lors de l'envoi à la ressource de message.

###Notifications basées sur les balises

Les notifications basées sur les balises sont des messages de notification qui sont envoyés à tous les périphériques abonnés à une balise
particulière. Elles permettent la segmentation des notifications en fonction de domaines ou de rubriques. Les destinataires des notifications peuvent
choisir de ne recevoir les notifications que si elles concernent un sujet ou une rubrique qui les intéresse. Par conséquent, les notifications en fonction d'une balise constituent un moyen de segmenter les destinataires. Cette fonction permet de définir des
balises, puis d'envoyer et de recevoir des messages en fonction des balises. Un message est ciblé pour les périphériques qui sont
abonnés à une balise particulière. Vous devez d'abord créer les balises pour l'application, configurer les abonnements aux balises, puis initier les
notifications en fonction d'une balise. Pour envoyer une notification en fonction d'une balise qui utilise l'API REST, vérifiez que les éléments
"tagNames" sont fournis lors de l'envoi à la ressource de message.

###Notifications Unicast

Les notifications Unicast sont des messages de notification qui sont envoyés à un périphérique spécifique. Elles ne requièrent pas de configuration supplémentaire et sont activées par défaut lorsque l'application est activée pour les notifications push. Pour envoyer une notification Unicast qui utilise l'API REST, veillez à ce que les ID de périphérique soient fournis lors de l'envoi à une ressource de message.

###Notifications en fonction de la plateforme

Les notifications peuvent être ciblées afin de viser une plateforme de périphérique
particulière. Par exemple, une notification peut être envoyée aux utilisateurs Android seulement. Pour envoyer une notification en fonction de la
plateforme qui utilise l'API REST, veillez à ce que les plateformes ciblées soient fournies lors de l'envoi à une ressource de message. Spécifiez les plateformes dans un tableau. Les plateformes prises en charge sont les suivantes :
* A (Apple)
* G (Google)
