---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Mit Objektversionierung arbeiten {: #work-with-object-versioning}

*Letzte Aktualisierung: 19. Oktober 2016*
{: .last-updated}

Mit Objektversionierung haben Sie die Möglichkeit, getrennte Versionen Ihrer Objekte beizubehalten, ohne Ihre Dateien umbenennen zu müssen. Dies ermöglicht Ihnen die Anzeige des Verlaufs für jedes Objekt und die Verfolgung von Änderungen.
{: shortdesc}


### Objektversionierung einrichten{: #setting-up-versioning}

Sie können unter Verwendung des Parameters `X-Versions-Location` Versionen jedes Objekts in Ihrem Container einrichten. Erstellen Sie hierfür wie folgt einen weiteren Container, um ältere Versionen Ihrer Objekte aufzubewahren.

Sie können Objektversionierung über den Swift-Client oder unter Verwendung von cURL-Befehlen einrichten.
* Wenn Sie den Swift-Client verwenden, führen Sie den folgenden Befehl aus:

    ```
    swift post <Containername> -H "X-Versions-Location:<Sicherungscontainer-Name>"
    ```
    {: pre}
    
* Bei Verwendung von cURL können Sie die Einrichtung wie folgt vornehmen:

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:<Sicherungscontainer-Name>" https://<Objektspeicher-URL>/<Containername>
    ```
    {: pre}
    
**Hinweis**: Die Objekte in Ihrem Sicherungscontainer werden automatisch im folgenden Format benannt: `<Länge><Objektname>/<Zeitmarke>`.
<table>
  <tr>
    <th> Attribut</th>
    <th> Beschreibung</th>
  </tr>
  <tr>
    <td> `Länge` </td>
    <td> Die Länge des Namens Ihres Objekts. Dies ist eine aus 3 Zeichen bestehende Hexadezimalzahl ohne Innenabstand.</td>
  </tr>
  <tr>
    <td> `Objektname` </td>
    <td> Der Name Ihres Objekts.</td>
  </tr>
  <tr>
    <td> `Zeitmarke` </td>
    <td> Die Zeitmarke für den ursprünglichen Upload dieser Version.</td>
  </tr>
</table>

### Objektversionierung inaktivieren{: #disabling-versioning}

Sie können die Versionierung über den Swift-Client oder unter Verwendung von cURL-Befehlen einrichten.

* Zur Verwendung des Swift-Clients führen Sie folgenden Befehl aus:

    ```
    swift post <Containername> -H "X-Remove-Versions-Location:"
    ```
    {: pre}
    
* Führen Sie folgenden cURL-Befehl aus, um die Versionierung zu inaktivieren:

    ```
    cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<Objektspeicher-URL>/<Containername>
    ```
    {: pre}


### Lernprogramm zur Objektversionierung{: #versioning-tutorial}
<!--- SHAWNA: This needs more background information. What are they doing? Why are they doing it? What is the outcome? --->

Das folgende Lernprogramm vermittelt Ihnen ein Verständnis des vollständigen Lebenszyklus der Objektversionierung.

1. Erstellen Sie einen Container mit dem Namen `container_one`.

    ```
    swift post container_one
    ```
    {: pre}
    
3. Erstellen Sie einen zweiten Container mit dem Namen `container_two`.

    ```
    swift post container_two
    ```
    {: pre}
    
2. Richten Sie die Versionierung ein.

    ```
    swift post container_one -H "X-Versions-Location:container_two"
    ```
    {: pre}
    
4. Laden Sie erstmalig ein Objekt in Ihren Hauptcontainer hoch.

    ```
    swift upload container_one object
    ```
    {: pre}
    
7. Laden Sie eine neue Version des Objekts nach container_one hoch. Wenn Sie eine neue Version Ihrer Datei hochladen, wird die vorherige Version automatisch in den Sicherungscontainer verschoben, den Sie bei der Versionierungseinrichtung angegeben haben.

    ```
    swift upload container_one object
    ```
    {: pre}
    
8. Um die neue Version Ihrer Datei im Container anzuzeigen, listen Sie die Objekte in container_one auf.

    ```
    swift list container_one
    ```
    {: pre}
    
9. Listen Sie die Objekte in container_two auf. Sie stellen fest, dass die vorherige Version Ihrer Datei in diesem Container gespeichert wird.

    ```
    swift list container_two
    ```
    {: pre}
    
10. Löschen Sie das Objekt in container_one. Wenn Sie das Objekt löschen, wird die vorherige Version in Ihrem Sicherungscontainer automatisch in Ihren Hauptcontainer verschoben.

    ```
    swift delete container_one object
    ```
    {: pre}
    
11. Listen Sie beide Container auf. Sie stellen fest, dass Ihre ursprüngliche Datei in `container_one` und `container_two` leer ist.

    ```
    swift list container_one
    swift list container_two
    ```
    {: pre}
