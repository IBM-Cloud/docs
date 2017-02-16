---

 

copyright:

  years: 2016
lastupdated: "2016-09-09"
 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Feeds implementieren
{: #openwhisk_feeds}

OpenWhisk unterstützt eine offene API, mit der jeder Benutzer einen Ereignisproduzent-Service als **Feed** in einem **Paket** verfügbar machen kann.   In diesem Abschnitt werden die Architektur- und Implementierungsoptionen beschrieben, mit denen Sie Ihren eigenen Feed bereitstellen können.

Die folgenden Informationen sind für erfahrene OpenWhisk-Benutzer gedacht, die ihre eigenen Feeds veröffentlichen möchten.  Weniger erfahrene OpenWhisk-Benutzer können diesen Abschnitt überspringen.

## Feedarchitektur

Es gibt mindestens 3 Architekturmuster zum Erstellen eines Feeds: **Hooks**, **Polling** und **Verbindungen**.

### Hooks
Im *Hooks*-Muster wird der Feed mit einer [Web-Hook](https://en.wikipedia.org/wiki/Webhook)-Funktion eingerichtet, die von einem anderen Service verfügbar gemacht wird.   Dazu wird ein Web-Hook in einem externen Service konfiguriert, um direkt per POST-Anforderung zu einer URL zu senden, um einen Auslöser zu aktivieren.  Dies ist die einfachste und bequemste Option, um Feeds mit geringer Frequenz zu implementieren.

### Polling
Im Polling-Muster wird eine OpenWhisk-*Aktion* angeordnet, um einen Endpunkt regelmäßig abzufragen, um neue Daten abzurufen.
Dieses Muster ist einfach zu erstellen, aber die Häufigkeit der Ereignisse wird vom Abfrageintervall bestimmt.

### Verbindungen
Im Verbindungsmuster wird ein Service automatisch installiert, der eine persistente Verbindung zu einer Feedquelle verwaltet.    Die verbindungsbasierte Implementierung kann mit einem Serviceendpunkt über ein langes Polling interagieren. Es kann auch eine Push-Benachrichtigung eingerichtet werden.


## Unterschied zwischen Feed und Auslöser

Feeds und Auslöser sind sich sehr ähnlich, aber technisch gesehen unterschiedliche Konzepte.   

- OpenWhisk verarbeitet **Ereignisse** im Systemablauf.

- Ein **Auslöser** ist ein Name für eine Klasse von Ereignissen.   Jedes Ereignis gehört zu genau einem Auslöser. Ein Auslöser ähnelt daher einem *Thema* in themenbasierten Publish/Subscribe-Systemen.    Die **Regel** *T -> A* bedeutet Folgendes: Sobald ein Ereignis vom Auslöser *T* eintrifft, wird die Aktion *A* mit den Auslöser-Nutzdaten aufgerufen.

- Ein **Feed** ist ein Strom von Ereignissen, die alle zum selben Auslöser *T* gehören. Ein Auslöser wird durch die **Feedaktion** gesteuert, die das Erstellen, Löschen, Anhalten und Fortsetzen des Ereignisstroms abwickelt, der einen Feed bildet.    Die Feedaktion interagiert in der Regel mit externen Services, die die Ereignisse über eine REST-API (die Benachrichtigungen verwaltet) erstellen.

##  Feedaktionen implementieren

Die *Feedaktion* ist eine normale OpenWhisk-*Aktion*, die die folgenden Parameter akzeptieren sollte:
* **lifecycleEvent**: entweder 'Erstellen', 'Löschen', 'Anhalten' oder 'Anhalten aufheben'
* **triggerName**: der vollständig qualifizierte Name des Auslösers, der die Ereignisse enthält, die von diesem Feed generiert werden.
* **authKey**: die grundlegenden Berechtigungsnachweise des OpenWhisk-Benutzers, der den genannten Auslöser besitzt.

Die Feedaktion akzeptiert alle anderen Parameter, die zum Verwalten des Feeds erforderlich sind.  Die Feedaktion für Cloudant-Änderungen erwartet beispielsweise, dass Parameter mit *'dbname'*, *'username'* usw. empfangen werden.

Wenn der Benutzer einen Auslöser aus der CLI mit dem Parameter **--feed** erstellt, wird die Feedaktion mit den entsprechenden Parametern automatisch aufgerufen.

Beispiel: Der Benutzer hat die Bindung `mycloudant` für das Paket `cloudant` mit dem Benutzernamen und dem Kennwort als gebundene Parameter erstellt.  Wenn der Benutzer den folgenden Befehl aus der CLI ausgibt,

`wsk trigger create T --feed mycloudant/changes -p dbName myTable`

wird im System Folgendes ausgeführt:

`wsk action invoke mycloudant/changes -p lifecycleEvent CREATE -p triggerName T -p authKey <userAuthKey> -p password <password value from mycloudant binding> -p username <username value from mycloudant binding> -p dbName mytype`

Die Feedaktion *changes* akzeptiert diese Parameter. Es wird erwartet, dass eine notwendige Aktion ergriffen wird, um einen Ereignisstrom von Cloudant mit der entsprechenden Konfiguration eingerichtet und an den Auslöser *T* weitergeleitet wird.    

Für den Cloudant-Feed *changes* kommuniziert die Aktion direkt mit dem Service *Cloudant-Auslöser*, der mit einer verbindungsbasierten Architektur implementiert wurde.   Die anderen Architekturen werden weiter unten beschrieben.

Ein ähnliches Feedaktionsprotokoll tritt für `wsk trigger delete` auf.    

## Feeds mit Hooks implementieren

Das Einrichten eines Feeds über einen Hook ist einfach, wenn der Ereignisproduzent die Webhook/Callback-Funktion unterstützt.

Mit dieser Methode ist es *nicht erforderlich* einen persistenten Service außerhalb von OpenWhisk automatisch zu installieren.  Die Feedverwaltung erfolgt über statusunabhängige OpenWhisk-*Feed-Aktionen*, die direkt mit einer Drittanbieter-Webhook-API kommunizieren.

Bei einem Aufruf mit `CREATE` installiert die Feedaktion einen Webhok für einen anderen Service. Dabei sendet der ferne Service Benachrichtigungen an die entsprechende `fireTrigger`-URL in OpenWhisk.

Der Webhook sollte angewiesen werden, Benachrichtigungen zu einer URL wie die folgende zu senden:

`POST /namespaces/{namespace}/triggers/{triggerName}`

Das Formular mit der POST-Anforderung wird als JSON-Dokument interpretiert, das Parameter zum Auslöserereignis definiert.
OpenWhisk-Regeln übergeben diese Auslöserparameter an Aktionen, die als Ergebnis des Ereignisses ausgelöst werden.

## Feeds mit Polling implementieren

Eine OpenWhisk-*Aktion* kann so eingerichtet werden, dass eine Feedquelle innerhalb von OpenWhisk vollständig abgefragt wird, ohne dass persistente Verbindungen oder ein externer Service automatisch installiert werden müssen.

Bei Feeds, bei denen kein Webhook verfügbar ist, die aber keine Antworten mit einem hohen Volumen oder einer geringen Latenz benötigen, ist Polling eine attraktive Option.

Um einen Polling-basierten Feed einzurichten, führt die Feedaktion die folgenden Schritte aus, wenn `Erstellen` aufgerufen wird:

1.   Die Feedaktion richtet einen regelmäßigen Auslöser (*T*) mit der gewünschten Frequenz ein, indem der Feed `whisk.system/alarms` verwendet wird.
2.   Der Feed-Entwickler erstellt die Aktion `pollMyService`, die den fernen Service abruft und neue Ereignisse zurückgibt.
3.  Die Feedaktion richtet die *Regel* *T -> pollMyService* ein.

Mit dieser Vorgehensweise wird ein Polling-basierter Auslöser implementiert, der nur OpenWhisk-Aktionen verwendet, ohne dass dazu ein separater Service benötigt wird.

## Feeds mit Verbindungen implementieren

Die vorherigen zwei Architekturoptionen sind einfach zu implementieren. Wenn Sie jedoch einen sehr leistungsfähigen Feed benötigen, sind persistente Verbindungen und Long-Polling- bzw. ähnliche Verfahren notwendig.

Da OpenWhisk-Aktionen eine kurze Laufzeit haben müssen, kann eine Aktion keine persistente Verbindung zu einer dritten Partei verwalten. Stattdessen muss ein separater Service (außerhalb von OpenWhisk) automatisch installiert werden, der durchgehend ausgeführt wird.   Dies sind *Provider-Services*.  Ein Provider-Service kann Verbindungen zu Drittanbieter-Ereignisquellen verwalten, die Long-Polling- oder andere verbindungsbasierte Benachrichtigungen unterstützen.   
Der Provider-Service muss eine REST-API bereitstellen, die der OpenWhisk-*Feedaktion* es ermöglicht, den Feed zu steuern.   Der Provider-Service fungiert als Proxy zwischen dem Ereignisprovider und OpenWhisk. Wenn er vom Drittanbieter Ereignisse empfängt, werden sie an OpenWhisk gesendet, indem ein Auslöser aktiviert wird.

Der Cloudant-Feed *changes* ist ein kanonisches Beispiel. Der Service `cloudanttrigger` wird automatisch installiert und kommuniziert zwischen Cloudant-Benachrichtigungen über eine persistente Verbindung und OpenWhisk-Auslösern.

Der Feed *alarm* wird mithilfe eines ähnlichen Musters implementiert.

Die verbindungsbasierte Architektur ist die beste Leistungsoption. Allerdings fällt ein hoher Aufwand an Operationen im Vergleich zu Polling- und Hook-Architekturen an.   
