---

copyright:
 years: 2015, 2016

---

# A propos de Push Notifications
{: #overview-push}
*Dernière mise à jour : 14 juin 2016*
{: .last-updated}

Push Notifications est un service que vous pouvez utiliser pour envoyer des notifications à des périphériques iOS ou Android. Les notifications peuvent être ciblées vers tous les utilisateurs d'application ou vers un ensemble spécifique d'utilisateurs et de périphériques à l'aide de balises. Vous pouvez administrer les périphériques, les
balises et les abonnements. Vous pouvez aussi utiliser un logiciel SDK (kit de développement de logiciels) et des API REST (K) pour développer davantage vos
applications client. 

La notification push est aussi disponible en tant que service Bluemix dédié. Pour plus d'informations sur le service dédié Push, voir [Services dédiés](../../dedicated/index.html). Notez que l'onglet de surveillance des notifications push n'affiche pas de données d'analyse.

Le service Notifications Push est maintenant activé pour OpenWhisk. Pour plus d'informations, voir [OpenWhisk](../../openwhisk/index.html).


## Processus du service Notifications push
{: #overview_push_process}

Les clients mobiles peuvent s'abonner et s'inscrire au service Notifications push. Au démarrage, les applications mobiles s'inscrivent et s'abonnent elles-mêmes au service Notifications Push. Les notifications sont expédiées vers le service APNS (Apple Push Notification Service) ou CGM (Google Cloud Messaging) puis envoyées aux clients mobiles enregistrés.

![Présentation de Push](images/overview.jpg)


###Applications mobiles

Au démarrage, les applications mobiles s'inscrivent et s'abonnent elles-mêmes au service Notifications push pour recevoir des notifications.

###Applications de back end

Les applications de back end peuvent être sur site ou dans un cloud public. Elles utilisent le service Notifications push pour envoyer des
notifications qui dépendent du contexte aux utilisateurs mobiles. Elles n'ont pas besoin d'assurer la maintenance et la gestion des périphériques mobiles et des
informations utilisateur pour l'envoi des notifications push. A la place, elles peuvent utiliser le service Notifications push.

###Propriétaire d'application de back end

Il s'agit du rôle qui a créé l'application de back end mobile comportant une instance du service Notifications push. Cette personne configure et définit le service Notifications push pour l'adapter aux applications de back end qui utilisent ce service et
aux applications mobiles ciblées par les notifications push

###Service Notifications push

Le service Notifications push gère toutes les informations liées aux périphériques qui s'enregistrent pour recevoir des notifications. Avec ce service, les détails de la technologie permettant d'envoyer des notifications à ces
plateformes mobiles hétérogènes restent transparents pour les applications.

###Passerelles

Il s'agit de services de cloud propres à une plateforme de périphérique mobile, comme CGM (Google Cloud Messaging (GCM) ou APNS (Apple Push Notification Service) utilisés par le service Notifications push pour envoyer des notifications aux applications mobiles.

## Types de notification Push
{: #overview-push-types}

###Diffusion

Quand une application mobile s'inscrit au service Notifications push, elle peut recevoir des diffusions. Les notifications de diffusion sont des messages de notification envoyés à tous les périphériques sur lesquels l'application est installée
et configurée pour le service Notifications Push. Les notifications de diffusion sont activées par défaut dans toute application activée pour les notifications push. Les applications activées pour le service Notifications push possèdent un abonnement prédéfini à l'étiquette Push.ALL, qui est utilisé par le serveur pour diffuser des messages de notification de diffusion à tous les périphériques. Pour envoyer une notification de diffusion qui utilise l'API REST Push, assurez-vous que la "cible" est un fichier
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

## Taille des messages de notification push
{: #push-message-size}

La taille d'un message de notification push dépend des médiateurs. 

###iOS

Pour iOS 8 et ultérieur, la taille maximale autorisée est de 2 kilo-octets. Le service des notifications push d'Apple n'envoie pas les notifications qui dépassent cette limite.

###Android

La plateforme Android n'impose aucune limite.
