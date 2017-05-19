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

# Einführung in Compose for etcd
{: #getting-started-with-compose-for-etcd}

"etcd" ist ein Schlüssel/Wert-Speicher mit den immer korrekten Daten, die Sie zum Koordinieren und Verwalten Ihres Server-Clusters für die Konfigurationsverwaltung für verteilte Server benötigen. "etcd" verwendet den RAFT-Datenkonsistenzalgorithmus zur Sicherstellung der Konsistenz in Ihrem Cluster. Er erzwingt die Reihenfolge der Operationen an den Daten, sodass jeder Knoten im Cluster auf demselben Weg zum selben Ergebnis kommt. {{site.data.keyword.composeForEtcd_full}} fügt automatische Sicherungen Ihrer Konfigurationsdaten durch, die in "etcd" gespeichert sind. Über eine intuitive Verwaltungsschnittstelle können Sie Ihre Bereitstellung mit Leichtigkeit überwachen, skalieren und verwalten.
{:shortdesc}

**Hinweis:** Alle Compose-Serviceinstanzen, die vor dem 14. September 2016 bereitgestellt wurden und noch aktiv sind, können weiterhin verwendet werden und sind über [https://www.compose.com/](https://www.compose.com) zugänglich. Jede Compose-Serviceinstanz, die ab diesem Punkt bereitgestellt wird, ist direkt über Ihr Bluemix-Konto zugänglich und kann dort verwendet werden.

Führen Sie zum Einstieg in {{site.data.keyword.composeForEtcd}} die folgenden Schritte aus.

1. [Erstellen Sie eine {{site.data.keyword.composeForEtcd}}-Instanz](https://console.ng.bluemix.net/catalog/services/compose-for-etcd/).

  Wenn Sie eine Instanz des Service erstellen, achten Sie darauf, sowohl einen Namen für den Service als auch einen Namen für den Berechtigungsnachweis auszuwählen. Lassen Sie den Service ungebunden; Sie können später eine Anwendung mit Ihrem Service verbinden, indem Sie die Berechtigungsnachweise verwenden, die bei der Bereitstellung des Service angegeben wurden. Die verschiedenen Werte für die Berechtigungsnachweise sind im Abschnitt *Verfügbare Berechtigungsnachweise* aufgeführt.

2. Stellen Sie eine Verbindung zu Ihrem {{site.data.keyword.composeForEtcd}}-Service her.

Zur Herstellung einer Verbindung von einer App zu Ihrem Service verwenden Sie die [Berechtigungsnachweise](./credentials.html), die zusammen mit dem Service erstellt werden. Die Beispiel-App veranschaulicht die Verwendung von Node.js zur Verbindung mit einem {{site.data.keyword.composeForEtcd}}-Service.

Laden Sie die Beispiel-App [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) herunter und befolgen Sie die Anweisungen in der Readme-Datei. Anschließend klicken Sie auf der Detailseite für die Anwendung in Bluemix auf **App anzeigen**, um den Inhalt von *examples* anzuzeigen.
