---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Code mit der Eclipse Orion {{site.data.keyword.webide}} bearbeiten
{: #web_ide}

Letzte Aktualisierung: 22. Juli 2016
{: .last-updated}

Die Eclipse Orion {{site.data.keyword.webide}} ist eine browserbasierte Entwicklungsumgebung, in der Sie Inhalte für das Web entwickeln. Sie können JavaScript, HTML und CSS mithilfe von Content-Assist, Codevervollständigung und Fehlerprüfung verwenden. Die {{site.data.keyword.webide}} arbeitet mit fast allen Sprachen und bietet eine Syntaxhervorhebung [für die meisten Dateitypen](https://hub.jazz.net/docs/overview/#dev_support){: new_window}. Eine Quellcodeverwaltung ist über Git oder Jazz SCM integriert. Sie können Code lokal bereitstellen, um Ihre Apps zu testen und zu debuggen.
{:shortdesc}

Sie arbeiten mit der {{site.data.keyword.webide}} über das Internet. Es ist keine Installation, keine Wartung und keine Skalierung notwendig. Zum Entwickeln von Inhalten benötigen Sie nur eine Internetverbindung.

## Editor einrichten
{: #editorsetup}

Die {{site.data.keyword.webide}} ist anpassbar, das heißt, Sie können das Farbschema, die technischen Tools und die Einstellungen auswählen, die Sie für die Entwicklung benötigen. Um die Einstellungen anzuzeigen und zu bearbeiten, klicken Sie im Menü links auf das Symbol **Einstellungen ** <img class="inline" src="./images/webide_settings_icon.png"  alt="Symbol 'Einstellungen'">.

<!-- LH: I don't think we need to include the following table, so I'm commenting it out. When you're viewing the settings in the Web IDE, this information should be obvious -->

<!--| Categories | Description  |
|---|---|
| Cloud Foundry  | Define a Cloud Foundry API and Manage URL  |
| CSS Validation | Define the severities for CSS linting rules that you use to check your code  |
| Editor Settings  | Configure editor-specific settings for key bindings, editor behavior, layout, and more  |
| Editor Styles  | Configure color schemes for the languages that you use, or import a theme from another editors  |
| Git  | Configure general settings for Git  |
| Globalization | Define globalization settings for your code |
| JavaScript Validation  | Define the severities for the JavaScript linting rules that you use to check your code  |
| Plug-ins  | Install, disable, or remove plug-ins from the editor  | -->

Wenn Sie bestimmte Einstellungen während der Bearbeitung häufig ändern müssen, können Sie im Editor oben rechts über das Symbol **Lokale Editoreinstellungen** <img class="inline" src="./images/webide_local_settings_icon.png"  alt="Symbol für lokale Editoreinstellungen"> schnell auf diese Einstellungen zugreifen.

![Lokale Editoreinstellungen](images/webide_local_editor_settings.png)

Die Einstellungen für den Stil des Editors und die Schriftgröße werden standardmäßig immer angezeigt. Führen Sie die folgenden Schritte aus, um andere Editoreinstellungen im Menü anzuzeigen:

1. Klicken Sie auf das Symbol **Lokale Editoreinstellungen** <img class="inline" src="./images/webide_local_settings_icon.png"  alt="Symbol 'Lokale Editoreinstellungen'">.

2. Klicken Sie auf **Editoreinstellungen**.

3. Um eine Einstellung im Menü **Lokale Editoreinstellungen** einzubeziehen oder auszuschließen, klicken Sie auf den Kreis neben der Einstellung.

![Editoreinstellungen ein-/ausschalten](images/webide_editor_settings_toggle.png)


## Code bearbeiten
{: #editcode}

Die {{site.data.keyword.webide}} hat zwei Abschnitte. Der erste Abschnitt ist der Dateinavigator links, in dem Ihre Projektdateien in einer Baumstruktur angezeigt werden. Im Dateinavigator können Sie Ihre Dateien und Ordner erstellen, umbenennen, löschen und verwalten.

**Tipp:** Um Dateien in den Dateinavigator hochzuladen, ziehen Sie sie von Ihrem Computer in den Dateinavigator.

Der zweite Abschnitt ist der Editorbereich rechts. Der Editor bietet mehrere Code-Funktionen an, einschließlich Content-Assist und Syntaxprüfung.

![Web-IDE](images/webide.png)

### Mit mehreren Dateien arbeiten
1. Um mit zwei Dateien gleichzeitig zu arbeiten, klicken Sie im Editor oben auf das Symbol **Teilungsmodus des Editors ändern** <img class="inline" src="./images/webide_split_editor_icon.png"  alt="Symbol 'Teilungsmodus des Editors'">.
2. Wählen Sie aus dem angezeigten Menü eine Ansicht aus.

 Nachdem Sie eine Ansicht ausgewählt haben, wird die Datei in beiden Editoransichten angezeigt, wenn sie im Editor bereits geöffnet war.

 Gehen Sie wie folgt vor, um eine Datei zu öffnen oder zu ändern, die in einer der Editoransichten angezeigt wird:
 1. Bewegen Sie den Mauszeiger über die Editoransicht, die Sie ändern möchten.
 2. Klicken Sie im Dateinavigator auf eine Datei.

### Tastenkombinationen
Die meisten Befehle in der {{site.data.keyword.webide}} können über Tastenkombinationen aufgerufen werden.

Um eine Liste der Tastenkombinationen im Editor anzuzeigen, drücken Sie Alt+Umschalt+?. Drücken Sie bei einem Mac auf Strg+Umschalt+?.

## Quellcode verwalten
{: #sourcecontrol}

Die {{site.data.keyword.webide}} enthält Management-Tools für den Quellcode. Klicken Sie zum Arbeiten mit Ihrem Git-Repository auf das Symbol **Git-Repository** <img class="inline" src="./images/webide_git_icon.png"  alt="Symbol 'Git-Repository'">. Weitere Informationen finden Sie im Abschnitt [Quellcodeverwaltung mit Git](https://hub.jazz.net/docs/git/){: new_window}.


## Eine App im Arbeitsbereich bereitstellen
{: #deploy}

1. Um Ihre App bereitzustellen wählen Sie in der Ausführungsleiste entweder eine Startkonfiguration oder [erstellen](https://hub.jazz.net/tutorials/livesync/#launch_configuration){: new_window} Sie sie.
1. Klicken Sie auf das Symbol 'Bereitstellen' <img class="inline" src="./images/webide_deploy_button.png"  alt="Symbol 'Bereitstellen'">. Eine Instanz Ihrer App wird bereitgestellt, indem die aktuellen Inhalte Ihrers Arbeitsbereichs und die Umgebung, die in Ihrer Startkonfiguration definiert ist, verwendet werden. 
2. Wenn Ihre App bereitgestellt wurde, können Sie über die Ausführungsleiste Ihre App stoppen, neu starten oder debuggen sowie Protokolle anzuzeigen usw.
![Ausführungsleiste](images/webide_runbar.png)

<!-- LH: I'm commenting out the following list because I think this information is obvious from the UI. I also updated the preceding sentence to mention a few things that you can do from the run bar.

 * Stop the app: <img  class="inline" src="./images/webide_stop_button.png"  alt="The stop icon">
 * Open the deployed app: <img class="inline" src="./images/webide_open_app_url.png"  alt="The open app URL icon">
 * View the logs of the deployed app: <img class="inline" src="./images/webide_view_logs.png"  alt="The view logs icon">
 * Open the app's Dashboard: <img  class="inline" src="./images/webide_open_dashboard.png"  alt="The open dashboard icon">
 * If you are developing a Node.js app, enable Live Edit mode: <img  class="inline"  src="./images/webide_enable_live_edit.png"  alt="The enable live edit slider">
 * With Live Edit mode enabled, restart the app quickly, without redeployment: <img  class="inline" src="./images/webide_live_edit_restart.png"  alt="The Live Edit restart icon">
 * With Live Edit mode enabled, access the debugger: <img  class="inline" src="./images/webide_debug_icon.png"  alt="The debug icon"> -->

 ## Bearbeitung außerhalb der {{site.data.keyword.webide}}
{: #editlocal}

Wenn Sie einen Editor außerhalb der {{site.data.keyword.webide}} verwenden möchten, richten Sie {{site.data.keyword.Bluemix_live}} so ein, dass Sie Ihre Projektdateien in jedem beliebigen Tool bearbeiten können. {{site.data.keyword.Bluemix_live_notm}} ist eine Befehlszeilenanwendung, die die Änderungen in Ihrem lokalen Dateisystem mit denen Ihres Cloud-Arbeitsbereichs in {{site.data.keyword.jazzhub}} synchronisiert. 

### Vorbereitende Schritte 

[Laden Sie die {{site.data.keyword.Bluemix_live_notm}}-Befehlszeilenschnittstelle herunter und installieren Sie sie.](http://livesyncdownload.ng.bluemix.net){: new_window}

### Ihre lokale Umgebung mit {{site.data.keyword.Bluemix_notm}} synchronisieren
{: #edit_local_download}

1. Öffnen Sie ein Befehlszeilenfenster.
2. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an:

	```
	bl login
	```
	{: pre}

3. Geben Sie Ihre IBM ID und Ihr Kennwort ein, wenn Sie dazu aufgefordert werden.
4. Zeigen Sie eine Liste Ihrer {{site.data.keyword.Bluemix_notm}}-Projekte an: 

	```
	bl projects
	```
	{: pre}

4. Synchronisieren Sie Ihre lokale Umgebung mit Ihrem Projekt in {{site.data.keyword.Bluemix_notm}}:

	```
	bl sync projectName
	```
	{: pre}

`projectName` ist der App-Name von {{site.data.keyword.Bluemix_notm}}.

Wenn Sie die Bearbeitung abgeschlossen haben, geben Sie `q` ein, um die Synchronisation zu beenden.

### Das Desktop Sync-Feature zum lokalen Bearbeiten des Codes aktivieren

Das Desktop Sync-Feature ähnelt dem Live Edit-Modus für die Befehlszeile. Sie verwenden das Desktop Sync-Feature, um in der Befehlszeile ein Debugging durchzuführen.
1. Aktivieren Sie in einem anderen Befehlszeilenfenster das Desktop Sync-Feature:

	```
	cd localDirectory
	bl start
	```
	{: codeblock}

2. Verwenden Sie die Startkonfiguration, die Sie in der {{site.data.keyword.webide}} erstellt haben. Sobald die Startkonfiguration ausgewählt haben, ist das Desktop Sync-Feature in Ihrer lokalen Umgebung aktiviert. In dem Befehlszeilenfenster, das Sie eben geöffnet haben, können Sie die App-URL sehen, die URL debuggen, die URL verwalten und den {{site.data.keyword.Bluemix_live_notm}}-Status anzeigen.

3. Aktualisieren Sie den Browser und überprüfen Sie, dass die Änderungen angezeigt werden, die Sie in statische Dateien im lokalen Arbeitsbereich gespeichert haben. 

### Das Desktop Sync-Feature inaktivieren

1. Geben Sie in das zweite Befehlszeilenfenster `bl stop` ein.
2. Geben Sie in das erste Befehlszeilenfenster `q stop` ein.
