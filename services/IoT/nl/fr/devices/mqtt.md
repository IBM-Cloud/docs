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


# Connectivité MQTT pour les terminaux
{: #mqtt}

MQTT est le principal protocole utilisé par les terminaux et les applications pour communiquer avec {{site.data.keyword.iot_full}}. Des bibliothèques client, des exemples et des informations vous sont fournis afin de vous aider à connecter et intégrer vos terminaux à {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Connexions client
{: #client_connections}

Pour plus d'informations sur la sécurité du client et pour savoir comment connecter des clients MQTT dans {{site.data.keyword.iot_short_notm}}, voir [Connexion d'applications, de terminaux et de passerelles à {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).


## Connexion de terminaux au service Quickstart
{: #connecting_devices}

Quickstart est le niveau de service le plus rapide. Il n'offre pas de confirmation de réception et ne prend pas en charge les niveaux de qualité de service MQTT (QoS) supérieurs à zéro. Lorsque vous vous connectez au service Quickstart, l'authentification ou l'enregistrement n'est pas obligatoire, et la valeur `quickstart` doit être affectée au paramètre `orgId`.

Si vous écrivez un code de terminal à utiliser avec Quickstart, vous devez savoir que les fonctions de service {{site.data.keyword.iot_short_notm}} suivantes ne sont pas prises en charge en mode Quickstart :

-  Abonnement à des commandes
-  Protocole de gestion des terminaux
-  Sessions propres ou durables

**Important :** Il se peut que les messages envoyés par les terminaux à une fréquence supérieure à un par seconde soient annulés.


## Authentification MQTT
{: #mqtt_authentication}

Pour les passerelles et les terminaux, {{site.data.keyword.iot_short_notm}} utilise une authentification MQTT basée sur un jeton.

Pour activer l'authentification MQTT, soumettez un nom d'utilisateur et un mot de passe lorsque vous effectuez une connexion MQTT.

### Nom d'utilisateur

La valeur pour le nom d'utilisateur est identique pour tous les terminaux : `use-token-auth`. Cette valeur indique à {{site.data.keyword.iot_short_notm}} qu'il doit utiliser le jeton d'authentification du terminal qui est spécifié comme mot de passe.

### Mot de passe

Le mot de passe de chaque terminal est le jeton d'authentification unique qui a été généré lors de l'enregistrement du terminal auprès de {{site.data.keyword.iot_short_notm}}.

## Publication d'événements
{: #publishing_events}

Les terminaux effectuent des publications sur les sujets d'événement au format suivant :

<pre class="pre">iot-2/evt/<var class="keyword varname">event_id</var>/fmt/<var class="keyword varname">format_string</var></pre>
{: codeblock}

Où

-  **event_id** est l'ID de l'événement, par exemple, `status`.  L'ID d'événement peut être n'importe quelle chaîne valide dans MQTT. Si aucun caractère générique n'est utilisé, les applications d'abonné doivent utiliser cette chaîne dans leur sujet d'abonnement afin de recevoir les événements publiés sur leur sujet.
-  **format_string** est une chaîne qui définit le type de contenu du message de manière à permettre au destinataire de celui-ci de savoir comment faire l'analyse syntaxique du contenu. Les valeurs de type de contenu les plus courantes sont notamment "json", "xml", "txt" et "csv". La valeur peut être n'importe quelle chaîne valide dans MQTT.

**Important :** La taille du contenu du message ne peut pas être supérieure à 131072 octets. Les messages dont la taille est plus grande sont rejetés.

### Messages conservés
Les organisations {{site.data.keyword.iot_short_notm}} ne sont pas autorisées à publier des messages MQTT conservés. Si un terminal envoie un message conservé, le service {{site.data.keyword.iot_short_notm}} écrase l'indicateur de message conservé lorsqu'il a pour valeur true et traite le message comme si l'indicateur de message conservé avait pour valeur false.


## Abonnement à des commandes
{: #subscribing_to_commands}

Les terminaux peuvent s'abonner à des sujets de commande en utilisant le format suivant :

<pre class="pre">iot-2/cmd/<var class="keyword varname">command_id</var>/fmt/<var class="keyword varname">format_string</var></pre>
{: codeblock}

Où
 - **command_id** est l'ID de la commande, par exemple, `update`. L'ID de commande peut être n'importe quelle chaîne valide dans le protocole MQTT.  Si aucun caractère générique n'est utilisé, un terminal doit utiliser cette chaîne dans son sujet d'abonnement afin de recevoir les commandes qui sont publiées sur son sujet.
 - **format_string** est une chaîne qui définit le type de contenu de la commande de manière à permettre au destinataire de celle-ci de savoir comment faire l'analyse syntaxique du contenu. Les valeurs de type de contenu les plus courantes sont notamment "json", "xml", "txt" et "csv". La valeur peut être n'importe quelle chaîne valide dans MQTT.

les terminaux ne peuvent pas s'abonner à des événements provenant d'autres terminaux. Un terminal reçoit des commandes qui sont publiées uniquement sur son propre terminal.

## Terminaux gérés
{: #managed-devices}

La prise en charge de la gestion du cycle de vie des terminaux est facultative. Le protocole de gestion des terminaux se sert de la même connexion MQTT que celle utilisée par le terminal pour les événements et le contrôle des commandes.

### Niveaux de qualité de service et option 'clean session'

Les terminaux gérés peuvent publier des messages dotés du niveau de qualité de service (QoS) 0 ou 1.

Les messages dotés du niveau QoS=0 peuvent être supprimés et ne sont pas conservés après le redémarrage du serveur de messagerie. Les messages dotés du niveau QoS=1 peuvent être placés en file d'attente et ne sont pas conservés après le redémarrage du serveur de messagerie. La durabilité de l'abonnement détermine si une demande a été placée en file d'attente. Le paramètre `cleansession` de la connexion qui a effectué l'abonnement détermine la durabilité de l'abonnement.  

{{site.data.keyword.iot_short_notm}} publie les demandes dotées du niveau QoS 1 pour prendre en charge la mise en file d'attente des messages. Pour placer en file d'attente les messages qui sont envoyés alors qu'un terminal géré n'est pas connecté, configurez le terminal pour qu'il n'utilise pas d'options 'clean session' en affectant la valeur false au paramètre `cleansession`.

**Avertissement :**
  Si votre terminal géré utilise un abonnement durable, les commandes qui sont envoyées à votre terminal alors que celui-ci est hors ligne sont signalées comme des opérations ayant échoué si le terminal ne se reconnecte pas au service avant l'expiration de la demande. En revanche, ces demandes sont traitées par le terminal lorsqu'il se reconnecte. Un abonnement durable est spécifié par le paramètre `cleansession=false`.

### Rubriques

Un terminal géré doit s'abonner au sujet suivant pour traiter les demandes et les réponses émanant du service {{site.data.keyword.iot_short_notm}} :

```
iotdm-1/#
```


Un terminal géré effectue des publications sur des sujets qui sont propres au type de demande de gestion effectuée :

- Le terminal géré publie des réponses de gestion des terminaux sur `iotdevice-1/response`.
- Pour connaître les autres sujets sur lesquels un terminal géré peut effectuer des publications, voir [Protocole de gestion des terminaux](device_mgmt/index.html) et  [Demandes de gestion des terminaux](device_mgmt/requests.html).



### Format de message

Tous les messages sont envoyés au format JSON.

**Demandes**  
Les demandes sont formatées comme illustré dans l'exemple de code suivant :

<pre class="pre">{  "d": {...}, "<var class="keyword varname">reqId</var>": "b53eb43e-401c-453c-b8f5-94b73290c056" }</pre>
{: codeblock}

Où :

 - **d** contient les données pertinentes pour la demande.
 - **reqId** est l'identificateur de la demande et doit être copié dans la réponse. Si aucune réponse n'est requise, vous pouvez omettre la zone *reqId*.

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
 - **rc** est le code de résultat de la demande d'origine.
 - **message** est un élément facultatif contenant la description textuelle du code de réponse.
 - **d** est un élément de données facultatif qui accompagne la réponse.
 - **reqId** est l'ID de la demande d'origine, utilisée pour corréler des réponses avec des demandes. Le terminal doit s'assurer que tous les ID de demande sont uniques. Les réponses aux demandes {{site.data.keyword.iot_short_notm}} doivent inclure la valeur **reqId** correcte.

Pour plus d'informations sur les messages propres aux demandes et aux réponses, voir [Protocole de gestion des terminaux](device_mgmt/index.html) et [Demandes de gestion des terminaux](device_mgmt/requests.html).
