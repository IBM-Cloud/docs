---

copyright:

years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# APIs
{: #api_overview}

Zum Entwickeln von Code für Geräte, Gateways und Anwendungen, die Verbindungen zu {{site.data.keyword.iot_full}} herstellen, stehen mehrere APIs zur Verfügung.

Die HTTP-APIs sind durch HTTP-Basisauthentifizierung geschützt. Wenn Sie im Dashboard einen API-Schlüssel generieren, erhalten Sie einen Schlüssel und ein Authentifizierungstoken. Weitere Informationen zu API-Schlüsseln und Token finden Sie in [Verbindung über API-Schlüssel](../platform_authorization.html#api-key).


## Informationen zu HTTP-APIs
{: #api_about}

Nachdem Sie sich für Ihre eigene Organisation registriert haben, erhalten Sie eine aus sechs Zeichen bestehende Organisations-ID, die im Hostnamen für alle HTTP-API-Aufrufe angegeben sein muss. Auf die Basis-URL für Ihre Organisation kann über die folgende Adresse zugegriffen werden:

https://<**orgId**>.internetofthings.ibmcloud.com/api/v0002

Zum Authentifizieren von Anforderungen bei der Anwendungs-API legen Sie den API-Schlüssel als Benutzernamen und das Authentifizierungstoken als Kennwort fest.

Verwenden Sie für Messaging-APIs die folgende Adresse:

https://<**orgId**>.messaging.internetofthings.ibmcloud.com/api/v0002

## HTTP-APIs
{: #api_http}

API                     | Verwendungszweck       
------------- | -------------
[Organizationsadministration ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html){: new_window} | Konfigurieren einer Organisation (einschließlich Erstellen und Löschen von Geräten), Prüfen der Verwendung und des Servicestatus und Diagnostizieren von Geräteverbindungsproblemen.
[Sicherheit ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/security.html){: new_window} | Verwalten von Benutzereinladungen, der Authentifizierung und Berechtigung von Benutzern sowie von API-Schlüsseln und Geräten.
[Information Management ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/info-mgmt.html){: new_window} |  Zugriff auf Geräteereignisdaten, Abrufen und Aktualisieren der Geräteposition sowie Abrufen von Wetterdaten für diese Position. **Hinweis:** Wetterinformationen können nur angezeigt werden, wenn 'The Weather Company'-Daten integriert sind.
[The Weather Company ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/info-mgmt.html#!/Device_Location_Weather){: new_window} | Integrieren von Daten von The Weather Company in Ihre vorhandenen Geräte.
[Gerätemanagement ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/deviceMgmt.html){: new_window} | Interagieren mit verwalteten Geräten mithilfe des Gerätemanagementprotokolls.
[Messaging ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}   | Publizieren von Ereignissen und Senden von Befehlen mithilfe von HTTP.



## Erweiterungs-HTTP-APIs
{: #api_extension}

API                     | Verwendungszweck       
------------- | -------------
[AT&T-Erweiterung ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-atnt.html){: new_window} | Verwalten von AT&T-Geräten.
[Jasper-Erweiterung  ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-jasper.html){: new_window} | Verwalten von Jasper-Geräten.
[Orange-Erweiterung ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-orange.html){: new_window} | Anzeigen von Daten der SIM-Karte von Geräten, die mit Ihrer {{site.data.keyword.iot_short_notm}}-Organisation verbunden sind und in die eine Orange-SIM-Karte installiert ist.

## Beta-HTTP-APIs
{: #api_beta}

API                     | Verwendungszweck       
------------- | -------------
[Gatewaysicherheit ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html){: new_window}   | Prüfen und Zuweisen von Rollen für Gateway-Geräte.
[Gerätesicherheit ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-devices-beta.html){: new_window} | Prüfen und Zuweisen von Rollen für Geräte.
[Schnittstellenzuordnung ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html){: new_window}   |   Zuordnen von und Zugreifen auf Gerätedaten mithilfe von Schnittstellen.
