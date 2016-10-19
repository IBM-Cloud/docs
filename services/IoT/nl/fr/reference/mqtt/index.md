---

copyright :
  années : 2015, 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Messagerie MQTT
{: #ref-mqtt}
Dernière mise à jour : 13 septembre 2016
{: .last-updated}

MQTT est le principal protocole utilisé par les terminaux et les applications pour communiquer avec {{site.data.keyword.iot_full}}. MQTT est un protocole de transport de messagerie de publication et d'abonnement conçu pour optimiser les échanges de données en temps réel entre le capteur et les terminaux mobiles.
{:shortdesc}

MQTT s'exécute sur TCP/IP, et bien qu'il soit possible d'effectuer directement un codage pour TCP/IP, vous pouvez également choisir d'utiliser une bibliothèque qui traite pour vous les détails du protocole MQTT. Une vaste gamme de bibliothèques client MQTT est disponible. IBM contribue au développement et au support de plusieurs bibliothèques client, y compris celles qui ne sont pas disponibles au niveau des sites suivants : 

- [Wiki de communauté MQTT](https://github.com/mqtt/mqtt.github.io/wiki)
- [Projet Eclipse Paho](http://eclipse.org/paho/)

## Support de version
{: #version-support}

{{site.data.keyword.iot_short_notm}} prend en charge les versions suivantes du protocole de messagerie MQTT :

Version MQTT | Ecarts | Notes
--- | --- | ---
[3.1.1](https://www.oasis-open.org/standards#mqttv3.1.1) (recommandé) | Les messages conservés ne sont pas pris en charge, par exemple, les abonnements partagés.  | <ul><li>Norme  OASIS.<li>Norme ISO (ISO/IEC PRF 20922) <li>Interopérabilité améliorée entre plusieurs clients et serveurs en raison d'une définition plus précise du protocole par rapport à la version 3.1. <li>La longueur maximale de l'identificateur de client MQTT (CientId) passe de 23 caractères (nombre imposé par la version 3.1) à 256 caractères. </br>Le service {{site.data.keyword.iot_short_notm}} requiert souvent des ID de client (ClientId) plus longs. </br>Les ID de client développés sont pris en charge quelle que soit la version du protocole MQTT, toutefois, certaines bibliothèques client de la version 3.1 vérifient la longueur de la valeur ClientId et imposent un nombre limite de caractères égal à 23. </ul>
3.1 | - | MQTT V3.1 est la version du protocole la plus utilisée.

{{site.data.keyword.iot_short_notm}} prend en charge tout contenu autorisé par la norme MQTT. MQTT est indépendant des données, par conséquent, il est possible d'envoyer des images, des textes dans n'importe quel codage, des données chiffrées et pratiquement tout type de données au format binaire. Pour plus d'informations sur les normes MQTT, voir les ressources suivantes :
- [MQTT.org](http://mqtt.org/)
- [HiveMQ: Introducing MQTT](http://www.hivemq.com/blog/mqtt-essentials-part-1-introducing-mqtt)

## Clients d'application, de terminal et de passerelle
{: #device-app-clients}

Dans {{site.data.keyword.iot_short_notm}}, les principales classes d'objet sont des terminaux et des applications. Une passerelle est une sous-classe de terminal. 

Classe d'objets identifiée par votre client MQTT pour le terminal conformément aux fonctions de votre client lorsqu'il est connecté. La classe d'objets détermine également le mécanisme d'authentification de client. 

Les applications et les terminaux fonctionnent avec des espaces de sujet MQTT différents.  Les terminaux fonctionnent dans un espace de sujet délimité pour les terminaux alors que les applications disposent d'un accès complet à l'espace de sujet de l'ensemble de l'organisation. Pour plus d'informations, voir les rubriques suivantes :

- [Terminaux](../../devices/mqtt.html)
- [Applications](../../applications/mqtt.html)
- [Passerelles](../../gateways/mqtt.html)

## Niveaux de qualité de service
{: #qos-levels}

Le protocole MQTT fournit trois qualités de service pour la distribution de messages entre les clients et les serveurs : "Une fois tout au plus" "Au moins une fois" et "Une fois exactement".
Vous pouvez envoyer des événements et des commandes en utilisant n'importe quel niveau de qualité de service. Toutefois, vous devez identifier minutieusement le niveau adapté à vos besoins.
La qualité de service de niveau 2 n'est pas toujours une option préférable au niveau zéro. 

### Une fois tout au plus (QoS0)

Parfois appelé "fire and forget", le niveau "Une fois tout au plus" (QoS0) de la qualité de service représente le mode de transmission le plus rapide.
Le message est distribué une fois tout au plus et il est possible qu'il ne soit pas distribué du tout. La distribution sur le réseau ne donne pas lieu à l'émission d'un accusé de réception et le message n'est pas stocké. Le message peut être perdu si le client est déconnecté ou si le serveur échoue.

Le protocole MQTT ne requiert pas que les serveurs réacheminent des publications avec le niveau de qualité de service zéro à un client. Si le client est déconnecté au moment où le serveur reçoit la publication, la publication risque d'être supprimée, selon la mise en oeuvre du serveur.

**Astuce :** Lors de l'envoi de données en temps réel au cours d'un intervalle donné, utilisez la qualité de service de niveau 0. Si un seul message est manquant, cela n'a pas vraiment d'importance car un autre message contenant des données plus récentes sera rapidement envoyé par la suite. Dans ce scénario, le surcoût entraîné par l'utilisation d'une qualité de service supérieure ne présente pas de réel avantage.


### Au moins une fois (QoS1)

Avec la qualité de service de niveau 1 {QoS1}, le message est toujours distribué au moins une fois. Si un échec se produit avant qu'un accusé de réception ne soit reçu par l'expéditeur, un message peut être envoyé plusieurs fois. Il doit être stocké en local au niveau de l'expéditeur jusqu'à ce que ce dernier reçoive une confirmation indiquant que le message a été publié par le destinataire.
Le message est stocké au cas où il devrait être une nouvelle fois envoyé.

### Une fois exactement (QoS2)

La qualité de service "Une fois exactement" (QoS2) est le mode de transmission le plus sûr mais le plus lent.
Le message est toujours distribué une fois exactement et doit également être stocké en local au niveau de l'expéditeur jusqu'à ce que ce dernier reçoive une confirmation indiquant que le message a été publié par le destinataire.
Le message est stocké au cas où il devrait être une nouvelle fois envoyé. La qualité de service de niveau 2 utilise une séquence plus complexe que la qualité de service QoS1, avec l'établissement d'une liaison et l'émission d'un accusé de réception, pour s'assurer qu'il n'y pas une duplication des messages.


**Astuce :** Lors de l'envoi de commandes, si vous souhaitez recevoir la confirmation que seule la commande spécifiée sera activée et qu'elle ne sera activée qu'une fois, utilisez la qualité de service de niveau 2. Il s'agit d'un exemple illustrant dans quelles circonstances les temps système supplémentaires liés au niveau 2 peuvent être avantageux par rapport aux autres niveaux. 

## Mémoires tampons des abonnements et option 'clean session'
{: #subscription-buffers-and-clean-session}

Chaque abonnement d'un terminal ou d'une application dispose d'une mémoire tampon de 5000 messages.  La mémoire tampon permet à une application ou à un terminal de prendre du retard lors du traitement des données en temps réel et d'accumuler 5000 messages en attente pour chaque abonnement souscrit.
Lorsque la mémoire tampon est pleine, les messages les plus anciens sont supprimés lorsqu'un nouveau message est reçu.

Utilisez l'option "clean session" de MQTT pour accéder à la mémoire tampon d'abonnement. Lorsque l'option "clean session" a pour valeur false, l'abonné reçoit des messages de la mémoire tampon. Lorsque l'option "clean session" a pour valeur true, la mémoire tampon est réinitialisée. 

**Remarque :** La limite de la mémoire tampon d'abonnement s'applique quelle que soit la qualité de service définie utilisée. Il est possible qu'un message envoyé avec le niveau de qualité de service 1 ou 2 ne soit pas distribué à une application qui ne peut pas soutenir le débit des messages associé à l'abonnement souscrit.


## Limitations en matière de taille pour le contenu des messages
{: #message-payload}

{{site.data.keyword.iot_short_notm}} prend en charge l'envoi et la réception de messages dans n'importe quel format autorisé par la norme MQTT. MQTT est indépendant des données, par conséquent, il est possible d'envoyer des images, des textes dans n'importe quel codage, des données chiffrées et pratiquement tout type de données au format binaire. Toutefois, il existe des limitations pour certains cas d'utilisation.   

Il existe également des limitations de taille pour le contenu des messages sur {{site.data.keyword.iot_short_notm}}.

### Restrictions en matière de format pour le contenu des messages

Les messages peuvent contenir n'importe quelle chaîne valide, cela dit, les formats JSON ("json"), texte ("text") et binaire ("bin") sont les plus couramment utilisés. 

Le tableau suivant présente les restrictions relatives au contenu des messages pour les différents types de format :

Format de contenu  | Instructions pour des cas d'utilisation spécifiques
--------- | ----------  
JSON | JSON est le format standard pour {{site.data.keyword.iot_short_notm}}. Si vous prévoyez d'utiliser les tableaux de bord, les tableaux et les cartes et les fonctions d'analyse {{site.data.keyword.iot_short_notm}} intégrés, assurez-vous que le format de contenu de message est conforme au texte JSON correctement mis en forme.
Texte | Utilisez un codage de caractères UTF-8 valide.
Binaire | Aucune restriction.


### Taille maximale de contenu de message

**Important :** La taille maximale de contenu de message sur {{site.data.keyword.iot_short_notm}} est 131072 octets. les messages dont le contenu est supérieur à la limite sont rejetés. Le client en cours de connexion est déconnecté et un message s'affiche dans les journaux de diagnostic, comme illustré dans l'exemple de message de terminal suivant :

`Connexion fermée à partir de x.x.x.x. La taille du message est trop importante pour ce noeud final. `
