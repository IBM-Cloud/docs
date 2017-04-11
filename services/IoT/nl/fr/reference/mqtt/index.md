---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Messagerie MQTT
{: #ref-mqtt}

MQTT est le principal protocole utilisé par les terminaux et les applications pour communiquer avec {{site.data.keyword.iot_full}}. MQTT est un protocole de transport de messagerie de publication et d'abonnement conçu pour optimiser les échanges de données en temps réel entre le capteur et les terminaux mobiles.
{:shortdesc}

MQTT s'exécute sur TCP/IP, et bien qu'il soit possible d'effectuer directement un codage pour TCP/IP, vous pouvez également choisir d'utiliser une bibliothèque qui traite pour vous les détails du protocole MQTT. Une vaste gamme de bibliothèques client MQTT est disponible. IBM contribue au développement et au support de plusieurs bibliothèques client, y compris celles qui ne sont pas disponibles au niveau des sites suivants :

- [Wiki de communauté MQTT ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/mqtt/mqtt.github.io/wiki){: new_window}
- [Projet Eclipse Paho ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](http://eclipse.org/paho/){: new_window}

## Support de version
{: #version-support}
Pour plus d'informations sur les versions de MQTT prises en charge par {{site.data.keyword.iot_short_notm}}, voir [Normes et exigences](../standards_and_requirements.html#mqtt).

## Clients d'application, de terminal et de passerelle
{: #device-app-clients}

Dans {{site.data.keyword.iot_short_notm}}, les principales classes d'objet sont des terminaux et des applications. Une passerelle est une sous-classe de terminal.

Votre client MQTT s'identifie auprès du service {{site.data.keyword.iot_short_notm}} en tant que classe de chose. La classe de chose détermine les fonctionnalités du client quand il est connecté. La classe d'objets détermine également le mécanisme d'authentification de client.

Les applications et les terminaux fonctionnent avec des espaces de sujet MQTT différents.  Les terminaux fonctionnent dans un espace de sujet délimité pour les terminaux alors que les applications disposent d'un accès complet à l'espace de sujet de l'ensemble de l'organisation. Pour plus d'informations, voir les rubriques suivantes :

- [Messagerie MQTT pour les terminaux](../../devices/mqtt.html)
- [Messagerie MQTT pour les applications](../../applications/mqtt.html)
- [Messagerie MQTT pour les passerelles](../../gateways/mqtt.html)

### Messages conservés
{{site.data.keyword.iot_short_notm}} fournit une prise en charge limitée pour la fonction de messages conservés de la messagerie MQTT. Si l'indicateur de message conservé a pour valeur true dans un message MQTT qui est envoyé d'un terminal, d'une passerelle ou d'une application à {{site.data.keyword.iot_short_notm}}, le message est traité comme un message non conservé. Les organisations {{site.data.keyword.iot_short_notm}} ne sont pas autorisées à publier des messages conservés. Le service {{site.data.keyword.iot_short_notm}} écrase l'indicateur de message conservé lorsqu'il a pour valeur true et traite le message comme si l'indicateur de message conservé avait pour valeur false.

## Niveaux de qualité de service
{: #qos-levels}

Le protocole MQTT fournit trois qualités de service pour la distribution de messages entre les clients et les serveurs : "Une fois tout au plus" "Au moins une fois" et "Une fois exactement".
Vous pouvez envoyer des événements et des commandes en utilisant n'importe quel niveau de qualité de service. Toutefois, vous devez identifier minutieusement le niveau adapté à vos besoins. La qualité de service de niveau '2' n'est pas toujours une option préférable au niveau '0'.

### Une fois tout au plus (QoS0)

Parfois appelé "fire and forget", le niveau "Une fois tout au plus" (QoS0) de la qualité de service représente le mode de transmission le plus rapide. Le message est distribué une fois tout au plus et il est possible qu'il ne soit pas distribué du tout. La distribution sur le réseau ne donne pas lieu à l'émission d'un accusé de réception et le message n'est pas stocké. Le message peut être perdu si le client est déconnecté ou si le serveur échoue.

Le protocole MQTT ne requiert pas que les serveurs réacheminent des publications avec le niveau de qualité de service '0' à un client. Si le client est déconnecté au moment où le serveur reçoit la publication, la publication risque d'être supprimée, selon la mise en oeuvre du serveur.

**Astuce :** Lors de l'envoi de données en temps réel au cours d'un intervalle donné, utilisez la qualité de service de niveau 0. Si un seul message est manquant, cela n'a pas vraiment d'importance car un autre message contenant des données plus récentes sera rapidement envoyé par la suite. Dans ce scénario, le surcoût entraîné par l'utilisation d'une qualité de service supérieure ne présente pas de réel avantage.

### Au moins une fois (QoS1)

Avec la qualité de service de niveau 1 {QoS1}, le message est toujours distribué au moins une fois. Si un échec se produit avant qu'un accusé de réception ne soit reçu par l'expéditeur, un message peut être envoyé plusieurs fois. Il doit être stocké en local au niveau de l'expéditeur jusqu'à ce que ce dernier reçoive une confirmation indiquant que le message a été publié par le destinataire. Le message est stocké au cas où il devrait être une nouvelle fois envoyé.

### Une fois exactement (QoS2)

La qualité de service "Une fois exactement" 2 (QoS2) est le mode de transmission le plus sûr mais le plus lent. Le message est toujours distribué une fois exactement et doit également être stocké en local au niveau de l'expéditeur jusqu'à ce que ce dernier reçoive une confirmation indiquant que le message a été publié par le destinataire. Le message est stocké au cas où il devrait être une nouvelle fois envoyé. La qualité de service de niveau 2 utilise une séquence plus complexe que la qualité de service QoS1, avec l'établissement d'une liaison et l'émission d'un accusé de réception, pour s'assurer qu'il n'y pas une duplication des messages.

**Astuce :** Lors de l'envoi de commandes, si vous souhaitez recevoir la confirmation que seule la commande spécifiée sera activée et qu'elle ne sera activée qu'une fois, utilisez la qualité de service de niveau 2. Il s'agit d'un exemple illustrant dans quelles circonstances les temps système supplémentaires liés au niveau 2 peuvent être avantageux par rapport aux autres niveaux.

## Mémoires tampons des abonnements et option 'clean session'
{: #subscription-buffers-and-clean-session}

Chaque abonnement d'un terminal ou d'une application dispose d'une mémoire tampon de 5000 messages.  La mémoire tampon permet à une application ou à un terminal de prendre du retard lors du traitement des données en temps réel et d'accumuler 5000 messages en attente pour chaque abonnement souscrit. Lorsque la mémoire tampon est pleine, les messages les plus anciens sont supprimés lorsqu'un nouveau message est reçu.

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

## Intervalle de signal de présence MQTT
{: #mqtt-keep-alive}

L'intervalle de signal de présence, mesuré en secondes, définit le temps maximum qui peut passer sans communication entre le client et le courtier. Le client MQTT doit s'assurer que, en l'absence de toute autre communication avec le courtier, un paquet PINGREQ est envoyé. L'intervalle de signal de présence permet à la fois au client et au courtier de détecter que le réseau a échoué, ce qui entraîne une connexion brisée, sans avoir à attendre que le délai de time-out TCP/IP soit atteint.

Si vos clients MQTT {{site.data.keyword.iot_short_notm}} utilisent des abonnements partagés, la valeur d'intervalle de signal de présence peut uniquement être définie entre 1 et 3600 secondes. Si une valeur de 0 ou une valeur supérieure à 3600 est demandée, le courtier {{site.data.keyword.iot_short_notm}} définit l'intervalle de signal de présence à 3600 secondes.
