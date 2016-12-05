---

copyright:
  years: 2014, 2016
lastupdated: "2016-11-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Temporäre URL erstellen {: #create-temporary-url}


Eine temporäre URL ist eine lange, schwer zu erratende URL, die für einen angegebenen Zeitraum zum Herunterladen von Objekten verwendet werden kann, ohne dass eine weitere Authentifizierung erforderlich ist.
{: shortdesc}


1. Ermitteln Sie Ihre Authentifizierungsinformationen durch Ausdrucken Ihrer Kontoinformationen, indem Sie folgenden Befehl ausführen:
```
swift stat
```
{: pre}

**Hinweis**: Suchen Sie das Kontofeld ("Account") und notieren Sie die vollständige Zeichenfolge hinter *Account*: einschließlich `AUTH_`.

2. Legen Sie einen geheimen Schlüssel fest. Dieser Schlüssel kann eine Zeichenfolge Ihrer Wahl sein. Ein bewährtes Verfahren ist, eine lange, zufällig zusammengesetzte und schwer zu erratende Zeichenfolge zu wählen. Zum Festlegen des Schlüssels führen Sie den folgenden Befehl aus:

```
swift post -m "Temp-URL-Key:<Schlüssel>"
```
{: pre}

3. Überprüfen Sie, ob `Temp-URL-Key` erfolgreich festgelegt wurde, indem Sie den folgenden Befehl ausführen.

```
swift stat
```
{: pre}

4. Erstellen Sie eine temporäre URL, indem Sie folgenden Befehl ausführen:

```
swift tempurl GET <Sekunden> <Pfad> <Schlüssel>
```
{: pre}

In der folgenden Tabelle sind die Positionsargumente aufgeführt, mit denen der Swift-Befehl `tempurl` arbeitet.
<table>
  <tr>
    <th> Argument </th>
    <th> Beschreibung </th>
  </tr>
  <tr>
    <td> [Methode] </td>
    <td> GET, um Downloads zuzulassen. PUT, um das Hochladen zuzulassen. </td>
  </tr>
  <tr>
    <td> [Sekunden] </td>
    <td> Zeit in Sekunden, in der die temporäre URL verfügbar sein soll. </td>
  </tr>
  <tr>
    <td> [Pfad] </td>
    <td> Der vollständige Pfad des Objekts im Format <code>/v1/<i>Authentifizierungskonto</i>/<i>Containername</i>/<i>Objektname</i>.</code> Weitere Informationen finden Sie in der Dokumentation zur <a href="https://console.bluemix.net/docs/services/ObjectStorage/os_api.html#access-points">{{site.data.keyword.objectstorageshort}}-URL</a>. </td>
  </tr>
  <tr>
    <td> [Schlüssel] </td>
    <td> Der in Schritt 2 festgelegte geheime Schlüssel.</td>
  </tr>
</table>

Tabelle 2: Temporäre URL-Positionsargumente

5. (Optional:) Hängen Sie die zurückgegebene URL an Ihren Clusternamen an, um eine vollständige URL zu erhalten. Anschließend können Sie die vollständige URL verwenden, um Objekte mit einem kompatiblen HTT_Client wie cURL, wget oder Firefox herunterzuladen.
