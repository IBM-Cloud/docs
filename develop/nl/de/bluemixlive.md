{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}

#{{site.data.keyword.Bluemix_notm}} Live Sync {: #live-sync}

*Letzte Aktualisierung: 8. Dezember 2015*  

Wenn Sie eine Node.js-Anwendung erstellen,
können Sie {{site.data.keyword.Bluemix}} Live Sync dazu verwenden, die Anwendungsinstanz ohne großen Zeitaufwand in
{{site.data.keyword.Bluemix_notm}} zu aktualisieren
und Entwicklungsprozesse wie auf dem Desktop durchzuführen, ohne dass eine erneute Bereitstellung erforderlich ist.    
{: shortdesc} 

Wenn Sie eine Änderung vornehmen, ist diese Änderung sofort in der aktiven {{site.data.keyword.Bluemix_notm}}-Anwendung sichtbar.
{{site.data.keyword.Bluemix_notm}} Live Sync kann sowohl über die Befehlszeile als auch über die Web-IDE ausgeführt werden. Sie können in Node.js geschriebene Anwendungen mithilfe von {{site.data.keyword.Bluemix_notm}} Live Sync debuggen.   

{{site.data.keyword.Bluemix_notm}} Live Sync setzt sich aus drei Features zusammen.  

**Desktop Sync**  
    Sie können jede beliebige Desktop-Verzeichnisbaumstruktur in ähnlicher Weise wie mit Dropbox mit einem cloudbasierten Projektarbeitsbereich synchronisieren. Die Web-IDE bearbeitet direkt denselben cloudbasierten Arbeitsbereich, so bleiben beide synchron. Desktop Sync kann für alle Anwendungstypen verwendet werden. Für die Verwendung von Desktop Sync müssen Sie die Befehlszeilenschnittstelle 'bl' herunterladen und installieren.   
	
**Live Edit**	
    Sie können Änderungen an einer in {{site.data.keyword.Bluemix_notm}} ausgeführten Node.js-Anwendung vornehmen und diese sofort in Ihrem Browser testen. Alle Änderungen in einem synchronisierten Desktop-Verzeichnis oder in der Web-IDE werden umgehend an das Dateisystem der Anwendung weitergegeben.   
	
**Debug**  
    Wenn sich eine Node.js-Anwendung im Live Edit-Modus befindet, können Sie einen Shellzugriff einrichten und die Anwendung debuggen. Sie können Code dynamisch bearbeiten, Unterbrechnungspunkte einfügen, Code schrittweise durchgehen, die Laufzeit erneut starten und weitere Aktionen mit dem Node Inspector-Debugger durchführen.   

Mit Desktop Sync können Sie den Desktop-Arbeitsbereich mit dem cloudbasierten Projektarbeitsbereich synchron halten, den Sie direkt mit der Web-IDE bearbeiten.
Mit Live Edit können Sie Änderungen am cloudbasierten Projektarbeitsbereich an die aktive Anwendung weitergeben. Sie können eines oder beide dieser Features verwenden. Wenn Sie mit Desktop Sync oder Live Edit die Anwendung in den Live Edit-Modus versetzen, können Sie die aktive Anwendung auch debuggen. 

Der Bluemix Live Sync-Prozess ist im folgenden Diagramm dargestellt. 	

*Abbildung 1. Der Bluemix Live Sync-Prozess*
![Abbildung des Bluemix Live Sync-Prozesses](images/bluemix-live-sync.png)
 
Wenn Sie eine Java-Anwendung entwickeln, die auf Liberty ausgeführt wird, können Sie mit [Eclipse Tools for Bluemix](../manageapps/eclipsetools/eclipsetools.html#eclipsetools) ein fernes Debugging durchführen. 

##Desktop Sync {: #desktop-sync} 

Mit dem Desktop Sync-Feature von Bluemix Live Sync können Sie die Anwendungsinstanz in {{site.data.keyword.Bluemix_notm}} ohne großen Zeitaufwand aktualisieren und Entwicklungsprozesse wie auf dem Desktop durchführen.  

Die folgenden Aspekte sind bei Desktop Sync zu beachten: 
* Desktop Sync wird auf diesen Betriebssystemen ausgeführt: 
  * Windows 7 oder 8
  * Mac OS X ab Version 10.9
      **Hinweis:** Für Windows ist .NET Framework Version 4.5 erforderlich. Wenn .NET nicht installiert ist, werden Sie bei der Installation des {{site.data.keyword.Bluemix_notm}} Live Sync-Befehlszeilenschnittstelle (CLI) dazu aufgefordert, .NET zu installieren.
  
* Das Git-Repository muss nicht geklont werden. 
* Unabhängig von dem Anwendungstyp, den Sie entwickeln, können Sie das Desktop-Projekt mit dem Cloud-Arbeitsbereich synchronisieren.  
* Wenn die Anwendung in Node.js geschrieben wurde, können Sie Änderungen an aktive Anwendungen weitergeben. 

Weitere Details zu den Befehlen finden Sie in der [Dokumentation zur Bluemix Live Sync-Befehlszeilenschnittstelle](../cli/reference/bl/index.html).  

<ol>
<li>Laden Sie die Befehlszeile 'bl' für {{site.data.keyword.Bluemix_notm}} Live Sync herunter und installieren Sie sie.    
<p>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/blive_setup.msi" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)"><img class="image" src="images/bl_gs_icons_windows_b.svg" alt="Schaltfläche zum Herunterladen der Windows-Befehlszeile 'bl'" /> </a>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/BluemixLive.pkg" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)"><img class="image" src="images/bl_gs_icons_mac-osx_b.svg" alt="Schaltfläche zum Herunterladen der Mac-Befehlszeile 'bl'" /> </a>
</p>  

<strong>Wichtig:</strong> Das Befehlszeilentool 'bl' ist nur für Windows 7 und 8
sowie für Mac OS X ab Version 10.9 verfügbar. </li>
<li>Melden Sie sich in einer Befehlszeile mit dem folgenden Befehl an. Sie werden zur Eingabe Ihrer IBM ID und des entsprechenden Kennworts aufgefordert.   
<pre class="codeblock">bl login</pre>
</li>

<li>Zeigen Sie die Liste der für die {{site.data.keyword.Bluemix_notm}} Live Sync-Synchronisation verfügbaren Projekte an, indem Sie den folgenden Befehl eingeben: <pre class="codeblock">bl projects</pre>
<p>Suchen Sie in der Liste nach dem Projektnamen, der Ihrer Anwendung entspricht. Der Projektname weist das Format <i>Alias</i> | <i>Anwendungsname</i> auf.
</p>
</li>
<li>Synchronisieren Sie die lokale Umgebung mit dem Projekt in {{site.data.keyword.Bluemix_notm}}, indem Sie den folgenden Befehl eingeben. Wenn Sie der Eigner des Projekts sind, müssen Sie für 'projectName' nur den Namen Ihrer eigenen Anwendung angeben. <pre class="codeblock">bl sync projectName -d localDirectory --verbose</pre>
<p>Dieser Befehl (und die Synchronisation) wird solange ausgeführt, bis Sie ein 'q' eingeben. Mit der Option '--verbose' werden die Protokollierungs- und Statusinformationen angezeigt. Wenn eines der Argumente ein Leerzeichen enthält, müssen Sie den Namen in Anführungszeichen setzen. </p></li>
<li>Stellen Sie in einem weiteren Befehlszeilenfenster in Ihrem lokalen Verzeichnis die Anwendung für {{site.data.keyword.Bluemix_notm}} im Live Edit-Modus bereit, indem Sie den folgenden Befehl eingeben: <pre class="codeblock">bl start</pre>
</li>
</ol>

Wenn Sie die Dateien in Ihrem lokalen Verzeichnis ändern, werden die Änderungen automatisch in der aktiven Anwendung in {{site.data.keyword.Bluemix_notm}} und im Cloud-Arbeitsbereich des Projekts bereitgestellt. Wenn Sie die Node-Anwendung erneut starten müssen, können Sie den folgenden Befehl verwenden: ```
bl start --restart 
```

##Live Edit {: #live-edit} 

Wenn Sie eine Node.js-Anwendung erstellen, können Sie beim Vornehmen von Änderungen am Projekt mit der Web-IDE das Live Edit-Feature von {{site.data.keyword.Bluemix_notm}} Live Sync dazu verwenden, die aktive Anwendungsinstanz in {{site.data.keyword.Bluemix_notm}} ohne großen Zeitaufwand zu aktualisieren.
Mit Live Edit können Sie Entwicklungsprozesse wie auf dem Desktop durchführen, ohne dass eine erneute Bereitstellung erforderlich ist.  

Live Edit wird nur für Node.js-Anwendungen unterstützt. 

Klicken Sie in der Web-IDE in der Ausführungsleiste auf **Live Edit**. 

![Abbildung der Ausführungsleiste mit Live Edit](images/run-bar-live-edit.png) 

Mit Live Edit können Sie schnell Änderungen an in {{site.data.keyword.Bluemix_notm}} ausgeführten Node.js-Anwendungen als Vorschau anzeigen. Wenn Sie den Code bei aktiviertem Live Edit-Feature aktualisieren, können Sie das Browserfenster Ihrer Webanwendung aktualisieren, um diese Änderungen Sekunden nach deren Durchsetzung anzeigen zu lassen.  

Ein Lernprogramm zur Verwendung des Live Edit-Features von {{site.data.keyword.Bluemix_notm}} Live Sync finden Sie im [Lernprogramm zum Testen
und Debuggen einer Node.js-App mit Bluemix Live Sync](https://hub.jazz.net/tutorials/livesync). 

Wenn Sie die Dateien in der Web-IDE ändern, werden sie automatisch erneut für die aktive Anwendung in {{site.data.keyword.Bluemix_notm}} bereitgestellt.
Wenn Sie die Node-Anwendung erneut starten müssen, können Sie die Schaltfläche **Erneut starten** in der Ausführungsleiste verwenden. 

##{{site.data.keyword.Bluemix_notm}} Live Debug {: #live-debug}

Sie haben Zugriff auf das Debug-Feature von {{site.data.keyword.Bluemix_notm}} Live
Sync, wenn {{site.data.keyword.Bluemix_notm}} Live Sync für
Ihre Node.js-App aktiviert ist.  

Mit dem Debug-Feature können Sie Code dynamisch bearbeiten, Unterbrechungspunkte einfügen, Code
schrittweise durchgehen, die Laufzeit erneut starten und weitere Aktionen durchführen, während Ihre App
von {{site.data.keyword.Bluemix_notm}} bereitgestellt wird. Sie können Ihre App
schrittweise flexibel entwickeln und haben dabei die Möglichkeit, in der umfangreichen
Liste der {{site.data.keyword.Bluemix_notm}}-Services Ihre Auswahl zu treffen.  

{{site.data.keyword.Bluemix_notm}} Live
Debug enthält die folgenden Features: 

* Anwendungslaufzeitsteuerung
* Debug mit [node-inspector](https://github.com/node-inspector/node-inspector) 
* Shellzugriff 

###Anwendungslaufzeitsteuerung{: #app-runtime} 

Mit der Anwendungslaufzeitsteuerung können Sie mithilfe des Debug-Features den Status der App zur Startzeit überprüfen. Diese Funktion ist nützlich, wenn Sie für eine App, die beim Start fehlschlägt,
Fehlerbehebungsmaßnahmen durchführen.


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

###Eine App zur Aktivierung von {{site.data.keyword.Bluemix_notm}} Live Debug konfigurieren{: #configure_app_debug} 

Die App muss das IBM SDK for Node.js-Buildpack verwenden. Angepasste Buildpacks werden nicht unterstützt. 

1. Lassen Sie zu, dass das Buildpack den App-Startbefehl erkennt. Der Startbefehl muss vom Buildpack automatisch erkannt werden, er darf nicht in der
Datei `manifest.yml` festgelegt werden.
  
    
    a. Stellen Sie sicher, dass die Datei `package.json` ein Startscript
enthält, das einen Startbefehl für die App beinhaltet.
  
    b. Wenn die App-Datei `manifest.yml` einen Befehl enthält, setzen Sie diesen auf null.  

2. Legen Sie die Umgebungsvariable fest.  
    
    a. Fügen Sie in der Datei `manifest.yml` diese Variable hinzu:
	```
	env:
      ENABLE_BLUEMIX_DEV_MODE: "true" 
	```

3. Erhöhen Sie die Speichermenge.  
    
    a. Fügen Sie in der App-Datei `manifest.yml` 128 M oder mehr zu dem Wert hinzu,
der für das Speicherattribut angegeben ist.
 
	
Nach der Installation von {{site.data.keyword.Bluemix_notm}} Live Debug können Sie die Debug-Tools verwenden. 

Stellen Sie die App per Push-Operation bereit und rufen Sie dann `https://app-host.mybluemix.net/bluemix-debug/manage` auf, um auf die Benutzerschnittstelle des {{site.data.keyword.Bluemix_notm}}-Debug-Features zuzugreifen.
Wenn Sie dazu aufgefordert werden, geben Sie zur Authentifizierung Ihre IBM ID und das zugehörige Kennwort ein.
 

###App-Konfigurationen wiederherstellen und Bluemix Live Debug inaktivieren{: #restore_live_debug} 

1. Entfernen Sie die Umgebungsvariable ENABLE_BLUEMIX_DEV_MODE aus der App-Datei `manifest.yml`.


2. Stellen Sie den ursprünglichen Startbefehl und Speicherwert der App wieder her. 

3. Stellen Sie die App per Push-Operation bereit.


># Zugehörige Links{:class="linklist"}
>## Lerntexte und Beispiele{:id="samples"}
>* [Testen und Debuggen einer Node.js-App mit Bluemix Live Sync](https://hub.jazz.net/tutorials/livesync)
>
># Zugehörige Links{:class="linklist"}
>## Zugehörige Links{:id="general"}
>* [bl-Befehle](https://www.ng.bluemix.net/docs/cli/bl_cli.html)   
>
>{:elementKind="article" id="rellinks"}
