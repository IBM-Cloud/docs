---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-07"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Dynatrace verwenden
{: #using_dynatrace}

Bei Dynatrace handelt es sich um einen Service eines anderen Anbieters, der Überwachungsmetriken für Ihre App bereitstellt.

Weitere Informationen zu Bereitstellungen des Service Dynatrace finden Sie in [Dynatrace Application Monitoring](http://www.dynatrace.com/en/products/application-monitoring.html).

Wenn Ihre Liberty-Anwendung für die Verwendung von Dynatrace konfiguriert ist,
ist das Standardverhalten wie folgt: Die Liberty-Laufzeit fordert von einer Dynatrace-Site
die JAR-Datei eines Dynatrace-Agenten an und führt diesen Dynatrace-Agenten mit Ihrer
App aus.  Bei diesem Standardverhalten besteht die minimal notwendige Konfiguration für die
Verwendung von Dynatrace im Erstellen eines vom Benutzer zur Verfügung gestellten Service,
der auf Ihren Dynatrace-Kollektor verweist.

## Einen vom Benutzer zur Verfügung gestellten Service erstellen, der auf Ihren Dynatrace-Kollektor verweist

Zunächst müssen Sie einen Dynatrace-Kollektor einrichten.  Dann müssen Sie einen vom Benutzer zur Verfügung gestellten
Service erstellen, um Informationen zu übergeben, damit der Dynatrace-Agent eine Verbindung zum Dynatrace-Kollektor herstellt. Lesen Sie [Dynatrace Architecture](https://community.dynatrace.com/community/display/DOCDT63/Architecture), um die Beziehung zwischen Dynatrace-Komponenten besser zu verstehen.

1. Richten Sie einen Dynatrace-Kollektor ein.
  
  * Lesen Sie die [Website der Dynatrace-Community](https://community.dynatrace.com/community/display/EVAL/Step+3+-+Connect+Agent+to+Dynatrace), um Anweisungen zum Herunterlade und Einrichten des Dynatrace-Kollektors zu erhalten.
  
  * Stellen Sie sicher, dass der Kollektor an einer Position eingerichtet wird, auf die der Dynatrace-Agent, der mit Ihrer App in Bluemix ausgeführt wird, zugreifen kann.
  
2. Erstellen Sie einen vom Benutzer zur Verfügung gestellten Service, der auf den aktiven Dynatrace-Agenten verweist. **ANMERKUNG:** Der Name des vom Benutzer zur Verfügung gestellten Service muss die Zeichenfolge **dynatrace** enthalten. Die Groß-/Kleinschreibung wird ignoriert. Verwenden Sie zum Beispiel den folgenden Befehl, wobei **my-dynatrace-collector** die Zeichenfolge **dynatrace** enthält:

          $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring"}'
{: codeblock}

    In diesem Beispiel ist 'my-dynatrace-collector' der angegebene Name des Service, 'DynatraceCollectorIPaddress' ist die IP-Adresse des von Ihnen konfigurierten Dynatrace-Kollektors und 'profile' ist der Name des optionalen Dynatrace-Profils, der dieser überwachten App zugeordnet ist. Der Standardwert für das Profil ist 'Monitoring' (Überwachung). Sie können wie im anschließenden Beispiel optional Parameter angeben.

        $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring",
                                              "options" : {"dynatrace-parameter-1": "value",
                                                           "dynatrace-parameter-2": "value"}}'
        {: codeblock}

    Im [Abschnitt 'Agent Settings' von 'Agent Configuration'](https://community.dynatrace.com/community/display/DOCDT62/Agent+Configuration) auf der Website der Dynatrace-Community finden Sie weitere Informationen zu verfügbaren Optionen. Beispielsweise können Sie mit der Ausschlussoption Klassen von der Überwachung durch Dynatrace ausnehmen. In [DynaTrace Agent Framework](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/framework-dynatrace-agent.md) finden Sie weitere Details zur Konfiguration des vom Benutzer zur Verfügung gestellten Service.

3. Übertragen Sie Ihre App mit einer Push-Operation an Bluemix und binden Sie den vom Benutzer zur Verfügung gestellten Service, den Sie erstellt haben, anschließend an die App. Verwenden Sie beispielsweise den folgenden Befehl:

  

          $ cf bs myApp my-dynatrace-collector
{: codeblock}

    **Hinweis**: Sie müssen nach dem Binden des Service ein erneutes Staging für Ihre Anwendung durchführen.

## Optionale Konfiguration
{: #optional_configuration}

Sie können die JAR-Datei des Dynatrace-Agenten selbst anfordern und hosten.  In diesem Fall sind die folgenden
zusätzlichen Konfigurationsschritte erforderlich.
1. Fordern Sie die JAR-Datei des Dynatrace-Agenten an und hosten Sie sie, damit das Liberty-Buildpack sie herunterladen kann.
2. Konfigurieren Sie Ihre Liberty-App, damit sie den Dynatrace-Agenten herunterladen kann.

### Dynatrace-Agent hosten
{: #hosting_dynatrace_agent}
Der Dynatrace-Agent muss als Host einen Web-Server haben und das Liberty-Buildpack muss die JAR-Datei des Agenten von diesem Server herunterladen können. Der Server muss mit der Datei `index.yml` konfiguriert werden, die Details zu der JAR-Datei des Agenten angibt. Führen Sie die Schritte aus, die im Folgenden für die Konfiguration des Dynatrace-Agenten angegeben sind:
  1. Laden Sie die JAR-Datei des Dynatrace-Agenten herunter. Lesen Sie [Dynatrace Server Platform Installers](https://community.dynatrace.com/community/display/EVAL/Step+1+-+Download+and+install+Dynatrace) auf der Website der Dynatrace-Community, um Anweisungen zum Herunterladen der JAR-Datei des Dynatrace-Agenten zu erhalten. Die entsprechende JAR-Datei des Agenten für die Ausführung in Bluemix ist **dynatrace-agent-unix.jar** Version **6.+**.
  2. Hosten Sie die JAR-Datei des Agenten an einer Position, von der das Liberty-Buildpack sie herunterladen kann. Sie können sie mithilfe einer beliebigen verfügbaren Serverfunktion in Bluemix selbst hosten oder Sie können sie an einer öffentlich verfügbaren Position hosten.
     * Stellen Sie sicher, dass Sie an der Hostingposition die Datei `index.yml` bereitstellen. Die Datei `index.yml` muss einen Eintrag enthalten, der aus der Versions-ID der JAR-Datei des Agenten besteht, auf die ein Doppelpunkt und die vollständige URL der Position folgt, an der sich diese JAR-Datei des Agenten befindet. Beispiel:

            ---
               6.3.0: https://my-dynatrace-agent.mybluemix.net/dynatrace-agent-6.3.0-unix.jar
            {: codeblock}
     
     * Die Datei **dynatrace-agent-6.3.0-unix.jar** muss an der Position verfügbar sein, die in der Datei `index.yml` angegeben ist. Die JAR-Datei und die Datei `index.yml` können als Position dasselbe Verzeichnis haben. 

### Liberty-App konfigurieren
{: #configuring_liberty_app}

Die zu überwachende Liberty-App muss konfiguriert werden, sodass sie nach der Agenten-JAR-Datei sucht, die Sie zuvor eingerichtet haben. Sie können die App mit der Umgebungsvariablen **JBP_CONFIG_DYNATRACEAPPMONAGENT** konfigurieren. Die Umgebungsvariable **JBP_CONFIG_DYNATRACEAPPMONAGENT** weist das Buildpack an, von welcher Position der Dynatrace-Agent herunterzuladen ist. Führen Sie zum Festlegen der Umgebungsvariablen folgende Schritte aus:

1. Legen Sie die Variable **JBP_CONFIG_DYNATRACEAPPMONAGENT** fest, sodass sie folgenden Wert aufweist: *"repository_root: URL_of_server_hosting_index.yml"*. Setzen Sie beispielsweise folgenden Befehl ab, nachdem Sie für Ihre Anwendung eine Push-Operation durchgeführt haben:

  
        $ cf se myApp JBP_CONFIG_DYNATRACEAPPMONAGENT 'repository_root: https://my-dynatrace-agent-host.mybluemix.net'
        {: codeblock}

    In diesem Beispiel ist *my-dynatrace-agent-host.mybluemix.net* die URL der Datei `index.yml`, die vom Server gehostet wird, den sie zuvor konfiguriert haben.

2. Führen Sie nach dem Festlegen der Umgebungsvariablen ein erneutes Staging für Ihre App durch. Überprüfen Sie das Staging-Protokoll, um eine Nachricht zu finden, in der gemeldet wird, dass der Dynatrace-Agent erfolgreich von dem Server heruntergeladen wurde, der den Agenten hostet. Beispiel:
```
    Downloading dynatrace-agent-6.3.0-unix.jar 6.3.0 from https://my-dynatrace-agent-host.mybluemix.net/dynatrace-agent-6.3.0-unix.jar (17.8s)
```
{: codeblock}

# Zugehörige Links
{: #rellinks notoc}
## Allgemein
{: #general notoc}
* [Liberty-Laufzeit](index.html)
* [Übersicht über das Liberty-Profil](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
