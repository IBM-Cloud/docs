---

copyright:
 years: 2015, 2017
lastupdated: "2017-03-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# API de messagerie HTTP pour les terminaux de passerelle (bêta)
{: #api}

**Important :** L'API HTTP {{site.data.keyword.iot_full}} pour les terminaux de passerelle est disponible uniquement dans le cadre d'un programme bêta limité. Il est possible que des mises à jour ultérieures incluent des modifications incompatibles avec la version en cours de cette fonction. Essayez-la et [dites-nous ce que vous en pensez ![ ](../../../icons/launch-glyph.svg)](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html){: new_window}.

## Accès à la documentation de l'API de messagerie HTTP pour les terminaux de passerelle
{: #rest_messaging_api}

Pour accéder à la documentation de l'API de messagerie HTTP {{site.data.keyword.iot_short_notm}} et obtenir davantage d'informations sur l'envoi d'événements à partir de terminaux de passerelle, voir [{{site.data.keyword.iot_short_notm}} HTTP Messaging API ![ ](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}.


## Connexions client
{: #client_connections}

Pour plus d'informations sur la sécurité du client et pour savoir comment connecter des terminaux de passerelle dans {{site.data.keyword.iot_short_notm}}, voir [Connexion d'applications, de terminaux et de passerelles à {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).


## Publication d'événements
{: #event_publication}

Outre l'utilisation du protocole de messagerie MQTT, vous pouvez également configurer vos terminaux de passerelle pour qu'ils publient des événements sur {{site.data.keyword.iot_short_notm}} via HTTP en exécutant des commandes d'API de messagerie HTTP.

Pour soumettre une demande `POST` à partir d'un terminal connecté à {{site.data.keyword.iot_short_notm}}, utilisez l'une des URL suivantes :

### Demande POST non sécurisée
<pre class="pre"><code class="hljs">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

### Demande POST sécurisée
<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

**Remarques importantes :**
- Vous ne pouvez soumettre des événements de terminal de passerelle qu'en utilisant la messagerie HTTP. Utilisez le protocole de messagerie MQTT afin de soumettre des demandes pour d'autres fonctions de contrôle et de gestion des terminaux de passerelle.
- Les connexions HTTP peuvent être réutilisées uniquement afin de publier des événements pour le même terminal, car l'en-tête HTTP d'autorisation ne peut pas être modifié.
- Le port 443, port SSL par défaut, peut également être spécifié pour les appels API HTTP sécurisés.
- Si le rôle *Passerelle standard* n'est pas affecté à une passerelle, celle-ci peut publier des événements pour le compte d'autres terminaux de l'organisation. Affectez le rôle *Passerelle standard* si vous souhaitez vérifier les niveaux d'autorisation de terminal et enregistrer automatiquement votre terminal. **Remarque :** Ce comportement est susceptible d'être modifié. 

Pour plus d'informations sur le rôle de passerelles et de groupes de ressources, voir [Contrôle d'accès des passerelles (bêta)](../gateways/gateway-access-control.html).

### Authentification

Toutes les demandes doivent inclure un en-tête d'autorisation. L'authentification de base est la seule méthode prise en charge. Lorsqu'un terminal effectue une demande HTTP via l'API REST HTTP {{site.data.keyword.iot_short_notm}}, les données d'identification suivantes sont requises :

|Données d'identification|Entrée requise|
|:---|:---|
|Nom d'utilisateur| `g/{orgId}/{gwType}/{gwDevId}` or `g-{orgId}-{gwType}-{gwDevId}`
|Mot de passe| Jeton d'authentification qui a été généré automatiquement ou que vous avez spécifié manuellement lors de l'enregistrement du terminal de passerelle.


Où :

<dl>
<dt>orgId</dt>  
<dd>Nom de l'organisation, qui doit correspondre au nom qui est spécifié dans l'en-tête d'hôte. </dd>

<p></p>
<dt>gwType</dt>  
<dd>Type de passerelle. </dd>
<dd>Si vous utilisez le caractère "-" comme délimiteur dans le nom d'utilisateur, cette valeur ne doit pas inclure de trait d'union. </dd>
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

### Qualité de service

Semblable au niveau 0 ("Une fois tout au plus") de la qualité de service MQTT pour la distribution, la messagerie REST HTTP fournit une distribution de message non permanente, mais vérifie que la demande est correcte et qu'elle peut être distribuée au serveur avant que celui-ci n'envoie la réponse HTTP. Une réponse contenant le code de statut HTTP 200 indique que le message a bien été distribué au serveur. Lorsque vous utilisez le niveau de qualité de service MQTT "Une fois tout au plus" ou l'équivalent HTTP pour distribuer des messages d'événement, le terminal ou l'application doit implémenter une logique de relance afin de garantir la distribution.

Pour plus d'informations sur le protocole MQTT et les niveaux de qualité de service pour {{site.data.keyword.iot_short_notm}}, voir [Messagerie MQTT](../reference/mqtt/index.html).

Pour plus d'informations sur la gestion d'événements de passerelle à l'aide d'API, voir [API REST HTTP pour les terminaux de passerelle](../gateways/gw_api.html).
