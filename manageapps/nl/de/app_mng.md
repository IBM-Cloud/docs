---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Liberty- und Node.js-Apps verwalten
{: #app_management}

*Letzte Aktualisierung: 17. März 2016*

Beim App-Management handelt es sich um eine Reihe von Entwicklungs- und Debugging-Dienstprogrammen, die für Ihre Liberty- und Node.js-Anwendungen in {{site.data.keyword.Bluemix}} aktiviert werden können.
{:shortdesc}

##Dienstprogramme für das App-Management
{: #Utilities}

Diese Dienstprogramme unterstützen Liberty und Node.js.

  1. *proxy*: Minimales Anwendungsmanagement, das als Proxy zwischen Ihrer Anwendung und {{site.data.keyword.Bluemix_notm}} dient.

    Falls es aktiviert ist, startet das Buildpack einen Proxy-Agenten, der zwischen die Laufzeit und den Container Ihrer Anwendung geschaltet ist. Der Dienstprogramm *proxy* verarbeitet alle Anforderungen, die von der Anwendung empfangen werden. Abhängig von dem Typ von Anforderung wird entweder eine App-Management-Aktion ausgeführt oder die Anforderung wird an Ihre Anwendung weitergeleitet. *proxy* ermöglicht die Aktivierung der meisten anderen App-Management-Dienstprogramme. Indem Sie *proxy* aktivieren, bleibt der Anwendungscontainer auch dann verfügbar, wenn die Anwendung ausfällt. Der Proxy-Agent ermöglicht auch inkrementelle Aktualisierungen, d. h. der Live Edit-Modus für Node.js-Anwendungen ist aktiviert.
	
  2. *devconsole*: Aktiviert das Entwicklungskonsolendienstprogramm, auf das unter der folgenden URL zugegriffen werden kann:
    ```
    http://<App-Name>.mybluemix.net/bluemix-debug/manage
    ```
	
    Über die Entwicklungskonsole können Benutzer ihre Anwendungen erneut starten, stoppen oder aussetzen. Außerdem können Benutzer die Shell- und Inspector-Dienstprogramme aktivieren oder darauf zugreifen.

    Das Dienstprogramm 'devconsole' startet auch *proxy*.
	
  3. *hc*: Health Center-Agent, der die Überwachung der Anwendung durch den Health Center-Client einrichtet.

    Das Health Center unterstützt die Analyse der Leistung Ihrer Liberty- und Node.js-Anwendungen mithilfe von IBM Monitoring and Diagnostic Tools. Weitere Informationen finden Sie im Abschnitt zum [Analysieren der Leistung von Liberty-Java- oder Node.js-Apps in {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){:new_window}.</p></li>
	
  4. *shell*: Aktiviert eine webbasierte Shell, die über das 'devconsole'-Dienstprogramm oder unter der folgenden URL zugänglich ist:
    ```
    http://<App-Name>.mybluemix.net/bluemix-debug/shell
    ```
	
    Ein Terminalfenster mit Shell-Zugriff auf Ihre Anwendung wird angezeigt, nachdem Sie das Shell-Dienstprogramm aufgerufen haben. Sie können alle Aktionen ausführen, die in einer regulären Shell unterstützt werden, z. B. das Bearbeiten von Dateien, das Überprüfen der Speicherbelegung oder das Ausführen von Diagnosebefehlen.
	
    Das Dienstprogramm *shell* startet auch *proxy*.

Diese Dienstprogramme unterstützen nur Liberty.

  1. *debug*: Schaltet die Liberty-Anwendung in den Debugmodus und ermöglicht Clients wie IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, eine ferne Debugsitzung mit der Anwendung zu erstellen.
  
   Weitere Informationen finden Sie im Abschnitt zum [fernen Debugging](../manageapps/eclipsetools/eclipsetools.html#remotedebug).
   
   Das Dienstprogramm *debug* startet auch *proxy*.
   
  2. *jmx*: Aktiviert den JMX-REST-Connector, damit ein ferner JMX-Client die Anwendung unter Verwendung von {{site.data.keyword.Bluemix_notm}}-Benutzerberechtigungsnachweisen verwalten kann.
  
  Weitere Informationen zur Konfiguration eines JMX-Connectors finden Sie im Abschnitt zum [Konfigurieren einer sicheren JMX-Verbindung zum Liberty-Profil](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}.
  
  Das Dienstprogramm *jmx* startet 'proxy' nicht.

Diese Dienstprogramme unterstützen nur Node.js.

  1. *inspector*: Aktiviert die Node Inspector-Debuggerschnittstelle, auf die über das Dienstprogramm *devconsole* oder unter *https://myApp.mybluemix.net/bluemix-debug/inspector* zugegriffen werden kann.
  
  Der Inspector-Prozess wird im Anwendungscontainer ausgeführt. Setzen Sie dieses Dienstprogramm ein, um CPU-Nutzungsprofile zu erstellen, Unterbrechungspunkte hinzuzufügen und Code zu debuggen,während Ihre Anwendung unter {{site.data.keyword.Bluemix_notm}} ausgeführt wird. Weitere Informationen zum Node Inspector-Modul finden Sie Thema zu ['node-inspector' unter GitHub](https://github.com/node-inspector/node-inspector){:new_window}.
  
  Das Dienstprogramm *inspector* startet auch *proxy*.
  
  2. *strongpm*: Aktiviert die Verwendung von [StrongLoop Arc](https://strongloop.com/node-js/arc){:new_window} zur Analyse Ihrer Node.js-Anwendung mit Dienstprogrammen wie [StrongLoop Metrics, Profiling und Tracing](https://strongloop.com/node-js/devops-tools/){:new_window}.
    
  Das Dienstprogramm *strongpm* startet auch *proxy*.
  
  Führen Sie die folgenden Schritte aus, um Ihre Node.js-Anwendung mit [StrongLoop Arc](https://strongloop.com/node-js/arc){:new_window} zu konfigurieren.

    1. Konfigurieren Sie die *strongpm*-Umgebungsvariable BlUEMIX_APP_MGMT_ENABLE und führen Sie ein erneutes Staging für Ihre Anwendung aus.
    
	```
    cf set-env <App-Name> BLUEMIX_APP_MGMT_ENABLE strongpm
    cf restage <App-Name>
    ```
	
    2. Fügen Sie in der Cloud Foundry-Befehlszeile eine Route zu Ihrer Anwendung hinzu, wobei an den Anwendungsnamen in der Route '-pm' angehängt wird, z. B. '<App-Name>-pm.mybluemix.net'.
    
	```
    cf map-route <App-Name> ng.bluemix.net -n <App-Name>-pm
    ```
	
    3. Installieren Sie das [StrongLoop-NPM-Modul](https://www.npmjs.com/package/strongloop){:new_window} auf Ihrer lokalen Workstation.
    
	```
    npm install -g strongloop
    ```
	
    4. Erstellen Sie ein Konto auf der [StrongLoop-Website](https://strongloop.com/register/){:new_window}.
    5. Starten Sie Arc auf Ihrer lokalen Workstation und melden Sie sich mit dem erstellten Konto an.
    
	```
    slc arc
    ```
	
    6. Navigieren Sie zur Process Manager-Ansicht innerhalb von Arc. Geben Sie die neu erstellte Route mit Port 80 in Process Manager ein. Drücken Sie die Schaltfläche zum Aktivieren. Weitere Details finden Sie in der [vollständigen Dokumentation zur Verwendung von Arc](https://docs.strongloop.com/display){:new_window}.
	
  3. *trace*: Legt Tracestufen dynamisch fest, wenn Ihre Anwendung *log4js*-, *ibmbluemix*- oder *bunyan*-Protokolliermodule verwendet.
  
  **Hinweis:** Unterstützte Abhängigkeitsversionen:

    * log4js:(0.6.0 - 0.6.24)
    * bunyan: (1.0.0, 1.0.1, 1.1.0 - 1.1.3, 1.2.0 - 1.2.3, 1.3.0 - 1.3.5)
    * ibmbluemix: (1.0.0-20140707-1250)-(1.0.0-20150409-1328)
  
  Wechseln Sie zur Seite 'Instanzdetails' in der {{site.data.keyword.Bluemix_notm}}-Webkonsole und wählen Sie **Aktionen** aus, um die Benutzerschnittstelle anzuzeigen.

  Das Dienstprogramm *trace* startet *proxy* nicht.

##Vorgehensweise zum Konfigurieren des App-Managements
{: #configure}

Für eine
Aktivierung der Dienstprogramme für das App-Management legen Sie die
Umgebungsvariable *BLUEMIX_APP_MGMT_ENABLE* fest und führen ein erneutes Staging für Ihre Anwendung aus. Es können mehrere Dienstprogramme aktiviert werden; hierfür trennen Sie diese durch ein Pluszeichen “+” voneinander.

Führen Sie beispielsweise zur Aktivierung der Dienstprogramme 'devconsole' und *shell* den folgenden Befehl aus:

```
cf set-env myApp BLUEMIX_APP_MGMT_ENABLE devconsole+shell
```

Vergessen Sie nicht, für Ihre Anwendung nach dem Festlegen der Umgebungsvariablen ein erneutes Staging durchzuführen:

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

##Einschränkungen
{: #restrictions}

* Das App-Management unterstützt nur Einzelinstanzanwendungen.
* Änderungen, die Sie an Ihrer Anwendung mithilfe von App-Management vornehmen, sind temporär und gehen verloren, wenn Sie diesen Modus verlassen. Dieser Modus dient nur temporären Entwicklungszwecken und ist aufgrund seiner Leistung nicht als Produktionsumgebung gedacht.
* Die meisten App-Management-Dienstprogramme funktionieren nicht, wenn Sie den Startbefehl in der Datei 'manifest.yml' (command) oder der Befehlszeilenschnittstelle 'cf' (-c) festlegen. Bei diesen Methoden handelt es sich um Buildpack-Überschreibungen und sie sind Anti-Patterns für das Starten von Node.js-Anwendungen. Die besten Ergebnisse erzielen Sie, indem Sie den Startbefehl in der Datei 'package.json' oder 'Procfile' festlegen.

##Entwicklungsmodus für Eclipse Tools
{: #devmode}

Der Entwicklungsmodus ist ein Feature von [Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](../manageapps/eclipsetools/eclipsetools.html#eclipsetools), das
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
