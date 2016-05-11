---



copyright:

  years: 2015, 2016



---
{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}

#{{site.data.keyword.Bluemix_notm}} Live Sync {: #live-sync}

*Letzte Aktualisierung: 8. April 2016*  

Wenn Sie eine Node.js-Anwendung erstellen, können Sie {{site.data.keyword.Bluemix}} Live Sync dazu verwenden, die Anwendungsinstanz ohne großen Zeitaufwand in {{site.data.keyword.Bluemix_notm}} zu aktualisieren und Entwicklungsprozesse wie auf dem Desktop durchzuführen, ohne dass eine erneute Bereitstellung erforderlich ist.   
{: shortdesc}

Wenn Sie eine Änderung vornehmen, ist diese Änderung sofort in der aktiven {{site.data.keyword.Bluemix_notm}}-Anwendung sichtbar. {{site.data.keyword.Bluemix_notm}} Live Sync kann sowohl über die Befehlszeile als auch über die Web-IDE ausgeführt werden. Sie können in Node.js geschriebene Anwendungen mithilfe von {{site.data.keyword.Bluemix_notm}} Live Sync debuggen.  

{{site.data.keyword.Bluemix_notm}} Live Sync setzt sich aus drei Features zusammen.

**Desktop Sync**  
    Sie können jede beliebige Desktop-Verzeichnisbaumstruktur in ähnlicher Weise wie mit Dropbox mit einem cloudbasierten Projektarbeitsbereich synchronisieren. Die Web-IDE bearbeitet direkt denselben cloudbasierten Arbeitsbereich, so bleiben beide synchron. Desktop Sync kann für alle Anwendungstypen verwendet werden. Für die Verwendung von Desktop Sync müssen Sie die Befehlszeilenschnittstelle 'bl' herunterladen und installieren.  

**Live Edit**
    Sie können Änderungen an einer in {{site.data.keyword.Bluemix_notm}} ausgeführten Node.js-Anwendung vornehmen und diese sofort in Ihrem Browser testen. Alle Änderungen in einem synchronisierten Desktop-Verzeichnis oder in der Web-IDE werden umgehend an das Dateisystem der Anwendung weitergegeben.  

**Debug**  
    Wenn sich eine Node.js-Anwendung im Live Edit-Modus befindet, können Sie einen Shellzugriff einrichten und die Anwendung debuggen. Sie können Code dynamisch bearbeiten, Unterbrechnungspunkte einfügen, Code schrittweise durchgehen, die Laufzeit erneut starten und weitere Aktionen mit dem Node Inspector-Debugger durchführen.  

Mit Desktop Sync können Sie den Desktop-Arbeitsbereich mit dem cloudbasierten Projektarbeitsbereich synchron halten, den Sie direkt mit der Web-IDE bearbeiten. Mit Live Edit können Sie Änderungen am cloudbasierten Projektarbeitsbereich an die aktive Anwendung weitergeben. Sie können eines oder beide dieser Features verwenden. Wenn Sie mit Desktop Sync oder Live Edit die Anwendung in den Live Edit-Modus versetzen, können Sie die aktive Anwendung auch debuggen.

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

Weitere Details zu den Befehlen finden Sie unter [Bluemix Live Sync-Befehle (bl)](bluemixlive.html#bl-commands).

<ol>
<li>Melden Sie sich für ein kostenloses Konto für <a class="xref" href="https://hub.jazz.net/" target="_blank" alt="Bluemix DevOps Services">Bluemix DevOps Services</a> an.</li>
<li>Laden Sie die Befehlszeile 'bl' für {{site.data.keyword.Bluemix_notm}} Live Sync herunter und installieren Sie sie.   
<p>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/blive_setup.msi" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)"><img class="image" src="images/bl_gs_icons_windows_b.svg" alt="Schaltfläche zum Herunterladen der Windows-Befehlszeile 'bl'" /> </a>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/BluemixLive.pkg" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)"><img class="image" src="images/bl_gs_icons_mac-osx_b.svg" alt="Schaltfläche zum Herunterladen der Mac-Befehlszeile 'bl'" /> </a>
</p>  

<strong>Wichtig:</strong> Das Befehlszeilentool 'bl' ist nur für Windows 7 und 8 sowie für Mac OS X ab Version 10.9 verfügbar. </li>

<li>Melden Sie sich in einer Befehlszeile mit dem folgenden Befehl an. Sie werden zur Eingabe Ihrer IBM ID und des entsprechenden Kennworts aufgefordert.  
<pre class="codeblock">bl login</pre>
</li>

<li>Zeigen Sie die Liste der für die {{site.data.keyword.Bluemix_notm}} Live Sync-Synchronisation verfügbaren Projekte an, indem Sie den folgenden Befehl eingeben:
<pre class="codeblock">bl projects</pre>
<p>Suchen Sie in der Liste nach dem Projektnamen, der Ihrer Anwendung entspricht. Der Projektname weist das Format <i>Alias</i> | <i>Anwendungsname</i> auf. </p>
</li>
<li>Synchronisieren Sie die lokale Umgebung mit dem Projekt in {{site.data.keyword.Bluemix_notm}}, indem Sie den folgenden Befehl eingeben. Wenn Sie der Eigner des Projekts sind, müssen Sie für 'projectName' nur den Namen Ihrer eigenen Anwendung angeben.
<pre class="codeblock">bl sync projectName -d localDirectory --verbose</pre>
<p>Dieser Befehl (und die Synchronisation) wird solange ausgeführt, bis Sie ein 'q' eingeben. Mit der Option '--verbose' werden die Protokollierungs- und Statusinformationen angezeigt. Wenn eines der Argumente ein Leerzeichen enthält, müssen Sie den Namen in Anführungszeichen setzen. </p></li>
<li>Stellen Sie in einem weiteren Befehlszeilenfenster in Ihrem lokalen Verzeichnis die Anwendung für {{site.data.keyword.Bluemix_notm}} im Live Edit-Modus bereit, indem Sie den folgenden Befehl eingeben:
<pre class="codeblock">bl start</pre>
</li>
</ol>

Wenn Sie die Dateien in Ihrem lokalen Verzeichnis ändern, werden die Änderungen automatisch in der aktiven Anwendung in {{site.data.keyword.Bluemix_notm}} und im Cloud-Arbeitsbereich des Projekts bereitgestellt. Wenn Sie die Node-Anwendung erneut starten müssen, können Sie den folgenden Befehl verwenden:
```
bl start --restart
```

##Live Edit {: #live-edit}

Wenn Sie eine Node.js-Anwendung erstellen, können Sie beim Vornehmen von Änderungen am Projekt mit der Web-IDE das Live Edit-Feature von {{site.data.keyword.Bluemix_notm}} Live Sync dazu verwenden, die aktive Anwendungsinstanz in {{site.data.keyword.Bluemix_notm}} ohne großen Zeitaufwand zu aktualisieren. Mit Live Edit können Sie Entwicklungsprozesse wie auf dem Desktop durchführen, ohne dass eine erneute Bereitstellung erforderlich ist.

Live Edit wird nur für Node.js-Anwendungen unterstützt.

Klicken Sie in der Web-IDE in der Ausführungsleiste auf **Live Edit**.

![Abbildung der Ausführungsleiste mit Live Edit](images/run-bar-live-edit.png)

Mit Live Edit können Sie schnell Änderungen an in {{site.data.keyword.Bluemix_notm}} ausgeführten Node.js-Anwendungen als Vorschau anzeigen. Wenn Sie den Code bei aktiviertem Live Edit-Feature aktualisieren, können Sie das Browserfenster Ihrer Webanwendung aktualisieren, um diese Änderungen Sekunden nach deren Durchsetzung anzeigen zu lassen.

Ein Lernprogramm zur Verwendung des Live Edit-Features von {{site.data.keyword.Bluemix_notm}} Live Sync finden Sie im [Lernprogramm zum Testen und Debuggen einer Node.js-App mit Bluemix Live Sync](https://hub.jazz.net/tutorials/livesync).

Wenn Sie die Dateien in der Web-IDE ändern, werden sie automatisch erneut für die aktive Anwendung in {{site.data.keyword.Bluemix_notm}} bereitgestellt. Wenn Sie die Node-Anwendung erneut starten müssen, können Sie die Schaltfläche **Erneut starten** in der Ausführungsleiste verwenden.

**Hinweis:** Für eine möglichst konsistente Verarbeitungsleistung der Funktion 'Live Edit' von {{site.data.keyword.Bluemix_notm}} Live Sync, ist eine zusätzliche Hauptspeicherkapazität von 256 MB erforderlich und wird hinzugefügt.

##{{site.data.keyword.Bluemix_notm}} Live Debug {: #live-debug}

Sie haben Zugriff auf das Debug-Feature von {{site.data.keyword.Bluemix_notm}} Live Sync, wenn {{site.data.keyword.Bluemix_notm}} Live Sync für Ihre Node.js-App aktiviert ist.

Mit dem Debug-Feature können Sie Code dynamisch bearbeiten, Unterbrechungspunkte einfügen, Code schrittweise durchgehen, die Laufzeit erneut starten und weitere Aktionen durchführen, während Ihre App von {{site.data.keyword.Bluemix_notm}} bereitgestellt wird. Sie können Ihre App schrittweise flexibel entwickeln und haben dabei die Möglichkeit, in der umfangreichen Liste der {{site.data.keyword.Bluemix_notm}}-Services Ihre Auswahl zu treffen.

{{site.data.keyword.Bluemix_notm}} Live Debug enthält die folgenden Features:

* Anwendungslaufzeitsteuerung
* Debug mit [node-inspector](https://github.com/node-inspector/node-inspector)
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

Stellen Sie die App per Push-Operation bereit und rufen Sie dann `https://app-host.mybluemix.net/bluemix-debug/manage` auf, um auf die Benutzerschnittstelle des {{site.data.keyword.Bluemix_notm}}-Debug-Features zuzugreifen. Wenn Sie dazu aufgefordert werden, geben Sie zur Authentifizierung Ihre IBM ID und das zugehörige Kennwort ein.

###App-Konfigurationen wiederherstellen und Bluemix Live Debug inaktivieren {: #restore_live_debug}

1. Entfernen Sie die Umgebungsvariable ENABLE_BLUEMIX_DEV_MODE aus der App-Datei `manifest.yml`.

2. Stellen Sie den ursprünglichen Startbefehl und Speicherwert der App wieder her.

3. Stellen Sie die App per Push-Operation bereit.

## {{site.data.keyword.Bluemix_notm}} Live Sync-Befehle (bl)  {: #bl-commands}

Wenn Sie eine Node.js-Anwendung erstellen, können Sie {{site.data.keyword.Bluemix_live}} dazu verwenden, die Anwendungsinstanz ohne großen Zeitaufwand in {{site.data.keyword.Bluemix_notm}} zu aktualisieren und Entwicklungsprozesse wie auf dem Desktop durchzuführen, ohne dass eine erneute Bereitstellung erforderlich ist. Wenn Sie eine Änderung vornehmen, ist diese Änderung sofort in der aktiven {{site.data.keyword.Bluemix_notm}}-Anwendung sichtbar. Die {{site.data.keyword.Bluemix_live}}-Befehlszeilenschnittstelle von Bluemix heißt *bl*.
{:shortdesc}

Mithilfe der Befehle der **bl**-Befehlszeilenschnittstelle können Sie die folgenden Aufgaben ausführen:

* Eine in {{site.data.keyword.Bluemix_notm}} ausgeführte Anwendung starten und stoppen.
* Ein neues cloudbasiertes Projekt über den Desktop erstellen.
* Änderungen auf dem Desktop mit dem cloudbasierten Projektarbeitsbereich und der aktiven Anwendung in {{site.data.keyword.Bluemix_notm}} synchronisieren.
* Die Liste der Projekte anzeigen, die für die Synchronisation verfügbar sind.
* Den Status von aktiven Anwendungen anzeigen.

Weitere Informationen zum Herunterladen und Verwenden des Befehls 'bl' finden Sie in der Veröffentlichung [Bluemix Live Sync](../develop/bluemixlive.html).

## bl-Befehle

Die {{site.data.keyword.Bluemix_live}}-Befehlszeile **bl** hat die folgende Syntax:

```
bl Befehl [Argumente][options] [--help]
```

### Befehle
<dl>
<dt>login, l</dt>
<dd>Anmeldung bei {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>logout, lo</dt>
<dd>Abmeldung des Benutzers.</dd>
<dt>sync, s</dt>
<dd>Synchronisationsprozess zwischen Desktop und Server starten.</dd>
<dt>create, c</dt>
<dd>Privates Projekt erstellen, mit dem Git-Repository in diesem Verzeichnis verknüpfen und den Inhalt in {{site.data.keyword.Bluemix_notm}} bereitstellen.</dd>
<dt>projects, p</dt>
<dd>Alle für die Synchronisation verfügbaren Projekte auflisten.</dd>
<dt>start, st</dt>
<dd>Anwendungsinstanz in {{site.data.keyword.Bluemix_notm}} starten.</dd>
<dt>stop, sp</dt>
<dd>Anwendungsinstanz in {{site.data.keyword.Bluemix_notm}} stoppen.</dd>
<dt>status, ss</dt>
<dd>Status der aktiven Anwendungsinstanz in {{site.data.keyword.Bluemix_notm}} auflisten.</dd>
</dl>

### Argumente
<dl>
<dd>Argumente für den Befehl.</dd>
</dl>

### Optionen
<dl>
<dd>Optionen für den Befehl.</dd>
</dl>

### Globale Optionen
<dl>
<dt>--help</dt>
<dd>Hilfetextseite für den angegebenen Befehl anzeigen.</dd>
<dt>--verbose</dt>
<dd>Ausführliche Protokollierung aktivieren.</dd>
</dl>

**Hinweis:** Wenn ein Argument oder eine Option ein Leerzeichen enthält, schließen Sie den Wert in doppelte Anführungszeichen ein.

## help

```
bl [ Befehl ] --help
```

### Verwendung
<dl>
<dd>Verwenden Sie diesen Befehl, um Hilfetext zu einem Befehl oder zur Befehlsliste anzuzeigen.</dd>
</dl>

### Beispiele

Mit dem folgenden Befehl wird die Liste der Befehle angezeigt:

```bl --help```

Mit dem folgenden Befehl werden detaillierte Informationen zum Befehl sync angezeigt:

```bl sync --help```

## login

```bl login|l [ -u username ][-p password ][ -s server ]```

### Zweck

Verwenden Sie diesen Befehl für die Anmeldung bei {{site.data.keyword.Bluemix_notm}}. Die Anmeldung muss nur einmal pro Sitzung erfolgen.

**Warnung:** Geben Sie Ihr Kennwort nicht als Befehlszeilenoption an, weil es auf diese Weise für andere sichtbar ist und als Teil Ihres Befehlsprotokolls aufgezeichnet wird.

**Hinweis:** Sie müssen sich für ein kostenloses Konto für <a class="xref" href="https://hub.jazz.net/" target="_blank" alt="Bluemix DevOps Services">Bluemix DevOps Services</a> registrieren, bevor Sie sich anmelden.

### Optionen

<dl>
<dt>-u username</dt>
<dd>Ihre IBM ID für die Anmeldung bei {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>-p password</dt>
<dd>Das zugehörige Kennwort zu Ihrer IBM ID.</dd>
<dt>-s server</dt>
<dd>Servername oder IP-Adresse des {{site.data.keyword.jazzhub_short}}-Servers.</dd>
</dl>

### Beispiele

Der folgende Befehl fordert zur Eingabe von *Benutzername* und *Kennwort* auf:

```bl login```

Mithilfe des folgenden Befehls wird der Benutzer `name@company.com` angemeldet:

```bl login –u name@company.com –p pa55w0rd```

Mithilfe des folgenden Befehls wird der Benutzer `name@company.com` mit dem Kennwort pa55 w0rd angemeldet. Das Kennwort enthält ein Leerzeichen und muss daher in Anführungszeichen gesetzt werden:

```bl login –u name@company.com –p “pa55 w0rd”```

## logout

```
bl logout|lo
```

### Zweck

<dl>
<dd>Verwenden Sie diesen Befehl zum Abmelden.</dd>
</dl>

## Projekte

```
bl projects|p
```

### Zweck

<dl>
<dd>Verwenden Sie diesen Befehl, um alle Projekte aufzulisten, die für die Synchronisation durch den angemeldeten Benutzer verfügbar sind.</dd>
</dl>

## sync

```
bl sync|s projectName -d localDirectory [ --overwritelocal ][ --overwriteremote ] [ --verbose ]
```

### Zweck

<dl>
<dd>Verwenden Sie diesen Befehl, um die Synchronisation des Inhalts eines Projekts mit Ihrem lokalen Verzeichnis zu starten. Dieser Befehl wird ausgeführt, bis ein <code>q</code> eingegeben wird. Der Befehl kann optional ein Protokoll aller Datei- und Anwendungsstatusänderungen anzeigen.</dd>
</dl>

### Argument

<dl>
<dt>projectName</dt>
<dd>Der Projektname im Format <i>“alias | myproject”</i> oder nur <i>myproject</i>, wenn der angemeldete Benutzer der Eigner des Projekts ist.</dd>
</dl>

### Optionen

<dl>
<dt>-d localDirectory</dt>
<dd>Pfad des lokalen Verzeichnisses. Ist standardmäßig der aktuelle Ordner ".".</dd>
<dt>--overwritelocal</dt>
<dd>Lokales Verzeichnis mit Inhalten des Projektarbeitsbereichs überschreiben.</dd>
<dt>--overwriteremote</dt>
<dd>Projektarbeitsbereich mit den Inhalten des lokalen Verzeichnisses überschreiben.</dd>
<dt>--verbose</dt>
<dd>Ausführliche Protokollierung anzeigen.</dd>
</dl>

### Beispiele

Der folgende Befehl beginnt mit der Synchronisation mit dem zugeordneten Projekt, wenn das aktuelle Verzeichnis ein vorhandenes Synchronisationsziel ist. Wenn das aktuelle Verzeichnis leer und kein vorhandenes Synchronisationsziel ist, fordert der Befehl zur Eingabe eines Projektnamens (*projectName*) auf. Wenn das aktuelle Verzeichnis nicht leer und kein vorhandenes Synchronisationsziel ist, ist eine Option zum Überschreiben erforderlich.

```
bl sync
```

Der folgende Befehl startet die Synchronisation und ist äquivalent zu diesem Befehl:
```bl sync “alias | myproject”```
Dies setzt voraus, dass der angemeldete Benutzer der Eigner des Projekts ist.

```bl sync  myproject```

Der folgende Befehl startet die Synchronisation mit dem Projekt <code>my pro ject</code>, dessen Name Leerzeichen enthält und daher in Anführungszeichen gesetzt ist:

```bl sync “my pro ject”```

Der folgende Befehl startet die Synchronisation des Projekts <code>myproject</code> mit dem Verzeichnis myfolder:

```bl sync myproject –d  myfolder```

## create

```
bl create|c [ -n PROJECT_NAME ][ -r REGION ] [ -o ORG ][ -s SPACE ] [ -g GIT_REPO ][-e GIT_EXE ] [ --creds ][ --fork ] [ --public ][ --prompt ]
```

### Zweck
<dl>
<dd>Mit diesem Befehl können Sie aus einem Verzeichnis mit Code ein privates Projekt erstellen, dieses mit einem Git-Repository verknüpfen und den Inhalt des Repositorys in {{site.data.keyword.Bluemix_notm}} bereitstellen.</dd>
</dl>

### Optionen

<dl>
<dt>-n PROJECT_NAME</dt>
<dd>Ein Name für das Projekt. Standardwert: Der Name des aktuellen Verzeichnisses.</dd>
<dt>-r REGION</dt>
<dd>Eine {{site.data.keyword.Bluemix_notm}}-Region. Standardwert: Vereinigte Staaten (Süden)</dd>
<dt>-o ORG</dt>
<dd>Eine {{site.data.keyword.Bluemix_notm}}-Organisation. Standardwert: Die erste Organisation, die gefunden wird.</dd>
<dt>-s SPACE</dt>
<dd>Ein {{site.data.keyword.Bluemix_notm}}-Bereich. Standardwert: Der erste Bereich, der gefunden wird.</dd>
<dt>-g GIT_REPO</dt>
<dd>Der Name des fernen Repositorys zur Verwendung für sämtliche vorhandenen Git-Repositorys. Standardwert: 'origin'.</dd>
<dt>-e GIT_EXE</dt>
<dd>Der vollständige Pfad zu einer ausführbaren Git-Datei. Standardwert: 'detected'.</dd>
<dt>--creds</dt>
<dd>Die Eingabeaufforderung für Ihre Git-Berechtigungsnachweise.</dd>
<dt>--fork</dt>
<dd>Verzweigung für dieses Verzeichnis sowie ein Projekt und ein Repositiory erstellen.</dd>
<dt>--public</dt>
<dd>Das neue Projekt öffentlich zugänglich machen.</dd>
<dt>--prompt</dt>
<dd>Eingabeaufforderung für alle erforderlichen Optionen mit verfügbaren Auswahlmöglichkeiten.</dd>
</dl>

### Beispiele

Der folgende Befehl startet den Prozess der Erstellung eines privaten Projekts und fordert zur Eingabe eines zu verwendenden Projektnamens auf.

```bl create```

Der folgende Befehl erstellt ein öffentliches Projekt mit dem Namen <code>myNewProject</code>.

```bl create -n myNewProject --public```

## status

```
bl status|ss [ projectName ]
```

### Zweck

<dl>
<dd>Verwenden Sie diesen Befehl, um den Status der Anwendungen aufzulisten, die den Startkonfigurationen im Verzeichnis <code>./launchConfigurations</code> zugeordnet sind.</dd>
</dl>

###Argument

<dl>
<dt>projectName</dt>
<dd>Der Projektname im Format “alias | myproject” oder nur myproject, wenn der angemeldete Benutzer der Eigner des Projekts ist.</dd>
</dl>

### Beispiele

In diesem Beispiel wird der Status der aktiven Anwendungen angezeigt. Wenn das aktuelle Verzeichnis ein vorhandenes
Synchronisationsziel ist, wird das zugeordnete Projekt verwendet. Wenn das aktuelle Verzeichnis kein vorhandenes Synchronisationsziel ist,
fordert der Befehl zur Eingabe von <i>Projektname</i> auf.

````bl status```

Dieser Beispielbefehl zeigt den Status des Projekts 'myproject' an und ist äquivalent zu folgendem Befehl:
```bl status “alias | myproject”```
Dies setzt voraus, dass der angemeldete Benutzer der Eigner des Projekts ist.

```bl status myproject```

Dieser Beispielbefehl zeigt den Status der aktiven Anwendung an, die dem Projekt <code>my pro ject</code> zugeordnet ist, dessen Name Leerzeichen enthält und daher in Anführungszeichen gesetzt ist:

```bl status “my pro ject”```

## start

```
bl start|st projectName [ -l launchConfigPath ] -m manifestPath ] [ --liveedit ][--noliveedit ] [ --restart ]
```

### Zweck

<dl>
<dd>Verwenden Sie diesen Befehl zum Starten der Anwendungsinstanz, die von der Start- oder Manifestdatei beschrieben wird. Die Anwendung wird im Live-Bearbeitungsmodus gestartet, sofern das Buildpack der Anwendung die Live-Bearbeitung unterstützt. Nach dem Starten werden die URLs für die Anwendung, die Debug Tools und das {{site.data.keyword.Bluemix_notm}}-Dashboard angezeigt.</dd>
</dl>

### Argument

<dl>
<dt>projectName</dt>
<dd>Der Projektname im Format <i>“alias | myproject”</i> oder nur <i>myproject</i>, wenn der angemeldete Benutzer der Eigner des Projekts ist.</dd>
</dl>

### Optionen

<dl>
<dt>-l launchConfiguration</dt>
<dd>Der Name der Startkonfiguration (zum Beispiel <code>mylaunchconfig</code>), der Dateiname (zum Beispiel <code>mylaunchconfig.launch</code> oder ein projektbezogener Pfad zur Startkonfigurationsdatei (zum Beispiel <code>launchConfigurations/mylaunchconf.launch</code>).</dd>
<dt>-m manifestPath</dt>
<dd>Der projektbezogene Pfad zur Manifestdatei (zum Beispiel <code>manifest.yml</code>).</dd>
<dt>--liveedit</dt>
<dd>Die zugeordnete Anwendung im Live-Bearbeitungsmodus starten oder mit einem Fehler beenden, wenn das Buildpack den Live-Bearbeitungsmodus nicht unterstützt.</dd>
<dt>--noliveedit</dt>
<dd>Die zugeordnete Anwendung im normalen Modus starten.</dd>
<dt>--view</dt>
<dd>Einen Browser der aktiven Anwendung öffnen.</dd>
<dt>--restart</dt>
<dd>Eine bereits aktive Anwendung im Live-Bearbeitungsmodus erneut starten, ohne sie erneut zu implementieren.</dd>
</dl>

### Beispiele

Der folgende Befehl startet eine Anwendungsinstanz des Projekts <code>myproject</code>, das der Startdatei <code>launchConfigurations/my.launch</code> zugeordnet ist.

```bl start myproject –l “launchConfigurations/my.launch”```

Der folgende Befehl startet eine Anwendungsinstanz des Projekts, das dem aktuellen Verzeichnis zugeordnet ist, mit der Startdatei <code>launchConfigurations/my.launch</code>. Wenn das aktuelle Verzeichnis kein Synchronisationsziel ist, wird ein Fehler angezeigt.

```bl start –l “launchConfigurations/my.launch” ```

Der folgende Befehl startet eine Anwendungsinstanz des Projekts, das dem aktuellen Verzeichnis zugeordnet ist, mit der Manifestdatei <code>manifest.yml</code>. Die im Manifest angegebenen Informationen werden zum Erstellen einer neuen Startkonfigurationsdatei verwendet. Der Befehl fordert Sie zur Eingabe der übrigen erforderlichen Informationen auf und startet anschließend die von der Startkonfiguration beschriebene Anwendung:

```bl start –m “mymanifest.yml” ```

Der folgende Befehl startet eine Anwendungsinstanz des Projekts, das dem aktuellen Verzeichnis zugeordnet ist, mit der Manifestdatei <code>manifest.yml</code> und ist äquivalent zu folgendem Befehl:
```bl start –m manifest.yml```.

```bl start```

## stop

```
bl stop|sp projectName [ -l launchConfiguration ]
```

### Zweck

<dl>
<dd>Verwenden Sie diesen Befehl zum Stoppen der Anwendungsinstanz, die der Startdatei zugeordnet ist.</dd>
</dl>

### Argument

<dl>
<dt>projectName</dt>
<dd>Der Projektname im Format “alias | mproject” oder nur mproject, wenn der angemeldete Benutzer der Eigner des Projekts ist.</dd>
</dl>

### Optionen

<dl>
<dt>-l launchConfiguration</dt>
<dd>Der Name der Startkonfiguration (zum Beispiel <code>mylaunchconfig</code>), der Dateiname (zum Beispiel <code>mylaunchconfig.launch</code> oder ein projektbezogener Pfad zur Startkonfigurationsdatei (zum Beispiel <code>launchConfigurations/mylaunchconf.launch</code>).</dd>
</dl>

### Beispiele

Der folgende Befehl stoppt die Anwendung, wenn das aktuelle Verzeichnis ein Synchronisationsziel ist. Andernfalls wird die Anwendung mit einem Fehler beendet. Falls keine Startkonfigurationen vorhanden sind, wird dieser Befehl mit einem Fehler beendet. Sind mehrere Startkonfigurationen vorhanden, fordert der Befehl Sie zur Eingabe der zu stoppenden Startkonfiguration auf.

```bl stop```

Der folgende Befehl stoppt eine Anwendungsinstanz des Projekts, das mit der Startdatei <code>mylaunchConfig</code> ausgeführt wird.

```bl stop myproject –l “mylaunchConfig” ```

Der folgende Befehl stoppt die Anwendung, wenn das aktuelle Verzeichnis ein Synchronisationsziel des zugeordneten Projekts ist, das mit der Startdatei <code>launchConfigurations/mylaunchconfig.launch</code> gestartet wurde. Andernfalls wird der Befehl mit einem Fehler beendet.

```bl stop –l “launchConfigurations/mylaunchconfig.launch” ```  

># Zugehörige Links {:class="linklist"}
>## Lerntexte und Beispiele {:id="samples"}
>* [Testen und Debuggen einer Node.js-App mit Bluemix Live Sync](https://hub.jazz.net/tutorials/livesync)
>
># Zugehörige Links {:class="linklist"}
>## Zugehörige Links {:id="general"}
>* [IBM Eclipse Tools for Bluemix](https://www.ng.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html)   
>
>{:elementKind="article" id="rellinks"}
