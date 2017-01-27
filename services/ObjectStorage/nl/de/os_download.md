---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Objekte herunterladen

Sie können gespeicherte Objekte zur Überprüfung oder Bearbeitung über die Benutzerschnittstelle oder CLI herunterladen.
{: shortdesc}


## Objekte über die Benutzerschnittstelle herunterladen {: #downloading-ui}

1. Um zu vermeiden, dass Daten durch unbeabsichtigte Überschreibungsaktionen zerstört werden, [richten Sie die Objektversionierung ein](/docs/services/ObjectStorage/os_versioning.html). Wenn Sie keine Objektversionierung wünschen, benennen Sie das Verzeichnis oder die Dateien vor dem Herunterladen bei Bedarf um.
2. Wählen Sie im Dashboard der Serviceinstanz den Container mit der Datei aus, die heruntergeladen werden soll.
3. Wählen Sie die Datei aus.
4. Wählen Sie im Dropdown-Menü **Aktionen** die Option **Datei herunterladen** aus.


## Mithilfe der Swift-CLI Objekte herunterladen {: #downloading-cli}

1.  Wenn Sie nicht bei {{site.data.keyword.Bluemix_notm}} angemeldet sind, melden Sie sich bei der Organisation und dem Bereich mit Ihrer Instanz von {{site.data.keyword.objectstorageshort}} an.

```
cf login -a api.ng.bluemix.net -u <Benutzer-ID> -p <Kennwort> -o <Organisation> -s <Bereich>
```
{: pre}

2. Um zu vermeiden, dass Daten durch unbeabsichtigte Überschreibungsaktionen zerstört werden, [richten Sie die Objektversionierung ein](/docs/services/ObjectStorage/os_versioning.html). Wenn Sie keine Objektversionierung wünschen, listen Sie Ihre im Speicher vorhandenen Dateien auf und, falls dies erforderlich sein sollte, benennen Sie das Verzeichnis oder die Dateien vor dem Herunterladen um.

3. Laden Sie eine Datei herunter, indem Sie folgenden Befehl ausführen:

```
swift download <Containername> <Dateiname>
```
{: pre}
