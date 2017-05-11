---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

---

{:shortdesc: .shortdesc}
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

Ein weiteres wichtiges Argument für {{site.data.keyword.openwhisk_short}} ist der Systemaufwand bei einer Disaster-Recovery-Konfiguration. Nachfolgend werden Mikroservices mit PaaS oder CaaS mit {{site.data.keyword.openwhisk_short}} verglichen. Hierbei wird von 10 Mikroservices ausgegangen, die Container oder CloudFoundry-Laufzeiten verwenden, also von 10 kontinuierlich ausgeführten und fakturierbaren Prozessen in einer einzigen Verfügbarkeitszone bzw. von 20 Prozessen bei Ausführung in zwei Verfügbarkeitszonen bzw. 40 Prozessen bei Ausführung in zwei Regionen mit jeweils zwei Zonen. Bei Ausführung der Mikroservices in {{site.data.keyword.openwhisk_short}} können Sie Mikroservicces in so vielen Verfügbarkeitszonen und Regionen ausführen, wie Sie möchten, ohne dass hierdurch zusätzliche Kosten entstehen.

[Logistics Wizard](https://www.ibm.com/blogs/bluemix/2017/02/microservices-multi-compute-approach-using-cloud-foundry-openwhisk/) ist eine auf Unternehmen abgestimmte Beispielanwendung, die {{site.data.keyword.openwhisk_short}} und CloudFoundry verwendet, um eine 12-Faktor-Anwendung zu erstellen. In dieser intelligenten Supply-Chain-Management-Lösung wird eine Umgebung simuliert, die ein ERP-System ausführt. Dieses ERP-System wird hierbei durch Anwendungen erweitert, die die Sichtbarkeit und geschäftliche Flexibilität der Supply-Chain-Manager verbessern.

## Web-Apps
{: #openwhisk_common_use_cases_webapps}

Aufgrund der ereignisgesteuerten Spezifik von {{site.data.keyword.openwhisk_short}} bietet das Produkt einige Vorteile für Anwendungen mit Benutzerinteraktion, bei denen die HTTP-Anforderungen, die aus dem Browser des Benutzers stammen, als Ereignisse dienen. {{site.data.keyword.openwhisk_short}}-Anwendungen verwenden Rechenkapazität und werden nur dann in Rechnung gestellt, wenn sie Benutzeranforderungen bedienen. Es gibt weder ein Idle Standby noch einen Wartemodus. Dies macht {{site.data.keyword.openwhisk_short}} deutlich günstiger als konventionelle Container oder CloudFoundry-Anwendungen, die möglicherweise einen Großteil der Zeit auf eingehende Benutzeranforderungen warten und bei denen diese gesamte 'Ruhezeit' in Rechnung gestellt wird. 

Mit {{site.data.keyword.openwhisk_short}} können vollständige Webanwendungen erstellt und ausgeführt werden. Die Kombination von serverunabhängigen APIs mit der Bereitstellung statischer Dateien für Siteressourcen, z. B. HTML-, JavaScript- und CSS-Dateien, ermöglicht die Erstellung vollständiger serverunabhängiger Webanwendungen. Der einfache Betrieb einer gehosteten {{site.data.keyword.openwhisk_short}}-Umgebung (oder eher der völlig aufwandslose Betrieb, da das Hosting in Bluemix erfolgt) ist ein großer Vorteil gegenüber dem Betrieb einer traditionellen Serverlaufzeit wie Node.js Express in eigener Regie.

Die folgenden Beispiele zeigen, wie {{site.data.keyword.openwhisk_short}} zum Erstellen einer Web-App verwendet werden kann:
- [Webaktionen: Serverunabhängige Web-Apps mit {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/web-actions-serverless-web-apps-with-openwhisk-f21db459f9ba).
- [{{site.data.keyword.openwhisk_short}}-Anwendung mit Benutzerinteraktion mit Bluemix und Node.js erstellen](https://www.ibm.com/developerworks/cloud/library/cl-openwhisk-node-bluemix-user-facing-app/index.html)
- [Serverunabhängige HTTP-Handler mit {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/serverless-http-handlers-with-openwhisk-90a986cc7cdd)

## IoT
{: #openwhisk_common_use_cases_iot}

IoT-Szenarios sind ihrer Spezifik nach häufig sensorgesteuert. Zum Beispiel könnte eine Aktion in {{site.data.keyword.openwhisk_short}} ausgelöst werden, wenn es erforderlich ist, auf einen Sensor zu reagieren, der eine bestimmte Temperatur überschreitet. IoT-Interaktionen sind in der Regel statusunabhängig mit einem Potenzial für sehr hohe Belastungen im Fall größerer Ereignisse (Naturkatastrophen, schwerwiegende Wetterereignisse, Verkehrsstaus, usw.). Dies macht ein elastisches System erforderlich, dessen normale Auslastung möglicherweise gering ist, das sich jedoch sehr schnell mit vorhersagbarer Antwortzeit skalieren lässt und extrem hohe Anzahlen von Ereignissen ohne Vorwarnung des Systems verarbeiten kann. Es ist recht schwierig, ein System, das diese Anforderungen erfüllt, mithilfe traditioneller Serverarchitekturen aufzubauen, da diese entweder nicht über die entsprechende Leistung verfügen, um Lastspitzen des Datenverkehrs auffangen zu können, oder mit solchen Überkapazitäten ausgestattet sind, dass sie extrem hohe Kosten verursachen.

Es ist sicherlich möglich, IoT-Anwendungen (IoT, Internet of Things - Internet der Dinge) mit traditionellen Serverarchitekturen zu implementieren. In vielen Fällen erfordert die Kombination verschiedener Services und Datenbridges eine sehr hohe Leistung und flexible Pipelines - Anforderungen, denen von IoT-Einheiten bis zur Cloudspeicherung und einer Analyseplattform alle Komponenten gerecht werden müssen. Bridges, die häufig vorkonfiguriert sind, bieten nicht die Programmierbarkeit, die zur Implementierung und Feinabstimmung der Architektur einer bestimmten Lösung erforderlich ist. Angesichts der immensen Auswahl an möglichen Pipelines und der fehlenden Standardisierung im Bereich der Datenfusion im Allgemeinen und im IoT-Bereich im Besonderen, erfordert die Pipeline in vielen Fällen eine angepasste Datenkonvertierung (zur Formatumsetzung, Filterung, Erweiterung usw.). {{site.data.keyword.openwhisk_short}} ist ein hervorragendes Tool zur Implementierung einer solchen Transformation in einer 'serverunabhängigen' Weise, bei der die angepasste Logik in einer vollständig verwalteten und elastischen Cloudplattform bereitgestellt wird.

Hier finden Sie ein Beispiel für eine IoT-Anwendung, die {{site.data.keyword.openwhisk_short}}, NodeRed, Cognitive und andere Services verwendet: [Serverunabhängige Transformation von bewegten IoT-Daten mit {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/serverless-transformation-of-iot-data-in-motion-with-openwhisk-272e36117d6c#.akt3ocjdt).

![Beispiel für die Architektur einer IoT-Lösung](images/IoT_solution_architecture_example.png)

## API-Back-End
{: #openwhisk_common_use_cases_iot}

Serverunabhängige IT-Plattformen bieten Entwicklern eine schnelle Möglichkeit zum Erstellen von APIs ohne Server. {{site.data.keyword.openwhisk_short}} unterstützt die automatische Generierung von REST-APIs für Aktionen. Die [experimentelle Funktion](./apigateway.md) von {{site.data.keyword.openwhisk_short}} ermöglicht Ihnen den Aufruf einer Aktion mit anderen HTTP-Methoden als POST und ohne den Berechtigungs-API-Schlüssel der Aktion über das {{site.data.keyword.openwhisk_short}}-API-Gateway. Diese Fähigkeit ist nicht nur zur Bereitstellung von APIs für externe Konsumenten, sondern auch zur Erstellung von Mikroserviceanwendungen hilfreich.

Außerdem können {{site.data.keyword.openwhisk_short}}-Aktionen mit einem API-Management-Tool Ihrer Wahl verbunden werden (z. B. [IBM API Connect](https://www-03.ibm.com/software/products/en/api-connect) oder ein anderes Tool). Ähnlich wie für andere Anwendungsfälle gelten auch hier alle Gesichtspunkte der Skalierbarkeit und anderer Aspekte der Servicequalität (QoS). 

[Emoting](https://github.com/l2fprod/openwhisk-emoting) ist eine Beispielapp, die {{site.data.keyword.openwhisk_short}}-Aktionen über die REST-API verwendet.

Hier finden Sie ein Beispiel und eine Beschreibung der [Verwendung einer serverunabhängigen Plattform als API-Back-End](https://martinfowler.com/articles/serverless.html#ACoupleOfExamples).

## Mobile-Back-End
{: #openwhisk_common_use_cases_mobile}

Viele mobile Anwendungen erfordern serverseitige Logik. In Anbetracht der Tatsache, dass Entwickler mobiler Anwendungen für gewöhnlich keine Erfahrungen bei der Verwaltung der serverseitigen Logik besitzen und sich eher auf die App konzentrieren, die auf dem Gerät ausgeführt wird, ist die Verwendung von {{site.data.keyword.openwhisk_short}} als serverseitigem Back-End-Programm eine sinnvolle Lösung. Darüber hinaus bietet die integrierte Unterstützung für Swift auf der Serverseite den Entwicklern die Möglichkeit, von vorhandenen iOS-Programmierkenntnissen erneut zu profitieren. Mobile Anwendungen haben häufig unvorhersehbare Auslastungsmuster und eine gehostete {{site.data.keyword.openwhisk_short}}-Lösung wie IBM Bluemix kann praktisch auf jeden Kapazitätsbedarf skaliert werden, ohne dass Ressourcen im Voraus bereitgestellt werden müssen.

[Skylink](https://github.com/IBM-Bluemix/skylink) ist eine Beispielanwendung, mit der Sie eine Flugdrone über iPad mit der IBM Cloud verbinden und unter Verwendung von {{site.data.keyword.openwhisk_short}}, IBM Cloudant, IBM Watson und Alchemy Vision die Bilder quasi in Echtzeit analysieren können.

[BluePic](https://github.com/IBM-Swift/BluePic) ist eine Anwendung für die gemeinsame Nutzung von Fotos und Bildern, mit der Sie Fotos aufnehmen und mit anderen BluePic-Benutzern teilen können. Diese Anwendung veranschaulicht, wie eine Kitura-basierte und in Swift geschriebene Serveranwendung, die {{site.data.keyword.openwhisk_short}}, Cloudant und Object Storage nutzt, in einer mobilen iOS 10-Anwendung für Bilddaten verwendet wird. AlchemyAPI wird auch in der {{site.data.keyword.openwhisk_short}}-Sequenz eingesetzt, um das Bild zu analysieren, Texttags basierend auf dem Inhalt des Bildes zu extrahieren und dann eine Push-Benachrichtigung an den Benutzer zu senden.

## Datenverarbeitung
{: #openwhisk_common_use_cases_data}

Angesichts der gegenwärtig verfügbaren Datenmengen erfordert die Anwendungsentwicklung die Fähigkeit, neue Daten zu verarbeiten und potenziell darauf zu reagieren. Diese Anforderung schließt die Verarbeitung sowohl strukturierter Datenbanksätze als auch nicht strukturierter Dokumente, Bilder und Videos mit ein. {{site.data.keyword.openwhisk_short}} kann durch vom System bereitgestellte oder angepasste Feeds konfiguriert werden, um auf Änderungen in Daten zu reagieren und automatisch Aktionen an den eingehenden Datenfeeds ausführen. Aktionen können programmiert werden, um Änderungen zu verarbeiten, Datenformate umzusetzen, Nachrichten zu senden und zu empfangen, andere Aktionen aufzurufen sowie verschiedene Datenspeicher zu aktualisieren, einschließlich SQL-basierter relationaler Datenbanken, speicherinterner Datengitter, NoSQL-Datenbanken, Dateien, Nachrichtenbroker und einer Reihe anderer Systeme. {{site.data.keyword.openwhisk_short}}-Regeln und -Sequenzen bieten die Flexibilität, Änderungen in der Verarbeitungspipeline ganz ohne Programmierungsaufwand, sondern einfach durch Konfigurationsänderungen, vornehmen zu können. Dies macht {{site.data.keyword.openwhisk_short}}-basierte Systeme extrem agil und problemlos anpassungsfähig an wechselnde Anforderungen.

Das [OpenChecks](https://github.com/krook/openchecks)-Projekt ist eine Art Machbarkeitsnachweis, der belegt, wie {{site.data.keyword.openwhisk_short}} zur Verarbeitung von Scheckeinreichungen bei einem Bankkonto unter Verwendung optischer Zeichenerkennung verwendet werden kann. Es basiert gegenwärtig auf dem öffentlichen {{site.data.keyword.openwhisk_short}}-Service von Bluemix und stützt sich auf Cloudant und SoftLayer Object Storage. Lokal könnte CouchDB und OpenStack Swift verwendet werden. Weitere Speicherservices sind unter anderem FileNet oder Cleversafe. Tesseract stellt die OCR-Bibliothek bereit.
## Kognitiv
{: #openwhisk_common_use_cases_cognitive}

Kognitive Technologien lassen sich effektiv mit {{site.data.keyword.openwhisk_short}} zu leistungsfähigen Anwendungen kombinieren. Zum Beispiel können IBM Alchemy API und Watson Visual Recognition zusammen mit {{site.data.keyword.openwhisk_short}} eingesetzt werden, um automatisch nützliche Informationen aus Videos zu extrahieren, ohne diese tatsächlich ansehen zu müssen. Dies kann einfach eine 'kognitive' Erweiterung des bereits erläuterten Anwendungsfalls für die [Datenverarbeitung](#data-processing) sein. Eine weitere sinnvolle Einsatzmöglichkeit von {{site.data.keyword.openwhisk_short}} ist die Implementierung einer Botfunktion in Kombination mit kognitiven Services. 

Hier ist eine Beispielanwendung [Dark Vision](https://github.com/IBM-Bluemix/openwhisk-darkvisionapp), die genau dies leistet. In dieser Anwendung lädt der Benutzer ein Video oder Bild mit der Webanwendung Dark Vision hoch, die es in einer Cloudant-Datenbank speichert. Wenn das Video hochgeladen ist, erkennt {{site.data.keyword.openwhisk_short}} durch die Empfangsbereitschaft für Cloudant-Änderungen (Auslöser) das neue Video. {{site.data.keyword.openwhisk_short}} löst anschließend die Videoextraktoraktion aus. Während der Ausführung generiert der Extraktor Rahmen (Bilder) und speichert diese in Cloudant. Die Rahmen werden anschließend mit Watson Visual Recognition verarbeitet und die Ergebnisse in derselben Cloudant-Datenbank gespeichert. Die Ergebnisse können mithilfe der Webanwendung Dark Vision oder einer iOS-Anwendung angezeigt werden. Neben Cloudant kann Object Storage verwendet werden. In diesem Fall werden Video- und Bildmetadaten in Cloudant gespeichert, während die Mediendateien in Object Storage gespeichert werden.

Hier ist eine [iOS-Swift-Beispielanwendung](https://github.com/gconan/BluemixMobileServicesDemoApp), die veranschaulicht, wie {{site.data.keyword.openwhisk_short}}, IBM Mobile Analytics und Watson verwendet werden, um Klänge zu analysieren und an einen Slack-Kanal zu senden.

## Ereignisverarbeitung mit Kafka oder Message Hub 

{{site.data.keyword.openwhisk_short}} eignet sich sehr gut für eine Kombination mit Kafka, dem Service von IBM Message Hub (Kafka-basiert) und anderen Nachrichtensystemen. Die ereignisgesteuerte Spezifik dieser Systeme erfordert eine ereignisgesteuerte Laufzeit für die Verarbeitung von Nachrichten und die Anwendung von Geschäftslogik auf Nachrichten. Genau dies leistet {{site.data.keyword.openwhisk_short}} mit seinen Feeds, Auslösern, Aktionen usw. Kafka und Message Hub werden häufig für sehr große und unvorhersehbare Workloadvolumina eingesetzt und machen es erforderlich, dass die Konsumenten dieser Nachrichten sofort skalierbar sein müssen, ein weiterer Vorteil von {{site.data.keyword.openwhisk_short}}. Dank integrierter Funktionalität ist {{site.data.keyword.openwhisk_short}} in der Lage, sowohl Nachrichten zu verarbeiten als auch Nachrichten zu veröffentlichen. Diese Funktionalität wird im Paket [openwhisk-package-kafka](https://github.com/openwhisk/openwhisk-package-kafka) bereitgestellt.

Hier ist eine [Beispielanwendung, die das Ereignisverarbeitungsszenario implementiert](https://github.com/IBM/openwhisk-data-processing-message-hub) und hierzu {{site.data.keyword.openwhisk_short}}, Message Hub und Kafka nutzt.
