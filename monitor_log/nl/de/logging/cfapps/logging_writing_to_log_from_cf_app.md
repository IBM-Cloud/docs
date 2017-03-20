---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Laufzeitanwendungsprotokollierung durch CF-Apps
{: #logging_writing_to_log_from_cf_app}

Wenn Sie in {{site.data.keyword.Bluemix}} Protokolldaten für eine Cloud Foundry-App und ihre Laufzeit speichern möchten, müssen Sie Ihre Protokolle in die Standardausgabe (STDOUT) und Standard-Fehlerausgabe (STDERR) schreiben.
{:shortdesc}

In {{site.data.keyword.Bluemix}} werden STDOUT- und STDERR-Protokolleinträge automatisch erfasst:

* STDOUT (Standardausgabe) stellt allgemeine Informationen bereit.  
* STDERR (Standard-Fehlerausgabe) stellt Informationen bereit, die Fehlernachrichten und andere Warnungen zur Diagnose enthalten. 

Loggregator ruft Daten in der Standardausgabe und Standard-Fehlerausgabe automatisch ab. Loggregator ist die Komponente, die Protokolle aus Cloud Foundry heraus weiterleitet. 

Beispiel: 

Für eine **Liberty Cloud Foundry-App** wird das Standardkonsolenprotokoll (console.log) für den Liberty-Server automatisch von Loggregator erfasst. 

* Das Konsolenprotokoll enthält die umgeleiteten STDOUT- und STDERR-Daten aus dem JVM-Prozess. Die Konsolenausgabe enthält wichtigere Ereignisse und Fehler, wenn Sie die Standardkonfiguration "consoleLogLevel" verwenden. Die Konsolenausgabe enthält außerdem alle Nachrichten, die an die Datenströme "system.out" und "system.err" geschrieben werden, wenn Sie die Standardkonfiguration "copySystemStreams" verwenden. Die Konsolenausgabe enthält immer Nachrichten, die direkt vom JVM-Prozess geschrieben werden, wie zum Beispiel Ausgaben mit der Option "-verbose:gc". Sie können die Protokollstufe von Liberty über die Datei "server.xml" anpassen.
* Die Konfiguration "consoleLogLevel" legt die Filterebene des Konsolenprotokollhandlers fest. Wenn Sie "consoleLogLevel" auf den Wert INFO setzen, konfigurieren Sie dadurch, dass alle Nachrichten der Protokollstufen INFO, AUDIT, WARNING und ERROR in die Datei "console.log" geschrieben werden. **Hinweis:** Protokolleinträge der Stufen FINE, FINER, FINEST werden nur in die Datei "trace.log" geschrieben.

Weitere Informationen zu Liberty for Java™-Anwendungen finden Sie unter [Liberty Profile: Logging and Trace ](http://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html).

Für eine **Node.js-Cloud Foundry-App** können Sie das Protokollierungsmodul "Built in Console" zur Konfiguration der Protokollierung für die Laufzeit in {{site.data.keyword.Bluemix}} verwenden. Sie können Nachrichten an die Standardausgabe (STDOUT) und die Standard-Fehlerausgabe (STDERR) leiten:

* console.log('message') sendet die Nachricht an den STDOUT-Datenstrom.
* console.error('error_message') sendet die Fehlernachricht an den STDERR-Datenstrom.

Weitere Informationen zu Node.js-Anwendungen finden Sie unter [How to log in node.js ](http://docs.nodejitsu.com/articles/intermediate/how-to-log).


Weitere Informationen zu **Ruby on Rails-Anwendungen** finden Sie unter [The Logger](http://guides.rubyonrails.org/debugging_rails_applications.html#the-logger).

In der folgenden Tabelle wird die Zuordnung zwischen den Protokollen einiger Anwendungslaufzeiten und den Protokollen, die automatisch von Loggregator erfasst werden, dargestellt:

| **Lautzeit** |    **STDOUT**     | **STDERR** |
|-----------------|-------------------|-------------------|
| Liberty | system.out | system.err |
| Node.js | console.log, console.info | console.error, console.warn |
| Ruby | stdout| stderr |
{: caption="Table 1. Mapping between some application runtimes logs and the logs that are picked automatically by Loggregator" caption-side="top"}

