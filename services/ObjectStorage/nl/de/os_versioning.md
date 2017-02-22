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


# Objektversionierung einrichten {: #setting-up-versioning}

Sie können ältere Versionen Ihrer Objekte automatisch beibehalten, indem Sie die Objektversionierung einrichten. Die Versionierung ermöglicht die Anzeige eine Verlaufsprotokolls für jedes Objekt.
{: shortdesc}

Wenn Sie eine neue Version Ihrer Datei in den Hauptcontainer hochladen, wird die vorherige Version automatisch in den Sicherungscontainer verschoben. Wenn Sie die Datei aus Ihrem Hauptcontainer löschen, wird die aktuelle Version automatisch vom Sicherungscontainer in den Hauptcontainer verschoben, um die gelöschte Datei zu ersetzen.

1. Erstellen Sie einen Container und geben Sie ihm einen Namen. Ersetzen Sie die Variable *Containername* mit dem Namen, den Sie dem Container geben möchten.

    ```
    swift post <Containername>
    ```
    {: pre}

2. Erstellen Sie einen zweiten Container als Sicherungsspeicher und geben Sie ihm einen Namen.

    ```
    swift post <Sicherungscontainer-Name>
    ```
    {: pre}

3. Richten Sie die Versionierung ein.

    Swift-Befehl:

    ```
    swift post <Containername> -H "X-Versions-Location:<Sicherungscontainer-Name>"
    ```
    {: pre}

    cURL-Befehl:

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:<Sicherungscontainer-Name>" https://<Objektspeicher-URL>/<Containername>
    ```
    {: pre}

4. Laden Sie erstmalig ein Objekt in Ihren Hauptcontainer hoch.

    ```
    swift upload <Containername> <object>
    ```
    {: pre}

5. Nehmen Sie eine Änderung an Ihrem Objekt vor.

6. Laden Sie die neue Version des Objekts in Ihren Hauptcontainer hoch.

    ```
    swift upload <Containername> <object>
    ```
    {: pre}

7.  Die Objekte in Ihrem Sicherungscontainer werden automatisch im folgenden Format benannt: `<Länge><Objektname>/<Zeitmarke>`.
  <table>
  <caption> Tabelle 1. Beschriebene Benennungsattribute</caption>
    <tr>
      <th> Attribut </th>
      <th> Beschreibung </th>
    </tr>
    <tr>
      <td> <i>Länge</i> </td>
      <td> Die Länge des Namens Ihres Objekts. Dies ist eine aus 3 Zeichen bestehende Hexadezimalzahl ohne Innenabstand. </td>
    </tr>
    <tr>
      <td> <i>Objektname</i> </td>
      <td> Der Name Ihres Objekts. </td>
    </tr>
    <tr>
      <td> <i>Zeitmarke</i> </td>
      <td> Die Zeitmarke für den ursprünglichen Upload dieser Version. </td>
    </tr>
  </table>


6. Listen Sie die Objekte in Ihrem Hauptcontainer auf, um die neue Version der Datei anzuzeigen.

    ```
    swift list --lh <Containername>
    ```
    {: pre}

7. Listen Sie Objekte in Ihrem Sicherungscontainer auf. Sie sehen, dass die vorherige Version Ihrer Datei in diesem Container gespeichert ist. Beachten Sie, das der Datei eine Zeitmarke hinzugefügt wird. 

    ```
    swift list --lh <Sicherungscontainer-Name>
    ```
    {: pre}

8. Löschen Sie das Objekt in Ihrem Hauptcontainer. Wenn Sie das Objekt löschen, wird die aktuelle Version in Ihrem Sicherungscontainer automatisch zurück in Ihren Hauptcontainer verschoben.

    ```
    swift delete <Containername> <object>
    ```
    {: pre}

9. Optional: Inaktivieren Sie die Objektversionierung.

    Swift-Befehl:

    ```
    swift post <Containername> -H "X-Remove-Versions-Location:"
    ```
    {: pre}

    cURL-Befehl:

    ```
    cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<Objektspeicher-URL>/<Containername>
    ```
    {: pre}
