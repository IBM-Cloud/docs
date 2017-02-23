---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-28"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
# Normes et exigences
{: #standards_and_requirements}

{{site.data.keyword.iot_full}} prend en charge un certain nombre de normes et d'exigences pour la messagerie et le développement général de terminaux et d'applications.
{:shortdesc}


<!-- ## Blockchain
{: #blockchain}

{{site.data.keyword.iot_short_notm}} supports the following versions of the Hyperledger fabric:
- 0.5

## Python
{: #python}

Support for MQTT over SSL requires at least Python v2.7.9 or v3.4, and OpenSSL v1.0.1.
-->

## MQTT
{: #mqtt}

{{site.data.keyword.iot_short_notm}} prend en charge les versions suivantes du protocole de messagerie MQTT :

Version MQTT | Notes
--- | --- | ---
[3.1.1](https://www.oasis-open.org/standards#mqttv3.1.1) (recommandé)  | <ul><li>Norme  OASIS.<li>Norme ISO (ISO/IEC PRF 20922) <li>Interopérabilité améliorée entre plusieurs clients et serveurs en raison d'une définition plus précise du protocole par rapport à la version 3.1. <li>La longueur maximale de l'identificateur de client MQTT (CientId) passe de 23 caractères (nombre imposé par la version 3.1) à 256 caractères. </br>Le service {{site.data.keyword.iot_short_notm}} requiert souvent des ID de client plus longs. </br>Les ID clients longs sont pris en charge quelle que soit la version du protocole MQTT. Toutefois, certaines bibliothèques client de la version 3.1 vérifient la longueur de la valeur ClientId et imposent un nombre limite de caractères égal à 23.</ul>
3.1 | MQTT V3.1 est la version du protocole la plus utilisée.

{{site.data.keyword.iot_short_notm}} prend en charge tout contenu autorisé par la norme MQTT. MQTT est indépendant des données, par conséquent, il est possible d'envoyer des images, des textes dans n'importe quel codage, des données chiffrées et pratiquement tout type de données au format binaire. Pour plus d'informations sur les normes MQTT, voir les ressources suivantes :
- [MQTT.org](http://mqtt.org/)
- [HiveMQ: Introducing MQTT](http://www.hivemq.com/blog/mqtt-essentials-part-1-introducing-mqtt)

Pour plus d'informations sur les limites de taille de la charge de message et les restrictions de format pour les cas d'utilisation spécifiques pour {{site.data.keyword.iot_short_notm}}, voir [Messagerie MQTT](mqtt/index.html).
