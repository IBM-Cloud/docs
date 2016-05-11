---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Dynatrace verwenden
{: #using_dynatrace}

*Letzte Aktualisierung: 08. April 2016*

Bei Dynatrace handelt es sich um einen Service eines anderen Anbieters, der Überwachungsmetriken für Ihre App bereitstellt.

Weitere Informationen zu Bereitstellungen des Service Dynatrace finden Sie in [Dynatrace Application Monitoring](http://www.dynatrace.com/en/products/application-monitoring.html).

Wenn Sie den Service Dynatrace für die Verwendung mit Ihrer Liberty-App aktivieren, müssen Sie folgende Verarbeitungsschritte ausführen:

1. Fordern Sie die JAR-Datei des Dynatrace-Agenten an und hosten Sie sie, damit das Liberty-Buildpack sie herunterladen kann.
2. Konfigurieren Sie eine Instanz des Dynatrace-Servers, damit der Dynatrace-Agent, der mit Ihrer Liberty-App ausgeführt wird, mit ihr kommunizieren kann.
3. Konfigurieren Sie Ihre Liberty-App, damit sie den Dynatrace-Agenten herunterladen und eine Verbindung zum Dynatrace-Server herstellen kann.

## Dynatrace-Agent hosten
{: #hosting_dynatrace_agent}
Der Dynatrace-Agent muss als Host einen Web-Server haben und das Liberty-Buildpack muss die JAR-Datei des Agenten von diesem Server herunterladen können. Der Server muss mit einer 'index.yml-Datei konfiguriert werden, die Details zu der JAR-Datei des Agenten angibt. Führen Sie die Schritte aus, die im Folgenden für die Konfiguration des Dynatrace-Agenten angegeben sind:
  1. Laden Sie die JAR-Datei des Dynatrace-Agenten herunter. Lesen Sie [Dynatrace Server Platform Installers](https://community.dynatrace.com/community/display/EVAL/Step+1+-+Download+and+install+Dynatrace) auf der Website der Dynatrace-Community, um Anweisungen zum Herunterladen der JAR-Datei des Dynatrace-Agenten zu erhalten. Die entsprechende JAR-Datei des Agenten, die für die Ausführung in Bluemix erforderlich ist, heißt **dynatrace-agent-unix.jar** Version **6.3.0+**.
  2. Hosten Sie die JAR-Datei des Agenten an einer Position, von der das Liberty-Buildpack sie herunterladen kann. Sie können sie mithilfe einer beliebigen verfügbaren Serverfunktion in Bluemix selbst hosten oder Sie können sie an einer öffentlich verfügbaren Position hosten.
     * Stellen Sie sicher, dass Sie an der Hostingposition eine index.yml-Datei bereitstellen. Die Datei 'index.yml' muss einen Eintrag enthalten, der aus der Versions-ID der JAR-Datei des Agenten besteht, auf die ein Semikolon und die vollständige URL der Position folgt, an der sich diese JAR-Datei des Agenten befindet. Beispiel:
```
      ---
      6.3.0: https://my-dynatrace-agent.mybluemix.net/dynatrace-agent-6.3.0-unix.jar
```
{: #codeblock}
     * Der Name der JAR-Datei am Ende der URL muss **dynatrace-agent-version-unix.jar** lauten. Die Version muss **6.3.0** oder **6.3.0_nnnn** lauten, wobei 'nnnn' die ID der Mikroversion ist. Beachten Sie, dass sich dies von dem Namen der JAR-Datei unterscheidet, den Dynatrace verwendet, und dass es daher möglicherweise erforderlich ist, dass Sie die JAR-Datei umbenennen.       
     * Die Datei **dynatrace-agent-6.3.0-unix.jar** muss an der Position verfügbar sein, die in der Datei 'index.yml' angegeben ist. Die JAR-Datei und die Datei 'index.yml' können als Position dasselbe Verzeichnis haben.

## Dynatrace-Kollektor einrichten

Als nächstes müssen Sie einen Dynatrace-Kollektor einrichten, auf den der Dynatrace-Agent zugreifen kann. Sie müssen auch einen vom Benutzer zur Verfügung gestellten Service erstellen, um Informationen zu übergeben, damit der Dynatrace-Agent eine Verbindung zum Dynatrace-Kollektor herstellen kann. Lesen Sie [Dynatrace Architecture](https://community.dynatrace.com/community/display/DOCDT63/Architecture), um die Beziehung zwischen Dynatrace-Komponenten besser zu verstehen.

  1. Richten Sie einen Dynatrace-Kollektor ein.
    * Lesen Sie die [Website der Dynatrace-Community](https://community.dynatrace.com/community/display/EVAL/Step+3+-+Connect+Agent+to+Dynatrace), um Anweisungen zum Herunterlade und Einrichten des Dynatrace-Kollektors zu erhalten.
    * Stellen Sie sicher, dass der Kollektor an einer Position eingerichtet wird, auf die der Dynatrace-Agent, der mit Ihrer App in Bluemix ausgeführt wird, zugreifen kann.
  2. Erstellen Sie einen vom Benutzer zur Verfügung gestellten Service, der auf den aktiven Dynatrace-Agenten verweist. <b>ANMERKUNG:</b> Der Name des vom Benutzer zur Verfügung gestellten Service muss <b>dynatrace</b> enthalten.  Verwenden Sie beispielsweise den folgenden Befehl:
```
    $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring"}'
```
{: #codeblock}
In diesem Beispiel ist 'my-dynatrace-collector' der angegebene Name des Service, 'DynatraceCollectorIPaddress' ist die IP-Adresse des von Ihnen konfigurierten Dynatrace-Kollektors und 'profile' ist der Name des optionalen Dynatrace-Profils, der dieser überwachten App zugeordnet ist. Der Standardwert für das Profil ist 'Monitoring' (Überwachung). Sie können wie im anschließenden Beispiel optional Parameter angeben.
```
    $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring",
                                          "options" : {
                                                       "dynatrace-parameter-1": "value",
                                                       "dynatrace-parameter-2": "value"
                                         }}'
```
{: #codeblock}
Im [Abschnitt 'Agent Settings' von 'Agent Configuration'](https://community.dynatrace.com/community/display/DOCDT62/Agent+Configuration) auf der Website der Dynatrace-Community finden Sie weitere Informationen zu verfügbaren Optionen. Beispielsweise können Sie mit der Ausschlussoption Klassen von der Überwachung durch Dynatrace ausnehmen. In [DynaTrace Agent Framework](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/framework-dynatrace-agent.md) finden Sie weitere Details zur Konfiguration des vom Benutzer zur Verfügung gestellten Service.
  3. Übertragen Sie Ihre App mit einer Push-Operation an Bluemix und binden Sie den vom Benutzer zur Verfügung gestellten Service, den Sie erstellt haben, anschließend an die App. Verwenden Sie beispielsweise den folgenden Befehl:
```
    $ cf bs myApp my-dynatrace-service
```
**Hinweis**: Sie müssen nach dem Binden des Service ein erneutes Staging für Ihre Anwendung durchführen.

## Liberty-App konfigurieren
{: #configuring_liberty_app}

Die zu überwachende Liberty-App muss konfiguriert werden, sodass sie nach der Agenten-JAR-Datei sucht, die Sie zuvor eingerichtet haben. Sie können die App mit der Umgebungsvariablen **JBP_CONFIG_DYNATRACEAGENT** konfigurieren. Die Umgebungsvariable **JBP_CONFIG_DYNATRACEAGENT** weist das Buildpack an, von welcher Position der Dynatrace-Agent herunterzuladen ist. Führen Sie zum Festlegen der Umgebungsvariablen folgende Schritte aus:
<ol>
   <li> Legen Sie die Variable **JBP_CONFIG_DYNATRACEAGENT** fest, sodass sie folgenden Wert aufweist: *"repository_root: URL_of_server_hosting_index.yml"*. Setzen Sie beispielsweise folgenden Befehl ab, nachdem Sie für Ihre Anwendung eine Push-Operation durchgeführt haben:
```
    $ cf se myApp JBP_CONFIG_DYNATRACEAGENT 'repository_root: https://my-dynatrace-agent-host.mybluemix.net'
```
{: #codeblock}
  In diesem Beispiel ist *my-dynatrace-agent-host.mybluemix.net* die URL der Datei 'index.yml', die vom Server gehostet wird, den sie zuvor konfiguriert haben.
  </li>
  <li> Führen Sie nach dem Festlegen der Umgebungsvariablen ein erneutes Staging für Ihre App durch. Das 'staging_task.log' für Ihre Liberty-App gibt eine Nachricht aus, in der gemeldet wird, dass der Dynatrace-Agent erfolgreich von dem Server heruntergeladen wurde, der den Agenten hostet. Beispiel:
```
    Downloading dynatrace-agent-6.3.0-unix.jar 6.3.0 from https://my-dynatrace-agent-host.mybluemix.net/dynatrace-agent-6.3.0-unix.jar (17.8s)
```
{: #codeblock}
</li>
<li>Setzen Sie folgenden Befehl ab, um das Protokoll 'staging_task.log' anzuzeigen:
```
    $ cf files myAppName logs/staging_task.log
```
{: #codeblock}
</li>
</ol>

# Zugehörige Links
## Allgemein
* [Liberty-Laufzeit](index.html)
* [Übersicht über das Liberty-Profil](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
