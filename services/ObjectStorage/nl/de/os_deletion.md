---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Objektlöschung planen {: #schedule-object-deletion}
*Letzte Aktualisierung: 19. Oktober 2016*
{: .last-updated}

Sie können die Löschung Ihrer Objekte planen. Hierfür können Sie den Header `X-Delete-At` oder `X-Delete-After` verwenden.
{: shortdesc}

Der Wert für den Header `X-Delete-At` ist eine ganze Zahl, die die Referenzzeit darstellt, zu der das Objekt gelöscht werden soll. Der Wert für den Header `X-Delete_After` ist eine ganze Zahl, die die Anzahl an Sekunden darstellt, nach deren Ablauf das Objekt gelöscht wird. Zur Verwendung des Swift-Clients für die Planung der Objektlöschung führen Sie nach Bedarf den folgenden Befehl aus.

* Verwenden Sie den folgenden Befehl, um für die Löschung des Objekts ein bestimmtes Datum und eine bestimmte Uhrzeit festzulegen:
    
    ```
    swift post -H "X-Delete-At:<Referenzzeit>" <Containername> <Objektname>
    ```
    {: pre}
    
    Beispiel:
    
    Führen Sie folgenden Befehl aus, um die Löschung des Objekts auf "2016/04/01 08:00:00" festzulegen:
    
    ```
    swift post -H "X-Delete-At:1459515600" <Containername> <Objektname>
    ```
    {: screen}
* Verwenden Sie den folgenden Befehl, um für das Objekt festzulegen, dass es eine Stunde nach dem aktuellen Zeitpunkt gelöscht werden soll:
    
    ```
    swift post -H "X-Delete-After:<Anzahl_Sekunden" <Containername> <Objektname>
    ```
    {: pre}
    
    Beispiel:
    
    Führen Sie folgenden Befehl aus, um die Löschung des Objekts für eine Stunde nach dem aktuellen Zeitpunkt festzulegen:
    
    ```
    swift post -H "X-Delete-After:3600" container object
    ```
    {: screen}
* Verwenden Sie den folgenden Befehl, um die Ablaufzeit aus Ihrem Objekt zu entfernen:
    
    ```
    swift post -H "X-Remove-Delete-After:<Anzahl_Sekunden>" container object
    ```
    {: pre}

Zur Verwendung von cURL-Befehlen für die geplante Objektlöschung führen Sie nach Bedarf den folgenden Befehl aus. Die Standardwerte für die Uhrzeit sind dieselben wie beim Swift-Client.

* Verwenden Sie den folgenden Befehl, um für das Objekt den Löschzeitpunkt auf "2016/04/01 08:00:00" festzulegen:
   
   ```
   cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:<Referenzzeit>" https://<Objektspeicher-URL>/<Containername/<Objektname>
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

**Anmerkung:** Die tatsächliche Löschung eines Objekts erfolgt möglicherweise nicht genau zur angegebenen Uhrzeit. Das Objekt läuft jedoch de facto zur angegebenen Zeit ab. Das bedeutet, dass es nicht mehr erreichbar ist. Die eigentliche Löschung findet bei der nächsten Ausführung des in Ihrem Swift-Cluster konfigurierten Dämons 'swift-object-expirer' statt.
