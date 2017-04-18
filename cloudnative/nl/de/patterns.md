
---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Mustertypen
{: #patterns}

Cloudorientierte Muster sind bewährte Designs, die dazu beitragen, eine konsistente, skalierbare und zuverlässige Topologie für die Anwendungen sicherzustellen. Wenn Sie ein Projekt erstellen, können Sie aus verschiedenen Mustertypen einen auswählen. Sie wählen einfach Mustertyp und Funktionen aus, die im Projekt enthalten sein sollen. Nachdem Sie die Projektvorgaben definiert haben, wird ein Starter-Projekt generiert, das Sie bearbeiten, ausführen oder debuggen und lokal oder in {{site.data.keyword.Bluemix}} bereitstellen können. 

## Web-App
{: #web}

Webprojekte ermöglichen das Bereitstellen von Inhalt in Form von HTML, JavaScript und Style-Sheets auf einem Web-Server. 

Die folgenden Web-Starter sind verfügbar: 

* Basic Web: Stellt die statische Datei `index.html`, ein Standard-Style-Sheet und ein leeres Style-Sheet und eine JavaScript-Datei bereit. 
* WebPack: Erstellt ein Projekt, in dem sich die ECMAScript 6-Quellendateien (ES6-Quellendateien) in `src/client` befinden und mit WebPack kompiliert werden, um sie zu verkleinern und für die Verwendung im Browser umzuwandeln. 
* WebPack + React: Eine umfassende Umgebung zum Erstellen von Benutzerschnittstellen. Die Quellendateien befinden sich in `src/client/app`, werden mit WebPack kompiliert und im öffentlichen Verzeichnis bereitgestellt. 


## Mobile App
{: #mobile}

Die Muster für mobile Apps erleichtern das Erstellen mobiler Apps, die direkt eine Verbindung zu Back-End-Services aufbauen, zum Beispiel zu {{site.data.keyword.mobilepushshort}}, {{site.data.keyword.mobileanalytics_short}}, {{site.data.keyword.appid_short}}, etc. Die Projekte können auch über sdkGen, wie BFFs, und Microservices hinzufügt werden. 

Sie können einen Starter aus einer Starterliste auswählen, zum Beispiel {{site.data.keyword.watson}} Conversation, {{site.data.keyword.visualrecognitionshort}}, {{site.data.keyword.openwhisk_short}}, etc. 

Sie können die mobilen Apps in Swift, Android oder Cordova generieren. 


## Backend for Frontend (BFF)
{: #bff}

BFF-Muster, die auch als BFFs bezeichnet werden, unterstützen Sie bei der Bereitstellung von Geschäftsdaten und Services in einer Form, die mit den Anforderungen für die Benutzerinteraktion übereinstimmt. Um die User Journey zu Ihrer Cloudlösung optimieren zu können, benötigen Sie für mobile Anwendungen möglicherweise eine separate User Journey sowie eine User Journey für Webanwendungen, die normalerweise umfangreicher und detaillierter gestaltet ist. Durch die Einführung sprachgesteuerter Einheiten wie z. B. den [{{site.data.keyword.conversationfull}} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/conversation.html)-Service kann die Interaktion mit einem Benutzer sprachlich gesteuert werden. Dieser digitale Vertriebskanal erfordert ein grundlegend anderes BFF zur Verwaltung dieser absichtsbasierten Sprachinteraktionen.

Mit {{site.data.keyword.Bluemix_notm}} können Sie ein BFF erstellen, indem Sie einen polyglotten Programmieransatz zum Definieren des BFF anwenden. IBM empfiehlt die Verwendung von Node.js, Swift oder Java und die Ausführung dieser Komponenten in einem cloudorientierten nativen Muster entweder mit Cloud Foundry, Container-Services oder ohne Server. 

Das BFF verwaltet die Integration mit Services für die Datenpersistenz, das Caching und die Integration mit hochwertigen Services wie {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}} sowie mit Datenanalyseprodukten wie {{site.data.keyword.sparks}}.

Das BFF stellt eine API bereit, die im Normalfall ein REST-Muster verwendet. Sie können das BFF jedoch auch so entwerfen, dass es über eine Nachrichtenarchitektur mit {{site.data.keyword.messagehub}} arbeitet.

Ein Basic-Starter für BFF steht bei Verwendung von Node.js oder Swift zur Verfügung. 


## Microservice
{: #microservice}

Microservice-Projekte bieten die Basis zum Erstellen von Back-End-Microservices, einschließlich eines Basiszustandsendpunkts und einer REST-API. Generierte Projekte enthalten alle Abhängigkeiten, die für den Microservice selbst und alle zugeordneten Cloud-Services erforderlich sind. 

Ein Basic-Starter für Microservice steht bei Verwendung von Java zur Verfügung. 

<!--
## Other
{: #other}

The Other pattern represents a project that consists of only the language-specific server-side web framework. It has all the other file assets to work with the project, such as needed libraries and config files.

Content to be provided by Karl Bishop.
-->


## Sprachen
{: #languages notoc}

Folgende Sprachen werden unterstützt: 

   * [Java ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](../runtimes/liberty/getting-started.html){: new_window}
   * [Node.js ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](../runtimes/nodejs/getting-started.html){: new_window}
   * [Swift ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](../runtimes/swift/getting-started.html){: new_window}


### Java
{: #java notoc}

Java verfügt über bewährte Funktionen zum Erstellen von auf Unternehmen abgestimmten Anwendungen. Aber aufgrund der neuen Funktionen in Java 8, kombiniert mit einfacheren Laufzeiten wie Liberty und Umgebungen wie Spring Boot, ist Java auch perfekt zum Erstellen von Microservices geeignet. 


### Node.js
{: #node notoc}

Node.js ist eine JavaScript-Laufzeit, von der ein ereignisgesteuertes, nicht blockierendes E/A-Modell verwendet wird, das sie einfach und effizient macht und einen außergewöhnlichen Durchsatz und eine hervorragende Skalierbarkeit für Webanwendungen, BFF-Muster und Microservices ermöglicht. Das direkte Geschäftsumfeld des Node.js-Pakets, NPM, bietet Zugriff auf eine große Auswahl an Open-Source-Modulen und somit ein großes Angebot an Funktionen zum Beschleunigen der Anwendungsentwicklung. 


### Swift
{: #swift notoc}

Swift ist eine moderne Programmiersprache, die 2014 von Apple geschaffen wurde, um Objective C und Open-Source-Programmen im Dezember 2015 zu ersetzen. Heute wird sie zum Erstellen von iOS-, macOS-, Web-Services- und Systemsoftware auf den Betriebssystemen Linux und macOS unter Verwendung der x86-, ARM- oder Z-Architektur verwendet. Sie wird wie eine Scripting-Sprache geschrieben, wird aber kompiliert, um mit wenig Aufwand eine hohe Leistung zu erreichen, die C ähnelt, und sich somit ideal für Cloudlaufzeiten eignet. Sie verwendet ein starkes und statisches Typsystem, das auch in Java vorhanden ist, aber auch den funktionalen Stil und die asynchronen Routinen, die in JavaScript üblich sind. Sie ist sehr leistungsfähig und die Quelle wird mit dem LLVM-Compiler Toolchain in nativen Code kompiliert; außerdem kann sie problemlos Fremdsystembibliotheken nutzen, die in C geschrieben sind. 
