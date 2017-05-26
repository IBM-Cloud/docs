---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Informationen zu Continuous Delivery  
{: #cd_about}  

Mit {{site.data.keyword.contdelivery_full}} können Anwendungen unter Verwendung bewährter DevOps-Verfahren und branchenführender Tools erstellt, getestet und bereitgestellt werden.
{:shortdesc}

Der {{site.data.keyword.contdelivery_short}}-Service unterstützt Ihre DevOps-Workflows:

 * Sie können integrierte offene DevOps-[Toolchains](/docs/services/ContinuousDelivery/toolchains_about.html){: new_window} erstellen, um Toolintegrationen zu aktivieren, die Ihre Entwicklungs-, Bereitstellungs- und Betriebstasks unterstützen.

  Eine Toolchain ist eine integrierte Gruppe von Tools für das gemeinsame Entwickeln, Erstellen, Bereitstellen, Testen und Verwalten von Anwendungen. Sie können Toolchains erstellen, die {{site.data.keyword.Bluemix_notm}}-Services, Open-Source-Tools und Tools von anderen Anbietern wie GitHub, PagerDuty und Slack enthalten, die Entwicklungsarbeiten und Operationen reproduzierbar machen und die Verwaltung vereinfachen.

 * Die Verwendung automatisierter [Pipelines](/docs/services/ContinuousDelivery/pipeline_about.html){: new_window} ermöglicht die fortlaufende Bereitstellung.

  Sie können beispielsweise Builds, Komponententests und Bereitstellungen automatisieren. Builds, Tests und Bereitstellungen sind reproduzierbar und erfordern nur geringe manuelle Eingriffen. Seien Sie jederzeit bereit für eine Produktionsfreigabe.

 * Mithilfe der [webbasierten IDE](/docs/services/ContinuousDelivery/web_ide.html){: new_window} kann Code überall bearbeitet und mit Push-Operation übertragen werden.

  In GitHub können Quellcodeverwaltungstasks erstellt, bearbeitet, ausgeführt und korrigiert werden. Sie können nahtlos von der Codebearbeitung zur Bereitstellung in der Produktion übergehen.

 * Qualitätsverbesserungen durch [{{site.data.keyword.DRA_short}}](/docs/services/ContinuousDelivery/di_working.html){: new_window}.

  Erhalten Sie während der Entwicklung und Bereitstellung von Code Einblick in die Dynamik Ihres Teams. Erfahren Sie, wie die Benutzer mit Ihrer Anwendung interagieren. Das Überprüfen von Daten unterstützt Sie bei der Verwaltung der Operationen Ihrer Anwendung.


## Die Toolchain-Verfügbarkeit auf Bluemix Public im Vergleich zu Bluemix Dedicated
{: #public_and_dedicated}

{{site.data.keyword.Bluemix_notm}} Public ist eine cloudbasierte Plattform mit offenen Standards, mit der Sie Anwendungen, auf die über [http://bluemix.net ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://bluemix.net){:new_window} zugegriffen wird, erstellen, ausführen und verwalten können. {{site.data.keyword.Bluemix_notm}} Dedicated stellt die Funktionalität von {{site.data.keyword.Bluemix_notm}} in einer dedizierten SoftLayer-Umgebung bereit, die sowohl mit der {{site.data.keyword.Bluemix_notm}} Public-Umgebung als auch mit Ihrem Netz sicher verbunden ist. Die {{site.data.keyword.Bluemix_notm}} Dedicated-Umgebung Ihres Unternehmens enthält möglicherweise nicht dieselben Toolintegrationen wie die {{site.data.keyword.Bluemix_notm}} Public-Site.

Für die Verwaltung von Quellcode und die Verfolgung von Problemen verwendet {{site.data.keyword.Bluemix_notm}} Public generell github.com. {{site.data.keyword.Bluemix_notm}} Dedicated ist zwar auch in der Lage, github.com zu nutzen, verwendet aber generell {{site.data.keyword.ghe_short}}, das entweder von Ihrem Unternehmen installiert oder von IBM verwaltet wird.

{{site.data.keyword.contdelivery_short}} ist in {{site.data.keyword.Bluemix_notm}} Public und in {{site.data.keyword.Bluemix_notm}} Dedicated verfügbar. Die einzelnen Toolchains unterscheiden sich je nachdem, ob Sie {{site.data.keyword.contdelivery_short}} auf {{site.data.keyword.Bluemix_notm}} Public oder auf {{site.data.keyword.Bluemix_notm}} Dedicated verwenden.

**Tipp**: Toolchains werden in den Südstaaten der USA gehostet. Wenn Ihre Toolchain für die Bereitstellung von Apps in
anderen Regionen konfiguriert ist, wird sie auch weiterhin Apps in diesen Regionen bereitstellen. 

|Toolchains |{{site.data.keyword.Bluemix_notm}} Public	|{{site.data.keyword.Bluemix_notm}} Dedicated |
|:----------|:------------------------------|:------------------|
|Toolintegrationen 		|Eine Liste der unterstützten Toolintegrationen enthält [Toolintegrationen konfigurieren](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}. 		|Welche Toolintegrationen verfügbar sind, richtet sich danach, wie {{site.data.keyword.contdelivery_short}} in Ihrer Umgebung eingerichtet wurde.			|
|Toolchain aus einer Vorlage erstellen		|Melden Sie sich bei [{{site.data.keyword.Bluemix_notm}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://console.ng.bluemix.net/devops){:new_window} an.		|Melden Sie sich bei Ihrer dedizierten Umgebung (Dedicated) auf {{site.data.keyword.Bluemix_notm}} an.			|
|Toolchain aus einer App erstellen		|Die App wird für die kontinuierliche Bereitstellung aus einem neuen GitHub-Repository konfiguriert, das den Startcode für die App enthält.		|Die App wird für die kontinuierliche Bereitstellung aus einem neuen GitHub oder GitHub Enterprise-Repository konfiguriert, das den Startcode für die App enthält.		|  
|Delivery Pipeline-Bereitstellungsregionen		|Alle {{site.data.keyword.Bluemix_notm}} Public-Regionen stehen Cloud Foundry-Bereitstellungsjobs zur Verfügung. 		|Die {{site.data.keyword.Bluemix_notm}} Dedicated-Region ist verfügbar. Gegebenenfalls sind weitere dedizierte oder lokale Regionen innerhalb desselben Kundenkontos verfügbar, je nachdem, wie {{site.data.keyword.contdelivery_short}} für Ihre spezielle Umgebung eingerichtet wurde.		|
|Delivery Pipeline-Bereitstellungsjobs		|Es sind alle [Jobtypen](/docs/services/ContinuousDelivery/pipeline_about.html#deliverypipeline_jobs) verfügbar.		|Jobtypen, die von {{site.data.keyword.Bluemix_notm}}-Services abhängen, die nicht in der dedizierten Umgebung installiert sind, stehen möglicherweise nicht zur Verfügung.	Die Jobtypen zum Ausführen eines Containerbuilds und zum Bereitstellen stehen in Umgebungen, die nicht über den {{site.data.keyword.Bluemix_notm}} Container-Service verfügen, gegebenenfalls nicht zur Verfügung.	|
{: caption="Tabelle 1. Unterschiede zwischen Toolchains unter Bluemix Dedicated und Bluemix Public" caption-side="top"}


## Vorlagen für Toolchains
{: #templates}

Als Ausgangspunkt zum [Erstellen einer Toolchain ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/devops/create){: new_window} können Sie eine Vorlage verwenden. Toolchain-Vorlagen umfassen bestimmte Gruppen von Toolintegrationen, die Entwicklungs-, Bereitstellungs- und Systemtasks unterstützen.

**Tipp**: Die {{site.data.keyword.Bluemix_notm}} Dedicated-Umgebung Ihres Unternehmens enthält möglicherweise nicht dieselben Toolchain-Vorlagen wie die {{site.data.keyword.Bluemix_notm}} Public-Site. Toolchain-Vorlagen, die sowohl auf {{site.data.keyword.Bluemix_notm}} Public als auch auf {{site.data.keyword.Bluemix_notm}} Dedicated verfügbar sind, enthalten möglicherweise jeweils verschiedene Gruppen von Toolintegrationen auf {{site.data.keyword.Bluemix_notm}} Dedicated.

Manche Toolchain-Vorlagen beinhalten Toolintegrationen, die Teil des {{site.data.keyword.contdelivery_short}}-Service sind. Falls Ihre Organisation nicht bereits eine Instanz dieses Service enthält, können Sie den Service durch Klicken auf **Erstellen** automatisch und kostenlos hinzufügen lassen. Weitere Informationen und die Bedingungen enthält der [Bluemix-Katalog ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/catalog/services/continuous-delivery/){:new_window}.

Die Toolchain-Vorlagen für Microservices stellen eine App mit Katalog- und Auftrags-APIs bereit, die von einem Cloudant-Geschäft gestützt werden. Im Rahmen der Bereitstellung der App wird eine kostenlose Instanz des Cloudant-Service erstellt. Weitere Informationen und die Bedingungen enthält der [Bluemix-Katalog ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/catalog/services/cloudant-nosql-db/){:new_window}.

|Vorlage |Beschreibung	|
|:----------|:------------------------------|
|[Cloudnative Garage Method-Toolchain - Lernprogramm![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fcloud-native-toolchain-tutorial){:new_window} 		|Diese Toolchain veranschaulicht die DevOps-Verfahren, die Garage Method bietet. Die Toolchain ist für Continuous Delivery, Quellcodeverwaltung, Testautomatisierung, automatisierte Überwachung und automatisierten Betrieb vorkonfiguriert. Sie wird mit einer Beispielapp bereitgestellt, die in Node.js Express 4 geschrieben ist und von Ihnen weiter erweitert werden kann. 		|
|[Microservice-Toolchain mit {{site.data.keyword.DRA_short}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Ftoolchain-demo){:new_window} 		|Mit dieser cloudnativen Toolchain können Sie ein Beispiel verwenden, um ein Onlinegeschäft zu erstellen, das aus drei Microservices besteht: einer Katalog-API, einer Auftrags-API und einer Benutzerschnittstelle, die beide API aufruft. Die Toolchain ist für Continuous Delivery, Quellcodeverwaltung, Funktionstests, Problemverfolgung, Onlinebearbeitung und Alertbenachrichtigung vorkonfiguriert. 		|
|[Microservice-Toolchain mit {{site.data.keyword.DRA_short}} (Version 2) ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fmicroservices-toolchain-hosted){:new_window} 		|Mit dieser cloudnativen Toolchain können Sie ein Beispiel verwenden, um ein Onlinegeschäft zu erstellen, das aus drei Microservices besteht: einer Katalog-API, einer Auftrags-API und einer Benutzerschnittstelle, die beide API aufruft. Die Toolchain ist für Continuous Delivery, Quellcodeverwaltung, Funktionstests, Problemverfolgung, Onlinebearbeitung und Alertbenachrichtigung vorkonfiguriert. 		|
|[Sichere Container-Toolchain ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsecure-container-toolchain){:new_window} 		|Mit dieser Toolchain können Sie eine sichere Docker-Container-App entwickeln und bereitstellen. Standardmäßig verwendet die Toolchain eine Node.js-Beispielapp vom Typ 'Hello World'. Sie können aber auch eine Verknüpfung zu Ihrem eigenen GitHub-Repository herstellen. Die Toolchain ist für Continuous Delivery mit Vulnerability Advisor (Advisorfunktion gegen Sicherheitslücken), Quellcodeverwaltung, Problemverfolgung und Onlinebearbeitung vorkonfiguriert. 		|
|[Einfache Cloud Foundry-Toolchain ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain){:new_window}		|Mit dieser Toolchain können Sie eine Cloud Foundry-App entwickeln und bereitstellen. Standardmäßig verwendet diese Toolchain eine Node.js-Beispielapp vom Typ 'Hello World'. Sie können aber auch eine Verknüpfung zu Ihrem eigenen GitHub-Repository herstellen. Die Toolchain ist für Continuous Delivery, Quellcodeverwaltung, Problemverfolgung und Onlinebearbeitung vorkonfiguriert. 		|
|[Einfache Cloud Foundry-Toolchain	(Version 2) ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain-hosted){:new_window}	|Mit dieser Toolchain können Sie eine Cloud Foundry-App entwickeln und bereitstellen. Standardmäßig klont diese Toolchain eine Node.js-Beispielapp vom Typ 'Hello World' in einem von IBM gehosteten Git-Repository, an dem Sie dann Änderungen vornehmen können. Die Toolchain ist für Continuous Delivery, Quellcodeverwaltung, Problemverfolgung und Onlinebearbeitung vorkonfiguriert. 		|
|[Einfache Cloud Foundry-Toolchain mit {{site.data.keyword.DRA_short}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdra-toolchain-demo){:new_window}		|Mit dieser cloudnativen Toolchain können Sie {{site.data.keyword.DRA_short}} für die Bereitstellung einer einfachen Cloud Foundry-App über ein Gateway nutzen. Standardmäßig verwendet die Toolchain die Node.js-Beispiel-App für Wetter. Sie können aber auch eine Verknüpfung zu Ihrem eigenen GitHub-Repository herstellen. 		|
|[Einfache Container-Toolchain ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-container-toolchain){:new_window}		|Mit dieser Toolchain können Sie eine Docker-Container-App entwickeln und bereitstellen. Standardmäßig verwendet die Toolchain eine Node.js-Beispielapp vom Typ 'Hello World'. Sie können aber auch eine Verknüpfung zu Ihrem eigenen GitHub-Repository herstellen. Die Toolchain ist für Continuous Delivery, Quellcodeverwaltung, Problemverfolgung und Onlinebearbeitung vorkonfiguriert. 		|
|[Delivery Insights mit IBM UrbanCode Deploy ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdeliveryinsights-toolchain){:new_window}		|Mit dieser Toolchain können Sie die Bereitstellungsmetriken von IBM UrbanCode Deploy anzeigen. Aktivieren Sie diese Toolchain für die Kommunikation mit IBM UrbanCode Deploy. Laden Sie dazu DevOps Connect in {{site.data.keyword.DRA_short}} von der Seite für Einstellungen herunter und konfigurieren Sie DevOps Connect. 		|
|[Deployment Risk Analytics mit GitHub und Jenkins ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevopsinsights-toolchain){:new_window}		|Mit dieser Toolchain können Sie sich Einblicke in Ihren Jenkins-Prozess für kontinuierliche Integration und Lieferung verschaffen. Sie können den Jenkins-Server so konfigurieren, dass er Daten an {{site.data.keyword.DRA_short}} sendet, wenn die Jobs von Jenkins ausgeführt werden. Sie können auch Qualitätsgateways implementieren, um Bereitstellungen richtlinienbasiert zu blockieren. Ergebnis können Sie im Deployment Risk-Dashboard in {{site.data.keyword.DRA_short}} anzeigen. Wenn Sie ein GitHub-Repository konfigurieren, um das Quellenrepository anzugeben, das Jenkins verwendet, so steht die Verfolgbarkeit von Änderungen zur Verfügung.  		|
|[Developer Insights und Team Dynamics mit GitHub und JIRA ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevteaminsights-toolchain){:new_window}		|Mit dieser Toolchain können Sie das Entwicklungsrisiko für Ihr Projekt untersuchen und die Analyse für Social Coding nutzen, um Interaktionsmuster zwischen den Entwicklern zu verstehen. Sie können GitHub-Quellcode in Verbindung mit GitHub-Problemen, JIRA-Problemen oder beidem analysieren. Verwenden Sie Developer Insights, um diejenigen Dateien ausfindig zu machen, die hochgradig fehlerträchtig sind, und erfahren Sie, inwieweit das Projekt mit DevOps-Verfahren konform ist. Die Analyse für Social Coding in Team Dynamics ermittelt den Grad der Interaktion zwischen Teammitgliedern, sodass das Team bei unproduktiven Verfahren entsprechend korrigierend eingreifen kann. 		|
|[Eigene Toolchain erstellen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fempty-toolchain){:new_window}		|Für diese Toolchain sind keine Tools vorkonfiguriert. Wenn Sie bereits mit Toolchains vertraut sind, können Sie Ihre eigene Toolchain einrichten. 		|
{: caption="Tabelle 2. Toolchain-Vorlagen" caption-side="top"}
