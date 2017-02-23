---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-12-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# API REST HTTP pour les applications
{: #api}

Utilisez l'API REST HTTP {{site.data.keyword.iot_full}} pour générer et personnaliser des applications qui interagissent avec votre organisation sur {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Fonctionnalités
{: #capabilities}

L'API REST HTTP {{site.data.keyword.iot_short_notm}} prend en charge les fonctionnalités et fonctions suivantes pour les applications :

- Extraction des informations d'organisation
- Opérations globales sur les terminaux (affichage de liste, ajout et retrait)
- Opérations relatives aux types de terminal (affichage de liste, création, suppression, affichage des détails et mise à jour)
- Opérations sur les terminaux (affichage de liste, ajout, retrait, affichage des détails, mise à jour, affichage d'emplacement et affichage des informations de gestion)
- Opérations de diagnostic d'un terminal (effacement de journaux, extraction de journaux, ajout d'informations de journal, suppression de journaux, obtention de journaux spécifiques, effacement de codes d'erreur, obtention de codes d'erreur de terminal et ajout de codes d'erreur)
- Identification des erreurs de connexion (affichage de la liste des événements du journal des connexions d'un terminal)
- Dernier cache d'événement (affichage du dernier événement pour un terminal spécifique)
- Opérations relatives aux demandes de gestion des terminaux (affichage de la liste des demandes de gestion des terminaux, lancement de demandes, effacement du statut d'une demande, obtention des détails d'une demande, affichage de tous les statuts de demande par terminal et obtention du statut d'une demande pour un terminal spécifique)
- Opérations de gestion de l'utilisation (extraction de la quantité totale de données utilisées)
- Publication d'événement de terminal (bêta)
- Interrogation de statut de service (extraction des statuts de service par organisation)

## Accès à la documentation de l'API REST HTTP
{: #api_link}

Pour accéder à la documentation de l'API REST HTTP {{site.data.keyword.iot_short_notm}} et obtenir davantage d'informations sur la génération et la personnalisation de vos applications, voir https://docs.internetofthings.ibmcloud.com/swagger/v0002.html.

La seule version de l'API REST HTTP {{site.data.keyword.iot_short_notm}} prise en charge est la version 2. Assurez-vous que vos solutions {{site.data.keyword.iot_short_notm}} utilisent bien la version 2.



# API de messagerie REST HTTP pour les applications
{: #rest_messaging_api}

## Publication d'événements et de commandes
{: #event_command_publication}

Outre l'utilisation du protocole de messagerie MQTT, vous pouvez également configurer vos applications pour qu'elles publient des événements et des commandes sur {{site.data.keyword.iot_short_notm}} via HTTP en exécutant l'une des commandes d'API REST HTTP suivantes :

### Demande de publication (POST) d'événement non sécurisée
<pre class="pre">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### Demande de publication (POST) d'événement sécurisée
<pre class="pre">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

**Remarque :** Le port 443, port SSL par défaut, peut également être spécifié pour les appels API HTTP sécurisés.

### Demande de publication (POST) de commande non sécurisée
<pre class="pre">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/commands/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### Demande de publication (POST) de commande sécurisée
<pre class="pre">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/commands/<var class="keyword varname">eventId</var></pre>
{: codeblock}

Si vous connectez un terminal ou une application au service Quickstart, remplacez la valeur d'**orgId** par la chaîne 'quickstart'.

**Remarques :** 
- Si les applications peuvent réutiliser une connexion HTTP pour publier des événements ou des commandes sur différents terminaux, l'en-tête HTTP d'autorisation quant à lui ne peut pas être modifié. 
- Le port 443, port SSL par défaut, peut également être spécifié pour les appels API HTTP sécurisés. 

### Authentification

Toutes les demandes doivent inclure un en-tête d'autorisation. L'authentification de base est la seule méthode prise en charge. Les applications sont authentifiées à l'aide de clés d'API. Lorsqu'une application effectue une demande via l'API REST HTTP {{site.data.keyword.iot_short_notm}}, les données d'identification suivantes sont requises :

```
username = API key (for example, a-orgId-a84ps90Ajs)
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
