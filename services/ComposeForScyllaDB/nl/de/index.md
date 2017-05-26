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

# Einführung in Compose for ScyllaDB
{: #getting-started-with-compose-for-scylladb}

ScyllaDB ist ursprünglich ein Ersatz für die verteilte Wide Column-Cassandra-Datenbank. ScyllaDB ist für eine bessere Ressourcennutzung, die zu einer zehnmal besseren Benchmarkleistung führen kann, in C++ geschrieben, nicht wie Cassandra in Java. ScyllaDB behält nicht nur die Kompatibilität mit Cassandra-Tools und Datendateien bei, sondern fügt auch Funktionen zur automatischen Leistungsoptimierung hinzu. Mithilfe von {{site.data.keyword.composeForScyllaDB_full}} werden die Funktionen von ScyllaDB dahingehend erweitert, dass die Verwaltung für Sie übernommen wird und Sie ein einfaches Bereitstellungssystem zur automatischen Skalierung für eine hohe Verfügbarkeit und Redundanz sowie automatisierte Backups angeboten bekommen.
{:shortdesc}

**Anmerkung:** {{site.data.keyword.composeForScyllaDB_full}} gewährt keinen Zugriff auf die Compose-Benutzerschnittstelle. Weitere Details finden Sie unter [Compose on Bluemix Support](https://help.compose.com/docs/bluemix-compose-support).

Führen Sie zum Einstieg in {{site.data.keyword.composeForScyllaDB}} die folgenden Schritte aus:

1. [Erstellen Sie eine {{site.data.keyword.composeForScyllaDB}}-Instanz](https://console.ng.bluemix.net/catalog/services/compose-for-scylladb/).

   Wenn Sie eine Instanz des Service erstellen, wählen Sie sowohl einen Namen für den Service als auch einen Namen für den Berechtigungsnachweis aus. Lassen Sie den Service ungebunden; Sie können später eine Anwendung mit Ihrem Service verbinden, indem Sie die Berechtigungsnachweise verwenden, die bei der Bereitstellung des Service angegeben wurden. Die verschiedenen Werte für die Berechtigungsnachweise sind im Abschnitt "Verfügbare Berechtigungsnachweise" aufgeführt.

2. Stellen Sie eine Verbindung zu Ihrem {{site.data.keyword.composeForScyllaDB}}-Service her.

   Zur Herstellung einer Verbindung von einer Anwendung zu Ihrem Service verwenden Sie die [Berechtigungsnachweise](./credentials.html), die zusammen mit dem Service erstellt werden. 

   Laden Sie die Beispielanwendung [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) herunter und befolgen Sie die Anweisungen in der Readme-Datei. Anschließend klicken Sie auf der Detailseite für die Anwendung der Bluemix-Konsole auf **App anzeigen**.

   Die Beispielanwendung veranschaulicht die Verwendung von Node.js zur Verbindung mit einem {{site.data.keyword.composeForScyllaDB}}-Service.
