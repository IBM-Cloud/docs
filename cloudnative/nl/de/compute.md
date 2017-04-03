---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Compute
{: #compute}

Wenn Sie eine cloudorientierte native Anwendung für digitale Vertriebskanäle für das Web und Mobilgeräte erstellen, dann hat es sich bewährt, mit einem BFF (Backend for Frontend) zu arbeiten, das entweder Ihrem digitalen Vertriebskanal zugeordnet ist oder die gleichen Daten und die gleiche Unterstützung für die logische Integration für Web-Client-Apps und mobile Client-Apps bietet. Weitere Informationen zu dieser Architektur finden Sie im Artikel zu den [Mikroservices für das Web und mobile Einheiten ![Symbol für externen Link](../icons/launch-glyph.svg)](https://www.ibm.com/devops/method/content/architecture/omnichannelArchitecture).

Im folgenden Diagramm wird eine Übersicht zur BFF-Architektur dargestellt.

![BFF-Architektur](images/bff-arch.png)

Abbildung 1: BFF-Architektur

Das BFF-Konzept basiert auf der Entfernung allgemeiner Geschäfts- und Integrationslogik aus den Mikroservices oder hochwertigen {{site.data.keyword.Bluemix}}-Cloud-Services. 

Mit dieser Architektur können Sie Updates für Ihre mobilen Anwendung oder Webanwendungen bereitstellen und freigeben und neue Versionen Ihres BFF bereitstellen, indem Sie kontinuierliche Delivery Pipelines für den DevOps-Service verwenden.

Wenn Sie über eine BFF für iOS und eine separate BFF für Android verfügen, dann sind die Entwicklungsteams, die die Funktion für diese Apps liefern, bei der Freigabe von Features nicht durch einen zentralisierten API-Freigabeplan eingeschränkt. Dies stellt ein gemeinsames Ziel für Mikroservice-Architekturen und Architekturen für digitale Vertriebskanäle dar, um den Teams die häufige Freigabe von Funktionen und Features zu ermöglichen, ohne dass eine enge Abhängigkeit zum Freigabeplan eines anderen Teams besteht.

<!--
## Backend for Frontends (BFF)
{: #bff}

Backend for Frontend patterns, commonly known as BFFs, really help you to focus on exposing business data and services in a form that matches the user interaction requirements. To optimize a user journey to your cloud solution, it may require a different user journey for the mobile application and a richer, more detailed journey for the Web application. With the introduction of voice-controlled devices like the [{{site.data.keyword.conversationfull}} ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/conversation.html) service, the interaction with a user could be controlled by voice. This digital channel will require a very different BFF for managing these voice intent-based interactions.

With {{site.data.keyword.Bluemix_notm}}, you can build a BFF by using polyglot programming approach to define the BFF. IBM recommends using Node, Swift, or Java and running them in a cloud native pattern with either Cloud Foundry, Container services, or serverless.

The BFF will manage the integration with services for data persistence, caching, and integration with high-value services like {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}}, and data analytics like {{site.data.keyword.sparks}}.

The BFF will expose an API most commonly using a REST pattern, but you can design your BFF to work from a messaging architecture using {{site.data.keyword.messagehub}}.
-->


## Mobilen Client in BFF integrieren
{: #integration}

Zur Bereitstellung einfacher Integrationsmöglichkeiten zwischen einem mobilen Client und einem BFF (Backend for Frontends) unterstützt {{site.data.keyword.Bluemix_notm}} die SDK-Generierung für mobile Clients für iOS und Android in Swift- bzw. Java-Sprachen. Zum Aktivieren dieses Features müssen Sie die BFF-Integration mithilfe eines Dokuments für Open API-Spezifikationen (Swagger) bereitstellen. Dieses Dokument kann im JSON- oder YAML-Format vorliegen.

Der SDK-Generator des Clients verwendet die Open API-Definitionsdatei zum Definieren eines clientoptimierten Entwickler-SDK, das in Ihrer nativen mobilen Anwendung einfach zu verarbeiten ist. Auf diese Weise kann die Integration Ihres BFF in Ihre mobile Anwendung beschleunigt werden.


## API definieren
{: #definition}

Das BFF muss eine der Open API-Spezifikation entsprechende API-Definitionsdatei bereitstellen, die auf einem Live-Serverendpunkt ausgeführt wird. Damit {{site.data.keyword.Bluemix_notm}} Developer Experience und die {{site.data.keyword.Bluemix_notm}}-SDK-CLI (Command Line Interface) diesen Endpunkt erkennen können, müssen Sie eine Umgebungsvariable mit dem Namen `OPENAPI_SPEC` zu Ihrer Cloud Foundry-Anwendung hinzufügen. Diese Umgebungsvariable muss mit einem relativen Pfad auf die Spezifikation verweisen.

Führen Sie die folgenden Schritte aus, um die Umgebungsvariable `OPENAPI_SPEC` in {{site.data.keyword.Bluemix_notm}} hinzuzufügen:

1. Melden Sie sich bei [{{site.data.keyword.Bluemix_notm}} ![Symbol für externen Link](../icons/launch-glyph.svg)](http://bluemix.net) an.
2. Wählen Sie eine Cloud Foundry-App aus.
3. Wählen Sie **Laufzeit** aus.
4. Wählen Sie **Umgebungsvariablen** aus.
5. Klicken Sie im Abschnitt **Benutzerdefiniert** auf **Hinzufügen**.
6. Legen Sie für **NAME** die Angabe `OPENAPI_SPEC` und einen relativen URL-Pfad zu Ihrer Open API-Definitionsdatei fest.
7. Klicken Sie auf **Speichern**.

<!--
To add the `OPENAPI_SPEC` environment variable locally and push your changes to {{site.data.keyword.Bluemix_notm}} with the [Cloud Foundry CLI ![External link icon](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli#getting-started), follow these steps:

1. Open Terminal and navigate to your project directory.
2. Add the following code to the `manifest.yml` file.

   ```
   env:
       "OPENAPI_SPEC": "<relative URL path to your Open API definition file>"
   ```
   {: codeblock}
3. Save your changes to the `manifest.yml` file.
4. Run `cf push` to deploy the changes to {{site.data.keyword.Bluemix_notm}}.
-->

Beispiel:

```
OPENAPI_SPEC='/explorer/swagger.json'
```
{: codeblock}

Dieser Ansatz bietet insbesondere bei Verwendung von {{site.data.keyword.apiconnect_long}}- und Loopback-Anwendungen Vorteile. Sie können das Loopback und {{site.data.keyword.apiconnect_short}} verwenden, um ein persistentes Modell zu definieren und die CRUD-Operation (CRUD = Create, Read, Update, and Delete) mit der Open API-Definitionsdatei bereitzustellen.

Außerdem können Sie Geschäftslogikoperationen definieren.


### Unterstützte Elemente der Open API-Spezifikation
{: #supported-elements notoc}

Der einzige Bereich der Open API-Spezifikation, der nicht vollständig unterstützt wird, betrifft die Dateistruktur. Die Spezifikation erlaubt das Aufteilen der Definitionsabschnitte auf verschiedene Dateien und ihre Referenzierung mithilfe des JSON-Felds `$ref`. Ihre gesamte Definition muss in einer Datei enthalten sein.


## BFF-Beispiel für Verwendung von Bluegen
{: #bff-bluegen}

{{site.data.keyword.Bluemix_notm}} hat mithilfe von {{site.data.keyword.apiconnect_short}} und Strongloop ein Referenz-BFF erstellt. Dabei wird eine Zuordnung zwischen einem Produktmodell und {{site.data.keyword.cloudant}} sowie einer Bild-API zur Referenzierung von Bildern in {{site.data.keyword.objectstorageshort}} hergestellt.

Sie können dieses BFF-Muster verwenden, um rasch ein voll funktionsfähiges BFF in {{site.data.keyword.Bluemix_notm}} bereitzustellen, das die Einarbeitung in die Vorgehensweise zur Integration eines BFF in ein mobiles Projekt und das Generieren nativer SDKs für iOS und Android in Swift bzw. Java vereinfacht.

Befolgen Sie die Anweisungen in der [README ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/backend-for-frontend-node) zur Erstellung eines Projekts und zu seiner Installation.


## BFF mit Developer Experience-Projekt verwenden
{: #bff-devex}

{{site.data.keyword.Bluemix_notm}} Mobile Developer Experience wurde so konzipiert, dass das Definieren eines mobilen Projekts mit einer Reihe zugeordneter Cloud-Services vereinfacht wird. Sie können [{{site.data.keyword.mobilepushshort}} ![Symbol für externen Link](../icons/launch-glyph.svg)](/docs/services/mobilepush/index.html), [Analytics ![Symbol für externen Link](../icons/launch-glyph.svg)](/docs/services/mobileanalytics/index.html) sowie Data- oder Storage-Services auf einfache Weise hinzufügen.

Die {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} bietet auf der Seite **Compute** die Möglichkeit zur Integration eines BFF in ein mobiles Projekt. Sie können vorhandene Compute-Serviceinstanzen zu Ihrem mobilen Projekt hinzufügen. Nach dem Hinzufügen können Sie entweder ein natives SDK für Ihre Sprachauswahl generieren oder Sie können das vollständige Projekt generieren. In diesem Fall wird das SDK auf der Seite **Code** in das Quellenpaket des Projekts integriert. Diese Vorgehensweise ist besonders nützlich, wenn Sie eine Integration mit BFFs durchführen, die bereits klar strukturiert sind.

Nach dem Download des Projekts können Sie es mit Xcode oder Android Studio öffnen und das Projekt mit dem Client-SDK kompilieren.


## CLI verwenden
{: #cli}

Während der Entwicklung des BFF kann es zu Änderungen an der API-Spezifikation kommen. Zur Unterstützung dieser Änderungen stehen Ihnen die beiden folgenden Optionen zur Verfügung.

* Neuerstellung des gesamten Projekts in einem neuen GitHub-Zweig und Zusammenführen der Änderungen in Ihrem Entwicklungszweig.
* Direkte Neuerstellung des SDK mithilfe des Befehlszeilentools (CLI) und ausschließliche Aktualisierung der SDK-Komponente des mobilen Projekts.

Zur Verwendung der CLI müssen Sie sie [installieren](sdk_cli.html#installation).

Verwenden Sie den folgenden Befehl, um die Aktionen aufzulisten, die ausgeführt werden können.

```
bluemix sdk
```
{: codeblock}

Verwenden Sie den folgenden Befehl, um die aktiven Cloud Foundry-Instanzen in Ihrem aktuellen {{site.data.keyword.Bluemix_notm}}-Bereich aufzulisten.

```
bluemix sdk list
```
{: codeblock}

Jede App wird aufgelistet und die API wird überprüft, wenn die Umgebungsvariable `OPENAPI_SPEC` festgelegt wurde. In der Spalte `VALID` befindet sich ein grünes Häkchen oder ein rotes `X`. Das Häkchen in der Spalte `VALID` für die Anwendung bedeutet, dass eine gültige Open API-Definition vorhanden ist. Ein `X` in der Spalte `VALID` der Anwendung kann Folgendes bedeuten:

* Es wurde keine Umgebungsvariable `OPENAPI_SPEC` für die Anwendung definiert ODER
* die API-Definition ist in Bezug auf die Open API-Spezifikation nicht gültig.

Verwenden Sie den folgenden Befehl, um die vollständig formatierte URL der API anzuzeigen. Die vollständig formatierte Route und der URI zur API-Spezifikation werden aufgelistet. Sie können die unaufbereitete Spezifikation in einem Browser anzeigen, sie in der CLI direkt verarbeiten oder überprüfen, ob die Umgebungsvariable `OPENAPI_SPEC` korrekt festgelegt wurde.

```
bluemix sdk list --url
```
{: codeblock}

Verwenden Sie den folgenden Befehl, um die Open API-Definitionsdatei von `<AppName>` zu überprüfen und so festzustellen, ob sie zum Generieren eines SDK verwendet werden kann. Der Befehl sucht `<AppName>` in Ihrem aktuellen Bereich und verwendet den relativen Pfad in der Umgebungsvariablen `OPENAPI_SPEC` zum Suchen der Spezifikation für die Überprüfung.

```
bluemix sdk validate <AppName>
```
{: codeblock}

Verwenden Sie den folgenden Befehl, um ein SDK für die native Plattform (`<Platform>`) Ihrer Wahl zu generieren und um eine komprimierte Datei im aktuellen Arbeitsverzeichnis zu platzieren.

```
bluemix sdk generate <AppName> <SDKName> --<Platform>
```
{: codeblock}

Bei Verwendung der Option `--unzip` führt das System eine automatische Extraktion des SDK in Ihr aktuelles Arbeitsverzeichnis durch. Optional können Sie die Position zur Extraktion des SDK auch angeben, indem Sie die Option `--output` verwenden. Sie können den Quellcode mit GitHub verwalten und einen neuen Zweig speziell für die Aktualisierung des SDK erstellen. Mit diesem Ansatz wird die Anzeige der Änderungen und das Zusammenführen des aktualisierten SDK mit Ihrem Entwicklungszweig vereinfacht.


## Mit einem SDK generierte Modelle und APIs verwenden
{: #models-apis}

Nachdem das BFF mithilfe eines generierten SDK in Ihre mobile App integriert wurde, können Sie damit arbeiten.

Das SDK umfasst eine vollständig generierte Dokumentation, die sich im Verzeichnis `docs` und im Verzeichnis `source` befindet. Sie können die Datei `README.html` öffnen, um eine Webansicht der Dokumente anzuzeigen. Alternativ hierzu können Sie die Datei `README.md` öffnen, um eine Markdown-Ansicht der Dokumente anzuzeigen. Die Markdown-Dokumente sind nützlich, wenn Sie das SDK in Cocoapods oder Maven Central veröffentlichen wollen.

Die Dokumentation enthält eine Liste der APIs, die generiert werden. Sie können auf die API klicken, um ein Code-Snippet anzuzeigen, das direkt in Ihre mobile App eingefügt werden kann.
