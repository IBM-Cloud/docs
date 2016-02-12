{:new_window: target="_blank"}

# Einführung {{site.data.keyword.objectstorageshort}} {: #getting-started-with-object-storage} 

{{site.data.keyword.objectstoragefull}} ermöglicht Ihnen zur Verwaltung Ihrer Daten den Zugriff auf ein vollständig eingerichtetes Swift {{site.data.keyword.objectstorageshort}}-Konto. Swift stellt eine vollständig verteilte Speicherplattform bereit, auf die von APIs zugegriffen werden kann. Diese Speicherplattform können Sie direkt in Ihren Anwendungen oder zu Backup-Zwecken verwenden, was sie zur einer idealen Lösung für kosteneffektiven Scale-out-Speicher macht.

IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} verwendet OpenStack Identity (Keystone) zur Authentifizierung und ist für Aufrufe der API von OpenStack Object Storage (Swift) V1 direkt zugänglich. IBM {{site.data.keyword.objectstorageshort}} kann an eine {{site.data.keyword.Bluemix_notm}}-Anwendung gebunden werden oder es kann von außerhalb einer {{site.data.keyword.Bluemix_notm}}-Anwendung darauf zugegriffen werden. 

Weitere Informationen und Dokumentation zur Verwendung von OpenStack Swift und Keystone sind auf der [OpenStack-Dokumentationssite](http://docs.openstack.org){: new_window} verfügbar.

Das {{site.data.keyword.objectstorageshort}}-Architekturdiagramm sieht wie folgt aus:

[![{{site.data.keyword.objectstorageshort}}-Architekturdiagramm](images/object_storage_solution_archectiture_small.png)](http://www.ng.bluemix.net/docs/api/content/services/ObjectStorage/images/object_storage_solution_archectiture.png){: new_window}

*Abbildung 1. {{site.data.keyword.objectstorageshort}}-Architekturdiagramm*

**Anmerkung:** Eine providerseitige Verschlüsselung wird nicht unterstützt. Für die Verschlüsselung von Daten vor dem Hochladen ist die Clientanwendung zuständig.

**Anmerkung:** Der Beta-Plan für den {{site.data.keyword.objectstorageshort}}-Service wird nach der allgemeinen Verfügbarkeit (GA) des {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}}-Service aus dem Katalog entfernt. Nach Ablauf einer Nachfrist werden Serviceinstanzen entfernt, die den Beta-Plan verwenden. [Aktualisieren Sie Ihren Preisstrukturplan](#changeplan), um die Verwendung des {{site.data.keyword.objectstorageshort}}-Service fortzusetzen. 




## {{site.data.keyword.objectstorageshort}}-Instanz in {{site.data.keyword.Bluemix_notm}} erstellen {: #creating-object-storage-instance} 

### Vorgehensweise zur Erstellung einer {{site.data.keyword.objectstorageshort}}-Serviceinstanz
1.	Wechseln Sie zur {{site.data.keyword.Bluemix_notm}}-Registerkarte **Katalog** und geben Sie **{{site.data.keyword.objectstorageshort}}** in das Suchfeld ein oder wechseln Sie zu **Services** und wählen Sie **Storage** aus. Klicken Sie auf den **{{site.data.keyword.objectstorageshort}}**-Service. 
2.	Wählen Sie Ihren Bereich, die App, den Servicenamen und den Plan aus und klicken Sie auf **Erstellen**. 
**Anmerkung:** Wenn Sie anfangs die Option **Nicht binden** für das Feld **App** auswählen, können Sie trotzdem weiterhin die Serviceinstanz an Ihre {{site.data.keyword.Bluemix_notm}}-Anwendung binden, wenn Sie die Konfiguration abgeschlossen haben. (Siehe folgende Anweisungen.)

## {{site.data.keyword.objectstorageshort}} über eine {{site.data.keyword.Bluemix_notm}}-App verwenden {: #using-object-storage-from-bluemix-app} 

### Vorgehensweise zum Binden eines {{site.data.keyword.objectstorageshort}}-Service an eine Anwendung nach der Erstellung {: #bind-object-storage-to-application} 
1.	Wählen Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard die App aus, die Sie binden möchten.
2.	Klicken Sie in der App-Übersicht auf **Service oder API binden**.
3.	Wählen Sie in der Liste der Services Ihre {{site.data.keyword.objectstorageshort}}-Instanz aus und klicken Sie auf **Hinzufügen**.
4.	Klicken Sie auf **Erneutes Staging**, wenn Sie dazu aufgefordert werden. Für die Verwendung des neuen Service ist für Ihre App ein erneutes Staging erforderlich.

### Gebundener Kontext

Wenn Sie {{site.data.keyword.objectstorageshort}} in einem gebundenen Kontext verwenden möchten, werden die Berechtigungsnachweise für die Cloud indirekt über den Anwendungsbindungsprozess bereitgestellt. Nach der erfolgreichen Bindung einer Serviceinstanz an Ihre Anwendung wird eine Konfiguration ähnlich der folgenden Beispielkonfiguration zur Umgebungsvariablen `VCAP_SERVICES` hinzugefügt.

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

## {{site.data.keyword.objectstorageshort}}-Benutzerschnittstelle verwenden {: #using-object-storage-ui}

### Benutzerschnittstelle - Elemente und Navigation
Wenn Ihr {{site.data.keyword.objectstorageshort}} bereitgestellt wurde, können Sie die Informationen zu Ihrer Instanz im {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}}-Dashboard für Serviceinstanzen anzeigen. Wählen Sie im Dashboard Ihre {{site.data.keyword.objectstorageshort}}-Instanz aus, um den Fensterbereich mit ausführlicheren Informationen anzuzeigen.  
#### Nutzungsdaten
Im oberen Bereich der Anzeige sehen Sie die Informationen zur Speicherbelegung für Ihre Instanz. Außerdem wird die aktuelle Anzahl der **Speichercontainer** und die Gesamtzahl der **Objekte** in allen Containern angezeigt, über die Sie verfügen. Ihre Speicherbelegung wird in Megabyte angegeben. **Belegter Speicher** bezieht sich auf die aktuelle Größe des Speicherplatzes, der belegt ist. 
#### Aktionen
Klicken Sie auf die Schaltfläche **Aktualisieren**, um die aktuellsten Nutzungsdaten abzurufen.   
####Objektbrowser 
Im unteren Bereich der Anzeige befindet sich der Objektbrowser. Verwenden Sie den Objektbrowser, um Object Storage-Container und -Objekte zu verwalten. Sie können Container erstellen, Dateien hochladen, Container löschen, Dateien löschen und andere Aktionen ausführen.

## Swift-Befehlszeilenschnittstelle (CLI) für den Zugriff auf {{site.data.keyword.objectstorageshort}} verwenden {: #using-swift-cli}

Sie können auf den {{site.data.keyword.objectstorageshort}}-Server über das Internet und durch Anwendungen und virtuelle Maschinen in {{site.data.keyword.Bluemix_notm}} zugreifen. Häufige Anwendungsfälle für den {{site.data.keyword.objectstorageshort}}-Service sind zum Beispiel:

* Sicherung durch Backups von Datenträgerdaten aus Ihren Instanzen
* Verwendung als Zwischenspeicherposition bei der Übertragung umfangreicher Datenvolumen
* Übertragung von Daten zwischen Umgebungen, die nicht direkt verbunden sind
* Einsatz als zentrales Repository

Der {{site.data.keyword.objectstorageshort}}-Service basiert auf OpenStack Swift und ist für jede beliebige kompatible Clientanwendung zugänglich. In diesem Abschnitt wird die Verwendung des Python Swift-Clients beschrieben. Dies ist die Befehlszeilenschnittstelle (CLI, Command-Line Interface) für die {{site.data.keyword.objectstorageshort}}-API und die zugehörigen Erweiterungen für die Arbeit mit Containern und Dateien.

### Swift-Client installieren

Installieren Sie die folgenden Softwarevoraussetzungen, falls diese noch nicht installiert sind. Weitere Informationen finden Sie in der [OpenStack-Dokumentation](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}. 
* Python 2.7 oder höher
* Setuptools-Paket
* Pip-Paket

Installieren Sie den Python Swift-Client mithilfe von Python-pip:

	sudo pip install python-swiftclient

### Client einrichten

Der Swift-Client entnimmt die Authentifizierungsinformationen den folgenden Umgebungsvariablen:
* ```OS_AUTH_URL``` - Endpunkt-URL
* ```OS_USER_ID``` - Benutzername
* ```OS_PASSWORD``` - Kennwort

Legen Sie die Authentifizierungsinformationen wie folgt fest. 

	export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
	export OS_PASSWORD=aaa55AAAaaaaa]?,
	export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
	export OS_AUTH_URL=https://identity.open.softlayer.com/v3
	export OS_REGION_NAME=dallas
	export OS_IDENTITY_API_VERSION=3
	export OS_AUTH_VERSION=3

Sie finden die Werte für die Berechtigungsnachweise für Ihren {{site.data.keyword.objectstorageshort}}-Service auf der Seite **Serviceberechtigungsnachweise** in der {{site.data.keyword.objectstorageshort}}-Benutzerschnittstelle. 

**Anmerkung:** Stellen Sie sicher, dass Sie dem Wert von ```auth_url``` aus den Berechtigungsnachweisen in der {{site.data.keyword.objectstorageshort}}-Benutzerschnittstelle den Wert ```/v3`` hinzufügen, wenn Sie die Umgebungsvariablen ```OS_AUTH_URL`` für den Swift-Client konfigurieren.


![{{site.data.keyword.objectstorageshort}}-Serviceberechtigungsnachweise](images/service_credentials.jpg)

*Abbildung 2. {{site.data.keyword.objectstorageshort}}-Serviceberechtigungsnachweise*

### Mit Containern arbeiten

Container auflisten:

	swift list
	
Container erstellen:

	swift post <Containername>
	
Inhalt eines Containers auflisten:

	swift list <Containername>

### Mit Objekten arbeiten

#### Datei einem Container hinzufügen

	swift upload <Containername> <Dateiname>

#### Dateien mit einer Größe über 5 GB einem Container hinzufügen

Wenn Sie eine Datei hochladen, die größer als 5 GB ist, müssen Sie sie in kleinere Segmente aufteilen. Sie können den Swift-Client durch Angabe des Parameters ```-segment-size``` anweisen, eine solche Hochladeoperation durchzuführen:

	swift upload <Containername> <Dateiname> --segment-size <Größe_in_Byte>
	
Jedes Segment wird parallel in einen separaten Container mit dem Namen ```<Containername>_segments``` hochgeladen. Nachdem Hochladen aller Segmente erstellt Swift eine Manifestdatei, sodass die Segmente in eine einzige Datei aus dem ursprünglichen Container ```<Containername>`` mit dem ursprünglichen Dateinamen ```<Dateiname>`` heruntergeladen werden können.

Beispiel: Mit dem folgenden Befehl wird eine Datei mit dem Namen ```large_file``` aus einem Container mit dem Namen ```test_container`` mit der Segmentgröße ```1073741824`` hochgeladen.

	swift upload test_container -S 1073741824 large_file

Sie können den folgenden Befehl ausführen, um die Datei herunterzuladen:

	swift download test_container large_file

#### Datei herunterladen

	swift download <Containername> <Dateiname>
	
#### Verzeichnis einem Container hinzufügen

Swift hat keine eigentliche Verzeichnisstruktur, verwendet jedoch eine entsprechende Benennung, um eine Verzeichnisstruktur darzustellen. Führen Sie den folgenden Befehl aus, um einem Container ein Verzeichnis hinzuzufügen:

	swift upload <Containername> <Verzeichnisname>
	
Durch diesen Befehl wird eine vollständige Verzeichnisstruktur als relativer Pfad hochgeladen. Beispiel: Wenn Sie ```/mnt/volume1``` angeben, wird die Verzeichnisstruktur 'mnt/volume1' an alle Dateinamen angefügt, um die Verzeichnisstruktur anzugeben.

	
#### Verzeichnis herunterladen

Zum Herunterladen einer Verzeichnisstruktur verwenden Sie den Parameter ```-prefix```, um das Verzeichnis bzw. die Verzeichnisstruktur anzugeben, die heruntergeladen werden soll.

	swift download <Containername> --prefix <Verzeichnis>
	
#### Datei löschen

	swift delete <Containername> <Dateiname>

### Temporäre URL erstellen

Eine temporäre URL ist eine lange, schwer zu erratende URL, die für einen angegebenen Zeitraum zum Herunterladen von Objekten verwendet werden kann, ohne dass eine weitere Authentifizierung erforderlich ist. Sie generieren eine temporäre URL mit den folgenden Schritten:

1. Geben Sie Ihr Authentifizierungskonto an.
2. Legen Sie einen geheimen Schlüssel fest.
3. Erstellen Sie eine temporäre URL.

#### Authentifizierungskonto angeben

Der Swift-Befehl ```stat``` gibt Informationen zu Ihrem Konto aus:

	swift stat

Suchen Sie das Kontofeld (Account) und notieren Sie die vollständige Zeichenfolge hinter *Account*: einschließlich ```AUTH_```.

#### Geheimen Schlüssel festlegen

Dieser Schlüssel kann eine Zeichenfolge Ihrer Wahl sein. Ein bewährtes Verfahren ist, eine lange, zufällig zusammengesetzte und schwer zu erratende Zeichenfolge zu wählen.

	swift post -m "Temp-URL-Key:<Schlüssel>"

#### Temporäre URL erstellen

Der Swift Befehl ```tempurl``` arbeitet mit den folgenden Positionsargumenten:

* [Methode] GET, um das Herunterladen zuzulassen, PUT, um das Hochladen zuzulassen
* [Sekunden] Zeit in Sekunden, die die temporäre URL verfügbar sein soll
* [Pfad] Der vollständige Pfad des Objekts in der Form /v1/<Authentifizierungskonto>/<Containername>/<Objektname>
* [Schlüssel] Der Schlüssel, den Sie in Schritt 2 festgelegt haben

```
swift tempurl GET <Sekunden> <Pfad> <Schlüssel>
```

Dieser Befehl gibt eine URL zurück, die Sie an Ihren Clusternamen anhängen können, um eine vollständige URL zu erhalten. Verwenden Sie die vollständige URL, um das Objekt mit einem kompatiblen HTTP-Client wie curl, wget oder Firefox herunterzuladen.

## Mit der Swift-REST-API auf {{site.data.keyword.objectstorageshort}} zugreifen {: #using-swift-restapi}

Sie können die Swift-REST-API in einer Befehlszeilen-Clientschnittstelle wie cURL verwenden oder Sie können die API in Ihrer Anwendung aufrufen.  

### {{site.data.keyword.objectstorageshort}}-URL {: #access-points}

Zur Interaktion mit der {{site.data.keyword.objectstorageshort}}-API erstellen Sie die {{site.data.keyword.objectstorageshort}}-URL wie folgt:

	https://<Zugriffspunkt>/<API-Version>/AUTH_<Projekt-ID>/<Containernamensbereich>/<object namespace>

Beispiel:

![{{site.data.keyword.objectstorageshort}}-URL](images/Swift_URL.png)

*Abbildung 3. {{site.data.keyword.objectstorageshort}}-URL*

Die URL besteht aus fünf Teilen. Die ```<API-Version>``` ist Version 1. Sie finden die Werte für ```<Projekt-ID>``, ```<Containernamensbereich>`` und ```<object namespace>`` für Ihren {{site.data.keyword.objectstorageshort}} in der {{site.data.keyword.objectstorageshort}}-Benutzerschnittstelle. Informationen für den ```<Zugriffspunkt>`` finden Sie in der folgenden Tabelle: 


| **Region**  |     **Interner Zugriffspunkt**                             |     **Öffentlicher Zugriffspunkt**                   |
|-------------|-----------------------------------------------------------|-----------------------------------------------|
| Dallas      | https://dal.objectstorage.service.open.networklayer.com/  | https://dal.objectstorage.open.softlayer.com/ | 
| London      | https://lon.objectstorage.service.open.networklayer.com/  | https://lon.objectstorage.open.softlayer.com/ |


*Tabelle 1. {{site.data.keyword.objectstorageshort}}-Zugriffspunkt*

Verwenden Sie den internen Zugriffspunkt, wenn Sie auf den {{site.data.keyword.objectstorageshort}}-Service innerhalb von {{site.data.keyword.Bluemix_notm}} zugreifen, oder den öffentlichen Zugriffspunkt, wenn Sie auf den {{site.data.keyword.objectstorageshort}}-Service außerhalb von {{site.data.keyword.Bluemix_notm}} zugreifen.

### {{site.data.keyword.objectstorageshort}}-API

Eine umfassende Liste der Optionen der {{site.data.keyword.objectstorageshort}}-REST-API mit Beispielen finden Sie in der [vollständigen Referenz zur OpenStack-Swift-API](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}.

## {{site.data.keyword.objectstorageshort}} regionsübergreifend verwenden {: #multi-regions}  

Der {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}}-Service unterstützt die Speicherregionen Dallas und London. Diese Speicherregionen sind unabhängig von der {{site.data.keyword.Bluemix_notm}}-Region, wie zum Beispiel 'US-South' und 'United Kingdom', in der die {{site.data.keyword.objectstorageshort}}-Serviceinstanz erstellt wurde.  Beispiel: Wenn Sie eine {{site.data.keyword.objectstorageshort}}-Instanz in der {{site.data.keyword.Bluemix_notm}}-Region 'US-South' erstellen, haben Sie Lese- und Schreibzugriff auf Daten in der Speicherregion Dallas oder in der Speicherregion London.  

Für die {{site.data.keyword.Bluemix_notm}}-Region 'US-South' ist Dallas die Standardspeicherregion. Für die {{site.data.keyword.Bluemix_notm}}-Region 'United Kingdom' ist London die Standardspeicherregion.  Die {{site.data.keyword.objectstorageshort}}-Benutzerschnittstelle startet immer mit der Standardspeicherregion der {{site.data.keyword.Bluemix_notm}}-Region. Wenn Sie die Region wechseln wollen, klicken Sie auf die Dropdown-Liste für die {{site.data.keyword.objectstorageshort}}-Regionen und wählen eine andere Region aus.

![{{site.data.keyword.objectstorageshort}}-Region ändern](images/change_region.png)

*Abbildung 4. {{site.data.keyword.objectstorageshort}}-Region ändern*

**Anmerkung:** Der {{site.data.keyword.objectstorageshort}}-Service unterstützt keine speicherregionsübergreifende Replikation.

### Zugriff auf mehrere Regionen

Für die Verwendung des {{site.data.keyword.objectstorageshort}}-Service müssen Sie sich [bei OpenStack Keystone authentifizieren](#keystone-authentication). Nach der erfolgreichen Authentifizierung werden ein ```X-Subject-Token``` und die {{site.data.keyword.objectstorageshort}}-Endpunkte in der Antwort zur Verfügung gestellt.

Beispiel: Wenn Sie einen Container mit dem Namen ```my_container``` in der Speicherregion Dallas erstellen wollen, geben Sie wie folgt einen Zugriffspunkt von Dallas im curl-Befehl an:

	# curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT


Wenn Sie einen Container mit dem Namen ```my_container``` in der Speicherregion London erstellen wollen, geben Sie wie folgt einen Zugriffspunkt von London im curl-Befehl an:

	# curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT

**Anmerkung:** Das ```X-Subject-Token```, das Sie von Keystone empfangen haben, funktioniert über Speicherregionen hinweg. 

Weitere Informationen zu den Zugriffspunkten für verschiedene Regionen finden Sie in der Tabelle mit den [Object Storage-Zugriffpunkten](#access-points).


## Informationen zu Authentifizierung und Berechtigungsnachweisen {: #understanding-authentication-credentials}

### {{site.data.keyword.objectstorageshort}}-Berechtigungsnachweise ohne Bindung einer Anwendung generieren

Zum Generieren von {{site.data.keyword.objectstorageshort}}-Cloudberechtigungsnachweisen für die Verwendung außerhalb einer {{site.data.keyword.Bluemix_notm}}-Anwendung müssen Sie einen Serviceschlüssel für Ihre {{site.data.keyword.objectstorageshort}}-Instanz generieren. Sie können einen neuen Schlüssel generieren, indem Sie **Serviceberechtigungsnachweise** in der Seitenleiste der Benutzerschnittstelle auswählen oder die Befehlszeilenschnittstelle Cloud Foundry CLI (Version 6.11.3 oder höher) verwenden. Nach der Generierung und dem Abruf eines Serviceschlüssels für Ihre {{site.data.keyword.objectstorageshort}}-Instanz können Sie die Informationen zur Cloudintegration verwenden, um ein Keystone-Token mit einem OpenStack-SDK oder der OpenStack-Identity-API anzufordern und anschließend mit der Verwendung des Swift-Kontos zur Objektverwaltung zu beginnen.
   
Wenn Sie den Schlüssel über Cloud Foundry CLI erstellen möchten, müssen Sie sich bei dieser Befehlszeilenschnittstelle anmelden und den folgenden Befehl ausführen:
 
    cf create-service-key <Object Storage-Instanzname> <eindeutiger Name für diesen Schlüssel>

Führen Sie den folgenden Befehl aus, um die Serviceberechtigungsnachweise über Cloud Foundry CLI abzurufen:

	cf service-key <Object Storage-Instanzname> <eindeutiger Name für diesen Schlüssel>


### Cloudprojekte und -benutzer
Durch die Bereitstellung einer neuen {{site.data.keyword.objectstorageshort}}-Instanz wird in der IBM Public Cloud ein isoliertes Keystone-Projekt erstellt. Wenn Sie eine neue Anwendung an die {{site.data.keyword.objectstorageshort}}-Instanz binden, wird ein neuer Keystone-Benutzer mit Zugriff auf das Projekt erstellt. Wenn Sie die Instanz löschen, werden auch Projekt und Benutzer gelöscht.

### OpenStack Identity (Keystone) v3 {: #keystone-authentication}
Die Struktur der Berechtigungsnachweise enthält einen vollständigen Satz von Attributen, sodass Sie die Methode für die OpenStack-Tokenanforderung oder das OpenStack-SDK auswählen können, das sich am besten für Ihre Anwendung eignet. 
 
Die empfohlene v3-Tokenanforderung ist eine POST-Anforderung an https://identity.open.softlayer.com/v3/auth/tokens, wie im folgenden curl-Befehl gezeigt:

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

Verwenden Sie den Wert des Felds ```X-Subject-Token``` aus dem Antwortheader als ```X-Auth-Token``, wenn Sie Anforderungen an den {{site.data.keyword.objectstorageshort}}-Service senden.

Eine Beispielantwort könnte wie folgt aussehen:

	HTTP/1.1 201 Created
	X-Subject-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9
	Vary: X-Auth-Token
	Content-Type: application/json
	Content-Length: 960
	Date: Tue, 10 Jun 2014 20:40:14 GMT
	
	{"token": 
	{"audit_ids": ["ECwrVNWbSCqmEgPnu0YCRw"], "methods": ["password"],
	 "roles": [{"id": "c703057be878458588961ce9a0ce686b", "name": "admin"}],
	 "expires_at": "2014-06-10T21:40:14.360795Z", 
	 "project": {"domain": {"id": "default", "name": "Default"}, "id": "3d4c2c82bd5948f0bcab0cf3a7c9b48c", "name": "demo"}, 
	 "catalog": [
	 {
		"endpoints": [
			{
			"adminURL": "https://lon.objectstorage.service.open.networklayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"id": "20cbfa6ff22b4a67a1484d30235bfc80",
			"internalURL": "https://lon.objectstorage.service.open.networklayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"publicURL": "https://lon.objectstorage.open.softlayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"region": "london"
			},
			{
			"adminURL": "https://dal.objectstorage.service.open.networklayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"id": "4207049680fa4effbecd044c7448a8cb",
			"internalURL": "https://dal.objectstorage.service.open.networklayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"publicURL": "https://dal.objectstorage.open.softlayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"region": "dallas"
			}
			],
		"endpoints_links": [],
		"name": "swift",
		"type": "object-store"
		},
	 ], 
	 "extras": {},
	 "user": {"domain": {"id": "default", "name": "Default"}, "id": "3ec3164f750146be97f21559ee4d9c51", "name": "admin"},  "issued_at": "2014-06-10T20:40:14.360822Z"}}


Die {{site.data.keyword.objectstorageshort}}-URL ist im Servicekatalog zu finden. Der Servicekatalog ist im Antworthauptteil der Tokenanforderung enthalten. Die Antwort ist ein vollständiger Katalog der OpenStack-Services, die verfügbar sind. Wählen Sie den Endpunkt im Servicekatalog mit dem Typ ```object-store``` und mit der Region, die dem Feld für die Region in den Berechtigungsnachweisen entspricht, sowie die interne Schnittstelle (`internalURL`) aus, wenn Sie auf den {{site.data.keyword.objectstorageshort}}-Service innerhalb von {{site.data.keyword.Bluemix_notm}} zugreifen, bzw. wählen Sie die öffentliche Schnittstelle (`publicURL`) aus, wenn Sie auf den {{site.data.keyword.objectstorageshort}}-Service außerhalb von {{site.data.keyword.Bluemix_notm}} zugreifen.



## Bindung und Bereitstellung von {{site.data.keyword.objectstorageshort}} aufheben {: #deprovisioning-object-storage}

### Vorgehensweise zum Löschen Ihres {{site.data.keyword.objectstorageshort}}-Service
1.	Wählen Sie Ihren Service im {{site.data.keyword.Bluemix_notm}}-Dashboard aus.  
2.	Klicken Sie in der rechten oberen Ecke auf das Zahnradsymbol und wählen Sie **Service löschen** aus.
	
**Warnung:** Wenn Sie eine IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}}-Serviceinstanz löschen, werden das Cloudprojekt und das Swift-Konto gelöscht. Alle Container und Objekte in der gelöschten Instanz werden aus Swift gelöscht und können nicht wiederhergestellt werden.

### Bindung für eine Anwendung aufheben oder einen Serviceschlüssel löschen

Wenn Sie die Bindung einer Anwendung an die {{site.data.keyword.objectstorageshort}}-Instanz aufheben oder den Serviceschlüssel löschen, werden die Berechtigungsnachweise gelöscht. Das {{site.data.keyword.objectstorageshort}}-Konto wird erst gelöscht, wenn die Bereitstellung der {{site.data.keyword.objectstorageshort}}-Instanz aufgehoben wird. Sie können neue Cloudberechtigungsnachweise generieren, indem Sie einen [neuen Serviceschlüssel binden oder erstellen](#bind-object-storage-to-application).

## FAQ {: #FAQ} 

### Wie variieren die Preise je nach ausgewähltem Plan?
Die Preisgestaltung ist vom ausgewählten Plan abhängig. Weitere Informationen zu Preisen finden Sie in der [IBM Bluemix-Preisliste](https://console.ng.bluemix.net/pricing/){: new_window} oder verwenden Sie den [Preisrechner](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet){: new_window}, um detailliertere Preisschätzungen zu ermitteln.

### Wie wird der Plan von der Beta-Version in die Standardversion geändert? {: #changeplan}  
Der Beta-Plan für den {{site.data.keyword.objectstorageshort}}-Service wird nach der allgemeinen Verfügbarkeit (GA) des {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}}-Service aus dem Katalog entfernt. Serviceinstanzen von Kunden werden möglicherweise nicht automatisch vom Beta-Plan auf den Standardplan migriert. Sie müssen die folgenden Schritte ausführen, um Ihren Plan zu aktualisieren:

1.	Klicken Sie in der Navigationsleiste auf der linken Seite in der {{site.data.keyword.objectstorageshort}}-Benutzerschnittstelle auf **Plan**.
2.	Wählen **Standard** als neuen Plan aus und klicken Sie auf **Speichern**.

![{{site.data.keyword.objectstorageshort}}-Preistarif ändern](images/Change_plan.png)

*Abbildung 5. {{site.data.keyword.objectstorageshort}}Preistarif ändern*

Ihre Serviceinstanzen und Kundendaten werden in den neuen Plan versetzt.

Sie können außerdem Ihren Zahlungsplan über die Befehlszeilenschnittstelle ändern. Weitere Informationen finden Sie in [Vorgehensweise zum Ändern des Plans](../../pricing/index.html#changing).  

**Anmerkung:** Serviceinstanzen des Beta-Plans können nicht in den kostenlosen Plan versetzt werden. Alle Serviceinstanzen, die nicht migriert werden, werden inaktiviert und nach 60 Tagen gelöscht. 

### Welche Konten und Zahlungspläne können für {{site.data.keyword.objectstorageshort}} verwendet werden?
Der {{site.data.keyword.objectstorageshort}}-Service wird mit mehreren Planoptionen bereitgestellt. Mit dem Release der allgemeinen Verfügbarkeit werden gegenwärtig zwei Pläne angeboten: Standard und Kostenlos. Der Standardplan ist nur für gebührenpflichtige {{site.data.keyword.Bluemix_notm}}-Konten verfügbar, entweder für 'Nutzungsabhängig' oder für 'Abonnement', sowie für interne IBM Benutzer.

Testkonten, die weiterhin aktiv sind, können den kostenlosen Plan nutzen, der nur das Vorhandensein einer Instanz in einer {{site.data.keyword.Bluemix_notm}}-Organisation zulässt. Wenn der Zeitraum für den {{site.data.keyword.Bluemix_notm}}-Test abläuft, wird die zugeordnete {{site.data.keyword.objectstorageshort}}-Serviceinstanz inaktiviert. Dies bedeutet, dass weder die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle noch die Befehlszeile auf das Speicherkonto zugreifen kann. Nach einer Frist von 30 Tagen wird Ihr {{site.data.keyword.Bluemix_notm}}-Konto bereinigt und alle Daten werden gelöscht. Zur Vermeidung von Datenverlust wird empfohlen, das gebührenpflichtige {{site.data.keyword.Bluemix_notm}}-Konto so bald wie möglich zu aktualisieren. Zum Aktualisieren Ihres Kontos klicken Sie auf das Benutzermanagementmenü in der rechten oberen Ecke und wählen **Konto** aus. Dadurch werden Anweisungen zum Aktualisierungsprozess bereitgestellt.

Instanzen, die im kostenlosen Plan erstellt werden, können mit den unter [Wie wird der Plan von der Beta-Version in die Standardversion geändert?](#changeplan) beschriebenen Schritten, auf den Standardplan aktualisiert werden. Zum Aktualisieren des Standardplans muss die zugeordnete Organisation ein gebührenpflichtiges {{site.data.keyword.Bluemix_notm}}-Konto sein. Testkonten mit {{site.data.keyword.objectstorageshort}}-Instanzen können nicht auf den Standardplan aktualisiert werden und Instanzen im Standardplan können nicht auf andere Pläne herabgestuft werden.

### Welche Gebühren werden für meine Nutzung von {{site.data.keyword.objectstorageshort}} fällig und wann werden sie in Rechnung gestellt?

Für den Service {{site.data.keyword.objectstorageshort}} werden nur Gebühren für das, was Sie nutzen, fällig.  Um mit der Verwendung des Service zu beginnen, sind keine Mindestgebühren oder Konfigurationsgebühren zu entrichten und es sind auch keine sonstigen Verpflichtungen einzugehen. Es sind keine Gebühren für API-Anforderungen oder für Netzverkehr für eingehende Daten zu entrichten.

Ihre Nutzung von {{site.data.keyword.objectstorageshort}} wird während des gesamten Fakturierungszyklus auf der Grundlage der durchschnittlichen Speichernutzung pro Tag in Rechnung gestellt. Dies schließt alle Objektdaten in Containern ein, die Sie mit Ihrem {{site.data.keyword.Bluemix_notm}}-Organisationskonto erstellt haben. 

Gebühren für die Übertragung abgehender Daten wird fällig, soabald Daten aus einem Ihrer Objektcontainer über das öffentliche Netz gelesen werden. Die Nutzung wird während des gesamten Fakturierungszyklus auf der Grundlage der durchschnittlichen öffentlichen Übertragung abgehender Daten pro Tag in Rechnung gestellt. 

Die Metrikkomponenten für die Preisbestimmung von {{site.data.keyword.objectstorageshort}} sind folgende:
* Speichernutzung - $0.04 pro GB pro Monat
* Öffentliche Übertragung abgehender Daten - $0.09 pro GB pro Monat 

Am Ende des Fakturierungszyklus wird Ihnen die Nutzung während des momentanen Fakturierungszeitraums von {{site.data.keyword.Bluemix_notm}} automatisch in Rechnung gestellt. Sie können Ihre Gebühren für den momentanen Fakturierungszeitraum über die {{site.data.keyword.Bluemix_notm}}-Berichterstellungsfunktion einsehen.

Der für London und Dallas freigegebene Standardserviceplan unterliegt derselben Preisbestimmung.

### Wie funktioniert die Datenreplikation in {{site.data.keyword.objectstorageshort}}?
Der Service {{site.data.keyword.objectstorageshort}} pflegt drei Kopien Ihrer Daten, die in mehreren Speicherknoten repliziert werden. Weitere Informationen finden Sie in der Dokumentation [OpenStack Swift Replication](http://docs.openstack.org/developer/swift/overview_replication.html){: new_window}.

># Zugehörige Links {:class="linklist"}
>## API-Referenz {:id="api"}
>* [OpenStack Object Storage (Swift) API v1](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}
>* [OpenStack Identity (Keystone) API v3.0](http://developer.openstack.org/api-ref-identity-v3.html){: new_window}
>
># Zugehörige Links {:class="linklist"}
>## SDK {:id="sdk"}
>* [OpenStack Software Development Kits (SDK)](https://wiki.openstack.org/wiki/SDKs){: new_window}
>
># Zugehörige Links {:class="linklist"}
>## Lernprogramme und Beispiele {:id="samples"}
>* [Verbindung zu IBM Object Storage for Bluemix mit Java herstellen](https://developer.ibm.com/recipes/tutorials/connecting-to-ibm-object-storage-for-bluemix-with-java/){: new_window}
>* [Mit Python auf Bluemix Object Storage zugreifen](https://developer.ibm.com/recipes/tutorials/use-python-to-access-your-bluemix-object-storage/){: new_window}
>* [Bluemix Object Storage-Community](https://www.ibm.com/developerworks/community/groups/service/html/communityoverview?communityUuid=1b48459f-4091-43cb-bca4-37863606d989){: new_window}
>
># Zugehörige Links {:class="linklist"}
>## Kompatible Laufzeiten {:id="buildpacks"}
>* [Liberty for Java](https://www.ng.bluemix.net/docs/starters/liberty/index.html){: new_window}
>* [SDK for Node.js](https://www.ng.bluemix.net/docs/starters/nodejs/index.html){: new_window}
>* [Go](https://www.ng.bluemix.net/docs/starters/go/index.html){: new_window}
>* [PHP](https://www.ng.bluemix.net/docs/starters/php/index.html){: new_window}
>* [Python](https://www.ng.bluemix.net/docs/starters/python/index.html){: new_window}
>* [Ruby](https://www.ng.bluemix.net/docs/starters/rails/index.html){: new_window}
>* [Community-Buildpacks](https://www.ng.bluemix.net/docs/starters/byob.html){: new_window}
>
># Zugehörige Links {:class="linklist"}
>## Zugehörige Links {:id="general"}
>* [IBM Bluemix-Preisliste](https://www.ng.bluemix.net/#/pricing){: new_window}
>* [Voraussetzung für IBM Bluemix](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
>
>{:elementKind="article" id="rellinks"}
