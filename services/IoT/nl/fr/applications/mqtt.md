---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Connectivité MQTT pour les applications
{: #mqtt}

MQTT est le principal protocole utilisé par les terminaux et les applications pour communiquer avec {{site.data.keyword.iot_full}}. Des bibliothèques client, des exemples et des informations vous sont fournis afin de vous aider à connecter et intégrer vos applications {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Connexions client
{: #client_connections}

Pour plus d'informations sur la sécurité du client et pour savoir comment connecter des clients MQTT en tant qu'applications dans {{site.data.keyword.iot_short_notm}}, voir [Connexion d'applications, de terminaux et de passerelles à {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).

## Authentification MQTT
{: #mqtt_authentication}

Les applications {{site.data.keyword.iot_short_notm}} requièrent une clé d'API pour se connecter à une organisation. Lorsqu'une clé d'API est enregistrée, un jeton d'authentification est généré et doit être utilisé avec cette clé d'API.

L'exemple suivant illustre une clé d'API standard :

<pre class="pre">a-<var class="keyword varname">orgId</var>-a84ps90Ajs</pre>
{: codeblock}


L'exemple suivant illustre un jeton d'authentification standard :

```
MP$08VKz!8rXwnR-Q*
```

Lorsque vous établissez une connexion MQTT à l'aide d'une clé d'API, prenez soin de suivre les instructions ci-dessous :

- L'ID de client MQTT doit être au format suivant : a:*orgId*:*appId*
- Le nom d'utilisateur MQTT doit correspondre à la clé d'API (par exemple, a-*orgId*-a84ps90Ajs)
- Le mot de passe MQTT doit correspondre au jeton d'authentification (par exemple, MP$08VKz!8rXwnR-Q*)


## Publication des événements d'un terminal
{: #publishing_device_events}

Une application peut publier des événements comme s'ils provenaient d'un terminal enregistré, par exemple :

-  Publish to topic iot-2/type/*device_type*/id/*device_id*/evt/*event_id*/fmt/*format_string*

Pour envoyer les données d'un terminal dans {{site.data.keyword.iot_short_notm}}, vous pouvez créer une application afin de traiter les données et les publier dans {{site.data.keyword.iot_short_notm}}.

**Important :** La taille du contenu du message ne peut pas être supérieure à 131072 octets.  Les messages dont la taille est plus grande sont rejetés.

### Messages conservés
Les organisations {{site.data.keyword.iot_short_notm}} ne sont pas autorisées à publier des messages MQTT conservés. Si une application, une passerelle ou un terminal envoie un message conservé, le service {{site.data.keyword.iot_short_notm}} écrase l'indicateur de message conservé lorsqu'il a pour valeur true et traite le message comme si l'indicateur avait pour valeur false.

## Publication des commandes d'un terminal
{: #publishing_device_commands}

Une application peut publier une commande sur n'importe quel terminal enregistré, par exemple :

-  Publish to topic iot-2/type/*device_type*/id/*device_id*/cmd/*command_id*/fmt/*format_string*

## Abonnement aux événements d'un terminal
{: #subscribe_device_events}

Une application peut s'abonner à des événements depuis un ou plusieurs terminaux, par exemple :

-  Subscribe to topic iot-2/type/*device_type*/id/*device_id*/evt/*event_id*/fmt/*format_string*

**Remarque :** Pour vous abonner à plus d'un type d'événement ou à des événements depuis plusieurs terminaux, utilisez le caractère générique MQTT + pour n'importe lequel des composants suivants :

- device_type
- device_id
- event_id
- format_string

## Abonnement aux commandes d'un terminal
{: #subscribe_device_commands}

Une application peut s'abonner à des commandes envoyées à un ou plusieurs terminaux, par exemple :

-  Subscribe to topic iot-2/type/*device_type*/id/*device_id*/cmd/*command_id*/fmt/*format_string*

**Remarque :** Pour vous abonner à plus d'un type d'événement ou à des événements depuis plusieurs terminaux, utilisez le caractère générique MQTT + pour n'importe lequel des composants suivants :

-  device_type
-  device_id
-  cmd_id
-  format_string

## Abonnement aux messages de statut d'un terminal
{: #subscribe_device_status}

Une application peut s'abonner pour surveiller le statut d'un ou de plusieurs terminaux, par exemple :

-  Subscribe to topic iot-2/type/*device_type*/id/*device_id*/mon

**Remarque :** Pour vous abonner aux mises à jour depuis plusieurs terminaux, utilisez le caractère générique MQTT + pour n'importe lequel des composants suivants :

- device_type
- device_id

## Abonnement aux messages de statut d'une application
{: #subscribe_app_status}

Une application peut s'abonner pour surveiller le statut d'un ou de plusieurs applications, par exemple :

- Subscribe to topic iot-2/app/*appId*/mon

**Remarque :** Pour vous abonner aux mises à jour pour toutes les applications, utilisez le caractère générique MQTT + pour le composant  *appId*.


## Restrictions liées à Quickstart
{: #quickstart_restrictions}
Si vous prévoyez de créer un code d'application à utiliser avec le service Quickstart, les fonctions suivantes ne sont pas prises en charge dans Quickstart :

- Publication de commandes
- Abonnement à des commandes
- Utilisation du caractère générique MQTT + dans les composants **deviceType** ou **appId**
- Connexion MQTT via le protocole TLS (Transport Layer Security)
- Applications évolutives

## Applications évolutives
{: #scalable_apps}

En ajustant le mode de connexion de vos applications {{site.data.keyword.iot_short_notm}}, vous pouvez les rendre plus évolutives en équilibrant le traitement de la charge des messages d'événement sur plusieurs instances d'une application.

Le nombre de clients requis pour optimiser l'équilibrage de charge et l'évolutivité varie d'un déploiement à l'autre. Pour déterminer le nombre optimal de clients, vous devez réaliser un test de charge sur votre système.

Des applications évolutives sont définies en tant qu'abonnements non durables ou abonnements partagés à durabilité mixte (bêta).

### Abonnements non durables
{: #shared_sub_non_durable}

Pour activer l'équilibrage de charge, assurez-vous que l'abonnement à une application est de type non durable et que l'ID de client défini dans l'abonnement respecte le format suivant :

<pre class="pre">A:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
{: codeblock}

Où :
-  Le caractère **A** indique que le client est une application évolutive.
-  *orgId* est l'ID d'organisation unique composé de six caractères ayant été généré lorsque vous avez enregistré le chaîne.
-  *appId* est un identificateur de chaîne unique défini par l'utilisateur pour le client. La chaîne ne peut contenir que des caractères alphanumériques (a-z, A-Z, 0-9), ainsi que les caractères spéciaux suivants : tiret (-), trait de soulignement (_) et point (.).


**Important :**
- L'ID de client doit débuter par un caractère **A** en majuscule pour être correctement désigné en tant qu'application évolutive par {{site.data.keyword.iot_short_notm}}.
- Les autres clients qui font partie de l'application évolutive doivent utiliser le même ID de client.
- La valeur de l'option clean session doit être false (0) pour des abonnements non durables.

### Abonnements partagés à durabilité mixte (bêta)
{: #shared_sub_mixed}

Le service {{site.data.keyword.iot_short_notm}} développe la spécification de protocole de messagerie MQTT V3.1.1 pour permettre la prise en charge d'une version d'essai bêta des abonnements partagés à durabilité mixte. Les abonnements partagés fournissent des fonctions d'équilibrage de charge pour les applications. Un abonnement partagé peut s'avérer nécessaire si une application d'entreprise de back end ne peut pas traiter le volume de messages publiés sur un espace de sujet spécifique. Par exemple, lorsque de nombreux terminaux publient des messages qui sont traités par une seule application, il peut s'avérer nécessaire d'utiliser la fonction d'équilibrage de charge d'un abonnement partagé.

Pour les abonnements partagés à durabilité mixte, assurez-vous que l'identificateur de client défini dans l'abonnement respecte le format suivant :

<pre class="pre">A:<var class="keyword varname">org</var>:<var class="keyword varname">appId</var>:<var class="keyword varname">instanceId</var></pre>
{: codeblock}

Où :
- Les caractères **A**, *orgId* et *appId* dans l'identificateur de client sont définis de la même manière que pour les [abonnements non durables](#shared_sub_non_durable).
- *instanceID* est une chaîne qui ne doit pas dépasser 36 caractères et qui peut uniquement contenir les caractères suivants :
   - Caractères alphanumériques (a-z, A-Z, 0-9)
   - Tirets (-)
   - Traits de soulignement (_)
   - Points (. )

**Important :**
- La prise en charge des abonnements partagés à durabilité mixte est uniquement disponible en tant que fonction bêta. N'implémentez pas les fonctions bêta dans les applications en production.
- La session de l'option clean session peut avoir pour valeur true (1) ou false (0) dans les abonnements partagés à durabilité mixte.
- Les clients qui se connectent à l'aide de l'ID instance utilisent des abonnements différents de ceux utilisés par les clients qui se connectent sans l'ID instance. Par conséquent, si vous souhaitez que plusieurs clients se connectent à un abonnement partagé à durabilité mixte, vous devez spécifier l'ID instance dans tous les abonnements.

**Exemple de scénario**

Le scénario suivant illustre l'une des manières dont une application évolutive non durable fonctionne dans {{site.data.keyword.iot_short_notm}} :

- Le client numéro un se connecte en tant que **A:abc123:myApplication** et s'abonne à tous les événements de terminal, ce qui signifie qu'il reçoit 100 % des événements de terminal qui sont publiés.
- Le client numéro deux se connecte en tant que **A:abc123:myApplication** et s'abonne également à tous les événements de terminal, ce qui signifie que le client numéro un et le client numéro deux partagent tous les événements qui sont publiés. La charge de traitement est partagée entre le client numéro un et le client numéro deux.
- Le client numéro trois se connecte en tant que **A:abc123:myApplication** et s'abonne également à tous les événements de terminal, ce qui signifie que le client numéro un, le client numéro deux et le client numéro trois partagent le traitement de la charge pour les événements.
- Le client numéro un et le client numéro trois se désabonnement de tous les événements de terminal, ce qui signifie que seul le client numéro un reçoit tous les événements de terminal qui sont publiés. Alors que le client numéro deux et le client numéro trois sont toujours connectés au service, le client numéro un reçoit 100 % des événements de terminal qui sont publiés.
- Lorsqu'au moins deux applications partagent un abonnement, il se peut que les messages n'arrivent pas dans l'ordre où ils ont été envoyés. Par exemple, le message B peut arriver au client numéro un avant que le message A n'arrive au client numéro deux, même si le message A a été envoyé en premier.
