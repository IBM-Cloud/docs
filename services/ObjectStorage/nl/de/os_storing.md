---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Objekte speichern

Sie können Objekte über die Benutzerschnittstelle oder die CLI in den Speicher hochladen. Das Hochladen von Objekten ist auf eine maximale Größe von 5 GB bei einem einzigen Übertragungsvorgang beschränkt. Sie können jedoch größere Objekte hochladen, indem Sie sie in kleinere Objekte segmentieren.
{: shortdesc}


## Objekte in Containern über die Benutzerschnittstelle speichern {: #storing-ui}

**Hinweis**: Wenn Sie eine Datei mit demselben Namen hochladen, ersetzt {{site.data.keyword.objectstorageshort}} die gespeicherte Datei durch die neue Datei. Wenn Sie eine Datei herunterladen und diese bearbeiten, stellen Sie sicher, dass sie der Datei einen anderen Namen geben oder vor dem Hochladen [die Objektversionierung einrichten](/docs/services/ObjectStorage/os_versioning.html), um beide Versionen der Datei beizubehalten.


1. Fügen Sie im Dashboard der Serviceinstanz über das Dropdown-Menü **Aktionen** einen Container hinzu.
2. Geben Sie dem Container einen Namen und klicken Sie auf **ERSTELLEN**.
3. Wählen Sie im Dropdown-Menü **Aktionen** die Option **Dateien hinzufügen** aus. Es wird ein Dialogfeld geöffnet.
4. Wählen Sie die Datei oder die Dateien aus, die Sie hochladen möchten, und klicken Sie auf **Öffnen**.



## Mithilfe der CLI Objekte in Containern speichern {: #storing-cli}

1. Wenn Sie nicht bei {{site.data.keyword.Bluemix_notm}} angemeldet sind, melden Sie sich bei der Organisation und dem Bereich mit Ihrer Instanz von {{site.data.keyword.objectstorageshort}} an.

  ```
  cf login -a api.ng.bluemix.net -u <Benutzer-ID> -p <Kennwort> -o <Organisation> -s <Bereich>
  ```
  {: pre}

2. Erstellen Sie einen {{site.data.keyword.objectstorageshort}}-Container, indem Sie folgenden Befehl ausführen. Die Variable *Containername* wird jetzt von Ihnen festgelegt.

  ```
  swift post <Containername>
  ```
  {: pre}

  **Hinweis**: Wenn Sie eine Fehlernachricht erhalten, stellen Sie sicher, dass die [Softwarevoraussetzungen](/docs/services/ObjectStorage/os_configuring.html#install-swift-client) installiert sind.

3. Optional: Um zu überprüfen, ob Ihr Container erstellt wurde, führen Sie folgenden Befehl zur Auflistung Ihrer Container aus.

  ```
  swift list
  ```
  {: pre}

4. Um zu vermeiden, dass Daten durch unbeabsichtigte Überschreibungsaktionen zerstört werden, [richten Sie die Objektversionierung ein](/docs/services/ObjectStorage/os_versioning.html). Wenn Sie keine Objektversionierung wünschen, listen Sie Ihre im Speicher vorhandenen Dateien auf und, falls dies erforderlich sein sollte, benennen Sie das Verzeichnis oder die Dateien vor dem Hochladen um.

5. Laden Sie eine Datei in Ihren Container hoch, indem Sie folgenden Befehl ausführen.

  ```
  swift upload <Containername> <Dateiname>
  ```
  {: pre}

  **Hinweis**: Zum Hochladen von Dateien von mehr als 5 GB [sind zusätzliche Schritte erforderlich](/docs/services/ObjectStorage/os_large_files.html).

6. Optional: Um zu überprüfen, ob der Upload erfolgreich war, führen Sie den folgenden Befehl aus, mit dem der Inhalt Ihres Containers angezeigt wird.

  ```
  swift list <Containername>
  ```
  {: pre}
