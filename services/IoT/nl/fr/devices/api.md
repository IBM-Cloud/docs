---

copyright :
  années : 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# API REST HTTP pour les terminaux
{: #api}
Dernière mise à jour : 9 septembre 2016
{: .last-updated}

**Important :** La fonction d'API REST HTTP {{site.data.keyword.iot_full}} pour les terminaux est disponible uniquement dans le cadre d'un programme bêta limité. Il est possible que des mises à jour ultérieures incluent des modifications incompatibles avec la version en cours de cette fonction. Essayez-la et [dites-nous ce que vous en pensez](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html).

## Accès à l'API REST HTTP
{: #api_link}

Pour accéder à l'API REST HTTP {{site.data.keyword.iot_short_notm}} et obtenir davantage d'informations sur l'intégration de terminaux dans votre organisation, voir https://docs.internetofthings.ibmcloud.com/swagger/v0002.html.

La seule version de l'API REST HTTP {{site.data.keyword.iot_short_notm}} prise en charge est la version 2. Assurez-vous que vos solutions {{site.data.keyword.iot_short_notm}} utilisent bien la version 2. 

# API de messagerie REST HTTP pour les terminaux
{: #rest_messaging_api}

## Publication d'événements
{: #event_publication}

Outre l'utilisation du protocole de messagerie MQTT, vous pouvez également configurer vos terminaux pour qu'ils publient des événements sur {{site.data.keyword.iot_short_notm}} via HTTP en exécutant des commandes d'API REST HTTP. 

Utilisez l'une des URL suivantes pour soumettre une demande `POST` à partir d'un terminal qui est connecté à {{site.data.keyword.iot_short_notm}} :

### Demande POST non sécurisée
<pre class="pre">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### Demande POST sécurisée
<pre class="pre">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

Si vous connectez un terminal ou une application au service Quickstart, utilisez l'une des URL suivantes à la place : 

### Demande POST non sécurisée sur Quickstart
<pre class="pre">http://quickstart.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### Demande POST sécurisée sur Quickstart
<pre class="pre">https://quickstart.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

**Remarques importantes :**
- Dans la version de l'API REST HTTP en cours, vous ne pouvez soumettre des événements de terminal qu'en utilisant la messagerie HTTP. Utilisez le protocole de messagerie MQTT afin de soumettre des demandes pour d'autres fonctions de contrôle et de gestion des terminaux. 
- Les connexions HTTP peuvent être réutilisées afin de publier des événements pour le même terminal, mais l'en-tête HTTP d'autorisation ne peut pas être modifié. 

### Authentification

Toutes les demandes doivent inclure un en-tête d'autorisation. L'authentification de base est la seule méthode prise en charge. Lorsqu'un terminal effectue une demande HTTP via l'API REST HTTP {{site.data.keyword.iot_short_notm}}, les données d'identification suivantes sont requises :

```
username = "use-token-auth"
password = Authentication token
```

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
