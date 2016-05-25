---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Auslöser und Regeln erstellen
{: #openwhisk_triggers}
*Letzte Aktualisierung: 22. Februar 2016*

{{site.data.keyword.openwhisk}}-Auslöser und -Regeln statten die Plattform mit ereignisgesteuerten Funktionen aus. Ereignisse aus externen und internen Ereignisquellen werden durch einen Auslöser kanalisiert. Regeln ermöglichen es Ihren Aktionen, auf diese Ereignisse zu reagieren.
{: shortdesc}

## Auslöser

Ein Auslöser ist ein benannter Kanal für eine Klasse von Ereignissen. Es gibt zum Beispiel die folgenden Auslöser:
- Auslöser von Ereignissen zur Positionsaktualisierung.
- Auslöser von Dokumentuploads auf eine Website.
- Auslöser von eingehenden E-Mails.

Auslöser können mithilfe eines Wörterverzeichnisses mit Schlüssel/Wert-Paaren *aktiviert* (ausgelöst) werden. Manchmal wird dieses Wörterverzeichnis als das *Ereignis* bezeichnet. Wie bei Aktionen führt das Aktivieren eines Auslösers zu einer Aktivierungs-ID.

Auslöser können explizit durch einen Benutzer oder für einen Benutzer durch eine externe Ereignisquelle aktiviert werden.
Ein *Feed* ist eine bequeme Methode zum Konfigurieren einer externen Ereignisquelle zum Aktivieren von Auslöserereignissen, die von {{site.data.keyword.openwhisk_short}} verarbeitet werden können. Beispiele für Feeds sind die folgenden:
- Der Feed für Cloudant-Datenbankänderungen, der jedes Mal ein Auslöserereignis aktiviert, wenn ein Dokument in einer Datenbank hinzugefügt oder geändert wird.
- Ein Git-Feed, der ein Auslöserereignis für jede Festschreibung (Commit) in einem Git-Repository aktiviert.

## Regeln

Eine Regel ordnet genau einen Auslöser genau einer Aktion zu, wobei jede Aktivierung des Auslösers zur Folge hat, dass die entsprechende Aktion mit dem Auslöserereignis als Eingabe aufgerufen wird.

Mit dem entsprechenden Satz von Regeln kann ein einzelnes Auslöserereignis mehrere Aktionen aufrufen oder eine Aktion als Reaktion auf Ereignisse aus mehreren Auslösern aufgerufen werden.

Betrachten Sie zum Beispiel ein System mit den folgenden Aktionen:
- `classifyImage`: Eine Aktion, die die Objekte in einem Bild ermittelt und klassifiziert.
- `thumbnailImage`: Eine Aktion, die eine Piktogrammversion eines Bilds erstellt.

Nehmen Sie außerdem an, dass zwei Ereignisquellen vorhanden sind, die die folgenden Auslöser aktivieren:
- `newTweet`: Ein Auslöser, der aktiviert wird, wenn ein neuer Tweet gepostet wird.
- `imageUpload`: Ein Auslöser, der aktiviert wird, wenn ein Bild auf eine Website hochgeladen wird.

Sie können Regeln so einrichten, dass ein einzelnes Auslöserereignis mehrere Aktionen aufruft und dass mehrere Auslöser dieselbe Aktion aufrufen:
- Regel `newTweet -> classifyImage`.
- Regel `imageUpload -> classifyImage`.
- Regel `imageUpload -> thumbnailImage`.

Diese drei Regeln definieren das folgende Verhalten: Bilder in Tweets und hochgeladene Bilder werden klassifiziert. Hochgeladene Bilder werden klassifiziert und es wird eine Piktogrammversion von ihnen generiert. 

## Auslöser erstellen und aktivieren
{: #openwhisk_triggers}

Auslöser können aktiviert werden, wenn bestimmte Ereignisse stattfinden, oder sie können manuell aktiviert werden.

Erstellen Sie zum Beispiel einen Auslöser, um Aktualisierungen an Benutzerstandorten zu senden, und aktivieren Sie den Auslöser manuell.

1. Geben Sie den folgenden Befehl ein, um den Auslöser zu erstellen:
 
  ```
  wsk trigger create locationUpdate
  ```
  {: pre}
 
  ```
  ok: created trigger locationUpdate
  ```
  {: screen}

2. Prüfen Sie, ob der Auslöser erstellt wurde, indem Sie die Gruppe von Auslösern auflisten.

  ```
  wsk trigger list
  ```
  {: pre}
 
  ```
  triggers
  /someNamespace/locationUpdate                            private
  ```
  {: screen}

  Bis hierhin haben Sie einen benannten "Kanal" erstellt, an den Ereignisse ausgelöst werden können.

3. Als Nächstes aktivieren Sie ein Auslöserereignis, indem Sie den Auslösernamen und die Parameter des Auslösers angeben:

  ```
  wsk trigger fire locationUpdate --param name "Donald" --param place "Washington, D.C."
  ```
  {: pre}

  ```
  ok: triggered locationUpdate with id fa495d1223a2408b999c3e0ca73b2677
  ```
  {: screen}

   Alle Ereignisse, die für den Auslöser "locationUpdate" aktiviert werden, haben zurzeit noch keine Wirkung. Um nützlich zu sein, benötigt der Auslöser eine Regel, die ihn einer Aktion zuordnet.


## Auslöser und Aktionen durch Regeln zuordnen
{: #openwhisk_rules}

Regeln werden dazu verwendet, einen Auslöser einer Aktion zuzuordnen. Jedes Mal, wenn ein Auslöserereignis aktiviert wird, wird die Aktion mit den Ereignisparametern aufgerufen.

Erstellen Sie zum Beispiel eine Regel, die die Aktion "hello" aufruft, wenn eine Standortaktualisierung gesendet wird. 

1. Erstellen Sie eine Datei 'hello.js' mit dem folgenden Aktionscode:
  ```
  function main(params) {
     return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

2. Stellen Sie sicher, dass der Auslöser und die Aktion vorhanden sind.
  ```
  wsk trigger update locationUpdate
  ```
  {: pre}
  
  ```
  wsk action update hello hello.js
  ```
  {: pre}

3. Erstellen und aktivieren Sie die Regel. Die drei Parameter sind der Name der Regel, der Auslöser und die Aktion.
  ```
  wsk rule create --enable myRule locationUpdate hello
  ```
  {: pre}

4. Aktivieren Sie den Auslöser 'locationUpdate'. Jedes Mal, wenn Sie ein Ereignis auslösen, wird die Aktion 'hello' mit den Ereignisparametern aufgerufen.
  ```
  wsk trigger fire locationUpdate --param name "Donald" --param place "Washington, D.C."
  ```
  {: pre}
  
  ```
  ok: triggered locationUpdate with id d5583d8e2d754b518a9fe6914e6ffb1e
  ```
  {: screen}

5. Stellen Sie fest, ob die Aktion aufgerufen wurde, indem Sie die letzte Aktivierung prüfen.
  ```
  wsk activation list --limit 1 hello
  ```
  {: pre}
  
  ```
  activations
  9c98a083b924426d8b26b5f41c5ebc0d             hello
  ```
  {: screen}
  
  ```
  wsk activation result 9c98a083b924426d8b26b5f41c5ebc0d
  ```
  {: pre}
  ```
  {
     "payload": "Hello, Donald from Washington, D.C."
  }
  ```
  {: screen}

  Wie Sie sehen, hat die Aktion 'hello' die Ereignisnutzdaten (payload) empfangen und die erwartete Zeichenfolge zurückgegeben.

  Sie können mehrere Regeln erstellen, die denselben Auslöser verschiedenen Aktionen zuordnen.
