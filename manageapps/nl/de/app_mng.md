---

copyright:
  years: 2015, 2016
lastupdated: "2016-12-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Liberty- und Node.js-Apps verwalten
{: #app_management}


Beim App-Management handelt es sich um eine Reihe von Entwicklungs- und Debugging-Dienstprogrammen, die für Ihre Liberty- und Node.js-Anwendungen in {{site.data.keyword.Bluemix}} aktiviert werden können.
{:shortdesc}

## Dienstprogramme für das App-Management
{: #Utilities}

### Diese Dienstprogramme unterstützen Liberty und Node.js
{: #liberty_and_node_utilities}

#### proxy
{: #proxy}

Mit *proxy* ist nur minimaler Anwendungsverwaltungsaufwand zwischen Ihrer Anwendung und {{site.data.keyword.Bluemix_notm}} erforderlich.

Falls es aktiviert ist, startet das Buildpack einen Proxy-Agenten, der zwischen die Laufzeit und den Container Ihrer Anwendung geschaltet ist. Der Dienstprogramm *proxy* verarbeitet alle Anforderungen, die von der Anwendung empfangen werden. Abhängig von dem Typ von Anforderung wird entweder eine App-Management-Aktion ausgeführt oder die Anforderung wird an Ihre Anwendung weitergeleitet. *proxy* ermöglicht die Aktivierung der meisten anderen App-Management-Dienstprogramme. Indem Sie *proxy* aktivieren, bleibt der Anwendungscontainer auch dann verfügbar, wenn die Anwendung ausfällt. Der Proxy-Agent ermöglicht auch inkrementelle Aktualisierungen, d. h. der Live Edit-Modus für Node.js-Anwendungen ist aktiviert.

#### devconsole
{: #devconsole}

Auf das Entwicklungskonsolendienstprogramm (*devconsole*) kann über die folgende URL zugegriffen werden:
```
  http://<App-Name>.mybluemix.net/bluemix-debug/manage
```

Über die Entwicklungskonsole können Benutzer ihre Anwendungen erneut starten, stoppen oder aussetzen. Außerdem können Benutzer die Shell- und Inspector-Dienstprogramme aktivieren oder darauf zugreifen.

Für Node-Versionen ab Version 6.3.0 bietet die Entwicklungskonsole eine Schaltfläche für den Neustart Ihrer Anwendung und Zugriff auf das Dienstprogramm 'shell'. Weitere Informationen finden Sie in der Beschreibung zu *inspector*.

Das Dienstprogramm 'devconsole' startet auch *proxy*.

#### hc
{: #hc}

Der Health Center-Agent (*hc*) ermöglicht die Überwachung Ihrer Anwendung durch den Health Center-Client.

Das Health Center unterstützt die Analyse der Leistung Ihrer Liberty- und Node.js-Anwendungen mithilfe von IBM Monitoring and Diagnostic Tools. Weitere Informationen finden Sie im Abschnitt zum [Analysieren der Leistung von Liberty-Java- oder Node.js-Apps in {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){:new_window}.</p></li>

#### shell
{: #shell}

Das Dienstprogramm *shell* dient zur Aktivierung einer webbasierten Shell. Auf diese kann über das Dienstprogramm *devconsole* oder über die folgende URL zugegriffen werden:

```
  http://<App-Name>.mybluemix.net/bluemix-debug/shell
```

Ein Terminalfenster mit Shell-Zugriff auf Ihre Anwendung wird angezeigt, nachdem Sie das Dienstprogramm *shell* aufgerufen haben. Sie können alle Aktionen ausführen, die in einer regulären Shell unterstützt werden, z. B. das Bearbeiten von Dateien, das Überprüfen der Speicherbelegung oder das Ausführen von Diagnosebefehlen.

Das Dienstprogramm *shell* startet auch *proxy*.

### Diese Dienstprogramme unterstützen ausschließlich Liberty
{: #liberty_utilities}

#### debug
{: #debug}

Mit dem Dienstprogramm *debug* wird die Liberty-Anwendung in den Debugmodus versetzt und es ermöglicht Clients wie IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, eine ferne Debugsitzung mit der Anwendung zu erstellen.

Weitere Informationen finden Sie im Abschnitt zum [fernen Debugging](/docs/manageapps/eclipsetools/eclipsetools.html#remotedebug).

Das Dienstprogramm *debug* startet auch *proxy*.

#### jmx
{: #jmx}

Mit dem Dienstprogramm *jmx* wird der JMX-REST-Connector aktiviert, damit ein ferner JMX-Client die Anwendung unter Verwendung von {{site.data.keyword.Bluemix_notm}}-Benutzerberechtigungsnachweisen verwalten kann.

Weitere Informationen zur Konfiguration eines JMX-Connectors finden Sie im Abschnitt zum [Konfigurieren einer sicheren JMX-Verbindung zum Liberty-Profil](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}.

Das Dienstprogramm *jmx* startet 'proxy' nicht.

### Diese Dienstprogramme unterstützen ausschließlich Node.js
{: #node_utilities}

#### inspector
{: #inspector}

Bei Versionen von Node.js vor Version 6.3.0 aktiviert *inspector* die Node Inspector-Debuggerschnittstelle, auf die über das Dienstprogramm *devconsole* oder unter *https://myApp.mybluemix.net/bluemix-debug/inspector* zugegriffen werden kann.

Der Prozess für *inspector* wird in Ihrem Anwendungscontainer ausgeführt. Setzen Sie dieses Dienstprogramm ein, um CPU-Nutzungsprofile zu erstellen, Unterbrechungspunkte hinzuzufügen und Code zu debuggen,während Ihre Anwendung unter {{site.data.keyword.Bluemix_notm}} ausgeführt wird. Weitere Informationen zum Node Inspector-Modul finden Sie Thema zu ['node-inspector' unter GitHub](https://github.com/node-inspector/node-inspector){:new_window}.

Das Dienstprogramm *inspector* startet auch *proxy*.

Bei Versionen von Node.js ab Version 6.3.0 verwendet *inspector* [V8 Inspector Integration für Node.js](https://nodejs.org/dist/latest-v6.x/docs/api/debugger.html#debugger_v8_inspector_integration_for_node_js){:new_window}. In den Protokollen Ihrer App befindet sich eine URL, die verwendet werden kann, um eine Verbindung zwischen Ihren Chrome DevTools und Ihrer App herzustellen. Die Protokollnachrichten haben das folgende Format:

```
  2016-11-30T16:40:56.03-0500 [APP/0]      OUT Starting app with 'node-hc --inspect=9229  app.js '
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR Debugger listening on port 9229.
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR To start debugging, open the following URL in Chrome:
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR     chrome-devtools://devtools/remote/serve_file...
```

Mit *devconsole* wird in diesem Szenario **kein** Link zu *inspector* angezeigt, da keine URL vorhanden ist. 

Mit *proxy* wird der Datenverkehr in diesem Szenario nicht an *inspector* weitergeleitet. Sie müssen einen SSH-Tunnel zu Ihrer App erstellen, damit die URL für Chrome DevTools ordnungsgemäß funktioniert. Zum Erstellen des SSH-Tunnels verwenden Sie den Befehl 'cf ssh' in ähnlicher Weise wie im folgenden Beispiel:

```
  cf ssh -N -T -L <port>:127.0.0.1:<hostport> <appName>
```

In diesem Befehl muss für *hostport* der Portwert aus der Protokollnachricht "Debugger listening on port xxxx" angegeben werden. Für *port* kann ein beliebiger verfügbarer Port auf dem System angegeben werden, auf dem der Befehl "cf ssh" abgesetzt wird. 

#### trace
{: #trace}

Mit dem Dienstprogramm *trace* können Tracestufen dynamisch festgelegt werden, wenn Ihre Anwendung *log4js*-, *ibmbluemix*- oder *bunyan*-Protokolliermodule verwendet.

**Hinweis:** Unterstützte Abhängigkeitsversionen:
* log4js:(0.6.0 - 0.6.24)
* bunyan: (1.0.0, 1.0.1, 1.1.0 - 1.1.3, 1.2.0 - 1.2.3, 1.3.0 - 1.3.5)
* ibmbluemix: (1.0.0-20140707-1250)-(1.0.0-20150409-1328)

Wechseln Sie zur Seite 'Instanzdetails' in der {{site.data.keyword.Bluemix_notm}}-Webkonsole und wählen Sie **Aktionen** aus, um die Benutzerschnittstelle anzuzeigen.

Das Dienstprogramm *trace* ist nicht verfügbar, wenn die Anwendung mit der Option "-b buildpack" gestartet wurde.

Das Dienstprogramm *trace* startet *proxy* nicht.

##  Vorgehensweise zum Konfigurieren des App-Managements
{: #configure}

Für eine
Aktivierung der Dienstprogramme für das App-Management legen Sie die
Umgebungsvariable *BLUEMIX_APP_MGMT_ENABLE* fest und führen ein erneutes Staging für Ihre Anwendung aus. Es können mehrere Dienstprogramme aktiviert werden; hierfür trennen Sie diese durch ein Pluszeichen “+” voneinander.

Führen Sie zur Aktivierung der Dienstprogramme *devconsole* und *shell* beispielsweise den folgenden Befehl aus:

```
cf set-env myApp BLUEMIX_APP_MGMT_ENABLE devconsole+shell
```

Führen Sie für Ihre Anwendung nach dem Festlegen der Umgebungsvariablen ein erneutes Staging durch:

```
cf restage myApp
```

Wenn die Dienstprogramme für das App-Management nicht mit Ihrer Anwendung installiert werden sollen,
setzen Sie die Umgebungsvariable
*BLUEMIX_APP_MGMT_INSTALL* auf 'false' und führen Sie für Ihre Anwendung ein erneutes Staging durch.

Beispiel:

```
cf set-env myApp BLUEMIX_APP_MGMT_INSTALL false
cf restage myApp
```

## Einschränkungen
{: #restrictions}

* Das App-Management unterstützt nur Einzelinstanzanwendungen.
* Änderungen, die Sie an Ihrer Anwendung mithilfe von App-Management vornehmen, sind temporär und gehen verloren, wenn Sie diesen Modus verlassen. Dieser Modus dient nur temporären Entwicklungszwecken und ist aufgrund seiner Leistung nicht als Produktionsumgebung gedacht.
* Die meisten App-Management-Dienstprogramme funktionieren nicht, wenn Sie den Startbefehl in der Datei 'manifest.yml' (command) oder der Befehlszeilenschnittstelle 'cf' (-c) festlegen. Bei diesen Methoden handelt es sich um Buildpack-Überschreibungen und sie sind Anti-Patterns für das Starten von Node.js-Anwendungen. Die besten Ergebnisse erzielen Sie, indem Sie den Startbefehl in der Datei 'package.json' oder 'Procfile' festlegen.

## Entwicklungsmodus für Eclipse Tools
{: #devmode}

Der Entwicklungsmodus ist ein Feature von [Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools), das
es Entwicklern ermöglicht,
mit ihren Anwendungen zu arbeiten, während diese in der Cloud ausgeführt werden.

Während die Entwickler mit ihren Anwendungen unter
{{site.data.keyword.Bluemix_notm}} arbeiten, könnten sie den Eindruck
gewinnen, dass normale Entwicklungsaktivitäten nicht so ausgeführt werden können, wie es in einer lokalen Umgebung möglich gewesen wäre. Hierfür
bietet Ihnen der Entwicklungsmodus über Eclipse Tools eine Methode zum Arbeiten in der Cloud, wobei Sie sich in einem temporären, sicheren Arbeitsbereich befinden.

Der Entwicklungsmodus wird sowohl für Liberty- als auch für Node.js-Anwendungen unterstützt. Mit dem für Ihre Liberty- oder Node.js-Anwendung aktivierten
Entwicklungsmodus können Sie Anwendungsdateien inkrementell aktualisieren, ohne
eine Push-Operation für Ihre Anwendung durchführen zu müssen. Sie können mit Ihrer Anwendung außerdem eine
Debugsitzung einrichten. Der Entwicklungsmodus für Liberty-Anwendungen entspricht
der Aktivierung der Dienstprogramme 'debug' und 'jmx' für das
App-Management. Für Node.js-Anwendungen entspricht er der Aktivierung
der Dienstprogramme *devconsole*, *inspector* und *shell*.
