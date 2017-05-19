---

copyright:
  years: 2016,2017
lastupdated: "2017-04-27"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Einführung in Compose for PostgreSQL
{: #getting-started-with-compose-for-postgreSQL}

{{site.data.keyword.composeForPostgreSQL}} bietet eine leistungsfähige objektbezogene Open-Source-Datenbank mit hoher Anpassbarkeit. Postgres ermöglicht die schnelle und leicht skalierbare Entwicklung. Die Entwicklung kann in einer Sprache erfolgen, mit der Sie vertraut sind, z. B. C/C++, Perl, Python, TCL/TK, Delphi/Kylix, VB, PHP, ASP oder Java. Sie erhalten eine mit vielen Funktionen ausgestattete Unternehmensdatenbank mit JSON-Unterstützung, mit der Sie das beste aus den zwei Welten SQL und NoSQL bekommen.
{:shortdesc}

**Hinweis:** Alle Compose-Serviceinstanzen, die vor dem 14. September 2016 bereitgestellt wurden und noch aktiv sind, können weiterhin verwendet werden und sind über [https://www.compose.com/](https://www.compose.com) zugänglich. Jede Compose-Serviceinstanz, die ab diesem Punkt bereitgestellt wird, ist direkt über Ihr Bluemix-Konto zugänglich und kann dort verwendet werden.

Führen Sie zum Einstieg in Compose for PostgreSQL die folgenden Schritte aus:

1. [Erstellen Sie eine {{site.data.keyword.composeForPostgreSQL}}-Instanz](https://console.ng.bluemix.net/catalog/services/compose-for-postgresql/).

  Wenn Sie eine Instanz des Service erstellen, achten Sie darauf, sowohl einen Namen für den Service als auch einen Namen für den Berechtigungsnachweis auszuwählen. Lassen Sie den Service ungebunden; Sie können später eine Anwendung mit Ihrem Service verbinden, indem Sie die Berechtigungsnachweise verwenden, die bei der Bereitstellung des Service angegeben wurden. Die verschiedenen Werte für die Berechtigungsnachweise sind im Abschnitt *Verfügbare Berechtigungsnachweise* aufgeführt.

2. Stellen Sie eine Verbindung zu Ihrem {{site.data.keyword.composeForPostgreSQL}}-Service her.

  Zur Herstellung einer Verbindung von einer App zu Ihrem Service verwenden Sie die [Berechtigungsnachweise](./credentials.html), die zusammen mit dem Service erstellt werden. Die Beispiel-App veranschaulicht die Verwendung von Node.js zur Verbindung mit einem {{site.data.keyword.composeForPostgreSQL}}-Service.

  Laden Sie die Beispiel-App [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs) herunter und befolgen Sie die Anweisungen in der Readme-Datei. Anschließend klicken Sie auf der Detailseite für die Anwendung in Bluemix auf **App anzeigen**, um den Inhalt der Tabelle *examples* anzuzeigen.
