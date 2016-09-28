---

copyright:
  years: 2014, 2016

---

{:new_window: target="_blank"}

# Einführung in {{site.data.keyword.objectstorageshort}}  {: #using-object-storage}

*Letzte Aktualisierung: 13. August 2016*
{: .last-updated}


## {{site.data.keyword.objectstorageshort}}-Benutzerschnittstelle verwenden {: #using-object-storage-ui}

### Benutzerschnittstelle - Elemente und Navigation
Wenn Ihr {{site.data.keyword.objectstorageshort}} bereitgestellt wurde, können Sie die Informationen zu Ihrer Instanz im {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}}-Dashboard für Serviceinstanzen anzeigen. Wählen Sie im Dashboard Ihre {{site.data.keyword.objectstorageshort}}-Instanz aus, um den Fensterbereich mit ausführlicheren Informationen anzuzeigen.  
#### Nutzungsdaten
Auf der Startseite Ihrer Anwendung sehen Sie die Informationen zur Speicherbelegung für Ihre Instanz. Außerdem wird die aktuelle Anzahl der **Speichercontainer** und die Gesamtzahl der **Objekte** in allen Containern angezeigt, über die Sie verfügen. Ihre Speicherbelegung wird in Megabyte angegeben. **Belegter Speicher** bezieht sich auf die aktuelle Größe des Speicherplatzes, der belegt ist.
#### Aktionen
Klicken Sie auf die Schaltfläche **Aktualisieren**, um die aktuellsten Nutzungsdaten abzurufen.   
####Objektbrowser
Verwenden Sie den Objektbrowser, um Object Storage-Container und -Objekte zu verwalten. Sie können Container erstellen, Dateien hochladen, Container löschen, Dateien löschen und andere Aktionen ausführen.


## {{site.data.keyword.objectstorageshort}} über eine {{site.data.keyword.Bluemix_notm}}-App verwenden {: #using-object-storage-from-bluemix-app}

### Vorgehensweise zum Binden eines {{site.data.keyword.objectstorageshort}}-Service an eine Anwendung nach der Erstellung {: #bind-object-storage-to-application}
1.	Wählen Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard die App aus, die Sie binden möchten.
2.	Klicken Sie in der App-Übersicht auf **Service oder API binden**.
3.	Wählen Sie in der Liste der Services Ihre {{site.data.keyword.objectstorageshort}}-Instanz aus und klicken Sie auf **Hinzufügen**.
4.	Klicken Sie auf **Erneutes Staging**, wenn Sie dazu aufgefordert werden. Für die Verwendung des neuen Service ist für Ihre App ein erneutes Staging erforderlich.

### Gebundener Kontext

Wenn Sie {{site.data.keyword.objectstorageshort}} in einem gebundenen Kontext verwenden möchten, werden die Berechtigungsnachweise für die Cloud indirekt über den Anwendungsbindungsprozess bereitgestellt. Nach der erfolgreichen Bindung einer Serviceinstanz an Ihre Anwendung wird eine Konfiguration ähnlich der folgenden Beispielkonfiguration der Umgebungsvariablen `VCAP_SERVICES` hinzugefügt.

```
{
"Object-Storage": [
    {
  "name": "Object-Storage - YP",
      "label": "Object-Storage",
      "plan": "Free",
      "credentials": {
     "auth_url": "https://identity.open.softlayer.com",
         "project": "object_storage_d049255b",
         "projectId": "0f47b41b06d047f9aae3b33f1db061ed",
         "region": "dallas",
         "userId": "ad78b2a3f843466988afd077731c61fc",
         "username": "user_202db1f8a7aa3f3ac51ec68f10dbe7dc29070bc7",
         "password": "K/jyIi2jR=1?D.TP",
         "domainId": "2df6373c549e49f8973fb6d22ab18c1a",
         "domainName": "639347"
        }
   }
  ]
}
```

## Swift-Befehlszeilenschnittstelle (CLI) für den Zugriff auf {{site.data.keyword.objectstorageshort}} verwenden {: #using-swift-cli}

Sie können auf den {{site.data.keyword.objectstorageshort}}-Service über das Internet und durch Anwendungen und virtuelle Server in IBM {{site.data.keyword.Bluemix_notm}} zugreifen. Häufige Anwendungsfälle für den {{site.data.keyword.objectstorageshort}}-Service sind zum Beispiel:

* Sicherung durch Backups von Datenträgerdaten aus Ihren Instanzen
* Verwendung als Zwischenspeicherposition bei der Übertragung umfangreicher Datenvolumen
* Übertragung von Daten zwischen Umgebungen, die nicht direkt verbunden sind
* Einsatz als zentrales Repository

Der {{site.data.keyword.objectstorageshort}}-Service basiert auf OpenStack Swift und ist für jede beliebige kompatible Clientanwendung zugänglich. In diesem Abschnitt wird die Verwendung des Python Swift-Clients beschrieben. Dies ist die Befehlszeilenschnittstelle (CLI, Command-Line Interface) für die {{site.data.keyword.objectstorageshort}}-API und die zugehörigen Erweiterungen für die Arbeit mit Containern und Dateien.

### Swift-Client installieren {: #install-swift-client}

Installieren Sie die folgenden Softwarevoraussetzungen, falls diese noch nicht installiert sind. Weitere Informationen finden Sie in der [OpenStack-Dokumentation](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}.
* Python 2.7 oder höher
* Setuptools-Paket
* Pip-Paket

Installieren Sie den Python Swift-Client mithilfe von Python-pip:

```
	sudo pip install python-swiftclient
```

Installieren Sie den Python Keystone-Client, indem Sie den folgenden Befehl ausführen:

```
	sudo pip install python-keystoneclient
```

### Client einrichten {: #setup-swift-client}

Der Swift-Client entnimmt die Authentifizierungsinformationen den folgenden Umgebungsvariablen:
* `OS_AUTH_URL` ist die Endpunkt-URL.
* `OS_USER_ID` ist der Benutzername.
* `OS_PASSWORD` ist das Kennwort.

Legen Sie die Authentifizierungsinformationen wie folgt fest.

```
export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
export OS_PASSWORD=aaa55AAAaaaaa]?,
export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
export OS_AUTH_URL=https://identity.open.softlayer.com/v3
export OS_REGION_NAME=dallas
export OS_IDENTITY_API_VERSION=3
export OS_AUTH_VERSION=3
```

Sie finden die Werte für die Berechtigungsnachweise für Ihren {{site.data.keyword.objectstorageshort}}-Service auf der Seite **Serviceberechtigungsnachweise** in der {{site.data.keyword.objectstorageshort}}-Benutzerschnittstelle.

**Anmerkung:** Stellen Sie sicher, dass Sie dem Wert von `auth_url` aus den Berechtigungsnachweisen in der {{site.data.keyword.objectstorageshort}}-Benutzerschnittstelle den Wert `/v3` hinzufügen, wenn Sie die Umgebungsvariablen `OS_AUTH_URL` für den Swift-Client konfigurieren.


### Mit Containern arbeiten {: #work-with-containers}

Container auflisten:
```
	swift list
```
Container erstellen:
```
	swift post <Containername>
```
Inhalt eines Containers auflisten:
```
	swift list <Containername>
```
### Mit Objekten arbeiten {: #work-with-objects}

#### Datei einem Container hinzufügen
```
	swift upload <Containername> <Dateiname>
```
#### Dateien mit einer Größe über 5 GB einem Container hinzufügen

Wenn Sie eine Datei hochladen, die größer als 5 GB ist, müssen Sie sie in kleinere Segmente aufteilen. Sie können den Swift-Client durch Angabe des Parameters `-segment-size` anweisen, eine solche Hochladeoperation durchzuführen:
```
	swift upload <Containername> <Dateiname> --segment-size <Größe_in_Byte>
```
Jedes Segment wird parallel in einen separaten Container mit dem Namen `<Containername>_segments` hochgeladen. Nach dem Hochladen aller Segmente erstellt Swift eine Manifestdatei, sodass die Segmente in eine einzige Datei aus dem ursprünglichen Container `<Containername>` mit dem ursprünglichen Dateinamen `<Dateiname>` heruntergeladen werden können.

Beispiel: Mit dem folgenden Befehl wird eine Datei mit dem Namen `large_file` aus einem Container mit dem Namen `test_container` mit der Segmentgröße `1073741824` hochgeladen.
```
	swift upload test_container -S 1073741824 large_file
```
Sie können den folgenden Befehl ausführen, um die Datei herunterzuladen:
```
	swift download test_container large_file
```
#### Datei herunterladen
```
	swift download <Containername> <Dateiname>
```
#### Verzeichnis einem Container hinzufügen

Swift hat keine eigentliche Verzeichnisstruktur, verwendet jedoch eine entsprechende Benennung, um eine Verzeichnisstruktur darzustellen. Führen Sie den folgenden Befehl aus, um einem Container ein Verzeichnis hinzuzufügen:
```
	swift upload <Containername> <Verzeichnisname>
```
Durch diesen Befehl wird eine vollständige Verzeichnisstruktur als relativer Pfad hochgeladen. Beispiel: Wenn Sie `/mnt/volume1` angeben, wird die Verzeichnisstruktur 'mnt/volume1' an alle Dateinamen angefügt, um die Verzeichnisstruktur anzugeben.


#### Verzeichnis herunterladen

Zum Herunterladen einer Verzeichnisstruktur verwenden Sie den Parameter `-prefix`, um das Verzeichnis bzw. die Verzeichnisstruktur anzugeben, das/die heruntergeladen werden soll.
```
	swift download <Containername> --prefix <Verzeichnis>
```
#### Datei löschen
```
	swift delete <Containername> <Dateiname>
```
### Mit Objektversionierung arbeiten {: #work-with-object-versioning}

Sie können unter Verwendung des Flags `X-Versions-Location` Versionen jedes Objekts in Ihrem Container einrichten. Erstellen Sie hierfür wie folgt einen weiteren Container, um ältere Versionen Ihrer Objekte aufzubewahren.

Bei der Verwendung des Swift-Clients können Sie die Einrichtung wie folgt vornehmen:
```
	swift post container_one -H "X-Versions-Location:container_two"
```
Bei der Verwendung von curl können Sie die Einrichtung wie folgt vornehmen:
```
	curl -i -X PUT -H "X-Auth-Token: <Token>" -H "X-Versions-Location:container_two" https://<Objektspeicher-URL>/container_one
```
In diesem Beispiel wurde `container_two` so eingerichtet, dass er die älteren Versionen Ihrer Objekte enthält, die in `container_one` gespeichert sind. Daher enthält `container_one` die aktuelle Version Ihrer Objekte, `container_two` enthält die älteren Versionen Ihrer Objekte. Stellen Sie sicher, dass `container_two` existiert, damit die Versionierung funktioniert.

Bei eingerichteter Versionierung wird die bereits vorhandene Version beim Hochladen eines Objekts in `container_one`, sofern es eine bereits vorhandene Version gibt, nach `container_two` verschoben, da die neue Version in `container_one` erstellt wird. Wenn Sie ein Objekt aus `container_one` löschen, wird die vorherige Version des Objekts von `container_two` wieder nach `container_one` verschoben.

Objekte in `container_two` werden automatisch im folgenden Format benannt: `<Länge><Objektname>/<Zeitmarke>`.

`Länge` bezieht sich dabei auf die Länge des Namens Ihres Objekts; dies ist eine aus drei Zeichen bestehende Hexadezimalzahl ohne Innenabstand. `Objektname` ist der Name Ihres Objekts. `Zeitmarke` ist die Zeitmarke des ursprünglichen Uploads dieser jeweiligen Version.

Verwenden Sie für die Inaktivierung der Versionierung das Flag `X-Remove-Versions-Location`:
```
	swift post container_one -H "X-Remove-Versions-Location:"
```
oder
```
	cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<Objektspeicher-URL>/container_one
```
Im Folgenden sehen Sie ein vollständiges Beispiel für die Nutzung der Versionierung:

1. Container erstellen:
```
		$ swift post container_one
		$
```
2. Versionierung für container_one einrichten:
```
		$ swift post container_one -H "X-Versions-Location:container_two"
		$
```
3. container_two erstellen:
```
		$ swift post container_two
		$
```
4. Objekt zum ersten Mal nach container_one hochladen:
```
		$ swift upload container_one object
		object
		$
```
5. Objekte in container_one auflisten:
```
		$ swift list container_one
		object
		$
```
6. Objekte in container_two auflisten:
```
		$ swift list container_two
		$
```
7. Neue Version des Objekts nach container_one hochladen:
```
		$ swift upload container_one object
		object
		$
```
8. Objekte in container_one auflisten:
```
		$ swift list container_one
		object
		$
```
9. Objekte in container_two auflisten:
```
		$ swift list container_two
		006object/1457456909.27383
		$
```
10. Objekt in container_one löschen:
```
		$ swift delete container_one object
		object
		$
```
11. Beide Container auflisten:
```
		$ swift list container_one
		object
		$ swift list container_two
		$
```

### Objektlöschung planen {: #schedule-object-deletion}

Sie können für Ihre Objekte festlegen, dass diese in einer angegebenen Zeitdauer ablaufen sollen. Das heißt, Sie können die Löschung Ihrer Objekte planen. Hierfür können Sie den Header `X-Delete-At` oder `X-Delete-After` verwenden. Der Wert für den Header `X-Delete-At` ist eine ganze Zahl, die die Referenzzeit darstellt, zu der das Objekt gelöscht werden soll. Der Wert für den Header `X-Delete_After` ist eine ganze Zahl, die die Anzahl an Sekunden darstellt, nach deren Ablauf das Objekt gelöscht wird.

Die folgenden Beispiele zeigen die Vorgehensweise, wenn Sie den Swift-Client für einen Post an das Objekt in Ihrem Container verwenden.

* Verwenden Sie den folgenden Befehl, um für das Objekt den Löschzeitpunkt auf "2016/04/01 08:00:00" festzulegen:
```
		swift post -H "X-Delete-At:1459515600" container object
```
* Verwenden Sie den folgenden Befehl, um für das Objekt festzulegen, dass es eine Stunde nach dem aktuellen Zeitpunkt gelöscht werden soll:
```
		swift post -H "X-Delete-After:3600" container object
```
  Anschließend wird durch den Befehl `swift stat container object` der Header `X-Delete-At` mit dem entsprechenden Ablaufdatum in der Referenzzeit angezeigt.

* Verwenden Sie den folgenden Befehl, um die Ablaufzeit aus Ihrem Objekt zu entfernen:
```
		swift post -H "X-Remove-Delete-After:" container object
```
Bei der Verwendung von cURL sehen die Befehle wie folgt aus:

* Verwenden Sie den folgenden Befehl, um für das Objekt den Löschzeitpunkt auf "2016/04/01 08:00:00" festzulegen:
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:1459515600" https://<Objektspeicher-URL>/container/object
```
* Verwenden Sie den folgenden Befehl, um für das Objekt festzulegen, dass es eine Stunde nach dem aktuellen Zeitpunkt gelöscht werden soll:
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:3600" https://<Objektspeicher-URL>/container/object
```
* Verwenden Sie den folgenden Befehl, um zu prüfen, ob das Objekt den Header aufweist:
```
		cURL -I -H "X-Auth-Token: <token>" https://<Objektspeicher-URL>/container/object
```
* Verwenden Sie den folgenden Befehl, um die Ablaufzeit zu entfernen:
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:" https://<Objektspeicher-URL>/container/object
```
**Anmerkung:** Die tatsächliche Löschung eines Objekts erfolgt möglicherweise nicht genau zur angegebenen Uhrzeit. Das Objekt läuft jedoch de facto zur angegebenen Zeit ab, d. h., es ist nicht mehr erreichbar. Die tatsächliche Löschung findet bei der nächsten Ausführung des in Ihrem Swift-Cluster konfigurierten Dämons 'swift-object-expirer' statt.





### Temporäre URL erstellen {: #create-temporary-url}

Eine temporäre URL ist eine lange, schwer zu erratende URL, die für einen angegebenen Zeitraum zum Herunterladen von Objekten verwendet werden kann, ohne dass eine weitere Authentifizierung erforderlich ist. Sie generieren eine temporäre URL mit den folgenden Schritten:

1. Geben Sie Ihr Authentifizierungskonto an.
2. Legen Sie einen geheimen Schlüssel fest.
3. Erstellen Sie eine temporäre URL.

#### Authentifizierungskonto angeben

Der Swift-Befehl `stat` gibt Informationen zu Ihrem Konto aus:
```
	swift stat
```
Suchen Sie das Kontofeld (Account) und notieren Sie die vollständige Zeichenfolge hinter *Account*: einschließlich `AUTH_`.

#### Geheimen Schlüssel festlegen

Dieser Schlüssel kann eine Zeichenfolge Ihrer Wahl sein. Ein bewährtes Verfahren ist, eine lange, zufällig zusammengesetzte und schwer zu erratende Zeichenfolge zu wählen.
```
	swift post -m "Temp-URL-Key:<Schlüssel>"
```
Führen Sie den Swift-Befehl `stat` aus, um zu überprüfen, ob `Temp-URL-Key` erfolgreich festgelegt wurde.
```
	swift stat
```

#### Temporäre URL erstellen

Der Swift-Befehl `tempurl` arbeitet mit den folgenden Positionsargumenten:

* [Methode] GET, um das Herunterladen zuzulassen. PUT, um das Hochladen zuzulassen.
* [Sekunden] Zeit in Sekunden, die die temporäre URL verfügbar sein soll.
* [Pfad] Der vollständige Pfad des Objekts im Format `/v1/<Authentifizierungskonto>/<Containername>/<Objektname>`. Weitere Informationen finden Sie bei der [{{site.data.keyword.objectstorageshort}}-URL](#access-points).
* [Schlüssel] Der Schlüssel, den Sie in Schritt 2 festgelegt haben.

```
swift tempurl GET <Sekunden> <Pfad> <Schlüssel>
```

Dieser Befehl gibt eine URL zurück, die Sie an Ihren Clusternamen anhängen können, um eine vollständige URL zu erhalten. Verwenden Sie die vollständige URL, um das Objekt mit einem kompatiblen HTTP-Client wie curl, wget oder Firefox herunterzuladen.

## Mit der Swift-REST-API auf {{site.data.keyword.objectstorageshort}} zugreifen {: #using-swift-restapi}

Sie können die Swift-REST-API in einer Befehlszeilen-Clientschnittstelle wie cURL verwenden oder Sie können die API in Ihrer Anwendung aufrufen.  

### {{site.data.keyword.objectstorageshort}}-URL {: #access-points}

Zur Interaktion mit der {{site.data.keyword.objectstorageshort}}-API erstellen Sie die {{site.data.keyword.objectstorageshort}}-URL wie folgt:
```
	https://<Zugriffspunkt>/<API-Version>/AUTH_<Projekt-ID>/<Containernamensbereich>/<object namespace>
```


Die URL besteht aus fünf Teilen. Die `<API-Version>` ist Version 1. Sie finden die Werte für `<Projekt-ID>`, `<Containernamensbereich>` und `<object namespace>` für Ihren {{site.data.keyword.objectstorageshort}} in der {{site.data.keyword.objectstorageshort}}-Benutzerschnittstelle.  Informationen für den `<Zugriffspunkt>` finden Sie in der folgenden Tabelle:


| **Region**  |   **Öffentlicher Zugriffspunkt**                     |
|-------------|-----------------------------------------------|
| Dallas      | https://dal.objectstorage.open.softlayer.com/ |
| London      | https://lon.objectstorage.open.softlayer.com/ |


*Tabelle 1. {{site.data.keyword.objectstorageshort}}-Zugriffspunkt*


### {{site.data.keyword.objectstorageshort}}-API

Eine umfassende Liste der Optionen der {{site.data.keyword.objectstorageshort}}-REST-API mit Beispielen finden Sie in der [vollständigen Referenz zur OpenStack-Swift-API](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}.

## {{site.data.keyword.objectstorageshort}} regionsübergreifend verwenden {: #multi-regions}  

Der {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}}-Service unterstützt die Speicherregionen Dallas und London. Diese Speicherregionen sind unabhängig von der {{site.data.keyword.Bluemix_notm}}-Region, wie zum Beispiel 'US-South' und 'United Kingdom', in der die {{site.data.keyword.objectstorageshort}}-Serviceinstanz erstellt wurde.  Beispiel: Wenn Sie eine {{site.data.keyword.objectstorageshort}}-Instanz in der {{site.data.keyword.Bluemix_notm}}-Region 'US-South' erstellen, haben Sie Lese- und Schreibzugriff auf Daten in der Speicherregion Dallas oder in der Speicherregion London.  

Für die {{site.data.keyword.Bluemix_notm}}-Region 'US-South' ist Dallas die Standardspeicherregion. Für die {{site.data.keyword.Bluemix_notm}}-Region 'United Kingdom' ist London die Standardspeicherregion.  Die {{site.data.keyword.objectstorageshort}}-Benutzerschnittstelle startet immer mit der Standardspeicherregion der {{site.data.keyword.Bluemix_notm}}-Region. Wenn Sie die Region wechseln wollen, klicken Sie auf die Dropdown-Liste für die {{site.data.keyword.objectstorageshort}}-Regionen und wählen eine andere Region aus.

**Anmerkung:** Der {{site.data.keyword.objectstorageshort}}-Service unterstützt keine speicherregionsübergreifende Replikation.

### Zugriff auf mehrere Regionen

Für die Verwendung des {{site.data.keyword.objectstorageshort}}-Service müssen Sie sich [bei OpenStack Keystone authentifizieren](#keystone-authentication). Nach der erfolgreichen Authentifizierung werden ein `X-Subject-Token` und die {{site.data.keyword.objectstorageshort}}-Endpunkte in der Antwort zur Verfügung gestellt.

Beispiel: Wenn Sie einen Container mit dem Namen `my_container` in der Speicherregion Dallas erstellen wollen, geben Sie wie folgt einen Zugriffspunkt von Dallas im curl-Befehl an:
```
	# curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT
```

Wenn Sie einen Container mit dem Namen `my_container` in der Speicherregion London erstellen wollen, geben Sie wie folgt einen Zugriffspunkt von London im curl-Befehl an:
```
	# curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT
```
**Anmerkung:** Das `X-Subject-Token`, das Sie von Keystone empfangen haben, funktioniert speicherregionsübergreifend.

Weitere Informationen zu den Zugriffspunkten für verschiedene Regionen finden Sie in der Tabelle mit den [Object Storage-Zugriffpunkten](#access-points).


## Informationen zu Authentifizierung und Berechtigungsnachweisen {: #understanding-authentication-credentials}

### {{site.data.keyword.objectstorageshort}}-Berechtigungsnachweise ohne Bindung einer Anwendung generieren

Zum Generieren von {{site.data.keyword.objectstorageshort}}-Cloudberechtigungsnachweisen für die Verwendung außerhalb einer {{site.data.keyword.Bluemix_notm}}-Anwendung müssen Sie einen Serviceschlüssel für Ihre {{site.data.keyword.objectstorageshort}}-Instanz generieren. Sie können einen neuen Schlüssel generieren, indem Sie **Serviceberechtigungsnachweise** in der Seitenleiste der Benutzerschnittstelle auswählen oder die Befehlszeilenschnittstelle Cloud Foundry CLI (Version 6.11.3 oder höher) verwenden. Nach der Generierung und dem Abruf eines Serviceschlüssels für Ihre {{site.data.keyword.objectstorageshort}}-Instanz können Sie die Informationen zur Cloudintegration verwenden, um ein Keystone-Token mit einem OpenStack-SDK oder der OpenStack-Identity-API anzufordern und anschließend mit der Verwendung des Swift-Kontos zur Objektverwaltung zu beginnen.

Wenn Sie den Schlüssel über die Cloud Foundry CLI erstellen möchten, müssen Sie sich bei dieser Befehlszeilenschnittstelle anmelden und den folgenden Befehl ausführen:
 ```
    cf create-service-key <Object Storage-Instanzname> <eindeutiger Name für diesen Schlüssel>
```
Führen Sie den folgenden Befehl aus, um die Serviceberechtigungsnachweise über die Cloud Foundry CLI abzurufen:
```
	cf service-key <Object Storage-Instanzname> <eindeutiger Name für diesen Schlüssel>
```

### Cloudprojekte und -benutzer
Durch die Bereitstellung einer neuen {{site.data.keyword.objectstorageshort}}-Instanz wird in der IBM Public Cloud ein isoliertes Keystone-Projekt erstellt. Wenn Sie eine neue Anwendung an die {{site.data.keyword.objectstorageshort}}-Instanz binden, wird ein neuer Keystone-Benutzer mit Zugriff auf das Projekt erstellt. Wenn Sie die Instanz löschen, werden auch Projekt und Benutzer gelöscht.

### OpenStack Identity (Keystone) v3 {: #keystone-authentication}
Die Struktur der Berechtigungsnachweise enthält einen vollständigen Satz von Attributen, sodass Sie die Methode für die OpenStack-Tokenanforderung oder das OpenStack-SDK auswählen können, das sich am besten für Ihre Anwendung eignet.

Die empfohlene v3-Tokenanforderung ist eine POST-Anforderung an https://identity.open.softlayer.com/v3/auth/tokens, wie im folgenden curl-Befehl gezeigt:
```
	curl -i \
	  -H "Content-Type: application/json" \
	  -d '
	{
		"auth": {
			"identity": {
				"methods": [
					"password"
				],
				"password": {
					"user": {
						"id": "ad78b2a3f843466988afd077731c61fc",
						"password": "K/jyIi2jR=1?D.TP"
					}
				}
			},
			"scope": {
				"project": {
					"id": "0f47b41b06d047f9aae3b33f1db061ed"
				}
			}
		}
	}' \
	  https://identity.open.softlayer.com/v3/auth/tokens ; echo
```
Verwenden Sie den Wert des Felds `X-Subject-Token` aus dem Antwortheader als `X-Auth-Token`, wenn Sie Anforderungen an den {{site.data.keyword.objectstorageshort}}-Service senden.

Eine Beispielantwort könnte wie folgt aussehen. Die Antwort wird so abgeschnitten, dass nur die für {{site.data.keyword.objectstorageshort}} releventen Informationen angezeigt werden.

	HTTP/1.1 201 Created
	Date: Mon, 29 Feb 2016 21:03:41 GMT
	Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.1e-fips mod_wsgi/3.4 Python/2.7.5
	X-Subject-Token: gAAAAABW1LIubUgqKl-eInzhZUHWEnXijp7t6_5inl4DTRLxDhNbJ25ly2X7bASNvH7ocxinaJu_kdhSfnHNRwPAeYY77Ii2Cwp02-bvxUA1S9lV_knT6EyCOW2mSBl_HuuDD2cEgdiKmyZTVt-RvDxhPKYD-rHkJz-dHO4Folg8TVXotilb1uw
	Vary: X-Auth-Token
	x-openstack-request-id: req-01e096c8-5393-4f98-8ff6-029c55e42524
	Content-Length: 12051
	Content-Type: application/json
```
	{
	  "token" : {
	    "roles" : [
	      {
	        "id" : "f61f06a84f6443e880210fa986bd8691",
	        "name" : "ObjectStorageOperator"
	      }
	    ],
	    "catalog" : [
	      {
	        "endpoints": [
			{
	            "id" : "20cbfa6ff22b4a67a1484d30235bfc80",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "38b8c081b11a452bb951698c334a406d",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "internal"
	          },
	          {
	            "id" : "4207049680fa4effbecd044c7448a8cb",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.open.softlayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "public"
	          },
	          {
	            "id" : "8a65a0cf38ac4211ad6a3c9c0eb337ff",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.open.softlayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "public"
	          },
	          {
	            "id" : "a60cf32be624491d89170ef8264de5e8",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "c769862200124a308d6748e418c971ba",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "internal"
	          }
	        ],
	        "id" : "896e4064cbe742afbf9a543c15f27ac0",
	        "type" : "object-store",
	        "name" : "swift"
	      },
	    ],
	    "extras" : {

	    },
	    "user" : {
	      "id" : "0b8aebd924ef4cc7aa9232f07e47e874",
	      "name" : "user_87c094ce47a9feae3a137ffcbbfa098a888c12a8",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "expires_at" : "2016-02-29T22:03:42.061343Z",
	    "audit_ids" : [
	      "cbA-iL2dSheyB72PHd7q8Q"
	    ],
	    "issued_at" : "2016-02-29T21:03:42.000000Z",
	    "project" : {
	      "id" : "3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	      "name" : "object_storage_c1d8b3a1",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "methods" : [
	      "password"
	    ]
	  }
	}
```

Die {{site.data.keyword.objectstorageshort}}-URL ist im Servicekatalog zu finden. Der Servicekatalog ist im Antworthauptteil der Tokenanforderung enthalten. Die Antwort ist ein vollständiger Katalog der OpenStack-Services, die verfügbar sind. Wählen Sie den Endpunkt im Servicekatalog mit dem Typ `object-store` und mit der Region aus, die dem Feld für die Region in den Berechtigungsnachweisen entspricht.

**Anmerkung:** Verwenden Sie die allgemein zugängliche Schnittstelle (`publicURL`). Auf die interne Schnittstelle (`internalURL`) kann von {{site.data.keyword.Bluemix_notm}} aus nicht zugegriffen werden.



## Dateien durch differenzierte Zugriffssteuerung schützen {: #fine-grained-access-control}

Differenzierte Zugriffssteuerungslisten (ACLs) sind für den Schutz von Dateien hilfreich, wenn mehrere Benutzer vorhanden sind, die Dateien in demselben Container speichern.

Anmerkung: Die in diesem Dokument erläuterten Prozeduren erfordern die Swift-CLI. Weitere Informationen finden Sie unter [{{site.data.keyword.objectstorageshort}} mit der Swift-CLI verwenden](https://console.ng.bluemix.net/docs/services/ObjectStorage/objectstorge_usingobjectstorage.html#using-swift-cli).


### Zugriffstypen {: #access-types}

Der Zugriff auf den Service wird durch Benutzerrollen und Zugriffssteuerungslisten für Container gesteuert. {{site.data.keyword.objectstorageshort}}-Benutzer können Benutzer mit Administratorberechtigungen oder Benutzer ohne Administratorberechtigungen sein. Zugriffssteuerungslisten werden durch Administratorbenutzer auf der Containerebene aktiviert und sind für die Serviceinstanz, das Speicherkonto oder auf Projektebene nicht verfügbar.

<table>
  <tr>
    <th> Benutzer mit Administratorberechtigungen (admin) </th>
    <th> Benutzer ohne Administratorberechtigungen (member) </th>
  </tr>
  <tr>
    <td> Zugriffssteuerung verwalten </td>
    <td> Standardmäßig kein Zugriff auf den Service oder seine Container </td>
  </tr>
  <tr>
    <td> Container erstellen und löschen </td>
    <td> Aktionen abhängig von den Lese-/Schreibzugriffssteuerungslisten der Container </td>
  </tr>
  <tr>
    <td> Containerinhalt lesen und schreiben </td>
    <td> Durch den Administrator festgelegte Aktionen </td>
  </tr>
</table>

*Tabelle 1: Definierte Benutzerrollen*

Sie können {{site.data.keyword.objectstorageshort}}-Benutzer über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle, die Cloud Foundry-API oder die Cloud Foundry CLI verwalten.



### {{site.data.keyword.objectstorageshort}}-Serviceberechtigungsnachweise generieren {: #generating}

Über die neue {{site.data.keyword.Bluemix_notm}}-Konsole können Sie neue Serviceberechtigungsnachweise für {{site.data.keyword.objectstorageshort}}-Benutzer generieren.  Zum Anzeigen der neuen Konsole klicken Sie auf die Option **Neues {{site.data.keyword.Bluemix_notm}} testen**.

1.  Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} als Benutzer mit einer Entwicklerrolle an. Sie müssen sich in dem Bereich der Serviceinstanz befinden, die Sie verwalten wollen.
2. Klicken Sie auf die Registerkarte **Serviceberechtigungsnachweise**.
3. Klicken Sie auf **Neuer Berechtigungsnachweis**.
4. Geben Sie einen Namen für den Berechtigungsnachweis an.
5. Geben Sie in das Textfeld **Lineare Konfigurationsparameter hinzufügen** die Informationen zu dem Berechtigungsnachweis für die Rolle ein, die Sie erstellen wollen. Die Informationen müssen als JSON-Nutzdaten formatiert sein.
  - Zum Erstellen eines Benutzers mit Administratorberechtigungen: `{"role":"admin"}`
  - Zum Erstellen eines Benutzers ohne Administratorberechtigungen: `{"role":"member"}`
5. Klicken Sie auf **Hinzufügen**.

Zum Generieren von Serviceberechtigungsnachweisen durch cURL-Befehle oder über die Swift-CLI können Sie die folgenden Schritte ausführen.

1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} als Benutzer mit einer Entwicklerrolle an. Sie müssen sich in dem Bereich der Serviceinstanz befinden, die Sie verwalten wollen.

  ```
  cf login -a api.ng.bluemix.net -u <Benutzer-ID> -p <Kennwort> -o <Organisation> -s <Bereich>
  ```

2. Generieren Sie Serviceberechtigungsnachweise. `Serviceschlüsselname` wird dabei zum Namen Ihres Berechtigungsnachweises. Sie können entweder den Cloud Foundry-Befehl oder den cURL-Befehl verwenden.

  Cloud Foundry-Befehl:
  ```
  cf create-service-key "<Name der Object Storage-Serviceinstanz>" <Serviceschlüsselname> -c '{"role":"<Object Storage-Rolle>"}'
  ```

  Beispiel:

  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'

  ```
  cURL-Befehl:
  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<Serviceinstanz-GUID>",   "name": "<Benutzername>", "role": "member"}' -X POST -H "Authorization: <Trägertoken>" -H "Content-Type: " -H "Cookie: "
  ```

3. Validieren Sie die Berechtigungsnachweise für den von Ihnen erstellten Serviceschlüssel.

  Cloud Foundry-Befehl:
  ```
  cf service-key <Serviceschlüsselname> <Member-Name>
  ```
  Beispiel:
  Erstellen eines Member-Serviceschlüssels für eine Serviceinstanz mit dem Namen Object-Storage-Acl-Test.
  ```
  {
    "auth_url": "https://identity.open.softlayer.com",
    "domainId": "8753ff40ac1a4f4a9f162ad8026b6ce0",
    "domainName": "757955",
    "password": "xxxxxxxx",
    "project": "object_storage_6046b6e2_ee53_4884_916f_89c65e4d408e",
    "projectId": "c727d7e248b448f6b268f31a1bd8691e",
    "region": "dallas",
    "role": "member",
    "userId": "3c5b516655e4479881d3d216895faedb",
    "username": "member_2afbeea1d58b1867f46c699553d1e4513e7df83a"
  }
  ```
  cURL-Befehl:
  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <Trägertoken>" -H "Cookie: "
  ```



### Zugriff zuweisen {: #assigning-access}  

Nur ein {{site.data.keyword.objectstorageshort}}-Benutzer mit Administratorrolle kann einem anderen Benutzer Lese- oder Schreibzugriff auf einen Container erteilen.

Zum Erteilen des Lesezugriffs über die CLI verwenden Sie die Option `--read-acl` oder die Option `-r`.

1. Authentifizieren Sie Ihre Berechtigungsnachweise mit den Informationen in den Serviceberechtigungsnachweisen, die Sie erstellt haben.  Sie empfangen Ihre Object Storage-URL und Ihr Authentifizierungstoken als Ausgabe.

  Swift-Befehl:
  ```
  export OS_USER_ID=<Benutzer-ID>
  export OS_PASSWORD=<Kennwort>
  export OS_TENANT_ID=<Projekt-ID>
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=<Region>
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

  swift auth
  ```
  cURL-Befehl:
  ```
  curl -i -H "X-Auth-User: <Benutzer-ID>" -H "X-Auth-Key: <Kennwort>" <Authentifizierungs-URL>
  ```
3. Führen Sie den folgenden Befehl aus, um Lesezugriff zu erteilen:

  Swift-Befehl:
  ```
  swift post <Containername> --read-acl "<Benutzer-ID>:<Projekt-ID>"
  ```
  cURL-Befehl:
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: <Tenant-ID>:<Projekt-ID>" -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
4. Überprüfen Sie den Wert für die Lesezugriffssteuerungsliste (Read ACL).

  Swift-Befehl:
  ```
  swift stat <Containername>
  ```
  cURL-Befehl:
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
  ```
  Beispielausgabe:
  ```
  HTTP/1.1 204 No Content
  Content-Length: 0
  X-Container-Object-Count: 1
  Accept-Ranges: bytes
  X-Storage-Policy: standard
  X-Container-Read: c727d7e248b448f6b268f31a1bd8691e:3c5b516655e4479881d3d216895faedb
  X-Container-Bytes-Used: 31512
  X-Timestamp: 1462818314.11220
  Content-Type: text/plain; charset=utf-8
  X-Trans-Id: txad7fe001da274b9ba39a6-005772e4d6
  Date: Tue, 28 Jun 2016 20:57:58 GMT
  ```

Sie können verschiedene ACL-Kombinationen für Lesezugriff angeben.

<table>
  <tr>
    <th> Berechtigung </th>
    <th> Optionen für Lesezugriffssteuerung (Read ACL) </th>
  </tr>
  <tr>
    <td> Lesen für alle Referrer unabhängig von der Kontozuordnung </td>
    <td> `.r,*` </td>
  </tr>
  <tr>
    <td> Lesen und Auflisten für alle Referrer und Listen </td>
    <td> `.r:*,.rlistings` </td>
  </tr>
  <tr>
    <td> Lesen und Auflisten für angegebenen Benutzer in bestimmtem Projekt </td>
    <td> `< Projekt-ID>:< Benutzer-ID>` </td>
  </tr>
  <tr>
    <td> Lesen und Auflisten für angegebenen Benutzer in jedem Projekt </td>
    <td> `<*>:< Benutzer-ID>` </td>
  </tr>
  <tr>
    <td> Lesen und Auflisten für jeden Benutzer in angegebenem Projekt </td>
    <td> `< Projekt-ID>:<*>` </td>
  </tr>
  <tr>
    <td> Lesen und Auflisten für jeden Benutzer in jedem Projekt  </td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*Tabelle 2: Lesezugriffsberechtigungen nach Option*

Anmerkung: Trennen Sie Zugriffssteuerungslisten durch ein Komma (,). Beispiel: `-read-acl projekt-id:benutzer-id1, projekt-id2:benutzer-id2`.


Zum Erteilen von Schreibzugriff verwenden Sie die Option `--write-acl` oder `-w` in der Swift-CLI.

1. Authentifizieren Sie Ihre Berechtigungsnachweise mit den Informationen in den Serviceberechtigungsnachweisen, die Sie erstellt haben.  Sie empfangen Ihre Object Storage-URL und Ihr Authentifizierungstoken als Ausgabe.

  Swift-Befehl:
  ```
  export OS_USER_ID="<Benutzer-ID>"
  export OS_PASSWORD="<Kennwort>"
  export OS_TENANT_ID=<Tenant-ID>
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=<Region>
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

  swift auth
  ```
  cURL-Befehl:
  ```
  curl -i -H "X-Auth-User:<Benutzer-ID>" -H "X-Auth-Key:<Kennwort>" https://identity.open.softlayer.com/v3
  ```
2. Führen Sie den folgenden Befehl aus, um Schreibzugriff zu erteilen:

  Swift-Befehl:
  ```
  swift post <Containername> --write-acl "<Benutzer-ID>:<Projekt-ID>"
  ```
  cURL-Befehl:
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: <Benutzer-ID>: <Projekt-ID>" -H "X-Auth-Token:<OS_AUTH_TOKEN>"

  ```
3. Überprüfen Sie den Wert für die Schreibzugriffssteuerungsliste (Write ACL).

  Swift-Befehl:
  ```
  swift stat <Containername>
  ```
  cURL-Befehl:
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
  ```


Sie können verschiedene ACL-Kombinationen für Schreibzugriff angeben.

<table>
  <tr>
    <th> Berechtigung </th>
    <th> Optionen für Schreibzugriffssteuerung (Write ACL) </th>
  </tr>
  <tr>
    <td> Schreiben für angegebenen Benutzer in bestimmtem Projekt </td>
    <td> `<Projekt-ID>:<Benutzer-ID>` </td>
  </tr>
  <tr>
    <td> Schreiben für angegebenen Benutzer in jedem Projekt </td>  
    <td> `*:<Benutzer-ID>` </td>
  </tr>
  <tr>
    <td> Schreiben für jeden Benutzer in angegebenem Projekt </td>
    <td> `<Projekt-ID>:<*>` </td>
  </tr>
  <tr>
    <td> Schreiben für jeden Benutzer in jedem Projekt </td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*Tabelle 3: Schreibzugriffsberechtigungen nach Option*

Anmerkung: Trennen Sie Zugriffssteuerungslisten durch ein Komma (,). Beispiel: `-write-acl projekt-id:benutzer-id1, projekt-id2:benutzer-id2`.




### Zugriff entfernen {: #removing-access}

Gehen Sie wie folgt vor, um Lesezugriffssteuerungslisten von einem Container zu entfernen:

  Swift-Befehl:
  ```
  swift post <Containername> --read-acl “”
  ```
  cURL-Befehl:
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```

Gehen Sie wie folgt vor, um Schreibzugriffssteuerungslisten von einem Container zu entfernen:

  Swift-Befehl:
  ```
  swift post <Containername> --write-acl “”
  ```
  cURL-Befehl:
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```

Überprüfen Sie, ob eine Zugriffssteuerungsliste (ACL) entfernt wurde:

  Swift-Befehl:
  ```
  swift stat <Containername>
  ```

  Beispielausgabe:
  ```
         Account: AUTH_c727d7e248b448f6b268f31a1bd8691e
       Container: Test
         Objects: 1
           Bytes: 31512
        Read ACL:
       Write ACL:
         Sync To:
        Sync Key:
   Accept-Ranges: bytes
X-Storage-Policy: standard
     X-Timestamp: 1462818314.11220
      X-Trans-Id: txf04968bc9ef8431982b77-005772e34b
    Content-Type: text/plain; charset=utf-8

  ```
  cURL-Befehl:
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```




## Bindung und Bereitstellung von {{site.data.keyword.objectstorageshort}} aufheben {: #deprovisioning-object-storage}

### Vorgehensweise zum Löschen Ihres {{site.data.keyword.objectstorageshort}}-Service
1.	Wählen Sie Ihren Service im {{site.data.keyword.Bluemix_notm}}-Dashboard aus.  
2.	Klicken Sie auf das Zahnradsymbol und wählen Sie **Service löschen** aus.

**Achtung:** Wenn Sie eine IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}}-Serviceinstanz löschen, werden das Cloudprojekt und das Swift-Konto gelöscht. Alle Container und Objekte in der gelöschten Instanz werden aus Swift gelöscht und können nicht wiederhergestellt werden.

### Bindung für eine Anwendung aufheben oder einen Serviceschlüssel löschen

Wenn Sie die Bindung einer Anwendung an die {{site.data.keyword.objectstorageshort}}-Instanz aufheben oder den Serviceschlüssel löschen, werden die Berechtigungsnachweise gelöscht. Das {{site.data.keyword.objectstorageshort}}-Konto wird erst gelöscht, wenn die Bereitstellung der {{site.data.keyword.objectstorageshort}}-Instanz aufgehoben wird. Sie können neue Cloudberechtigungsnachweise generieren, indem Sie einen [neuen Serviceschlüssel binden oder erstellen](#bind-object-storage-to-application).
