---

copyright:
  years: 2016, 2017
lastupdated: "2016-04-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Cloudorientierte Projekte erstellen
{: #web-mobile}

Sie können cloudorientierte Apps unter Verwendung des Konzepts der {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}-[Projekte](projects.html) verwalten. Sie können ein Projekt mit der [{{site.data.keyword.dev_console}}](devex.html) oder dem [{{site.data.keyword.dev_cli_notm}}](dev_cli.html) für die {{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}} CLI verwalten. Die {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} stellt die am meisten gebräuchlichen Servicefunktionen, die für einen cloudorientierten Anwendungsentwickler erforderlich sind, in einer einzigen übergreifenden Umgebung bereit, die für Entwickler optimiert wurde.

Die {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} ermöglicht einem cloudorientierten Anwendungsentwickler die Erstellung eines Projekts über eine Vielzahl von [Mustertypen](patterns.html) und [Startern](starters.html), die Erstellung wichtiger {{site.data.keyword.Bluemix_notm}}-optimierter Services und deren Verbindung mit Ihrem Projekt sowie das schnelle Herunterladen von Code mithilfe von SDKs. Die SDKs sind vollständig mit den Funktionsberechtigungsnachweisen oder Abhängigkeiten integriert, um Ihnen die Ausführung innerhalb weniger Minuten zu ermöglichen. Wenn Ihre Anwendung aktiv ist und Sie die Funktionen eingerichtet und konfiguriert haben, können Sie zu Ihrem Projekt zurückkehren, um die Aktivitäten Ihrer Anwendungsbenutzer zu überwachen und zu verwalten. Sie können die Services auch über die {{site.data.keyword.dev_console}} konfigurieren und verwalten.

<!--
While the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} provides an integrated development experience, some developers might still want to have finer-grained control and wire services together manually. If this is your preferred approach, you might want to consider using the [{{site.data.keyword.mobilefirstbp}} Starter boilerplate](try_mobile.html).
-->

<!--With {{site.data.keyword.Bluemix}} Mobile services, you can incorporate pre-built, managed, and scalable cloud services into your mobile applications. You can focus on building your mobile apps, instead of the complexities of managing the back-end infrastructure.

The Mobile dashboard provides an integrated experience on {{site.data.keyword.Bluemix_notm}} where you can create mobile projects easily from within the dashboard.
-->


## Projekte
{: #projects}

Die {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} kombiniert die App-Benutzerschnittstelle, die Daten und Services zu einem vollständigen Projekt (*project*). Indem Sie ein Projekt erstellen, werden alle erforderlichen Teile Ihrer App und die hinzugefügten Funktionen auf dem {{site.data.keyword.Bluemix_notm}}-Server beibehalten. Sie können den App-Code und die erforderlichen Berechtigungsnachweise und Initialisierungsoperatoren herunterladen, wenn die Services im Projekt konfiguriert sind. Durch Auswahl von **Projekte** können Sie alle Projekte anzeigen.  

Sie können zusätzliche Informationen zu einem einzelnen Projekt anzeigen; hierfür müssen Sie es auf der Seite **Projekte** auswählen. Dadurch wird die Seite **Projektübersicht** angezeigt; dort sind die Services aufgeführt, die konfiguriert und für das Projekt verfügbar sind. Services sind separate Funktionen, die Ihre App durch Hinzufügen einer Funktion erweitern. Da sie einzeln hinzugefügt werden, können Sie sich auf die Services beschränken, die Sie benötigen, wie zum Beispiel Push-, Authentication-, Data- und Storage-Services oder andere Services. Wenn Sie auf der Seite **Projektübersicht** einen Service zu Ihrem Projekt hinzufügen und die Anweisungen zum Konfigurieren des Service befolgen, wird der Service automatisch Ihrer App zugeordnet. Weitere Informationen zur Seite 'Projektübersicht' finden Sie im Abschnitt [Seite 'Projektübersicht'](project_overview_page.html).

Zum Erstellen eines Projekts müssen Sie ein [Muster](patterns.html) und danach einen [Starter](starters.html) auswählen.


### Seite 'Projektübersicht'
{: #project_overview}

Sie können ein einzelnes Projekt in der {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} anzeigen und verwenden, indem Sie das Projekt auf der Seite **Projekte** auswählen. Durch diese Aktion wird die Seite 'Projektübersicht' geöffnet. 
{: shortdesc}

Auf der Seite **Projektübersicht** wird eine Kachel für jede Funktion angezeigt, die für das ausgewählte Projekt konfiguriert oder zum Konfigurieren verfügbar ist. In der Kachel werden der Funktionstyp und die Schaltfläche *Aktionen* mit drei vertikal ausgerichteten Punkten angezeigt. Zu den verfügbaren bzw. konfigurierten Funktionen können beispielsweise {{site.data.keyword.mobilepushshort}}, Analytics oder Data und Storage gehören. Welche Funktionen kompatibel sind, hängt vom Typ des Projekts und von den Funktionen ab, die in der jeweiligen Region verfügbar sind (d. h. nicht alle Funktionen können allen Projekten zugeordnet werden). 

Wenn ein Funktionstyp noch nicht dem Projekt zugeordnet ist, wird auf der Kachel die Schaltfläche **Erstellen** angezeigt. Die verfügbaren Optionen der Schaltfläche für Aktionen ermöglichen das Erstellen einer Serviceinstanz oder das Hinzufügen einer vorhandenen Serviceinstanz, falls die betreffende Funktion noch nicht zugeordnet ist. Nach dem Auswählen der Option **Vorhandene hinzufügen** wird eine Liste der Serviceinstanzen des betreffenden Typs im Bereich angezeigt.

Wenn die Funktion bereits diesem Projekt zugeordnet ist, wird der Name der zugehörigen Serviceinstanz auf der Kachel nach dem Funktionstyp angezeigt. Dies vereinfacht das Auffinden der zugehörigen Serviceinstanz für dieses Projekt in der {{site.data.keyword.dev_console}}. Über die Aktionsschaltfläche stehen die Aktionen **Anzeigen** und **Entfernen** zur Verfügung, wenn die Funktion bereits dem Projekt zugeordnet ist. Beim Entfernen einer Serviceinstanz wird lediglich die Zuordnung zu diesem Projekt aufgehoben. Die Serviceinstanz in der {{site.data.keyword.dev_console}} wird nicht gelöscht. Klicken Sie zum Löschen einer Serviceinstanz auf die Seite **Web and Mobile > Services**, um die Serviceinstanzen anzuzeigen und zu löschen.

Wählen Sie **Code abrufen** in der Kachel **Code** aus, um den Code für Ihr Projekt herunterzuladen. Weitere Informationen zum Herunterladen von Code finden Sie unter [Code abrufen](get_code.html).


### Projekt zur Verwendung eines neuen Starters aktualisieren
{: #update-starter}

1. Klicken Sie auf der Seite **Projekte** oder **Projektübersicht** auf das Symbol **Überlaufmenü** und wählen Sie **Starter aktualisieren** aus.

2. Wählen Sie einen neuen Starter aus und klicken Sie auf **Aktualisieren**.

3. Klicken Sie auf der Seite **Projektübersicht** auf **Code abrufen**, um Ihre Sprache auszuwählen.

   Alternativ können Sie auf die Seite **Code** klicken.


### Projekt zum Generieren einer neuen Sprache aktualisieren
{: #update-language}

1. Klicken Sie auf der Seite **Projekte** oder **Projektübersicht** auf das Symbol **Überlaufmenü** und wählen Sie **Starter aktualisieren** aus.

2. Wählen Sie eine neue Sprache aus und klicken Sie auf **Aktualisieren**.

3. Klicken Sie auf der Seite **Projektübersicht** auf **Code abrufen**, um Ihre Sprache auszuwählen.


## Mustertypen
{: #patterns}

Cloudorientierte Muster sind bewährte Designs, die dazu beitragen, eine konsistente, skalierbare und zuverlässige Topologie für die Anwendungen sicherzustellen. Wenn Sie ein Projekt erstellen, können Sie aus verschiedenen Mustertypen einen auswählen. Sie wählen einfach Mustertyp und Funktionen aus, die im Projekt enthalten sein sollen. Nachdem Sie die Projektvorgaben definiert haben, wird ein Starter-Projekt generiert, das Sie bearbeiten, ausführen oder debuggen und lokal oder in {{site.data.keyword.Bluemix}} bereitstellen können.


### Web-App
{: #web}

Webprojekte ermöglichen das Bereitstellen von Inhalt in Form von HTML, JavaScript und Style-Sheets auf einem Web-Server.

Die folgenden Web-Starter sind verfügbar:

* Basic Web: Stellt die statische Datei `index.html`, ein Standard-Style-Sheet und ein leeres Style-Sheet und eine JavaScript-Datei bereit.
* WebPack: Erstellt ein Projekt, in dem sich die ECMAScript 6-Quellendateien (ES6-Quellendateien) in `src/client` befinden und mit WebPack kompiliert werden, um sie zu verkleinern und für die Verwendung im Browser umzuwandeln.
* WebPack + React: Eine umfassende Umgebung zum Erstellen von Benutzerschnittstellen. Die Quellendateien befinden sich in `src/client/app`, werden mit WebPack kompiliert und im öffentlichen Verzeichnis bereitgestellt.


### Mobile App
{: #mobile}

Die Muster für mobile Apps erleichtern das Erstellen mobiler Apps, die direkt eine Verbindung zu Back-End-Services aufbauen, zum Beispiel zu {{site.data.keyword.mobilepushshort}}, {{site.data.keyword.mobileanalytics_short}}, {{site.data.keyword.appid_short}}, etc. Die Projekte können auch über sdkGen, wie BFFs, und Microservices hinzufügt werden.

Sie können einen Starter aus einer Starterliste auswählen, zum Beispiel {{site.data.keyword.watson}} Conversation, {{site.data.keyword.visualrecognitionshort}}, {{site.data.keyword.openwhisk_short}}, etc.

Sie können die mobilen Apps in Swift, Android oder Cordova generieren.


### Backend for Frontend (BFF)
{: #bff}

BFF-Muster, die auch als BFFs bezeichnet werden, unterstützen Sie bei der Bereitstellung von Geschäftsdaten und Services in einer Form, die mit den Anforderungen für die Benutzerinteraktion übereinstimmt. Um die User Journey zu Ihrer Cloudlösung optimieren zu können, benötigen Sie für mobile Anwendungen möglicherweise eine separate User Journey sowie eine User Journey für Webanwendungen, die normalerweise umfangreicher und detaillierter gestaltet ist. Durch die Einführung sprachgesteuerter Einheiten wie z. B. den [{{site.data.keyword.conversationfull}} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/conversation.html)-Service kann die Interaktion mit einem Benutzer sprachlich gesteuert werden. Dieser digitale Vertriebskanal erfordert ein grundlegend anderes BFF zur Verwaltung dieser absichtsbasierten Sprachinteraktionen. 

Mit {{site.data.keyword.Bluemix_notm}} können Sie ein BFF erstellen, indem Sie einen polyglotten Programmieransatz zum Definieren des BFF anwenden. IBM empfiehlt die Verwendung von Node.js, Swift oder Java und die Ausführung dieser Komponenten in einem cloudorientierten nativen Muster entweder mit Cloud Foundry, Container-Services oder ohne Server.

Das BFF verwaltet die Integration mit Services für die Datenpersistenz, das Caching und die Integration mit hochwertigen Services wie {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}} sowie mit Datenanalyseprodukten wie {{site.data.keyword.sparks}}. 

Das BFF stellt eine API bereit, die im Normalfall ein REST-Muster verwendet. Sie können das BFF jedoch auch so entwerfen, dass es über eine Nachrichtenarchitektur mit {{site.data.keyword.messagehub}} arbeitet. 

Ein BFF Basic Starter steht bei Verwendung von Node.js oder Swift zur Verfügung. 


### Microservice
{: #microservice}

Microserviceprojekte bieten die Grundlage zum Erstellen von Back-End-Microservices, einschließlich eines Basisstatusendpunkts und einer REST-API. Generierte Projekte enthalten alle Abhängigkeiten, die für den Microservice selbst und alle zugeordneten Cloud-Services erforderlich sind.

Ein Microservice Basic Starter steht bei Verwendung von Java zur Verfügung.

<!--
## Other
{: #other}

The Other pattern represents a project that consists of only the language-specific server-side web framework. It has all the other file assets to work with the project, such as needed libraries and config files.

Content to be provided by Karl Bishop.
-->


### Sprachen
{: #languages notoc}

Folgende Sprachen werden unterstützt:

   * [Java ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](../runtimes/liberty/getting-started.html){: new_window}
   * [Node.js ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](../runtimes/nodejs/getting-started.html){: new_window}
   * [Swift ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](../runtimes/swift/getting-started.html){: new_window}


#### Java
{: #java notoc}

Java verfügt über bewährte Funktionen zum Erstellen von auf Unternehmen abgestimmten Anwendungen. Aber aufgrund der neuen Funktionen in Java 8, kombiniert mit einfacheren Laufzeiten wie Liberty und Umgebungen wie Spring Boot, ist Java auch perfekt zum Erstellen von Microservices geeignet.


#### Node.js
{: #node notoc}

Node.js ist eine JavaScript-Laufzeit, von der ein ereignisgesteuertes, nicht blockierendes E/A-Modell verwendet wird, das sie einfach und effizient macht und einen außergewöhnlichen Durchsatz und eine hervorragende Skalierbarkeit für Webanwendungen, BFF-Muster und Microservices ermöglicht. Das direkte Geschäftsumfeld des Node.js-Pakets, NPM, bietet Zugriff auf eine große Auswahl an Open-Source-Modulen und somit ein großes Angebot an Funktionen zum Beschleunigen der Anwendungsentwicklung.


#### Swift
{: #swift notoc}

Swift ist eine moderne Programmiersprache, die 2014 von Apple geschaffen wurde, um Objective C und Open-Source-Programmen im Dezember 2015 zu ersetzen. Heute wird sie zum Erstellen von iOS-, macOS-, Web-Services- und Systemsoftware auf den Betriebssystemen Linux und macOS unter Verwendung der x86-, ARM- oder Z-Architektur verwendet. Sie wird wie eine Scripting-Sprache geschrieben, wird aber kompiliert, um mit wenig Aufwand eine hohe Leistung zu erreichen, die C ähnelt, und sich somit ideal für Cloudlaufzeiten eignet. Sie verwendet ein starkes und statisches Typsystem, das auch in Java vorhanden ist, aber auch den funktionalen Stil und die asynchronen Routinen, die in JavaScript üblich sind. Sie ist sehr leistungsfähig und die Quelle wird mit dem LLVM-Compiler Toolchain in nativen Code kompiliert; außerdem kann sie problemlos Fremdsystembibliotheken nutzen, die in C geschrieben sind.


## Starter
{: #starters}

In der {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} können Sie für jeden Mustertyp einen Starter aus einer Vielzahl an Startern auswählen.

Starter werden als produktionsbereiter Startercode mit Fokus auf der Veranschaulichung einer wichtigen {{site.data.keyword.Bluemix_notm}}-Integration mit einem hochwertigen Service optimiert. Jeder Starter konzentriert sich auf einen Service und zeigt die Integration der Service-SDKs in den Code. In einigen Fällen bieten Starter eine einfache Benutzerumgebung, in der die Integration der Servicedaten oder Interaktionen mit dem Benutzer besser sichtbar wird. Jeder Starter ist für die Aktivierung mit der Authentication-Funktion, Data-Funktion und möglicherweise weiteren Leistungsmerkmalen konfiguriert, falls Sie beschließen, diese für Ihr Projekt zu konfigurieren.
