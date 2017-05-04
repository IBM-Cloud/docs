---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Message Hub-Paket verwenden
{: #openwhisk_catalog_message_hub}

Dieses Paket ermöglicht Ihnen die Kommunikation mit [Message Hub](https://developer.ibm.com/messaging/message-hub)-Instanzen, um Nachrichten mithilfe der nativen, hochleistungsfähigen Kafka-API zu veröffentlichen und zu verarbeiten.
{: shortdesc}

## Auslöser erstellen, der für eine IBM Message Hub-Instanz empfangsbereit ist
{: #openwhisk_catalog_message_hub_trigger}

Um einen Auslöser zu erstellen, der reagiert, wenn Nachrichten an eine Message Hub-Instanz gesendet werden, müssen Sie den Feed `/messaging/messageHubFeed` verwenden. Diese Feedaktion unterstützt die folgenden Parameter:

|Name|Typ|Beschreibung|
|---|---|---|
|kafka_brokers_sasl|JSON-Array aus Zeichenfolgen|Dieser Parameter ist ein Array aus Zeichenfolgen im Format `<Host>:<Port>`, die die Broker in Ihrer Message Hub-Instanz umfassen.|
|user|Zeichenfolge|Ihr Message Hub-Benutzername|
|password|Zeichenfolge|Ihr Message Hub-Kennwort|
|topic|Zeichenfolge|Das Thema, in dem der Auslöser empfangsbereit sein soll|
|kafka_admin_url|URL-Zeichenfolge|Die URL der Message Hub-REST-Schnittstelle für Administratoren|
|isJSONData|Boolesch (optional: Standard=false)|Wenn dieser Parameter auf `true` gesetzt wird, veranlasst dies den Provider, zu versuchen, den Nachrichtenwert als JSON-Daten zu parsen, bevor er ihn als Nutzdaten für den Auslöser weitergibt.|
|isBinaryKey|Boolesch (optional: Standard=false)|Wenn dieser Parameter auf `true` gesetzt wird, veranlasst dies den Provider, den Schlüsselwert in Base64 zu codieren, bevor er ihn als Nutzdaten für den Auslöser weitergibt.|
|isBinaryValue|Boolesch (optional: Standard=false)|Wenn dieser Parameter auf `true` gesetzt wird, veranlasst dies den Provider, den Nachrichtenwert in Base64 zu codieren, bevor er ihn als Nutzdaten für den Auslöser weitergibt.|

Diese Parameterliste kann zwar abschreckend wirken, jedoch können die Parameter automatisch mit dem CLI-Befehl zum Aktualisieren des Pakets für Sie festgelegt werden:

1. Erstellen Sie eine Instanz des Message Hub-Service unter Ihrer aktuellen Organisation und dem aktuellen Bereich, die bzw. den Sie für OpenWhisk verwenden.

2. Stellen Sie sicher, dass das zu überwachende Thema bereits in Message Hub vorhanden ist, oder erstellen Sie ein neues Thema. Beispiel: `mytopic`.

3. Aktualisieren Sie die Pakete in Ihrem Namensbereich. Die Aktualisierung erstellt automatisch eine Paketbindung für die Message Hub-Serviceinstanz, die Sie erstellt haben.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Message_Hub_Credentials-1
  ```

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1 private
  ```

  Ihre Paketbindung enthält nun die Ihrer Message Hub-Instanz zugeordneten Berechtigungsnachweise.

4. Nun müssen Sie nur noch einen Auslöser erstellen, der aktiviert werden soll, wenn neue Nachrichten an Ihr Message Hub-Thema gesendet werden.

  ```
  wsk trigger create MyMessageHubTrigger -f /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1/messageHubFeed -p topic mytopic
  ```
  {: pre}

## Message Hub-Paket außerhalb von Bluemix einrichten

Wenn Sie Message Hub außerhalb von Bluemix einrichten, müssen Sie manuell eine Paketbindung für Ihren Message Hub-Service erstellen. Dazu benötigen Sie die Berechtigungsnachweise für den Message Hub-Service und die Verbindungsinformationen.

1. Erstellen Sie eine Paketbindung, die für Ihren Message Hub-Service konfiguriert ist.

  ```
  wsk package bind /whisk.system/messaging myMessageHub -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p user <your Message Hub user> -p password <your Message Hub password> -p kafka_admin_url https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443
  ```
  {: pre}

2. Jetzt können Sie einen Auslöser mit Ihrem neuen Paket erstellen, der aktiviert wird, wenn neue Nachrichten an Ihr Message Hub-Thema gesendet werden.

  ```
  wsk trigger create MyMessageHubTrigger -f myMessageHub/messageHubFeed -p topic mytopic -p isJSONData true
  ```
  {: pre}


## Nachrichten überwachen
{: #openwhisk_catalog_message_hub_listen}

Nach dem Erstellen eines Auslösers überwacht das System das angegebene Thema in Ihrem Messaging-Service. Wenn neue Nachrichten gesendet werden, wird der Auslöser aktiviert.

Die Nutzdaten dieses Auslösers enthalten das Feld `messages`. Dabei handelt es sich um ein Array aus Nachrichten, die seit der letzten Aktivierung des Auslösers gesendet wurden. Jedes Nachrichtenobjekt im Array enthält die folgenden Felder:
- topic
- partition
- offset
- key
- value

In Bezug auf Kafka sollten diese Felder selbsterklärend sein. Das Feld `key` ist jedoch mit der optionalen Funktion `isBinaryKey` ausgestattet, die die Übertragung von binären Daten im Feld `key` ermöglicht. Außerdem erfordert das Feld `value` besondere Aufmerksamkeit. Die optionalen Felder `isJSONData` und `isBinaryValue` sind verfügbar, um JSON- und Binärnachrichten zu verarbeiten. Die Felder `isJSONData` und `isBinaryValue` können nicht miteinander kombiniert werden.

Beispiel: Falls für `isBinaryKey` der Wert `true` bei der Erstellung des Auslösers festgelegt wurde, wird das Feld `key` bei der Rückgabe aus den Nutzdaten eines ausgelösten Auslösers als Base64-Zeichenfolge codiert.

Beispiel: Falls ein Feld `key` mit dem Wert `Some key` gesendet wird und für `isBinaryKey` der Wert `true` festgelegt ist, sehen die Nutzdaten des Auslösers in etwa folgendermaßen aus:

```json
{
    "messages": [
    {
            "partition": 0,
            "key": "U29tZSBrZXk=",
            "offset": 421760,
            "topic": "mytopic",
            "value": "Some value"
        }
    ]
}
```

Wurde der Parameter `isJSONData` bei der Erstellung des Auslösers auf den Wert `false` (oder gar nicht) festgelegt, enthält das Feld `value` den Rohwert der gesendeten Nachricht. Wenn `isJSONData` bei der Erstellung des Auslösers jedoch auf `true` festgelegt wurde, versucht das System, diesen Wert nach Möglichkeit als JSON-Objekt zu parsen. Wenn das Parsing erfolgreich war, enthält das Feld `value` in den Nutzdaten des Auslösers das resultierende JSON-Objekt.

Beispiel: Wenn eine Nachricht mit dem Inhalt `{"title": "Some string", "amount": 5, "isAwesome": true}` gesendet wird und dabei `isJSONData` auf `true` gesetzt ist, sehen die Nutzdaten für den Auslöser in etwa wie folgt aus:

```json
{
  "messages": [
    {
      "partition": 0,
        "key": null,
        "offset": 421760,
        "topic": "mytopic",
        "value": {
          "amount": 5,
            "isAwesome": true,
            "title": "Some string"
        }
    }
  ]
}
```

Wird jedoch derselbe Nachrichteninhalt mit dem Wert `false` für `isJSONData` gesendet, sehen die Nutzdaten für den Auslöser wie folgt aus:

```json
{
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421761,
      "topic": "mytopic",
      "value": "{\"title\": \"Some string\", \"amount\": 5, \"isAwesome\": true}"
    }
  ]
}
```

Analog zu `isJSONData` gilt: Falls für das Feld `isBinaryValue` bei der Erstellung des Auslösers der Wert `true` festgelegt wurde, wird das resultierende Feld `value` in den Nutzdaten des Auslösers als Base64-Zeichenfolge codiert.

Beispiel: Falls ein Feld `value` mit dem Wert `Some data` gesendet wird und für `isBinaryValue` der Wert `true` festgelegt ist, sehen die Nutzdaten des Auslösers in etwa folgendermaßen aus:

```json
{
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421760,
      "topic": "mytopic",
      "value": "U29tZSBkYXRh"
    }
  ]
}
```

Wird dieselbe Nachricht gesendet, ohne dass für `isBinaryData` der Wert `true` festgelegt ist, ähneln die Nutzdaten des Auslösers dem folgenden Beispiel:

```json
{
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421760,
      "topic": "mytopic",
      "value": "Some data"
    }
  ]
}
```

### Nachrichten werden stapelweise verarbeitet
Die Nutzdaten für den Auslöser enthalten ein Array aus Nachrichten. Das bedeutet, dass der Feed versucht, für die gesendeten Nachrichten mit einer Stapeloperation eine einzige Anwendung des Auslösers herbeizuführen, wenn sehr schnell Nachrichten in Ihrem Messaging-System erstellt werden. Dadurch können die Nachrichten schneller und effizienter an Ihren Auslöser gesendet werden.

Berücksichtigen Sie beim Codieren von Aktionen, die von Ihrem Auslöser gestartet werden, dass die Anzahl der Nachrichten in den Nutzdaten technisch unbegrenzt ist, aber immer größer als 0 ist. Das folgende Beispiel zeigt eine gestapelte Nachricht (beachten Sie die Änderungen im Wert *offset*):
 
 ```json
 {
   "messages": [
    {
         "partition": 0,
         "key": null,
         "offset": 100,
         "topic": "mytopic",
         "value": {
             "amount": 5
         }
       },
       {
         "partition": 0,
         "key": null,
         "offset": 101,
         "topic": "mytopic",
         "value": {
             "amount": 1
         }
       },
       {
         "partition": 0,
         "key": null,
         "offset": 102,
         "topic": "mytopic",
         "value": {
             "amount": 999
         }
       }
   ]
 }
 ```

## Nachrichten für Message Hub erstellen
Falls Sie eine OpenWhisk-Aktion verwenden wollen, um eine Nachricht für Message Hub zu erstellen, können Sie die Aktion `/messaging/messageHubProduce` verwenden. Diese Aktion verwendet die folgenden Parameter:

|Name|Typ|Beschreibung|
|---|---|---|
|kafka_brokers_sasl|JSON-Array aus Zeichenfolgen|Dieser Parameter ist ein Array aus Zeichenfolgen im Format `<Host>:<Port>`, die die Broker in Ihrer Message Hub-Instanz umfassen.|
|user|Zeichenfolge|Ihr Message Hub-Benutzername|
|password|Zeichenfolge|Ihr Message Hub-Kennwort|
|topic|Zeichenfolge|Das Thema, in dem der Auslöser empfangsbereit sein soll|
|value|Zeichenfolge|Der Wert für die Nachricht, die Sie erstellen wollen|
|key|Zeichenfolge (optional)|Der Schlüssel für die Nachricht, die Sie erstellen wollen|

Die ersten drei Parameter können mittels `wsk package refresh` automatisch gebunden werden. Das folgende Beispiel zeigt hingegen, wie die Aktion mit allen erforderlichen Parametern aufgerufen wird:

```
wsk action invoke /messaging/messageHubProduce -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p topic mytopic -p user <your Message Hub user> -p password <your Message Hub password> -p value "This is the content of my message"
```
{: pre}

## Beispiele

### OpenWhisk mit IBM Message Hub, Node Red, IBM Watson IoT, IBM Object Storage und IBM Data Science Experience integrieren
Ein Beispiel, das OpenWhisk mit IBM Message Hub, Node Red, IBM Watson IoT, IBM Object Storage und dem Service von IBM Data Science Experience (Spark) integriert, finden Sie [hier](https://medium.com/openwhisk/transit-flexible-pipeline-for-iot-data-with-bluemix-and-openwhisk-4824cf20f1e0).

## Referenzinformationen
- [IBM Message Hub](https://developer.ibm.com/messaging/message-hub/)
- [Apache Kafka](https://kafka.apache.org/)
