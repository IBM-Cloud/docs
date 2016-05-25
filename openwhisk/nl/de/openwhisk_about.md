---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Informationen zu {{site.data.keyword.openwhisk}}

*Letzte Aktualisierung: 22. Februar 2016*

Die folgenden Abschnitte enthalten detaillierte Informationen zu {{site.data.keyword.openwhisk}}.
{: shortdesc}

## Funktionsweise von {{site.data.keyword.openwhisk_short}}
{: #openwhisk_how}

{{site.data.keyword.openwhisk_short}} ist eine ereignisgesteuerte Berechnungsplattform, die Code in Reaktion auf Ereignisse oder direkte Aufrufe ausführt.

In der folgenden Abbildung ist die allgemeine {{site.data.keyword.openwhisk_short}}-Architektur dargestellt.

![{{site.data.keyword.openwhisk_short}}-Architektur](OpenWhisk.png)

Beispiele für Ereignisse sind Änderungen an Datenbanksätzen, IoT-Sensormesswerte (IoT, Internet of Things - Internet der Dinge), die einen bestimmten Temperaturwert überschreiten, neues Codefestschreibungen (Commits) in einem GitHub-Repository oder einfache HTTP-Anforderungen von Web-Apps oder mobilen Apps. Ereignisse aus externen und internen Ereignisquellen werden durch einen Auslöser kanalisiert. Regeln ermöglichen es Aktionen, auf diese Ereignisse zu reagieren.

Aktionen können kleine Snippets aus Javascript- oder Swift-Code oder angepasste Binärdateien sein, die in einem Docker-Container eingebettet sind. Aktionen in {{site.data.keyword.openwhisk_short}} werden in kürzester Zeit bereitgestellt und ausgeführt, wenn ein Auslöser aktiviert wird. Je mehr Auslöser aktiviert werden, desto mehr Aktionen werden aufgerufen. Wenn kein Auslöser aktiviert wird, wird kein Aktionscode ausgeführt und es entstehen keine Kosten.

Neben der Verknüpfung von Aktionen mit Auslösern ist es möglich, eine Aktion direkt über die API, die CLI oder das iOS-SDK von {{site.data.keyword.openwhisk_short}} aufzurufen. Eine Gruppe von Aktionen kann außerdem verkettet werden, ohne dass dazu Code geschrieben werden muss. Jede Aktion in der Kette wird in der Reihenfolge aufgerufen, wobei die Ausgabe einer Aktion als Eingabe an die nächste Aktion in der Folge übergeben wird.

Bei traditionellen virtuellen Maschinen mit langer Laufzeit oder Containern ist es ein allgemein übliches Verfahren, mehrere virtuelle Maschinen (VMs) bzw. Container bereitzustellen, um flexibel auf Ausfälle einer einzelnen Instanz reagieren zu können. {{site.data.keyword.openwhisk_short}} bietet jedoch ein alternatives Modell ohne Kostenaufwand für den Ausfallschutz an. Die bedarfsgesteuerte Ausführung von Aktionen ermöglicht eine inhärente Skalierbarkeit und eine optimale Auslastung, da die Anzahl der aktiven Aktionen immer der Auslöserrate entspricht. Darüber hinaus kann sich der Entwickler jetzt allein auf seinen Code konzentrieren und braucht sich nicht um die Überwachung, die Programmkorrekturen oder den Schutz für den zugrunde liegenden Server, den Speicher, das Netz und die Betriebssysteminfrastruktur zu kümmern.

Integrationen in zusätzliche Services und Ereignisprovider können durch Pakete hinzugefügt werden. Ein Paket ist ein Bündel aus Feeds und Aktionen. Ein Feed ist ein Codeabschnitt, der eine externe Ereignisquelle zum Auslösen von Auslöserereignissen konfiguriert. Zum Beispiel konfiguriert ein Auslöser, der mit einem Feed für Cloudant-Änderungen erstellt wurde, einen Service, der den Auslöser jedes Mal dann aktiviert, wenn ein Dokument in einer Cloudant-Datenbank geändert oder hinzugefügt wird. Aktionen in Paketen stellen wiederverwendbare Logik da, die ein Service-Provider verfügbar machen kann, sodass Entwickler den Service nicht nur als Ereignisquelle verwenden können, sondern auch APIs dieses Service aufrufen können.

Ein bestehender Katalog mit Paketen bietet eine schnelle Möglichkeit, Anwendungen mit nützlichen Funktionen zu erweitern und auf externe Services im direkten Geschäftsumfeld zuzugreifen. Zu den externen Services, die für {{site.data.keyword.openwhisk_short}} eingerichtet sind, gehören zum Beispiel Cloudant, The Weather Company, Slack und GitHub.


## Häufige Anwendungsfälle
{: #openwhisk_use_cases}

Das von {{site.data.keyword.openwhisk_short}} angebotene Ausführungsmodell unterstützt eine Reihe von Anwendungsfällen. In den folgenden Abschnitten werden typische Beispiele beschrieben.

### Dekomposition von Anwendungen in Microservices
Durch seinen modularen und inhärent skalierbaren Aufbau ist {{site.data.keyword.openwhisk_short}} für die Implementierung differenzierter Teile von Logik in Aktionen geeignet. {{site.data.keyword.openwhisk_short}} kann zum Beispiel nützlich sein, wenn auslastungsintensive und potenziell zu Spitzenlasten führende Tasks (Hintergrundtasks) aus dem Front-End-Code herausgenommen und die entsprechenden Tasks als Aktionen implementiert werden sollen.

### Mobile-Back-End
Viele mobile Anwendungen erfordern serverseitige Logik. Aufgrund der Tatsache, das Entwickler mobiler Apps in der Regel wenig Erfahrung mit der Verwaltung serverseitiger Logik haben und sich lieber auf die App, die auf dem Gerät ausgeführt wird, konzentrieren, ist die Verwendung von {{site.data.keyword.openwhisk_short}} als serverseitiges Back-End eine gute Lösung. Darüber hinaus bietet die integrierte Unterstützung für Swift Entwicklern die Möglichkeit, von vorhandenen iOS-Programmierkenntnissen erneut zu profitieren.

### Datenverarbeitung
Angesichts der gegenwärtig verfügbaren Datenmengen erfordert die Anwendungsentwicklung die Fähigkeit, neue Daten zu verarbeiten und potenziell darauf zu reagieren. Diese Anforderung schließt die Verarbeitung sowohl strukturierter Datenbanksätze als auch nicht strukturierter Dokumente, Bilder und Videos mit ein.

### Internet der Dinge (IoT)
Internet der Dinge-Szenarios (Internet of Things, IoT) sind ihrer Spezifik nach häufig sensorgesteuert. Zum Beispiel könnte eine Aktion in {{site.data.keyword.openwhisk_short}} ausgelöst werden, wenn es erforderlich ist, auf einen Sensor zu reagieren, der eine bestimmte Temperatur überschreitet.



