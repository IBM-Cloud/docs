---

copyright:
  years: 2016,2017
lastupdated: "2017-04-027"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Einführung in Compose for RabbitMQ
{: #getting-started-with-compose-for-rabbitmq}

RabbitMQ verarbeitet asynchron die Nachrichten zwischen Ihren Anwendungen und Datenbanken und ermöglicht damit die Trennung der Daten und Anwendungsebenen. Mit RabbitMQ haben Entwickler die Möglichkeit, Nachrichten mit anpassbaren Persistenzstufen, Bereitstellungseinstellungen und bestätigter Veröffentlichung weiterzuleiten, zu verfolgen und in die Warteschlange zu stellen. Durch die Verwendung von {{site.data.keyword.composeForRabbitMQ_full}} erhalten Sie Zugriff auf die leicht zu bedienende Verwaltungsschnittstelle mit einer Vielzahl von Verwaltungsfunktionen, wie z. B. Bereitstellungsüberwachung, Skalierung mit einem Mausklick, Benutzereinrichtung und Zugriff auf Protokolldateien.
{:shortdesc}

**Hinweis:** Alle Compose-Serviceinstanzen, die vor dem 14. September 2016 bereitgestellt wurden und noch aktiv sind, können weiterhin verwendet werden und sind über [https://www.compose.com/](https://www.compose.com) zugänglich. Jede Compose-Serviceinstanz, die ab diesem Punkt bereitgestellt wird, ist direkt über Ihr Bluemix-Konto zugänglich und kann dort verwendet werden.

Führen Sie zum Einstieg in {{site.data.keyword.composeForRabbitMQ}} die folgenden Schritte aus.

1. [Erstellen Sie eine {{site.data.keyword.composeForRabbitMQ}}-Instanz](https://console.ng.bluemix.net/catalog/services/compose-for-rabbitmq/).

  Wenn Sie eine Instanz des Service erstellen, achten Sie darauf, sowohl einen Namen für den Service als auch einen Namen für den Berechtigungsnachweis auszuwählen. Lassen Sie den Service ungebunden; Sie können später eine Anwendung mit Ihrem Service verbinden, indem Sie die Berechtigungsnachweise verwenden, die bei der Bereitstellung des Service angegeben wurden.  Die verschiedenen Werte für die Berechtigungsnachweise sind im Abschnitt *Verfügbare Berechtigungsnachweise* aufgeführt.

2. Stellen Sie eine Verbindung zu Ihrem {{site.data.keyword.composeForRabbitMQ}}-Service her.

  Zur Herstellung einer Verbindung von einer App zu Ihrem Service verwenden Sie die [Berechtigungsnachweise](./credentials.html), die zusammen mit dem Service erstellt werden. Die Beispiel-App veranschaulicht die Verwendung von Node.js zur Verbindung mit einem {{site.data.keyword.composeForRabbitMQ}}-Service.

  Laden Sie die Beispiel-App [compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs) herunter und befolgen Sie die Anweisungen in der Readme-Datei. Anschließend klicken Sie auf der Detailseite für die Anwendung in Bluemix auf **App anzeigen**.
