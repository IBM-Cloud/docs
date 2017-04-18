---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# Verwendung des Gerätetoolkits
{: #iot4i_connecting_devices}
Mithilfe des {{site.data.keyword.iotinsurance_full}}-Gerätetoolkits können Sie Geräte, die von einem beliebigen Geräteanbieter hergestellt werden, mit Ihrem {{site.data.keyword.iotinsurance_short}}-Service verbinden.
{:shortdesc}

Geräte können Daten direkt an {{site.data.keyword.iot_full}} oder über die Cloud des Geräteanbieters senden. Sie verbinden Geräte durch die Registrierung berechtigter Benutzer und durch anschließende Einrichtung von Geräteereignisgenerierung und -empfang. Eine Liste der unterstützten Geräte und Anbieter sowie Beispiele für Integrationsprozeduren finden Sie im Abschnitt zu den [unterstützten Geräten und Anbietern](iotinsurance_supporteddevices.html).

Befolgen Sie für die Verbindung Ihrer Geräte die Anweisungen in den folgenden Abschnitten.

## Berechtigte Benutzer registrieren
{: #reg_users}
Wenn die Cloud des Geräteanbieters OAuth als Berechtigungsprotokoll unterstützt, kann {{site.data.keyword.iotinsurance_short}} als OAuth-Client agieren und eine Verbindung zur Cloud des Anbieters herstellen. Eine Client-ID und eine Berechtigung, die vom Geräteanbieter abgerufen werden, sind für den Empfang und die Aktualisierung von Daten seitens des Benutzers erforderlich.  

### OAuth-Ablauf
{: #oauth_flow}
Im folgenden Diagramm sehen Sie einen vereinfachten OAuth-Ablauf, bei dem {{site.data.keyword.iotinsurance_short}} über einen OAuth-Provider wie Facebook berechtigt wird. In dem Diagramm fordert {{site.data.keyword.iotinsurance_short}} Zugriff auf einen OAut-Client an, der die Zugriffsanforderung an den OAuth-Provider weiterleitet. Der Provider erstellt ein HTML-Formular, in das der {{site.data.keyword.iotinsurance_short}}-Benutzer eine Benutzer-ID und ein Kennwort eingibt. Der Provider erteilt dann die Berechtigung und gibt optional einen OAuth-Code zurück, um Aktualisierungen zu ermöglichen. Das Diagramm zeigt einen sehr einfachen Ablauf; OAuth-Provider bieten in der Regel mehrere REST-Endpunkte für die Schritte an, die in dem Diagramm aufgezeigt sind.  

![{{site.data.keyword.iotinsurance_short}}-OAuth-Prozessablauf. Dieses Diagramm wird im Textkörper des Themas beschrieben.](images/IoT4I_oauth_flow.svg "{{site.data.keyword.iotinsurance_short}}-OAuth-Prozessablauf")

### Benutzerregistrierungsablauf
{: #user_reg_flow}

Die Benutzerregistrierung variiert nach Anbieter. Informationen zum Abrufen der erforderlichen Cloudzugriffstoken sowie zu deren Registrierung in {{site.data.keyword.iotinsurance_short}} mithilfe der API finden Sie im Abschnitt zu den [unterstützten Geräten und Anbietern](iotinsurance_supporteddevices.html).

#### Ablauf einer mobilen Registrierung (*veraltet*)

**Hinweis**: Die mobile App unterstützt nur Wink; außerdem wurde durch Änderungen an {{site.data.keyword.amashort}}
der in diesem Abschnitt beschriebene Ablauf einer Benutzerregistrierung inaktiviert. Dieser Ablauf ist nur für vorhandene Instanzen der Version 1.0 von {{site.data.keyword.iotinsurance_short}} verfügbar.

Im folgenden Diagramm ist ein vereinfachter Benutzerregistrierungsablauf zu sehen. In diesem Beispiel wird eine neue Benutzerregistrierungsanforderung von einem Mobilgerät abgesetzt. Die Anforderung wird von {{site.data.keyword.amafull}} verarbeitet; diese Funktion stellt dem Kundenunterstützungssystem eine ID bereit und sendet die Anforderung an den API-Registrierungsservice. Der API-Registrierungsservice leitet die OAuth-Anforderung an die Cloud des Geräteanbieters weiter, der wiederum die Authentifizierung mit dem Kundenunterstützungssystem verifiziert. Die Cloud des Geräteanbieters gibt den Berechtigungscode oder das Token an den API-Registrierungsservice zurück. Der Registrierungsservice erstellt dann den Benutzer und ein eindeutiges API-Token in {{site.data.keyword.iot_short_notm}} und in {{site.data.keyword.cloudant}}.

![{{site.data.keyword.iotinsurance_short}}-Benutzerregistrierungsablauf. Dieses Diagramm wird im Textkörper des Themas beschrieben.](images/IoT4I_reg_user.svg "{{site.data.keyword.iotinsurance_short}}-Benutzerregistrierungsablauf")

## Geräteereignisse generieren
{: #generating_device_events}
Geräte können eine Verbindung zu {{site.data.keyword.iot_short_notm}} herstellen, wenn der Hersteller einen Code für eine direkte Berechtigung bereitstellt, der mit dem während der Benutzerregistrierung generierten API-Schlüssel verwendet werden kann. Dieser Typ von Verbindung wird im Abschnitt zum Thema [Geräte mit {{site.data.keyword.iot_short_notm}} entwickeln](https://console.{DomainName}/docs/services/IoT/devices/device_dev_index.html) beschrieben.

Wenn das Gerät über die Cloud des Anbieters verbunden ist, werden Geräteereignisse über eine Verbindung gesendet, die den vom Geräteanbieter bereitgestellten REST-Endpunkt nutzt. Das OAuth-Trägertoken, das bei der Benutzerregistrierung abgerufen wird, erteilt für diese Aufrufe eine Berechtigung. Der {{site.data.keyword.iotinsurance_short}}-Transformator entnimmt der Anbietercloud die zugeordneten Benutzerdaten für die einzelnen Geräte. Darin enthalten ist dann die Benutzerzuordnung mit den Geräteereignisdaten, die an {{site.data.keyword.iot_short_notm}} übergeben werden.

Wenn das Gerät direkt mit {{site.data.keyword.iot_short_notm}} verbunden ist, wird die Verknüpfung zwischen dem Gerät und dem Benutzer in {{site.data.keyword.iot_short_notm}} gespeichert. Der {{site.data.keyword.iotinsurance_short}}-Transformator stellt diese Informationen in den Caches und versieht Geräteereignisse dann mit der Verknüpfung zum Benutzer.

### Cloud-to-Cloud - Geräteereignisablauf
{: #device_event_flow}
Im folgenden Diagramm ist ein vereinfachter Geräteereignisablauf zu sehen. In diesem Beispiel erkennt das Gerät einen Wasserleitungsschaden. Der {{site.data.keyword.iotinsurance_short}}-Transformator setzt in regelmäßigen Abständen einen Sendeaufruf an die Anbietercloud ab, um Änderungen am Gerätestatus abzurufen. Wird das Ereignis erkannt, sendet der Transformator es an {{site.data.keyword.iot_short_notm}}. Die {{site.data.keyword.iotinsurance_short}}-Shield-Engine analysiert das Ereignis und generiert anschließend einen Alert und speichert den Alert in {{site.data.keyword.cloudant}}. {{site.data.keyword.iot_short_notm}} leitet den Alert zur Analyse an die {{site.data.keyword.iotinsurance_short}}-Aktionsengine weiter. Die Aktionsengine überträgt den Alert dann mit {{site.data.keyword.mobilepushshort}} per Push-Operation an die mobile App des Kunden.  

![{{site.data.keyword.iotinsurance_short}}-Registrierungsablauf für Geräteereignisse. Dieses Diagramm wird im Textkörper des Themas beschrieben.](images/IoT4I_device_reg.svg "{{site.data.keyword.iotinsurance_short}}Registrierungsablauf für Geräteereignisse")

### Polling für Gerätestatus einrichten
{: #device_polling}
Der Transformatormikroservice ist für das Polling und den Empfang von Statusaktualisierungen verantwortlich. Wenn die REST-API des Geräteanbieters asynchrone Geräteaktualisierungen unterstützt, können Sie eine Subskription einrichten, die es dem Transformator ermöglicht, Aktualisierungen des Gerätestatus zu empfangen, sobald diese verfügbar sind. Sie können aber auch den Transformator so einrichten, dass Aktualisierungen des Gerätestatus abgefragt werden.

Mit den folgenden Pseudofunktionsaufrufen wird der Pollingprozess definiert:

*Tabelle 1: Pseudofunktionsaufrufe*

Pseudofunktion | Beschreibung
------------- | -------------
`getRegisteredUserDevices(userName)` | Ruft die verfügbaren, registrierten Benutzergeräte ab, die den Benutzernamen verwenden.
`getProviderDevices(providerUserToken)` | Ruft die REST-API des Geräteproviders auf, um den Status von Benutzergeräten anzufordern, die das Trägertoken des Benutzers verwenden.
`findDevicesToAdd(), findDevicesToDel(), findDevicesToUpdate()` | Sucht nach neuen Geräten, nach gelöschten und geänderten Geräten, und zwar durch Vergleichen der registrierten Geräte mit Geräten, die derzeit beim Geräteprovider existieren.
` syncData()` | Synchronisiert die Benutzergeräte durch Löschen alter Geräte, durch Hinzufügen neuer Geräte und durch Aktualisieren geänderter Geräte.  
 `notifyIoTP()` | Die {{site.data.keyword.iot_short_notm}} über Änderungen wie MQTT-Ereignisse informieren.

Der Transformator sendet Statusaktualisierungen an {{site.data.keyword.iot_short_notm}}, wie im folgenden Codebeispiel dargestellt.
```
// as specified in VCAP.services
var appClientConfig = {
  "org":iot_org,
  "id":iot_appid,
  "auth-key":iot_authkey,
  "auth-token":iot_authtoken
};

var appClient = new iotclient.IotfApplication(appClientConfig);
try {
  appClient.connect();
} catch (err) {
  console.log('IoT connect failed with error' +err);
}

...

// generate IoT event, note that the content is an arbitrary JSON object  
try {
  appClient.publishDeviceEvent("iOS",userToken.username, "status", "json", JSON.stringify(iotDevice));
} catch (err) {
  console.log('IoT publish failed with error' +err +'foruser' +userToken.username);
}

```

Der Transformator nutzt {{site.data.keyword.cloudant}}, um auf Benutzerdaten wie das Trägertoken zuzugreifen und um den letzten bekannten Gerätestatus zu Vergleichszwecken zu speichern.  Die folgenden {{site.data.keyword.cloudant}}-Methoden und Codeausschnitte dienen zur Referenz.  

`getUserTokensByProvider` - Mit dieser Methode werden alle Benutzertoken eines bestimmten Providers abgerufen.

```
dbHelper.getUserTokensByProvider(provider, function (err,results) {
  if (!err) {
    console.log(results.token.length + " tokens retrieved for provider: " + Provider);
  } else {
    console.log("no tokens returned, err:",err);
  }
  });
```

`getDevicesByUser` - Mit dieser Methode werden alle registrierten Benutzergeräte nach Benutzername abgerufen.
```
dbHelper.getDevicesByUser(username, function (err,results) {
  if (!err) {
    console.log(results.length + " devices retrieved for username: " + username);
  } else {
    console.log("no devices returned, err:",err);
  }
  });
```

`bulkUpdateDevices` - Mit dieser Methode wird eine Gruppe von Benutzergeräten aktualisiert oder hinzugefügt.
```
dbHelper.bulkUpdateDevices(userDevices, function (err,results) {
  if (!err) {
    console.log(results.length + " devices updated");
    } else {
      console.log("no devices updated, err:",err);
    }
  });
```

`bulkDelDevices` - Mit dieser Methode wird eine Gruppe von Benutzergeräten gelöscht.
```
dbhelper.bulkDelDevices(userDevices, function (err, results) {
  if (!err) {
    console.log(results.length + "devices deleted");
  } else {
    console.log("no devices deleted, err:",err);
  }
  });

```


## Neue Transformatorinstanz bereitstellen
{: #deploy_new_transformer}
Sie können eine neue Transformatorinstanz in derselben Organisation und im selben Bereich bereitstellen, in dem auch {{site.data.keyword.iotinsurance_short}} bereitgestellt ist.  

**Hinweis:** Informationen und Unterstützung zur Bereitstellung einer neuen Transformerinstanz finden Sie im Abschnitt zur [Kontaktaufnahme mit dem Support](../support/index.html#contacting-support).

Bevor Sie beginnen, müssen Sie die Cloud Foundry-Befehlszeilenschnittstelle herunterladen und installieren. Verwenden Sie die Cloud Foundry-Befehlszeilenschnittstelle, um Serviceinstanzen für {{site.data.keyword.iot_short_notm}} zu ändern und bereitzustellen. Weitere Informationen finden Sie im Thema zum [Starten der Codierung mit der CF-Befehlszeilenschnittstelle ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://www.ng.bluemix.net/docs/#starters/install_cli.html){:new_window}.

1. Wechseln Sie in der Befehlszeilenschnittstelle mithilfe des folgenden Befehls zum `Verzeichnis mit Quellen und YML-Datei des Bereitstellungsdeskriptors`:
```
$ cd directory_name
```
2. Listen Sie alle Apps in {{site.data.keyword.iotinsurance_short}} auf und notieren Sie sich den Namen des Transformators. Der Name endet mit `transformer`.

3. Stoppen Sie den {{site.data.keyword.iotinsurance_short}}-Transformator. Beispiel:
```
$ cf stop iot4i-dev-transformer
```
4. Listen Sie alle Services in {{site.data.keyword.iotinsurance_short}} auf und notieren Sie sich die Namen der {{site.data.keyword.iot_short_notm}}- und {{site.data.keyword.cloudant}}-Services.  Der Name der {{site.data.keyword.iot_short_notm}}-Services enthält die Buchstaben `iotf`. Der Name des {{site.data.keyword.cloudant}}-Service enthält die Zeichenfolge `cloudant`.

5. Erstellen Sie mithilfe der in den vorherigen Schritten notierten Namen eine Bereitstellungsdeskriptordatei, die der im folgenden Beispiel ähnlich ist.  
  ```
  applications:
  - path: .
    memory: 1024M
    instances: 1
    name: iot4i-dev-transformer
    no-route: false
    disk_quota: 1024M
    command: node index.js
    services:
    - iot4i-iotf-service
    - iot4i-cloudantNoSQLDB
    env:
       ENV: dev
       APIDOMAIN: iot4insurance-api-v.mybluemix.net
       NODE_MODULES_CACHE: false
  ```
6. Übertragen Sie mithilfe des folgenden Befehls Ihren Transformator per Push-Operation an {{site.data.keyword.Bluemix_notm}} und ersetzen Sie `newtransformer` durch den Namen Ihrer Bereitstellungsdeskriptordatei:
  ```
  $ cf push -f newtransformer.yml
  ```
7. Mithilfe des folgenden Befehls können Sie die Protokolle überprüfen, um die Bereitstellungsnachrichten anzuzeigen:
  ```
  $ cf logs iot4i-dev-transformer
  ```
