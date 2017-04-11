---



copyright:
  years: 2015，2017
lastupdated: "2017-3-10"

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}

#{{site.data.keyword.Bluemix_notm}} Live Sync
{: #live-sync}

 
Wenn Sie eine Node.js-Anwendung erstellen, können Sie {{site.data.keyword.Bluemix}} Live Sync dazu verwenden, die Anwendungsinstanz ohne großen Zeitaufwand in {{site.data.keyword.Bluemix_notm}} zu aktualisieren und Entwicklungsprozesse ohne eine erneute manuelle Bereitstellung durchzuführen.   
{: shortdesc}

Wenn Sie eine Änderung vornehmen, ist diese Änderung sofort in der aktiven {{site.data.keyword.Bluemix_notm}}-Anwendung sichtbar. {{site.data.keyword.Bluemix_notm}} Live Sync kann in  
<!--from both the command line and -->
Eclipse Orion Web IDE (Web-IDE) ausgeführt werden. Sie können in Node.js geschriebene Anwendungen mithilfe von {{site.data.keyword.Bluemix_notm}} Live Sync debuggen.  

{{site.data.keyword.Bluemix_notm}} Live Sync setzt sich aus zwei Features zusammen.
<!-- three -->

<!--
**Desktop Sync**  

You can synchronize any desktop directory tree with a cloud-based project workspace similar to the way Dropbox works. The Web IDE directly edits the same cloud-based workspace, so both stay in sync. Desktop Sync works for any kind of application. To use Desktop Sync, you need to download and install the BL command line interface.  
-->

**Live Edit**

Sie können Änderungen an einer in {{site.data.keyword.Bluemix_notm}} ausgeführten Node.js-Anwendung vornehmen und diese sofort in Ihrem Browser testen. Alle Änderungen in der Web-IDE werden umgehend an das Dateisystem der Anwendung weitergegeben.  

**Debug**  

Wenn sich eine Node.js-Anwendung im Live Edit-Modus befindet, können Sie einen Shellzugriff einrichten und die Anwendung debuggen. Sie können Code dynamisch bearbeiten, Unterbrechungspunkte einfügen, Code schrittweise durchgehen, die Laufzeit erneut starten und weitere Aktionen mit dem Node Inspector-Debugger durchführen.  

<!-- You can use Desktop Sync to keep your desktop workspace in sync with the cloud-based project workspace that you edit directly with the Web IDE. -->

Mit Live Edit können Sie Änderungen am cloudbasierten Projektarbeitsbereich an die aktive Anwendung weitergeben. 
<!-- You can use one or both of these features. And if you use Desktop Sync or -->
Wenn Sie mit Live Edit die Anwendung in den Live Edit-Modus versetzen, können Sie die aktive Anwendung auch debuggen.Der Bluemix Live Sync-Prozess ist im folgenden Diagramm dargestellt.    

Abbildung 1. Der Bluemix Live Sync-Prozess
    

![Abbildung des Bluemix Live Sync-Prozesses](images/bluemix-live-sync.png)

Wenn Sie eine Java-Anwendung entwickeln, die auf Liberty ausgeführt wird, können Sie mit [Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools) ein fernes Debugging durchführen.


##Live Edit {: #live-edit}

Wenn Sie eine Node.js-Anwendung erstellen, können Sie beim Vornehmen von Änderungen am Projekt mit der Web-IDE das Live Edit-Feature von {{site.data.keyword.Bluemix_notm}} Live Sync dazu verwenden, die aktive Anwendungsinstanz in {{site.data.keyword.Bluemix_notm}} ohne großen Zeitaufwand zu aktualisieren. Mit Live Edit können Sie Entwicklungsprozesse wie auf dem Desktop durchführen, ohne dass eine erneute Bereitstellung erforderlich ist.

Live Edit wird nur für Node.js-Anwendungen unterstützt.

Klicken Sie in Eclipse Orion Web IDE (Web-IDE) in der Ausführungsleiste auf **Live Edit**.

![Abbildung der Ausführungsleiste mit Live Edit](images/bluemix-live-sync-light.png)

Mit Live Edit können Sie schnell Änderungen an in {{site.data.keyword.Bluemix_notm}} ausgeführten Node.js-Anwendungen als Vorschau anzeigen. Wenn Sie den Code bei aktiviertem Live Edit-Feature aktualisieren, können Sie das Browserfenster Ihrer Webanwendung aktualisieren, um diese Änderungen Sekunden nach deren Durchsetzung anzeigen zu lassen.

<!--
For a tutorial on using the Live Edit feature of {{site.data.keyword.Bluemix_notm}} Live Sync, see the tutorial [Test and debug a Node.js app with Bluemix Live Sync![External link icon](../icons/launch-glyph.svg "External link icon")](https://hub.jazz.net/tutorials/livesync){:new_window}.
-->

Wenn Sie die Dateien in der Web-IDE ändern, werden sie automatisch erneut für die aktive Anwendung in {{site.data.keyword.Bluemix_notm}} bereitgestellt. Wenn Sie die Node-Anwendung erneut starten müssen, können Sie die Schaltfläche **Erneut starten** in der Ausführungsleiste verwenden.

**Hinweis:** Für eine möglichst konsistente Verarbeitungsleistung der Funktion 'Live Edit' von {{site.data.keyword.Bluemix_notm}} Live Sync, ist eine zusätzliche Hauptspeicherkapazität von 256 MB erforderlich und wird hinzugefügt.

##{{site.data.keyword.Bluemix_notm}} Live Debug {: #live-debug}

Sie haben Zugriff auf das Debug-Feature von {{site.data.keyword.Bluemix_notm}} Live Sync, wenn {{site.data.keyword.Bluemix_notm}} Live Sync für Ihre Node.js-App aktiviert ist.

Mit dem Debug-Feature können Sie Code dynamisch bearbeiten, Unterbrechungspunkte einfügen, Code schrittweise durchgehen, die Laufzeit erneut starten und weitere Aktionen durchführen, während Ihre App von {{site.data.keyword.Bluemix_notm}} bereitgestellt wird. Sie können Ihre App schrittweise flexibel entwickeln und haben dabei die Möglichkeit, in der umfangreichen Liste der {{site.data.keyword.Bluemix_notm}}-Services Ihre Auswahl zu treffen.

{{site.data.keyword.Bluemix_notm}} Live Debug enthält die folgenden Features:

* Anwendungslaufzeitsteuerung
* Debug mit [node-inspector![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/node-inspector/node-inspector){:new_window}
* Shellzugriff

###Anwendungslaufzeitsteuerung {: #app-runtime}

Mit der Anwendungslaufzeitsteuerung können Sie mithilfe des Debug-Features den Status der App zur Startzeit überprüfen. Diese Funktion ist nützlich, wenn Sie für eine App, die beim Start fehlschlägt, Fehlerbehebungsmaßnahmen durchführen.

Bei der Entwicklung Ihrer App haben Sie die Auswahl zwischen den folgenden Aktionen:

* Schneller Neustart der App
* Aussetzen der App, bevor App-Code ausgeführt wird

###Debug {: #debug}

Das Debug-Feature umfasst die folgenden Leistungsmerkmale:

**Einschränkung:** Google Chrome ist erforderlich.

* Festlegen von Unterbrechungspunkten im App-Code, um die Ausführung in einer bestimmten Zeile anzuhalten.
* Bearbeiten von Unterbrechungspunktbedingungen, um die Ausführung nur anzuhalten, wenn bestimmte Kriterien erfüllt sind.
* Überprüfen des Status lokaler Variablen und Felder.
* Sofortiges Anzeigen der Debugausgabe für Aufrufe von `console.log()`. Diese Aktion nimmt weniger Zeit in Anspruch als die Überwachung von cf-Protokollen.
* Verwenden des integrierten Quellcodeeditors, um sofortige, aber temporäre Änderungen am Code der aktiven App vorzunehmen.

###Shell {: #shell}

Mit diesem Tool erhalten Sie Shellzugriff auf den Container, in dem Ihre App ausgeführt wird. Mithilfe dieses Terminals können Sie Shellbefehle für die Diagnose fern ausführen, um Ihre App zu verwalten.

Sie können die Speicher- und CPU-Auslastung in der Instanz überwachen, die Linux-Standardbefehle wie **top**, **ps** und **kill** verwendet.

###Eine App zur Aktivierung von {{site.data.keyword.Bluemix_notm}} Live Debug konfigurieren {: #configure_app_debug}

Die App muss das IBM SDK for Node.js-Buildpack verwenden. Angepasste Buildpacks werden nicht unterstützt.

1. Lassen Sie zu, dass das Buildpack den App-Startbefehl erkennt. Der Startbefehl muss vom Buildpack automatisch erkannt werden, er darf nicht in der Datei `manifest.yml` festgelegt werden.  

    a. Stellen Sie sicher, dass die Datei `package.json` ein Startscript enthält, das einen Startbefehl für die App beinhaltet.  
    b. Wenn die App-Datei `manifest.yml` einen Befehl enthält, setzen Sie diesen auf null.  

2. Legen Sie die Umgebungsvariable fest.  

    a. Fügen Sie in der Datei `manifest.yml` diese Variable hinzu:
	```
	env:
      ENABLE_BLUEMIX_DEV_MODE: "true"
	```

3. Erhöhen Sie die Speichermenge.  

    a. Fügen Sie in der App-Datei `manifest.yml` 128 M oder mehr zu dem Wert hinzu, der für das Speicherattribut angegeben ist.

Nach der Installation von {{site.data.keyword.Bluemix_notm}} Live Debug können Sie die Debug-Tools verwenden.

Stellen Sie die App per Push-Operation bereit und rufen Sie dann `https://app-host.mybluemix.net/bluemix-debug/manage` auf, um auf die Benutzerschnittstelle des {{site.data.keyword.Bluemix_notm}}-Debug-Features zuzugreifen. Wenn Sie aufgefordert werden, sich zu authentifizieren, geben Sie Ihre Benutzer-ID und das persönliche Zugriffstoken oder das Kennwort zur IBMid ein.    

<!--
   **Note**: Your user ID for DevOps Services can be either an IBMid or a federated ID (corporate ID). If you use federated authentication, to log in to your Bluemix Live Sync command-line client, you must use a personal access token instead of a password. If you don't use federated authentication, your IBMid and password work with all clients. For more information about creating a personal access token, see [What's federated authentication and how does it affect me?![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/devops-services/2016/06/23/whats-federated-authentication-and-how-does-it-affect-me/){:new_window}
   -->

###App-Konfigurationen wiederherstellen und Bluemix Live Debug inaktivieren {: #restore_live_debug}

1. Entfernen Sie die Umgebungsvariable ENABLE_BLUEMIX_DEV_MODE aus der App-Datei `manifest.yml`.

2. Stellen Sie den ursprünglichen Startbefehl und Speicherwert der App wieder her.

3. Stellen Sie die App per Push-Operation bereit.


## Zugehörige Links
{: #general}

* [Eclipse Tools for Bluemix![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ng.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html){:new_window}
