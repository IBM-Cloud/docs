---

copyright:
  years: 2015, 2017
lastupdated: "2016-11-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Connectivité MQTT pour les passerelles
{: #mqtt}

MQTT est le principal protocole utilisé par les terminaux et les applications pour communiquer avec {{site.data.keyword.iot_full}}. Des bibliothèques client, des informations et des exemples vous sont fournis afin de vous aider à utiliser les clients MQTT en tant que passerelles pour la connexion de vos terminaux à {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Connexions client
{: #client_connections}

Pour plus d'informations sur la sécurité du client et pour savoir comment connecter des clients MQTT en tant que passerelles, voir [Connexion d'applications, de terminaux et de passerelles à {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).

## Authentification MQTT
{: #authentication}
Pour les passerelles et les terminaux, {{site.data.keyword.iot_short_notm}} utilise une authentification MQTT basée sur un jeton.

Pour activer l'authentification MQTT, soumettez un nom d'utilisateur et un mot de passe lorsque vous effectuez une connexion MQTT.

### Nom d'utilisateur
{: #username}

La valeur pour le nom d'utilisateur est identique pour toutes les passerelles : `use-token-auth`. Cette valeur indique à {{site.data.keyword.iot_short_notm}} qu'il doit utiliser le jeton d'authentification de la passerelle qui est spécifié comme mot de passe.

### Mot de passe
{: #password}

Le mot de passe de chaque passerelle est le jeton d'authentification unique qui a été généré lors de l'enregistrement de la passerelle auprès de {{site.data.keyword.iot_short_notm}}.

## Publication d'événements
{: #pub_events}

Une passerelle peut publier des événements elle-même ou pour le compte de n'importe quel terminal connecté via la passerelle. Pour publier des événements, utilisez le sujet suivant et remplacez les attributs `typeId` et `deviceId` appropriés en fonction de l'origine de l'événement :

<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/evt/<var class="keyword varname">eventId</var>/fmt/<var class="keyword varname">formatString</var></pre>
{: codeblock}


**Exemple**


|    |'typeID'|'deviceID'|
|:---|:---|:---|
|Passerelle 1 |mapasserelle |passerelle1 |
|Terminal 1 |monterminal |terminal1 |

-   La passerelle 1 peut publier ses propres événements de statut :
      
    `iot-2/type/mygateway/id/gateway1/evt/status/fmt/json`
-   La passerelle 1 peut publier ses propres événements de statut pour le compte du terminal 1 :
      
    `iot-2/type/mydevice/id/device1/evt/status/fmt/json`

**Important :** La taille du contenu du message ne peut pas être supérieure à 131072 octets. Les messages dont la taille est plus grande sont rejetés.

### Messages conservés
Les organisations {{site.data.keyword.iot_short_notm}} ne sont pas autorisées à publier des messages MQTT conservés. Si une passerelle envoie un message conservé, le service {{site.data.keyword.iot_short_notm}} écrase l'indicateur de message conservé lorsqu'il a pour valeur true et traite le message comme si l'indicateur de message conservé avait pour valeur false.

## Abonnement à des commandes
{: #subscribing_cmds}

Une passerelle peut s'abonner aux commandes qui lui sont envoyées directement et qui sont envoyées à tout terminal de l'organisation, y compris d'autres passerelles. Pour vous abonner à des commandes, utilisez le sujet suivant et remplacez les attributs `typeId` et `deviceId` appropriés :

<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/cmd/<var class="keyword varname">commandId</var>/fmt/<var class="keyword varname">formatString</var></pre>
{: codeblock}

Le caractère générique `+` MQTT sera utilisé pour `typeId`, `deviceId`, `commandId` et `formatString` pour l'abonnement à plusieurs sources de commande.

**Exemple :**

|Terminal |`typeId`|`deviceId`|
|:---|:---|
|Passerelle 1| mapasserelle   | passerelle1   |
|Terminal 1 | monterminal    | terminal1    |


-   La passerelle 1 peut s'abonner à des commandes qui lui sont envoyées :
      
    `iot-2/type/mygateway/id/gateway1/cmd/+/fmt/+`
-   La passerelle 1 peut s'abonner à des commandes envoyées au terminal 1 :
      
    `iot-2/type/mydevice/id/device1/cmd/+/fmt/+`
-   La passerelle 1 peut s'abonner à n'importe quelle commande envoyée aux  terminaux de type `mydevice` :
       
     `iot-2/type/mydevice/id/+/cmd/+/fmt/+`

**Important :** Les sessions persistantes MQTT spécifiées sous la forme `cleansession=false` ne recherchent pas les terminaux qui se connectent à des passerelles. Si un terminal se connecte à la passerelle A, puis à la passerelle B, il ne reçoit aucun des messages qui ont été publiés sur la passerelle A pour ce terminal alors qu'il était déconnecté. Une passerelle possède le client et l'abonnement MQTT, mais pas les terminaux qui sont connectés à la passerelle.

## Enregistrement automatique de la passerelle
{: #auto-reg}

Les terminaux de passerelle peuvent enregistrer automatiquement les terminaux qui leur sont connectés. Lorsqu'une passerelle publie un message ou s'abonne à un sujet pour le compte d'un terminal non enregistré, ce terminal est automatiquement enregistré.

Le nombre de demandes d'enregistrement en attente simultanées provenant des terminaux de passerelle ne peut pas être supérieur à 128. Essayer de connecter un grand nombre de nouveaux terminaux peut retarder l'enregistrement des terminaux via la passerelle.

**Avertissement**

Si la passerelle ne parvient pas à enregistrer un terminal automatiquement, elle ne tente pas de réenregistrer ce terminal pendant une courte période. Tous les messages ou abonnements provenant du terminal ayant échoué sont supprimés pendant cette période.

## Notifications de la passerelle
{: #notification}

Lorsque des erreurs se produisent lors de la validation du sujet de publication ou d'abonnement ou lors de l'enregistrement automatique, une notification est envoyée au terminal de passerelle. Une passerelle peut recevoir ces notifications en s'abonnant au sujet suivant, en remplaçant les valeurs `typeId` et `deviceId` :

```
iot-2/type/**typeId**/id/**deviceId**/notify
```
<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/notify</pre>
{: codeblock}

Le format des messages reçus dans le sujet de notification est le suivant :

```   
{
   "Request": "<Request_Type>",
   "Time": "<Timestamp>",
   "Topic": "<Topic>",
   "Type": "<Device_Type>",
   "Id": "<Device_Id>",
   "Client": "<Client_ID>",
   "RC": "<Return_Code>",
   "Message": "<Message>"
}
```
Où
-   `Request_Type` peut prendre les valeurs `publish` ou `subscribe`
-   `Timestamp` correspond à l'heure au format ISO 8601
-   `Topic` correspond au sujet de demande issu de la passerelle
-   `Device_Type` correspond au type de terminal issu du sujet
-   `Device_Id` correspond à l'ID de terminal issue du sujet
-   `Client_ID` correspond à l'ID de client de la demande
-   `Return_Code` correspond au code retour
-   `Message` correspond au message d'erreur

Une passerelle peut recevoir les notifications suivantes :

-   Le sujet ne correspond à aucune règle de sujet autorisée.
-   Le type de terminal n'est pas valide.
-   L'ID de terminal n'est pas valide.
-   Le nombre maximal de terminaux par passerelle a été atteint.
-   Le nombre maximal de terminaux par organisation a été atteint.
-   Echec de la création du terminal en raison d'erreurs internes.

## Passerelles gérées
{: #managed_gateways}

La prise en charge de la gestion du cycle de vie des terminaux est facultative. Le protocole de gestion des terminaux utilisé par {{site.data.keyword.iot_short_notm}} se sert de la même connexion MQTT que celle utilisée par la passerelle pour les événements et le contrôle des commandes.

### Niveaux de qualité de service et option 'clean session'
{: #quality_service}

Les passerelles gérées peuvent publier des messages dotés du niveau de qualité de service (QoS) 0 ou 1.

Les messages dotés du niveau QoS=0 peuvent être supprimés et ne sont pas conservés après le redémarrage du serveur de messagerie. Les messages dotés du niveau QoS=1 peuvent être placés en file d'attente et ne sont pas conservés après le redémarrage du serveur de messagerie. La durabilité de l'abonnement détermine si une demande a été placée en file d'attente. Le paramètre `cleansession` de la connexion qui a effectué l'abonnement détermine la durabilité de l'abonnement.  

{{site.data.keyword.iot_short_notm}} publie les demandes dotées du niveau QoS 1 pour prendre en charge la mise en file d'attente des messages. Pour placer en file d'attente les messages qui sont envoyés alors qu'une passerelle gérée n'est pas connectée, configurez le terminal pour qu'il n'utilise pas d'options 'clean session' en affectant la valeur false au paramètre `cleansession`.

**Avertissement**

Lorsqu'une passerelle gérée utilise un abonnement durable, les commandes de gestion des terminaux qui sont envoyées à la passerelle alors qu'elle est hors ligne sont signalées comme ayant échoué si la passerelle ne se reconnecte pas au service avant l'expiration de la demande. Lorsque la passerelle se reconnecte, ces demandes sont traitées par la passerelle. Les abonnements durables sont spécifiés par le paramètre `cleansession=false`.

La passerelle possède la session MQTT, quels que soient les terminaux qui sont derrière elle. Lorsqu'un terminal soumet une demande d'abonnement via une passerelle, la demande ne passe pas par les autres passerelles, que les options `cleansession=false` soient définies ou non.

### Rubriques
{: #topics}

Une passerelle gérée doit s'abonner aux sujets suivants pour traiter les demandes et les réponses émanant de {{site.data.keyword.iot_short_notm}} :

-   La passerelle gérée s'abonne aux réponses de gestion des terminaux sur :  
<pre class="pre">iotdm-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/response/+</pre>
{: codeblock}
-   La passerelle gérée s'abonne aux demandes de gestion des terminaux sur :  
<pre class="pre">iotdm-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/+</pre>
{: codeblock}

Une passerelle gérée publie les réponses et demandes suivantes :

- Les réponses de gestion des terminaux sont publiées sur :  
<pre class="pre">iotdevice-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/response/</pre>
{: codeblock}
- Les demandes Gérer le terminal sont publiées sur :  
<pre class="pre">iotdevice-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/</pre>
{: codeblock}

La passerelle peut traiter des messages de protocole de gestion des terminaux à la fois pour elle-même et pour le compte d'autres terminaux connectés en utilisant les attributs **typeId** et **deviceId** appropriés.

### Format de message
{: #msg_format}

Tous les messages sont envoyés au format JSON.

**Demandes**

Les demandes sont formatées comme illustré dans l'exemple de code suivant :

```   
    {  "d": {...}, "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056" }
```

-   `d` contient les données relatives à la demande
-   `reqId` est l'identificateur de la demande et doit être copié dans la réponse. Si aucune réponse n'est requise, la zone n'est pas utilisée.

**Réponses**

Les réponses sont formatées comme illustré dans l'exemple de code suivant :

```
    {
        "rc": 0,
        "message": "success",
        "d": {...},
        "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056"
    }
```
Où :
-   `rc` est le code de résultat de la demande d'origine.
-   `message` est un élément facultatif contenant la description textuelle du code de réponse.
-   `d` est un élément de données facultatif qui accompagne la réponse.
-   `reqId` est l'ID de demande de la demande d'origine. L'ID de demande est utilisé pour corréler les réponses aux demandes et le terminal doit s'assurer que tous les ID de demande sont uniques. Les réponses aux demandes {{site.data.keyword.iot_short_notm}} doivent contenir la valeur `reqId` correcte.
