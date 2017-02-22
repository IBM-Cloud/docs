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


# Objekte löschen

Wenn Sie Objekte nicht mehr benötigen, können Sie diese und auch Container aus der Speicherinstanz löschen. Sie können den Löschvorgang entweder manuell vornehmen oder [einen Zeitpunkt festlegen](/docs/services/ObjectStorage/os_deletion.html#schedule-object-deletion), zu dem die Objekte ablaufen sollen.
{: shortdesc}

**Achtung**: Mit dem Löschen Ihres Containers löschen Sie alle Objekte, die im Container enthalten sind.


## Objekte und Container über die Benutzerschnittstelle löschen {: #deleting-ui}

1. Wählen Sie im Dashboard der Serviceinstanz den Container mit der Datei aus, die Sie nicht mehr benötigen.
2. Wählen Sie im Dropdown-Menü **Aktionen** die Option **Datei löschen** aus.
3. Wenn Sie einen Container nicht mehr benötigen, wählen Sie **Container löschen** aus dem Dropdown-Menü **Aktionen** aus.



## Mithilfe der CLI Objekte und Container löschen {: #deleting-cli}

1.  Wenn Sie nicht bei {{site.data.keyword.Bluemix_notm}} angemeldet sind, melden Sie sich bei der Organisation und dem Bereich mit Ihrer Instanz von {{site.data.keyword.objectstorageshort}} an.
  ```
  cf login -a api.ng.bluemix.net -u <Benutzer-ID> -p <Kennwort> -o <Organisation> -s <Bereich>
  ```
  {: pre}

2. Optional: Vergewissern Sie sich vor dem Löschen Ihrer Dateien und Container, dass eine Sicherung Ihrer Objekte vorhanden ist. 

3. Führen Sie folgenden Befehl aus, um eine Datei zu löschen:
  ```
  swift delete <Containername> <Dateiname>
  ```
  {: pre}

4. Zum Löschen des Containers führen Sie folgenden Befehl aus:
  ```
  swift delete <Containername>
  ```
  {: pre}



## Objektlöschung planen {: #schedule-object-deletion}


Sie können das Löschen Ihrer Objekte planen, indem Sie den Header `X-Delete-At` oder `X-Delete-After` verwenden.
{: shortdesc}

Der Wert für den Header `X-Delete-At` ist eine ganze Zahl, die die Referenzzeit darstellt, zu der das Objekt gelöscht werden soll. Der Wert für den Header `X-Delete_After` ist eine ganze Zahl, die die Anzahl an Sekunden darstellt, nach deren Ablauf das Objekt gelöscht wird. 

**Hinweis:** Die tatsächliche Löschung eines Objekts erfolgt möglicherweise nicht genau zur angegebenen Uhrzeit. Das Objekt läuft jedoch tatsächlich zur angegebenen Zeit ab. Von diesem Zeitpunkt an ist das Objekt nicht mehr erreichbar. Die eigentliche Löschung findet bei der nächsten Ausführung des in Ihrem Swift-Cluster konfigurierten Dämons 'swift-object-expirer' statt.

#### Gehen Sie zur Verwendung von Swift-Befehlen folgendermaßen vor:

* Verwenden Sie den folgenden Befehl, um für die Löschung des Objekts ein bestimmtes Datum und eine bestimmte Uhrzeit festzulegen:

    ```
    swift post -H "X-Delete-At:<Referenzzeit>" <Containername> <Objektname>
    ```
    {: pre}

    Beispiel:
    Führen Sie folgenden Befehl aus, um die Löschung des Objekts auf "2016/04/01 08:00:00" festzulegen:

    ```
    swift post -H "X-Delete-At:1459515600" container1 file7
    ```
    {: screen}

* Verwenden Sie den folgenden Befehl, um für die Löschung des Objekts nach einer bestimmten festzulegen:

    ```
    swift post -H "X-Delete-After:<Anzahl_Sekunden>" <Containername> <Objektname>
    ```
    {: pre}

    Beispiel:
    Führen Sie folgenden Befehl aus, um die Löschung des Objekts für eine Stunde nach dem aktuellen Zeitpunkt festzulegen:

    ```
    swift post -H "X-Delete-After:3600" container1 file7
    ```
    {: screen}

* Verwenden Sie den folgenden Befehl, um die Ablaufzeit aus Ihrem Objekt zu entfernen:

    ```
    swift post -H "X-Remove-Delete-After:<Anzahl_Sekunden>" <Containername> <Objektname>
    ```
    {: pre}



#### Gehen Sie zur Verwendung von cURL-Befehlen folgendermaßen vor:

* Verwenden Sie den folgenden Befehl, um für das Objekt den Löschzeitpunkt auf "2016/04/01 08:00:00" festzulegen:

    ```
    cURL -X POST -H "X-Auth-Token: <Token>" -H "X-Delete-At:<Referenzzeit>" https://<Objektspeicher_URL>/<Containername>/<Objektname>
    ```
    {: pre}

* Verwenden Sie den folgenden Befehl, um für das Objekt festzulegen, dass es eine Stunde nach dem aktuellen Zeitpunkt gelöscht werden soll:

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:<Anzahl_Sekunden>" https://<Objektspeicher_URL>/<Containername>/<Objektname>
    ```
    {: pre}

* Verwenden Sie den folgenden Befehl, um zu prüfen, ob das Objekt den Header aufweist:

    ```
    cURL -I -H "X-Auth-Token: <token>" https://<Objektspeicher-URL>/<Containername>/<Objektname>
    ```
    {: pre}

* Verwenden Sie den folgenden Befehl, um die Ablaufzeit zu entfernen:

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:<Referenzzeit>" https://<Objektspeicher-URL>/<Containername>/<Objektname>
    ```
    {: pre}
