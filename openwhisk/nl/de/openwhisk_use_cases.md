---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Häufige {{site.data.keyword.openwhisk_short}}-Anwendungsfälle
{: #openwhisk_common_use_cases}

Das von {{site.data.keyword.openwhisk_short}} angebotene Ausführungsmodell unterstützt eine Reihe von Anwendungsfällen. In den folgenden Abschnitten werden typische Beispiele beschrieben. Eine ausführlichere Beschreibung der serverunabhängigen Architektur (Serverless Architecture), Beispielanwendungsfälle, eine Erörterung der Vor- und Nachteile sowie bewährte Verfahren zur Implementierung finden Sie in dem hervorragenden [Artikel von Mike Roberts im Blog von Martin Fowler (englisch)](https://martinfowler.com/articles/serverless.html).
{: shortdesc}

## Microservices
{: #openwhisk_common_use_cases_microservices}

Trotz ihrer Vorteile bleiben auf Microservices basierende Lösungen in ihrer Erstellung mit gängigen Cloudtechnologien schwierig, da sie häufig die Steuerung einer komplexen Toolchain sowie separate Pipelines für Buildoperationen und Betrieb erfordern. Insbesondere kleine und agile Teams, die sehr viel Zeit für Fragen der komplexen Infrastruktur und des Betriebs (Fehlertoleranz, Lastverteilung, automatische Skalierung und Protokollierung) aufwenden, wünschen sich oft eine Möglichkeit, optimierten und nützlichen Code mit ihren bekannten und bevorzugten Programmiersprachen und mit Programmiersprachen, die am besten zur Lösung bestimmter Probleme geeignet sind, entwickeln zu können.  

Durch seinen modularen und inhärent skalierbaren Aufbau eignet sich {{site.data.keyword.openwhisk_short}} ideal für die Implementierung differenzierter Teile von Logik in Aktionen. {{site.data.keyword.openwhisk_short}}-Aktionen sind voneinander unabhängig und können in einer ganzen Reihe verschiedener Sprachen, die von  {{site.data.keyword.openwhisk_short}} unterstützt werden, implementiert werden und auf verschiedene Back-End-Systeme zugreifen. Jede Aktion kann unabhängig bereitgestellt und verwaltet werden und lässt sich unabhängig von anderen Aktionen skalieren. Die Interkonnektivität zwischen Aktionen wird durch {{site.data.keyword.openwhisk_short}} in Form von Regeln, Sequenzen und Namenskonventionen realisiert. Dies ist für Anwendungen, die auf Microservices basieren, durchaus geeignet.

## Web-Apps
{: #openwhisk_common_use_cases_webapps}

Obwohl {{site.data.keyword.openwhisk_short}} ursprünglich auf eine ereignisgesteuerte Programmierung ausgerichtet war, bietet es verschiedene Vorteile für Anwendungen mit Benutzerinteraktion. Wenn Sie es zum Beispiel mit einem kleinen Node.js-Stub kombinieren, können Sie damit Anwendungen bedienen, die sich relativ einfach debuggen lassen. Da {{site.data.keyword.openwhisk_short}}-Anwendungen zudem mit einem wesentlich geringeren Rechenaufwand verbunden sind als die Ausführung eines Serverprozesses auf einer PaaS-Plattform, sind sie außerdem beträchtlich kostengünstiger.  

Mit OpenWhisk kann eine vollständige Webanwendung erstellt und ausgeführt werden. Die Kombination von serverunabhängigen APIs mit der Bereitstellung statischer Dateien für Siteressourcen, z. B. HTML-, JavaScript- und CSS-Dateien, ermöglicht die Erstellung vollständiger serverunabhängiger Webanwendungen. Der einfache Betrieb einer gehosteten {{site.data.keyword.openwhisk_short}}-Umgebung (oder eher der völlig aufwandslose Betrieb, da das Hosting in Bluemix erfolgt) ist ein großer Vorteil gegenüber dem Betrieb einer traditionellen Serverlaufzeit wie Node.js Express in eigener Regie.

Eine nützliche Einrichtung ist die Option des Tools *wsk* der {{site.data.keyword.openwhisk_short}}-Befehlszeilenschnittstelle (CLI) mit der Bezeichnung "--annotation web-export true", die den Code für einen Web-Browser zugänglich macht.

Die folgenden Beispiele zeigen, wie {{site.data.keyword.openwhisk_short}} zum Erstellen einer Web-App verwendet werden kann:
- [Webaktionen: Serverunabhängige Web-Apps mit OpenWhisk](https://medium.com/openwhisk/web-actions-serverless-web-apps-with-openwhisk-f21db459f9ba).
- [{{site.data.keyword.openwhisk_short}}-Anwendung mit Benutzerinteraktion mit Bluemix und Node.js erstellen](https://www.ibm.com/developerworks/cloud/library/cl-openwhisk-node-bluemix-user-facing-app/index.html)
- [Serverunabhängige HTTP-Handler mit OpenWhisk](https://medium.com/openwhisk/serverless-http-handlers-with-openwhisk-90a986cc7cdd)

## IoT
{: #openwhisk_common_use_cases_iot}

Es ist sicherlich möglich, IoT-Anwendungen (IoT, Internet of Things - Internet der Dinge) mit traditionellen Serverarchitekturen zu implementieren. In vielen Fällen erfordert die Kombination verschiedener Services und Datenbridges eine sehr hohe Leistung und flexible Pipelines - Anforderungen, denen von IoT-Einheiten bis zur Cloudspeicherung und einer Analyseplattform alle Komponenten gerecht werden müssen. Bridges, die häufig vorkonfiguriert sind, bieten nicht die Programmierbarkeit, die zur Implementierung und Feinabstimmung der Architektur einer bestimmten Lösung erforderlich ist. Angesichts der immensen Auswahl an möglichen Pipelines und der fehlenden Standardisierung im Bereich der Datenfusion im Allgemeinen und im IoT-Bereich im Besonderen, erfordert die Pipeline in vielen Fällen eine angepasste Datenkonvertierung (zur Formatumsetzung, Filterung, Erweiterung usw.). {{site.data.keyword.openwhisk_short}} ist ein hervorragendes Tool zur Implementierung einer solchen Transformation in einer 'serverunabhängigen' Weise, bei der die angepasste Logik in einer vollständig verwalteten und elastischen Cloudplattform bereitgestellt wird.

IoT-Szenarios sind ihrer Spezifik nach häufig sensorgesteuert. Zum Beispiel könnte eine Aktion in {{site.data.keyword.openwhisk_short}} ausgelöst werden, wenn es erforderlich ist, auf einen Sensor zu reagieren, der eine bestimmte Temperatur überschreitet. IoT-Interaktionen sind in der Regel statusunabhängig mit einem Potenzial für sehr hohe Belastungen im Fall größerer Ereignisse (Naturkatastrophen, schwerwiegende Wetterereignisse, Verkehrsstaus, usw.). Dies macht ein elastisches System erforderlich, dessen normale Auslastung möglicherweise gering ist, das sich jedoch sehr schnell mit vorhersagbarer Antwortzeit skalieren lässt und extrem hohe Anzahlen von Ereignissen ohne Vorwarnung des Systems verarbeiten kann. Es ist recht schwierig, ein System, das diese Anforderungen erfüllt, mithilfe traditioneller Serverarchitekturen aufzubauen, da diese entweder nicht über die entsprechende Leistung verfügen, um Lastspitzen des Datenverkehrs auffangen zu können, oder mit solchen Überkapazitäten ausgestattet sind, dass sie extrem hohe Kosten verursachen.

Hier finden Sie ein Beispiel für eine IoT-Anwendung, die OpenWhisk, NodeRed, Cognitive und andere Services verwendet: [Serverunabhängige Transformation von bewegten IoT-Daten mit OpenWhisk](https://medium.com/openwhisk/serverless-transformation-of-iot-data-in-motion-with-openwhisk-272e36117d6c#.akt3ocjdt).

![Beispiel für die Architektur einer IoT-Lösung](images/IoT_solution_architecture_example.png)

## API-Back-End
{: #openwhisk_common_use_cases_iot}

Serverunabhängige IT-Plattformen bieten Entwicklern eine schnelle Möglichkeit zum Erstellen von APIs ohne Server. {{site.data.keyword.openwhisk_short}} unterstützt eine automatische Generierung von REST-APIs für Aktionen und es ist sehr einfach, Ihr API-Management-Tool der Wahl (z. B. [IBM API Connect](https://www-03.ibm.com/software/products/en/api-connect) oder ein anderes) mit diesen REST-APIs zu verbinden, die von OpenWhisk bereitgestellt werden. Ähnlich wie für andere Anwendungsfälle gelten auch hier alle Gesichtspunkte der Skalierbarkeit und anderer Aspekte der Servicequalität (QoS). 

Hier finden Sie ein Beispiel und eine Beschreibung der [Verwendung einer serverunabhängigen Plattform als API-Back-End](https://martinfowler.com/articles/serverless.html#ACoupleOfExamples).

## Mobile-Back-End
{: #openwhisk_common_use_cases_mobile}

Viele mobile Anwendungen erfordern serverseitige Logik. Für Entwickler mobiler Anwendungen, die keine serverseitige Logik verwalten wollen, sondern sich lieber auf die App konzentrieren, die auf dem Gerät und in dem Browser ausgeführt wird, ist die Verwendung von {{site.data.keyword.openwhisk_short}} als serverseitiges Back-End eine gute Lösung. Darüber hinaus bietet die integrierte Unterstützung für Swift Entwicklern die Möglichkeit, von vorhandenen iOS-Programmierkenntnissen erneut zu profitieren. Mobile Anwendungen haben häufig unvorhersehbare Auslastungsmuster und eine gehostete {{site.data.keyword.openwhisk_short}}-Lösung wie IBM Bluemix kann praktisch auf jeden Kapazitätsbedarf skaliert werden, ohne dass Ressourcen im Voraus bereitgestellt werden müssen. 

## Datenverarbeitung
{: #openwhisk_common_use_cases_data}

Angesichts der gegenwärtig verfügbaren Datenmengen erfordert die Anwendungsentwicklung die Fähigkeit, neue Daten zu verarbeiten und potenziell darauf zu reagieren. Diese Anforderung schließt die Verarbeitung sowohl strukturierter Datenbanksätze als auch nicht strukturierter Dokumente, Bilder und Videos mit ein. {{site.data.keyword.openwhisk_short}} kann durch vom System bereitgestellte oder angepasste Feeds konfiguriert werden, um auf Änderungen in Daten zu reagieren und automatisch Aktionen an den eingehenden Datenfeeds ausführen. Aktionen können programmiert werden, um Änderungen zu verarbeiten, Datenformate umzusetzen, Nachrichten zu senden und zu empfangen, andere Aktionen aufzurufen sowie verschiedene Datenspeicher zu aktualisieren, einschließlich SQL-basierter relationaler Datenbanken, speicherinterner Datengitter, NoSQL-Datenbanken, Dateien, Nachrichtenbroker und einer Reihe anderer Systeme. {{site.data.keyword.openwhisk_short}}-Regeln und -Sequenzen bieten die Flexibilität, Änderungen in der Verarbeitungspipeline ganz ohne Programmierungsaufwand, sondern einfach durch Konfigurationsänderungen, vornehmen zu können. Dies macht {{site.data.keyword.openwhisk_short}}-basierte Systeme extrem agil und problemlos anpassungsfähig an wechselnde Anforderungen.

## Kognitiv
{: #openwhisk_common_use_cases_cognitive}

Kognitive Technologien lassen sich effektiv mit {{site.data.keyword.openwhisk_short}} zu leistungsfähigen Anwendungen kombinieren. Zum Beispiel können IBM Alchemy API und Watson Visual Recognition zusammen mit {{site.data.keyword.openwhisk_short}} eingesetzt werden, um automatisch nützliche Informationen aus Videos zu extrahieren, ohne diese tatsächlich ansehen zu müssen.  

Hier ist eine Beispielanwendung [Dark Vision](https://github.com/IBM-Bluemix/openwhisk-darkvisionapp), die genau dies leistet. In dieser Anwendung lädt der Benutzer ein Video oder Bild mit der Webanwendung Dark Vision hoch, die es in einer Cloudant-Datenbank speichert. Wenn das Video hochgeladen ist, erkennt {{site.data.keyword.openwhisk_short}} durch die Empfangsbereitschaft für Cloudant-Änderungen (Auslöser) das neue Video. {{site.data.keyword.openwhisk_short}} löst anschließend die Videoextraktoraktion aus. Während der Ausführung generiert der Extraktor Rahmen (Bilder) und speichert diese in Cloudant. Die Rahmen werden anschließend mit Watson Visual Recognition verarbeitet und die Ergebnisse in derselben Cloudant-Datenbank gespeichert. Die Ergebnisse können mithilfe der Webanwendung Dark Vision oder einer iOS-Anwendung angezeigt werden. Neben Cloudant kann Object Storage verwendet werden. In diesem Fall werden Video- und Bildmetadaten in Cloudant gespeichert, während die Mediendateien in Object Storage gespeichert werden.
