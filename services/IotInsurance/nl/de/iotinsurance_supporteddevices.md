---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-07"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Unterstützte Geräte und Anbieter
{: #supportedcloud}

{{site.data.keyword.iotinsurance_full}} unterstützt die Integration mit mehreren Cloudanbietern und Geräten.
{: shortdesc}

## Unterstützte Geräte nach Anbieter
{: #supportedvendors}
In der folgenden Tabelle sind die Anbieter und Geräte aufgeführt, die von {{site.data.keyword.iotinsurance_short}} unterstützt werden; außerdem wird der jeweilige Integrationstyp beschrieben. Die folgenden Integrationstypen sind verfügbar:

  - **{{site.data.keyword.iot_short_notm}}** - Das Gerät oder der Hub veröffentlicht die Sensorereignisse direkt in {{site.data.keyword.iot_short_notm}}. {{site.data.keyword.iotinsurance_short}} kann die Sensorereignisse entweder direkt oder nach einer geringfügigen Änderung durch den {{site.data.keyword.iotinsurance_short}} Transformer verarbeiten.

  - **Cloud-to-Cloud** - Das Gerät oder der Hub veröffentlicht die Sensorereignisse in der Cloud eines Drittanbieters. Der {{site.data.keyword.iotinsurance_short}} Transformer liest diese Ereignisse aus der Cloud des Drittanbieters und veröffentlicht sie in {{site.data.keyword.iot_short_notm}}.

<table>
<thead>
<tr>
<th>Anbietername</th>
<th>Integrationstyp</th>
<th>Getestete Geräte</th>
<th>Anbieterinformationen </th>
</tr>
</thead>
<tbody>
<tr>
<td>Bosch E-Call</td>
<td>{{site.data.keyword.iot_short_notm}}.  
Zum Testen der Integration wurde eine Gateway-App geschrieben.</td>
<td>Bosch Retrofit E-Call</td>
<td>[Anbieterwebsite ![Symbol für externen Link](../../icons/launch-glyph.svg)](http://www.bosch-connectivity.com/en/what_we_offer/products_and_solutions_1/retrofit_ecall/connected_devices_3){: new_window}</td>
</tr>
<tr>
<td>EnOcean</td>
<td>{{site.data.keyword.iot_short_notm}}</td>
<td>
<ul>
<li>Schaltfläche</li>
<li>Kontakt</li>
<li>Temperatur</li>
</ul>
</td>
<td>[Anbieterwebsite ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://www.enocean.com/en/</td>){: new_window}
</tr>
<tr>
<td>WiButler (iExergy)</td>
<td>{{site.data.keyword.iot_short_notm}}</td>
<td>
<ul>
<li>Rauchmelder</li>
<li>Schaltfläche</li></td>
</ul>
<td>[Anbieterwebsite ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://www.wibutler.com/en_GB){: new_window}</td>
</tr>
<tr>
<td>Wink</td>
<td>Cloud-to-Cloud</td>
<td>Wasserleitungsschaden</td>
<td>[Anbieterwebsite ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://www.wink.com/){: new_window}</td>
</tr>
<tr>
<td>Yanzi</td>
<td>{{site.data.keyword.iot_short_notm}} und Cloud-to-Cloud</td>
<td>Es wurden keine Sensoren getestet.</td>
<td>[Anbieterwebsite ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://ibm.ent.box.com/notes/126680846739){: new_window}</td>
</tr>
</tbody>
</table>

## Geräte und Anbieterclouds integrieren
{: #integratingdevices}
Sie können Ihre Geräte und Anbieterclouds mit {{site.data.keyword.iotinsurance_short}} integrieren. In den folgenden Abschnitten sind Prozeduren zur Integration sowie Beispiele für Benutzerdatensätze für die einzelnen Anbieter enthalten.

Weitere Informationen zur Integration von Sensoren und Geräten finden Sie im Abschnitt zum [Gerätetoolkit](iotinsurance_device_toolkit.html):


### EnOcean
#### Integrationsprozedur
  1. Erstellen Sie ein Gateway in der {{site.data.keyword.iot_short_notm}}-Instanz, wobei eine Verbindung zu {{site.data.keyword.iotinsurance_short}} besteht.
  2. Stellen Sie eine Verbindung zwischen dem EnOcean-Hub und dem {{site.data.keyword.iot_short_notm}}-Gateway her.
  3. Fügen Sie die Gateway-ID zum Benutzerdatensatz in {{site.data.keyword.iotinsurance_short}} hinzu.

#### Beispiel für Benutzerdatensatz

```
{
    "username": "user@example.com",
    "password": "",
    "accessLevel": "13",
    "fullname": "John Doe",
    "email": "user@example.com",
    "phonenumber": "+123456789",
    "address": {
      ...
    },
    "gatewayIds": [
      "digital-concepts-gateway1"
    ],
    ...
}
```

### WiButler (iExergy)

#### Integrationsprozedur
Die Integration mit WiButler-Daten wird derzeit nur als Konzeptnachweis bzw. technische Neuentwicklung unterstützt und ist nicht für den Einsatz in der Produktion gedacht. Für die WiButler-Hardware ist eine Firmware-Update erforderlich, um Daten an die {{site.data.keyword.iot_short_notm}} zu streamen.

#### Beispiel für Benutzerdatensatz

```
{
    "username": "user@example.com",
    "password": "",
    "accessLevel": "13",
    "fullname": "John Doe",
    "email": "user@example.com",
    "phonenumber": "+123456789",
    "address": {
      ...
    },
    "gatewayIds": [
      "Wibutler-Gateway-ID"
    ],
    ...
}
```

### Wink

#### Integrationsprozedur

**Option 1**
  1. Rufen Sie die [Wink-Berechtigungstoken ![Symbol für externen Link](../../icons/launch-glyph.svg)](http://docs.winkapiv2.apiary.io/#){: new_window} ab.
  2. Fügen Sie das Berechtigungstoken zum entsprechenden Benutzer im {{site.data.keyword.iotinsurance_short}}-System hinzu; verwenden Sie hierfür die {{site.data.keyword.iotinsurance_short}}-API.

**Option 2**  
Die Integration wird mithilfe der mobilen App durchgeführt (veraltet). Diese Methode funktioniert nur mit Version 1.0 von {{site.data.keyword.iotinsurance_short}}.

#### Beispiel für Benutzerdatensatz

```
{
  "username": "user@example.com",
  "password": "",
  ....
  "deviceID": "528DB5CA-7F3D-4478-A4EB-994E7F118B6B",
  "assets": [
    {
      "name": "default",
      "providers": [
        {
          "name": "wink",
          "tokens": {
            "data": {
              "access_token": "fjyw9nN_YhU-fZU9kCqTQ6Ijsr_9XdvO",
              "refresh_token": "OOMyB8JGCHgjOHku8zp2Yrevoeci48Ou",
              "token_type": "bearer",
              "token_endpoint": "https://api.wink.com/oauth2/token",
              "scopes": "full_access"
            },
            "errors": [],
            "pagination": {},
            "access_token": "fjyw9nN_YhU-fZU9kCqTQ6Ijsr_9XdvO",
            "refresh_token": "OOMyB8JGCHgjOHku8zp2Yrevoeci48Ou",
            "token_type": "bearer",
            "token_endpoint": "https://api.wink.com/oauth2/token",
            "scopes": "full_access"
          }
        }
      ]
    }
  ]
}

```

### Yanzi
#### Integrationsprozedur
**Option 1**  
  Fügen Sie Berechtigungsnachweise der Yanzi-Cloud zur Datei yanzi-config.json im Verzeichnis des Providers des Transformerrepositorys hinzu.  Das Objekt "yanziCloud" ist die richtige Position der Berechtigungsnachweise.  

**Option 2**  
  Yanzi nutzt die Cloud-to-Cloud-Integration zwischen der Yanzi-Cloud und der {{site.data.keyword.iot_short_notm}}. Zu der Berechtigung für diese Integration kommt es in der Yanzi-Cloud. Nachdem die Berechtigung ausgeführt wurde, sendet die Yanzi-Cloud Ereignisse an {{site.data.keyword.iot_short_notm}}. Sie müssen auch die Berechtigungsnachweise der {{site.data.keyword.iot_short_notm}}-Instanz zur Datei yanzi-config.json im Verzeichnis des Providers des Transformerrepositorys hinzufügen, und zwar mithilfe des Objekts "iotfCredentials".

#### Beispiel für Benutzerdatensatz

```
{
  "yanziCloud": {
      "cirrusHost": "wss://",
      "username": "",
      "password": "",
      "locationId": "",
      "unitDid": ""
  },
  "iotfCredentials": {
      "org": "",
      "apiKey": "",
      "apiToken": "",
      "type": "shared",
      "mqtt_host": "gbdprt.messaging.internetofthings.ibmcloud.com",
      "domain": "internetofthings.ibmcloud.com"
  }
}
```

### Weather Company Data
#### Integrationsprozedur
Die Integration mit Weather Company Data wird derzeit nur als Konzeptnachweis bzw. technische Neuentwicklung unterstützt und ist nicht für den Einsatz in der Produktion gedacht.

Geben Sie eine Adresse zum Abrufen der aktuellen Wetterdaten (Außentemperatur) der Weather Company für einen bestimmten Standort an.



#### Beispiel für Benutzerdatensatz

```
{ "username": "johndoe",
   "fullname": "John Doe",
    "firstname": "John",
    "lastname": "Doe",
    "password": "",
     "accessLevel": 13,
     "address": "Mies-van-der-Rohe-Straße 6, 80807 München, Germany",
     ...
}

```
