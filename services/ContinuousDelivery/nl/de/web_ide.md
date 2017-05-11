---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-31"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Code mit der IDE für Eclipse Orion bearbeiten
{: #web_ide}

Die Eclipse Orion-{{site.data.keyword.webide}} ist eine browserbasierte Entwicklungsumgebung, in der Sie Anwendungen für das Web entwickeln können. Für die Entwicklung in JavaScript, HTML und CSS stehen Content-Assist-Funktionen, Codevervollständigung und Fehlerprüfung zur Verfügung. Die {{site.data.keyword.webide}} ist mit nahezu jeder Programmiersprache verwendbar und bietet Syntaxhervorhebung für die meisten Dateitypen. Die Quellcodeverwaltung ist integriert und Sie können Code lokal bereitstellen, um Ihre Apps zu testen und zu debuggen.
{:shortdesc}

Als weiterer wesentlicher Vorteil kommt hinzu, dass {{site.data.keyword.webide}} auf der Webtechnologie basiert. Es entsteht keinerlei Installations-, Wartungs- und Skalierungsaufwand. Für die Codeentwicklung benötigen Sie lediglich einen Internetanschluss.

## Editor einrichten
{: #editorsetup}

Die {{site.data.keyword.webide}} ist konfigurierbar, d. h. Sie können Farbschemen, technische Tools und Einstellungen wählen, die Ihren Entwicklungsanforderungen entsprechen. Um die Einstellungen anzuzeigen und zu ändern, klicken Sie links im Menü auf das Symbol **Einstellungen** <img class="inline" src="images/webide_settings_icon_light_small.png"  alt="Symbol 'Einstellungen'">.

Wenn Sie bestimmte Einstellungen beim Bearbeiten häufig ändern müssen, können Sie auf diese Einstellungen schnell über das Symbol **Lokale Einstellungen für Editor** <img class="inline" src="images/webide_local_settings_icon_light_small.png"  alt="Symbol 'Lokale Einstellungen für Editor"> zugreifen. 

![Lokale Einstellungen für Editor](images/webide_local_editor_settings_light.png)

Standardmäßig werden die Einstellungen für den Editorstil und die Schriftgröße immer angezeigt. Führen Sie die folgenden Schritte aus, um weitere Einstellungen in das Menü aufzunehmen:

1. Klicken Sie auf das Symbol **Lokale Einstellungen für Editor** icon <img class="inline" src="images/webide_local_settings_icon_light_small.png"  alt="Symbol 'Lokale Einstellungen für Editor'">.

2. Klicken Sie auf **Editoreinstellungen**.

3. Um eine Einstellung in das Menü **Lokale Einstellungen für Editor** aufzunehmen oder aus diesem zu entfernen, klicken Sie jeweils auf den Stern neben der betreffenden Einstellung.

![Umschalter für Editoreinstellungen](images/webide_editor_settings_toggle_light.png)


## Code bearbeiten
{: #editcode}

Die {{site.data.keyword.webide}} setzt sich aus zwei Hauptabschnitten zusammen. Der erste Abschnitt ist der Dateinavigator, der Ihre Projektdateien in einer Baumstruktur anzeigt. Über den Dateinavigator können Sie Dateien und Ordner erstellen, umbenennen, löschen und verwalten.

**Tipp:** Um Dateien in den Dateinavigator hochzuladen, ziehen Sie sie von Ihrem Computer in den Dateinavigator.

Der zweite Abschnitt ist das Editorteilfenster. Der Editor bietet verschiedene Codierungsfunktionen, einschließlich Content-Assist und Syntaxprüfung.

![Web-IDE](images/webide_light.png)

### Mit mehreren Dateien arbeiten
1. Um mit zwei Dateien gleichzeitig zu arbeiten, klicken Sie auf das Symbol **Teilungsmodus des Editors ändern** <img class="inline" src="images/webide_split_editor_icon_light_small.png"  alt="Symbol 'Geteilter Editor'">. 
2. Wählen Sie in dem geöffneten Menü eine Ansicht aus.

 Wenn bereits eine Datei im Editor geöffnet war, wird sie nach Auswahl einer Ansicht in beiden Editoransichten angezeigt.

 Gehen Sie wie folgt vor, um eine Datei, die in einer der Editoransichten angezeigt wird, zu öffnen oder zu ändern:
 1. Bewegen Sie den Cursor zu der Editoransicht, die Sie ändern wollen.
 2. Klicken Sie im Dateinavigator auf eine Datei.

### Tastenkombinationen
Die meisten Befehle in der {{site.data.keyword.webide}} können nur über die Tastatur ausgeführt werden.

Verwenden Sie die Tastenkombination Alt+Umschalttaste+?, um eine Liste mit den Tastenbelegungen anzuzeigen. Wenn Sie Mac OS verwenden, lautet die Tastenkombination Strg+Umschalttaste+?.

## Quellcode verwalten
{: #sourcecontrol}

Die {{site.data.keyword.webide}} ist mit Quellcodeverwaltungstools integriert. Um mit dem Git-Repository zu arbeiten, klicken Sie auf das Symbol **Git-Repository** <img class="inline" src="images/webide_git_icon_light_small.png"  alt="Symbol 'Git-Repository'">. 

 **Tipp**: Wenn Sie die {{site.data.keyword.webide}} in Verbindung mit offenen Toolchains verwenden, werden in Ihrem Arbeitsbereich bereits Ihre GitHub-, {{site.data.keyword.ghe_short}}- oder Git Repos and Issue Tracking-Repositorys angezeigt. Die Repositorys, die Ihrer aktuellen Toolchain zugeordnet sind, sind hervorgehoben.


## App vom Arbeitsbereich aus bereitstellen
{: #deploy}

1. Um die App bereitzustellen, wählen Sie in der Ausführungsleiste entweder eine Startkonfiguration aus oder erstellen Sie ein solche. 
1. Klicken Sie auf das Symbol für die Bereitstellung <img class="inline" src="images/webide_deploy_button_light_small.png"  alt="Symbol 'Bereitstellung'">. Bei der Bereitstellung einer Instanz Ihrer App werden der aktuelle Inhalt Ihres Arbeitsbereichs und die Umgebung verwendet, die in Ihrer Startkonfiguration definiert sind. 
2. Wenn Ihre App bereitgestellt wurde, können Sie die Ausführungsleiste verwenden, um Ihre App zu stoppen, erneut zu starten oder zu debuggen, um Protokolle anzuzeigen usw.
![Ausführungsleiste](images/webide_runbar_light.png)    

<!-- 3/6/2016: bl commands don't work with V2/CD 
## Editing outside of the {{site.data.keyword.webide}}
{: #editlocal}

To use an editor besides the {{site.data.keyword.webide}}, set up {{site.data.keyword.Bluemix_live}} so that you can work directly with your project files in any tool. {{site.data.keyword.Bluemix_live_notm}} is a command-line application that synchronizes the changes in your local file system with your cloud workspace in {{site.data.keyword.jazzhub}}. 

### Before you begin 

Download and install the [{{site.data.keyword.Bluemix_live_notm}} command-line interface![External link icon](../../icons/launch-glyph.svg "External link icon")](http://livesyncdownload.ng.bluemix.net){: new_window}.

### Synchronizing your local environment with {{site.data.keyword.Bluemix_notm}}
{: #edit_local_download}

1. Open a command-line window.
2. Sign in to {{site.data.keyword.Bluemix_notm}}:

	```
	bl login
	```
	{: pre}

3. When you are prompted, enter your IBMid and password.
4. View a list of your {{site.data.keyword.Bluemix_notm}} projects: 

	```
	bl projects
	```
	{: pre}

4. Synchronize your local environment with your project on {{site.data.keyword.Bluemix_notm}}:

	```
	bl sync projectName
	```
	{: pre}

where `projectName` is your {{site.data.keyword.Bluemix_notm}} app's name.

When you are finished editing, enter `q` to end synchronization.

### Enabling the Desktop Sync feature to edit code locally

The Desktop Sync feature is like Live Edit mode for the command line. You need the Desktop Sync feature to debug on the command line.
1. In another command-line window, enable the Desktop Sync feature:

	```
	cd localDirectory
	bl start
	```
	{: codeblock}

2. Use the launch configuration that you created in the {{site.data.keyword.webide}}. After you select the launch configuration, the Desktop Sync feature is enabled in your local environment. In the command-line window that you just opened, you can view the app's URL, the debug URL, the manage URL, and view the {{site.data.keyword.Bluemix_live_notm}} state.

3. Refresh the browser and verify that you can see the changes that you saved to static files in the local workspace. 

### Disabling the Desktop Sync feature

1. In the second command-line window, enter `bl stop`.
2. In the first command-line window, enter `q`.

--> 
