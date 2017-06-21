---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-07"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# API REST HTTP pour les terminaux de passerelle
{: #api_link}


Pour accéder à la documentation de l'API REST HTTP {{site.data.keyword.iot_short_notm}} et obtenir davantage d'informations sur la création, la mise à jour, la suppression et l'affichage de listes de terminaux, voir [API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html).

La seule version de l'API REST HTTP {{site.data.keyword.iot_short_notm}} prise en charge est la version 2. Assurez-vous que vos solutions {{site.data.keyword.iot_short_notm}} utilisent bien la version 2.

## Connexions client
{: #client_connections}

Pour plus d'informations sur la sécurité du client et pour savoir comment connecter des terminaux de passerelle dans {{site.data.keyword.iot_short_notm}}, voir [Connexion d'applications, de terminaux et de passerelles à {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).


### Authentification

Toutes les demandes doivent inclure un en-tête d'autorisation. L'authentification de base est la seule méthode prise en charge. Lorsqu'un terminal effectue une demande HTTP via l'API REST HTTP {{site.data.keyword.iot_short_notm}}, les données d'identification suivantes sont requises :

|Données d'identification|Entrée requise|
|:---|:---|
|Nom d'utilisateur| `g/{orgId}/{gwType}/{gwDevId}`
|Mot de passe| Jeton d'authentification qui a été généré automatiquement ou que vous avez spécifié manuellement lors de l'enregistrement du terminal de passerelle.

où :

<dl>
<dt>orgId</dt>  
<dd>Nom de l'organisation, qui doit correspondre au nom qui est spécifié dans l'en-tête d'hôte.</dd>

<p></p>
<dt>gwType</dt>  
<dd>Type de passerelle. </dd>
<p></p>
<dt>gwDevId</dt>  
<dd>Identificateur de terminal de passerelle. </dd>
</dl>


### En-têtes de demande Content-Type

Un en-tête de demande `Content-Type` doit être fourni avec la demande. Le tableau suivant présente le mappage entre les types pris en charge et les formats internes de {{site.data.keyword.iot_short_notm}} :

|En-tête Content-Type|Format dans {{site.data.keyword.iot_short_notm}}|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

## Dernier cache d'événement
{: #last-event-cache}

A l'aide de l'API de dernier cache d'événement {{site.data.keyword.iot_short_notm}}, vous pouvez extraire le dernier événement qui a été envoyé par un terminal. Cette API fonctionne alors que le terminal est en ligne ou hors ligne, ce qui vous permet d'extraire le statut de terminal, quel que soit l'emplacement physique ou le statut d'utilisation du terminal. Vous pouvez extraire la dernière valeur enregistrée d'un ID d'événement pour un terminal spécifique ou la dernière valeur enregistrée pour chaque ID d'événement signalé par un terminal spécifique. Les données de dernier événement d'un terminal peuvent être extraites pour n'importe quel événement spécifique qui s'est produit au cours des 365 derniers jours.

Pour obtenir la valeur la plus récente d'un ID d'événement spécifique, utilisez la demande d'API ci-après, qui renvoie la dernière valeur enregistrée pour l'ID d'événement "power" :

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
