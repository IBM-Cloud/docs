---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Mit umfangreichen Dateien arbeiten{: #large-files}
*Letzte Aktualisierung: 19. Oktober 2016*
{: .last-updated}

Das Hochladen von Objekten ist auf eine maximale Größe von 5 GB bei einem einzigen Übertragungsvorgang beschränkt. Sie können aber Objekte, die größer sind als 5 GB, hochladen, nachdem Sie sie in kleinere Objekte segmentiert haben. Nach dem Hochladen der segmentierten Objekte ist außerdem eine Manifestdatei erforderlich, um die Segmente zum ursprünglichen Objekt zu verketten. Dafür gibt es zwei Wege: über dynamische große Objekte (Dynamic Large Objects, DLO) und über statische große Objekte (Static Large Objects, SLO).
{: shortdesc}

### Dynamic Large Objects (DLO): {: #dynamic}

Für die Bearbeitung von DLO gibt es zwei Methoden:
  * Der Swift-Client bearbeitet alle Objekte automatisch
  * Sie bearbeiten die Objekte manuell unter Verwendung der Swift-API

#### Verwendung des Swift-Clients zur Bearbeitung von DLO

Der Swift-Client verwendet den Parameter `-segment-size`, um Ihr Objekt in kleinere Teile aufzugliedern. Der Client erstellt einen neuen Container mit dem Namen des Containers, in den die Dateien hochgeladen werden sollen, und fügt ein Suffix mit der Segmentnummer (`<Containername>_segments`) hinzu. Die Segmente werden parallel hochgeladen. Nachdem alle Segmente hochgeladen sind, werden sie als ein einziges verkettetes Objekt in eine Manifestdatei mit dem ursprünglichen Dateinamen heruntergeladen.

1. Nachdem Sie sich bei {{site.data.keyword.Bluemix_notm}} angemeldet haben und Sie für den Upload bereit sind, führen Sie folgenden Befehl aus, um Ihre Datei zu segmentieren.

    ```
    swift upload <Containername> <Dateiname> --segment-size <Größe_in_Byte>
    ```
    {: pre}

#### Verwendung der Swift-API zur Bearbeiten von DLO

Sie können die Objekte manuell auf eine Größe von maximal 5 GB segmentieren und sie anschließend über die Swift-API hochladen. Beim Hochladen ist es wichtig, zuerst alle Segmente hochzuladen, bevor das Manifest hochgeladen wird. Wenn das Objekt heruntergeladen wird, bevor alle Segmente fertig gestellt sind, wird das heruntergeladene Objekt inkonsistent sein. Sie können große Dateien hochladen, indem Sie folgende Schritte durchführen.

1. Sortieren Sie die Segmente nach Namen in der Reihenfolge, in der sie zur Bildung des ursprünglichen Objekts verkettet werden sollen.
2. Laden Sie Ihre Segmente in einen einzigen Container hoch, der von dem Container getrennt ist, der die Manifestdatei enthält. Die Regulierung für Uploads startet nach dem Hochladen des 10. Segments und erhöht die Zeit für das Hochladen erheblich. Aus diesem Grund wird empfohlen, dass die Segmente nicht kleiner als ein Zehntel der Datei werden zu lassen.

    ```
    curl -i -X PUT --data-binary @segment1 -H "X-Auth-Token: <token>" https://<Objektspeicher-URL>/<Containername>/<Objektname>/000001
    curl -i -X PUT --data-binary @segment2 -H "X-Auth-Token: <token>" https://<Objektspeicher-URL>/<Containername>/<Objektname>/000002
    ```
    {: pre}
    
3. Laden Sie eine leere Manifestdatei hoch, wobei der Header `X-Object-Manifest` auf den entsprechenden Wert für `<container>/prefix>` festgelegt ist.

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Object-Manifest: <Containername>/<Objektname>/" https://<Objektspeicher-URL>/<Manifest-Containername>/<Objektname>
    ```
    {: pre}
    
    **Hinweis**: Die Manifestdatei muss leer sein. Ist sie nicht leer, wird der Inhalt der Datei als eines der Segmente betrachtet und fällt in die Reihenfolge der Verkettung, die von den sortierten Namen bestimmt ist.
4. Laden Sie das Objekt herunter. Sie erhalten als Ergebnis das gesamte Objekt. Sie können Segmente hinzufügen oder entfernen, ohne die Manifestdatei aktualisieren zu müssen. Segmente mit dem korrekten Präfix bleiben ein Teil des Objekts. Beim Löschen des Manifests werden die Segmente nicht gelöscht.

    ```
    curl -i -O -H "X-Auth-Token: <token>" https://<Objektspeicher-URL>/<Manifest-Containername>/<Objektname>
    ```
    {: pre}


### Static Large Objects (SLO){: #static}

Statische große Objekte (Static Large Objects, SLO) verwenden Segmente und eine Manifestdatei, ermöglichen Ihnen aber eine größere Kontrolle. Bei SLO müssen sich die Segmente nicht im selben Container befinden; jedes Segment kann in einem beliebigen Container gespeichert werden und mit beliebigen Namen benannt werden. Die Segmente müssen jedoch eine Größe von mindestens 1 MB aufweisen. Es ist nicht erforderlich, einen Header für die Manifestdatei einzurichten, wenngleich der Header "X-Static-Large-Object" automatisch hinzugefügt und nach dem Hochladen eines korrekten Manifests auf 'true' gesetzt wird.
{: shortdesc}

Die Manifestdatei ist ein JSON-Dokument, das Details der Segmente bereitstellt und hochgeladen werden muss, nachdem alle Segmente hochgeladen wurden. Die für jedes Segment bereitgestellten Daten im Manifest werden mit den Metadaten der tatsächlichen Segmente verglichen. Wenn Elemente nicht übereinstimmen, wird das Manifest nicht hochgeladen.

<table>
  <tr>
    <th> Attribut</th>
    <th> Beschreibung</th>
  </tr>
  <tr>
    <td> Pfad</td>
    <td> Die Position und der Name des Segments. Angegeben mit Containername/Objektname. </td>
  </tr>
  <tr>
    <td> etag</td>
    <td> Wird beim Hochladen des Objekts von der PUT-Anforderung bereitgestellt. Sie finden dieses Attribut auch, indem Sie eine HEAD-Operation am Objekt ausführen. </td>
  </tr>
  <tr>
    <td> Größe_in_Byte</td>
    <td> Die Größe des Objekts in Byte.</td>
  </tr>
</table>

*Tabelle 1: JSON-Attribute in der Manifestdatei in der Reihenfolge ihrer Verkettung*

Sie können große Dateien hochladen, indem Sie folgende Schritte durchführen:

1. Führen Sie folgenden Befehl aus, um die Segmente hochzuladen. Die Regulierung für Uploads startet nach dem Hochladen des 10. Segments und erhöht die Zeit für das Hochladen erheblich. Aus diesem Grund wird empfohlen, die Segmente nicht kleiner als ein Zehntel der Datei werden zu lassen.

    ```
    curl -i -X PUT --data-binary @segment1 -H "X-Auth-Token: <token>" https://<Objektspeicher-URL>/<container_one>/<segment>
    curl -i -X PUT --data-binary @segment2 -H "X-Auth-Token: <token>" https://<Objektspeicher-URL>/<container_two>/<segment>
    curl -i -X PUT --data-binary @segment3 -H "X-Auth-Token: <token>" https://<Objektspeicher-URL>/<container_one>/<segment>
    ```
    {: pre}
    
2. Erstellen Sie das Manifest:

    ```
    [
        {
            "Pfad": "<container_one>/<segment>",
            "etag": "e0ed3b751eb8d4b2c648d2dd78576e36",
            "Größe_in_Byte": 801882690
        },
        {
            "path": "container_two/<segment>",
            "etag": "65a301e71c82cbd325a5efe5877e1a24",
            "Größe_in_Byte": 1048576
        },
        {
            "Pfad": "<container_one>/<segment>",
            "etag": "aea8b7462d527ad5ed0cfc22ea161062",
            "Größe_in_Byte": 138257
        }
    ]
    ```
    {: pre}
    
3. Laden Sie das Manifest hoch. Dazu müssen Sie die Abfrage `multipart-manifest=put` dem Namen des Manifests hinzufügen, indem Sie folgenden Befehl ausführen:

    ```
    curl -i -X PUT --data-binary @object_name -H "X-Auth-Token: <token>" https://<Objektspeicher-URL>/container_two/<Objektname>?multipart-manifest=put
    ```
    {: pre}
    
4. Laden Sie das Objekt herunter.

    ```
    curl -O -X GET -H "X-Auth-Token: <token>" https://<Objektspeicher-URL>/<container_two>/<Objektname>
    ```
    {: pre}
    
Nachstehend einige Befehle, die Sie bei der Arbeit mit SLO möglicherweise benötigen.

* Zum Herunterladen des Inhalts der Manifestdatei müssen Sie Ihrem Befehl die Abfrage `multipart-manifest=get` hinzufügen. Der Inhalt, den Sie erhalten, wird nicht identisch mit dem hochgeladenen Inhalt sein.

    ```
    curl -O -X GET -H "X-Auth-Token:<token>" https://<Objektspeicher-URL>/<container_two>/<Objektname>?multipart-manifest=get
    ```
    {: pre}
    
* Zum Löschen des Manifests führen Sie den folgenden Befehl aus:

    ```
    curl -i -X DELETE -H "X-Auth-Token: <token>" https://<Objektspeicher-URL>/<container_two>/<Objektname>
    ```
    {: pre}
    
* Zum Löschen des Manifests und aller Segmente fügen Sie die Abfrage `multipart-manifest=delete` nach dem Namen des Manifests hinzu:

    ```
    curl -i -X DELETE -H "X-Auth-Token: <token>" https://<Objektspeicher-URL>/<container_two>/<Objektname>?multipart-manifest=delete
    ```
    {: pre}

**Hinweis**: Zum Hinzufügen von Segmenten zum Objekt oder zum Entfernen von Segmenten aus dem Objekt müssen Sie eine neue Manifestdatei mit einer neuen Liste von Segmenten hochladen. Der Manifestname kann belassen werden.
