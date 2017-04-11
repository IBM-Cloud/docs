---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-14"
---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# API REST HTTP pour les terminaux
{: #api}

**Important :** La fonction d'API REST HTTP {{site.data.keyword.iot_full}} pour les terminaux est disponible uniquement dans le cadre d'un programme bêta limité. Il est possible que des mises à jour ultérieures incluent des modifications incompatibles avec la version en cours de cette fonction. Essayez-la et [dites-nous ce que vous en pensez ![Icône de lien externe](../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html){: new_window}.

## Accès à la documentation de l'API REST HTTP
{: #api_link}

Pour accéder à la documentation de l'API REST HTTP {{site.data.keyword.iot_short_notm}} et obtenir davantage d'informations sur l'intégration de terminaux dans votre organisation, voir [API](../reference/api.html).

La seule version de l'API REST HTTP {{site.data.keyword.iot_short_notm}} prise en charge est la version 2. Assurez-vous que vos solutions {{site.data.keyword.iot_short_notm}} utilisent bien la version 2.

## Connexions client
{: #client_connections}

Pour plus d'informations sur la sécurité du client et pour savoir comment connecter des clients dans {{site.data.keyword.iot_short_notm}}, voir [Connexion d'applications, de terminaux et de passerelles à {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).

# API de messagerie REST HTTP pour les terminaux
{: #rest_messaging_api}

Pour accéder à la documentation de l'API de messagerie HTTP {{site.data.keyword.iot_short_notm}} et obtenir davantage d'informations sur l'intégration de terminaux dans votre organisation, voir [{{site.data.keyword.iot_short_notm}} HTTP Messaging API ![Icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}.

## Publication d'événements
{: #event_publication}

Outre l'utilisation du protocole de messagerie MQTT, vous pouvez également configurer vos terminaux pour qu'ils publient des événements sur {{site.data.keyword.iot_short_notm}} via HTTP en exécutant des commandes d'API REST HTTP.

Utilisez l'une des URL suivantes pour soumettre une demande `POST` à partir d'un terminal qui est connecté à {{site.data.keyword.iot_short_notm}} :

### Demande POST non sécurisée
<pre class="pre"><code class="hljs">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

### Demande POST sécurisée

<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

**Remarque : **Le port 443, port SSL par défaut, peut également être spécifié pour les appels API HTTP sécurisés.

Si vous connectez un terminal ou une application au service Quickstart, utilisez l'une des URL suivantes à la place :

### Demande POST non sécurisée sur Quickstart
<pre class="pre"><code class="hljs">http://quickstart.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

### Demande POST sécurisée sur Quickstart
<pre class="pre"><code class="hljs">https://quickstart.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

**Remarques importantes :**
- Dans la version de l'API REST HTTP en cours, vous ne pouvez soumettre des événements de terminal qu'en utilisant la messagerie HTTP. Utilisez le protocole de messagerie MQTT afin de soumettre des demandes pour d'autres fonctions de contrôle et de gestion des terminaux.
- Les connexions HTTP peuvent être réutilisées afin de publier des événements pour le même terminal, mais l'en-tête HTTP d'autorisation ne peut pas être modifié.
- Le port 443, port SSL par défaut, peut également être spécifié pour les appels API HTTP sécurisés.

### Authentification

Toutes les demandes doivent inclure un en-tête d'autorisation. L'authentification de base est la seule méthode prise en charge. Lorsqu'un terminal effectue une demande HTTP via l'API REST HTTP {{site.data.keyword.iot_short_notm}}, les données d'identification suivantes sont requises :

|Données d'identification|Entrée requise|
|:---|:---|
|Nom d'utilisateur|`use-token-auth`
|Mot de passe| Jeton d'authentification qui a été généré automatiquement ou que vous avez spécifié manuellement lors de l'enregistrement du terminal.


### En-têtes de demande Content-Type

Un en-tête de demande `Content-Type` doit être fourni avec la demande. Le tableau suivant présente le mappage entre les types pris en charge et les formats internes de {{site.data.keyword.iot_short_notm}}.

|En-tête Content-Type|Format dans {{site.data.keyword.iot_short_notm}}|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

### Qualité de service

Semblable au niveau 0 ("Une fois tout au plus") de la qualité de service MQTT pour la distribution, la messagerie REST HTTP fournit une distribution de message non permanente, mais vérifie que la demande est correcte et qu'elle peut être distribuée au serveur avant que celui-ci n'envoie la réponse HTTP. Une réponse contenant le code de statut HTTP 200 indique que le message a bien été distribué au serveur. Lorsque vous utilisez le niveau de qualité de service MQTT "Une fois tout au plus" ou l'équivalent HTTP pour distribuer des messages d'événement, le terminal ou l'application doit implémenter une logique de relance afin de garantir la distribution.

Pour plus d'informations sur le protocole MQTT et les niveaux de qualité de service pour {{site.data.keyword.iot_short_notm}}, voir [Messagerie MQTT](../reference/mqtt/index.html).

## Dernier cache d'événement
{: #last-event-cache}

A l'aide de l'API de dernier cache d'événement {{site.data.keyword.iot_short_notm}}, vous pouvez extraire le dernier événement qui a été envoyé par un terminal. Cela fonctionne alors que le terminal est en ligne ou hors ligne, ce qui vous permet d'extraire le statut de terminal, quel que soit l'emplacement physique ou le statut d'utilisation du terminal. Vous pouvez extraire la dernière valeur enregistrée d'un ID d'événement pour un terminal spécifique ou la dernière valeur enregistrée pour chaque ID d'événement signalé par un terminal spécifique. Les données de dernier événement d'un terminal peuvent être extraites pour n'importe quel événement spécifique qui s'est produit au cours des 365 derniers jours.

Pour obtenir la valeur la plus récente d'un ID d'événement spécifique, utilisez la demande d'API ci-après, qui renvoie la dernière valeur enregistrée pour l'ID d'événement "power".

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events/power
```

La réponse est renvoyée au format JSON suivant :

```
{
    "deviceId": "<device-id>",
    "eventId": "power",
    "format": "json",
    "payload": "eyJzdGF0ZSI6Im9uIn0=",
    "timestamp": "2016-03-14T14:12:06.527+0000",
    "typeId": "<device-type>"
}
```

**Remarque :** Si la réponse d'API est au format JSON, les contenus d'événement quant à eux peuvent être écrits dans n'importe quel format. Les contenus renvoyés par l'API de dernier cache d'événement sont codés en base 64.

Pour obtenir la valeur la plus récente de chaque ID d'événement signalé par un terminal, utilisez la demande d'API suivante :

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events
```

La réponse inclut tous les ID d'événement qui ont été envoyés par le terminal. Dans l'exemple suivant, des valeurs sont renvoyées pour les événements "power" et "temperature".

```
[
    {
        "deviceId": "<device-id>",
        "eventId": "power",
        "format": "json",
        "payload": "eyJzdGF0ZSI6Im9uIn0=",
        "timestamp": "2016-03-14T14:12:06.527+0000",
        "typeId": "<device-type>"
    },
    {
        "deviceId": "<device-id>",
        "eventId": "temperature",
        "format": "json",
        "payload": "eyJpbnRlcm5hbCI6MjIsICJleHRlcm5hbCI6MTZ9",
        "timestamp": "2016-03-14T14:17:44.891+0000",
        "typeId": "<device-type>"
    }
]
```
