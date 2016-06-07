---

copyright:
  years: 2015, 2016

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}


# Fehlerbehebung
{: #debugging}

*Letzte Aktualisierung: 3. März 2016*

Wenn Probleme mit {{site.data.keyword.Bluemix}} auftreten, können Sie die Protokolldateien anzeigen, um die Probleme zu untersuchen und die Fehler zu beheben. 
{:shortdesc}

In Protokollen sind z. B. Informationen darüber enthalten, ob
ein Job erfolgreich ausgeführt wird oder ob er fehlschlägt. Sie enthalten auch
relevante Informationen, die für Debugzwecke und zum Feststellen der Ursache eines Problems
verwendet werden können.

Protokolle haben ein festes Format. Bei ausführlichen Protokollen ist eine Filterung möglich; Sie können auch externe Protokollierungshosts zum Speichern und Verarbeiten der Protokolle verwenden. Weitere Informationen zu Protokollformaten, zum Anzeigen und Filtern von Protokollen sowie zur Konfiguration einer externen Protokollierung finden Sie im Abschnitt zur [Protokollierung für Apps, die in Cloud Foundry ausgeführt werden](../monitor_log/monitoringandlogging.html#logging_for_bluemix_apps){: new_window}.


## Staging-Fehler beheben
{: #debugging-staging-errors}
Beim Durchführen des Stagings für die Anwendungen unter Verwendung von {{site.data.keyword.Bluemix_notm}} können Fehler auftreten. Wenn die Durchführung des Stagings für eine App fehlschlägt, können Sie die Protokolle prüfen, um die Ursache des Fehlers zu ermitteln und das Problem zu beheben.

Um zu verstehen, warum in einer App unter {{site.data.keyword.Bluemix_notm}} ein Fehler auftritt, müssen Sie wissen, wie eine App unter {{site.data.keyword.Bluemix_notm}} bereitgestellt und ausgeführt wird. Detaillierte Informationen hierzu finden Sie in [Bereitstellung von Anwendung](../manageapps/depapps.html#appdeploy){: new_window}.

Anhand der folgenden Prozedur wird veranschaulicht, wie Sie mit dem Befehl `cf logs` Staging-Fehler beheben können. Stellen Sie vor der Ausführung der folgenden Schritte sicher, dass Sie die cf-Befehlszeilenschnittstelle installiert haben. Weitere Informationen zum Installieren der cf-Befehlszeilenschnittstelle finden Sie unter [cf-Befehlszeilenschnittstelle installieren](../starters/install_cli.html){: new_window}.

  1. Stellen Sie durch Eingeben des folgenden Codes in der cf-Befehlszeilenschnittstelle eine Verbindung zu {{site.data.keyword.Bluemix_notm}} her:
     ```
	 cf api https://api.ng.bluemix.net
	 ```
	 
  2. Melden Sie sich durch Eingeben von `cf login` an {{site.data.keyword.Bluemix_notm}} an.
  
  3. Rufen Sie die neusten Protokolle durch Eingeben von `cf logs anwendungsname --recent` ab. Wenn Sie ein ausführliches Protokoll filtern möchten, verwenden Sie die Option `grep`. Sie können zum Beispiel den folgenden Code eingeben, um nur Protokolle des Typs [STG] anzuzeigen:
    ```
	cf logs anwendungsname --recent | grep '\[STG\]'
	```
  4. Zeigen Sie den ersten Fehler an, der im Protokoll aufgeführt wird.
  
Wenn Sie das IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}-Plug-In zum Implementieren von Anwendungen verwenden, werden in der Registerkarte **Konsole** des Eclipse-Tools Protokolle angezeigt, die der Ausgabe des Befehls 'cf logs' ähneln. Sie können auch ein separates Eclipse-Fenster zum Verfolgen der `Protokolle` öffnen, wenn Sie die Anwendung bereitstellen.

Zusätzlich zum Befehl `cf logs` in {{site.data.keyword.Bluemix_notm}} können Sie auch den Service 'Monitoring and Analytics' zum Erfassen der Protokolldetails verwenden. Vom Service 'Monitoring and Analytics' werden zusätzlich auch Leistung, Status und Verfügbarkeit der Anwendungen überwacht. Außerdem werden von ihm Protokollanalysedaten für Node.js- und Liberty-Laufzeitanwendungen bereitgestellt.  

### Staging-Fehler für eine Node.js-Anwendung beheben

Im folgenden Beispiel wird ein Protokoll dargestellt, das nach dem Eingeben des Befehls `cf logs anwendungsname --recent` angezeigt wird. In dem Beispiel wird davon ausgegangen, dass für eine Node.js-Anwendung Staging-Fehler aufgetreten sind:
```
2014-08-11T14:19:36.17+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({name"=>"SampleExpressApp"}
2014-08-11T14:20:44.17+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({"state"=>"STOPPED"})
2014-08-11T14:20:44.19+0100 [App/0]   ERR
2014-08-11T14:20:44.43+0100 [DEA]     OUT Stopping app instance (index 0) with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:44.44+0100 [DEA]     OUT Stopped app instance (index 0) with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:48.97+0100 [DEA]     OUT Got staging request for app with id 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:50.94+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({"state"=>"STARTED"})
2014-08-11T14:20:51.66+0100 [STG]     OUT -----> Download app package (4.1M)
2014-08-11T14:20:51.90+0100 [STG]     OUT -----> Download app buildpack cache (1.1M)
2014-08-11T14:20:52.78+0100 [STG]     OUT -----> Buildpack Version: v1.1-20140717-1447
2014-08-11T14:20:52.78+0100 [STG]     ERR parse error: Expected another key-value pair at line 18, column 3
2014-08-11T14:20:52.79+0100 [STG]     OUT 0 info it worked if it ends with ok
```
{: screen}


Aus dem ersten Fehler im Protokoll geht hervor, warum das Staging fehlgeschlagen ist. Im Beispiel wird der erste Fehler durch eine Ausgabe der Komponente 'Droplet Execution Agent' (DEA) während der Staging-Phase verursacht.
```
2014-08-11T14:20:52.78+0100 [STG]   ERR parse error: expected another key-value pair at line 18, column 3
```
{: screen}


Bei einer Node.js-Anwendung werden die Informationen in der Datei `package.json` von der Komponente DEA zum Herunterladen der Module verwendet. Aus diesem Fehler lässt sich erkennen, dass der Fehler für das Modul aufgetreten ist. Somit ist es sinnvoll, die 18. Zeile der Datei `package.json` zu überprüfen. 

```
15   "jade": "~1.3.0",
16   "mongodb": "*",
17   "monk":"*",
18   }
```
{: screen}


Da Zeile 17 mit einem Komma endet, wird in Zeile 18 ein Schlüssel/Wert-Paar erwartet. Entfernen Sie zum Beheben des Problems das Komma:

```
15   "jade": "~1.3.0",
16   "mongodb": "*",
17   "monk":"*"
18   }
```
{: screen}


## Laufzeitfehler beheben
{: #debugging-runtime-errors}
Wenn während der Laufzeit der Anwendung Probleme auftreten, können Anwendungsprotokolle bei der Ermittlung der Fehlerursache und Behebung des Problems hilfreich sein. 

Insbesondere die Protokollierung der Standardausgabe (stdout) und Standardfehler (stderr) kann aktiviert sein. Weitere Informationen zum Konfigurieren der Protokolldateien für Anwendungen, die mit den integrierten {{site.data.keyword.Bluemix_notm}}-Buildpacks bereitgestellt wurden, finden Sie in der folgenden Liste:

  * Informationen zu Liberty for Java™-Anwendungen finden Sie unter [Liberty Profile: Logging and Trace](http://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html){: new_window}.
  * Informationen zu Node.js-Anwendungen finden Sie unter [How to log in node.js](http://docs.nodejitsu.com/articles/intermediate/how-to-log){: new_window}. 
  * Informationen zu PHP-Anwendungen finden Sie unter [error_log](http://php.net/manual/en/function.error-log.php){: new_window}.
  * Informationen zu Python-Anwendungen finden Sie unter [Logging HOWTO](https://docs.python.org/2/howto/logging.html){: new_window}.
  * Informationen zu Ruby on Rails-Anwendungen finden Sie unter [The Logger](http://guides.rubyonrails.org/debugging_rails_applications.html#the-logger){: new_window}.
  * Informationen zu Ruby Sinatra-Anwendungen finden Sie unter [Logging](http://www.sinatrarb.com/intro.html#Logging){: new_window}.
  
Wenn Sie `cf logs anwendungsname --recent` in die cf-Befehlszeilenschnittstelle eingeben, werden nur die neuesten Protokoll angezeigt. Wenn Sie Protokolle für Fehler anzeigen möchten, die früher aufgetreten sind, müssen Sie alle Protokolle abrufen und in ihnen nach den Fehlern suchen. Verwenden Sie zum Abrufen aller Protokolle für Ihre Anwendung eine der folgenden Methoden:
<dl> 
<dt><strong>Service {{site.data.keyword.Bluemix_notm}} Monitoring and Analytics</strong></dt> 
<dd>Die Funktionen für die integrierte Protokolldateisuche und -analyse des Service 'Monitoring and Analytics' können Ihnen dabei helfen, Fehler schnell zu finden. Weitere Informationen finden Sie unter <a href="../services/monana/index.html#gettingstartedtemplate" target="_blank">Monitoring and Analytics</a>.</dd> 
<dt><strong>Tools von Drittanbietern</strong></dt> 
<dd>Sie können die Protokolle aus Ihrer Anwendung erfassen und in einen externen Protokollhost exportieren. Weitere Informationen finden Sie unter <a href="../monitor_log/monitoringandlogging.html#thirdparty_logging" target="_blank">Externe Protokollierung konfigurieren</a>.</dd> 
<dt><strong>Scripts zum Erfassen und Exportieren der Protokolle</strong></dt> 
<dd>Wenn Sie ein Script verwenden möchten, um die Protokolle automatisch zu erfassen und in eine externe Datei zu exportieren, müssen Sie von Ihrem Computer eine Verbindung zum {{site.data.keyword.Bluemix_notm}}-Server herstellen und auf Ihrem Computer muss ausreichend Speicherplatz zum Herunterladen der Protokolle vorhanden sein. Weitere Informationen hierzu finden Sie unter <a href="../support/index.html#collecting-diagnostic-information" target="_blank">Diagnoseinformationen erfassen</a>. </dd>
</dl>

Auf die Dateien `stdout.log` und `stderr.log` konnte früher standardmäßig über die Anwendungsansicht im {{site.data.keyword.Bluemix_notm}}-Dashboard unter **Dateien** > **Protokolle** zugegriffen werden. Diese Anwendungsprotokollierung ist jedoch mit der aktuellen Version von Cloud Foundry nicht mehr verfügbar, von der {{site.data.keyword.Bluemix_notm}} per Hosting bereitgestellt wird. Wenn Sie weiterhin im {{site.data.keyword.Bluemix_notm}}-Dashboard über **Dateien** > **Protokolle** auf die Anwendungsprotokollierung mithilfe von 'stdout' und 'stderr' zugreifen möchten, können Sie die Protokollierung abhängig von der jeweils verwendeten Laufzeit in andere Dateien im {{site.data.keyword.Bluemix_notm}}-Dateisystem umleiten. 

  * Bei Liberty for Java-Anwendungen ist die an 'stdout' und 'stderr' übertragene Ausgabe bereits in der Datei `messages.log` im Protokollverzeichnis enthalten. Suchen Sie nach Einträgen mit dem Präfix 'SystemOut' bzw. 'SystemErr'.
  * Bei Node.js-Anwendungen können Sie die Funktion 'console.log' überschreiben, um explizit in eine Datei im Protokollverzeichnis zu schreiben.
  * Bei PHP-Anwendungen können Sie die Funktion 'error_log' verwenden, um in eine Datei im Protokollverzeichnis zu schreiben.
  * Bei Python-Anwendungen können Sie konfigurieren, dass von der Protokollfunktion in eine Datei im Protokollverzeichnis geschrieben wird: logging.basicConfig(filename='../../logs/example.log',level=logging.DEBUG)
  * Bei Ruby-Anwendungen können Sie konfigurieren, dass von der Protokollfunktion in eine Datei im Protokollverzeichnis geschrieben wird.
 

# Zugehörige Links
{: #rellinks}

## Allgemein
{: #general}

  * [Droplet Execution Agent (DEA)](http://docs.cloudfoundry.org/concepts/architecture/execution-agent.html){: new_window}
  * [Erste Schritte mit dem IBM Bluemix-Service 'Monitoring and Analytics'](../services/monana/index.html#gettingstartedtemplate){: new_window}
  * [Arbeitsweise von Bluemix](../public/index.html#howwork){: new_window}
  * [cf-Befehlstool installieren](../starters/install_cli.html){: new_window}
  * [Protokolle anzeigen](../monitor_log/monitoringandlogging.html#viewing_logs){: new_window}
  
  
 














