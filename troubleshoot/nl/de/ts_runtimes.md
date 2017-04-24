---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-10"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 


# Fehlerbehebung für Laufzeiten
{: #runtimes}

Es können Probleme bei der Verwendung von {{site.data.keyword.Bluemix}}-Laufzeiten auftreten. In vielen Fällen können Sie diese Probleme durch Ausführen weniger einfacher Schritte beheben.
{:shortdesc}


## Bei einer Push-Operation für eine App wird ein veraltetes Buildpack verwendet
{: #ts_loading_bp}

Bei einer Push-Operation für eine App können möglicherweise nicht die neuesten Buildpack-Komponenten verwendet werden. Sie können Buildpacks mit integrierten Mechanismen verwenden, die das Laden veralteter Komponenten verhindern, oder Sie können den Inhalt des Cacheverzeichnisses der App löschen, bevor Sie eine Push-Operation oder ein erneutes Staging für die App durchführen. 

Wenn Sie eine Push-Operation oder erneutes Staging für eine App durchführen, nachdem das Buildpack aktualisiert wurde, werden die neuesten Buildpack-Komponenten nicht automatisch geladen. Dies führt dazu, dass die App die veralteten Buildpack-Komponenten aus dem Cache verwendet. Aktualisierungen, die für das Buildpack angewendet wurden, seit die letzte Push-Operation für die App ausgeführt wurde, werden nicht implementiert. 
{: tsSymptoms}

Einige Buildpacks sind nicht so konfiguriert, dass sie alle aktualisierten Komponenten automatisch aus dem Internet herunterladen, um sicherzustellen, dass stets die neueste Version verwendet wird.
{: tsCauses} 

Sie können Buildpacks verwenden, die über integrierte Mechanismen verfügen, mit denen das Laden veralteter Komponenten vermieden wird, beispielsweise die folgenden Buildpacks: 
{: tsResolve}

  * [Cloud Foundry Java Buildpack ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/cloudfoundry/java-buildpack){: new_window}. Dieses Buildpack verfügt über einen integrierten Mechanismus, der sicherstellt, dass die neueste Version des Buildpacks verwendet wird. Weitere Informationen zur Funktionsweise dieses Mechanismus finden Sie unter [extending-caches.md ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window}. 
  * [Cloud Foundry Node.js buildpack ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}. Dieses Buildpack bietet eine ähnliche Funktionalität, die Umgebungsvariablen nutzt. Damit das Node.js-Buildpack jedes mal Knotenmodule aus dem Internet herunterladen kann, geben Sie in der cf-Befehlszeilenschnittstelle den folgenden Befehl ein: 	
  ```
  set NODE_MODULES_CACHE=false
  ```

Wenn das verwendete Buildpack keinen Mechanismus zum automatischen Laden der neuesten Komponenten bereitstellt, können Sie den Inhalt des Cacheverzeichnisses manuell löschen und eine Push-Operation für Ihre App durchführen. Führen Sie die folgenden Schritte aus:

 1. Checken Sie eine Verzweigung eines Null-Buildpacks aus, z. B. https://github.com/ryandotsmith/null-buildpack. Informationen zum Auschecken einer Verzweigung finden Sie unter [Git Basics - Getting a Git Repository ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window}.  
 2. Fügen Sie die folgende Zeile zur Datei `null-buildpack/bin/compile` hinzu und schreiben Sie die Änderungen fest. Informationen zum Festschreiben von Änderungen finden Sie unter [Git Basics - Recording Changes to the Repository ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window}.
  ```
  rm -rfv $2/*
  ```
 3. Führen Sie für Ihre App eine Push-Operation mit dem modifizierten Null-Buildpack durch, um den Inhalt des Cache zu löschen. Verwenden Sie hierzu den folgenden Befehl: Nach der Ausführung dieses Schritts ist der gesamte Inhalt des Cacheverzeichnisses Ihrer App gelöscht.
  ```
  cf push appname -p app_path -b <modified_null_buildpack>
  ```
 4. Führen Sie für Ihre App eine Push-Operation mit dem neuesten Buildpack durch, das Sie verwenden möchten. Geben Sie hierzu den folgenden Befehl ein: 
  ```
  cf push appname -p app_path -b <latest_buildpack>
  ```
 
## NOTICE-Nachrichten des PHP-Buildpacks
{: #ts_phplog}

Möglicherweise werden Nachrichten angezeigt, die einen Hinweis (NOTICE) aus den Protokollen enthalten. Sie können die Protokollierung dieser Nachrichten stoppen, indem Sie die Protokollstufe ändern.	

Wenn Sie eine App per Push-Operation an {{site.data.keyword.Bluemix_notm}} übertragen, indem Sie ein PHP-Buildpack verwenden, werden möglicherweise Nachrichten angezeigt, die das Wort `NOTICE` (Hinweis) enthalten:
{: tsSymptoms}

```
• 2015-01-26T15:00:59.70+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: fpm is running, pid 93
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: ready to handle connections
```
Im PHP-Buildpack definiert der Parameter 'error_log' die Protokollstufe. Der Wert des Parameters `error_log` lautet standardmäßig **stderr notice**. Das folgende Beispiel zeigt die Standardkonfiguration für die Protokollstufe in der Datei `nginx-defaults.conf` des von Cloud Foundry bereitgestellten PHP-Buildpacks. Weitere Informationen finden Sie unter [cloudfoundry/php-buildpack ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window}.
{: tsCauses} 

```
daemon off;
error_log stderr notice;
pid @{HOME}/nginx/logs/nginx.pid;
```
	
Die `NOTICE`-Nachrichten dienen zu Ihrer Information und weisen nicht zwangsläufig auf ein Problem hin. Sie können die Protokollierung dieser Nachrichten stoppen, indem Sie in der Datei 'nginx-defaults.conf' Ihres Buildpacks die Protokollstufe von `stderr notice` in `stderr error` ändern. Beispiel: 	
{: tsResolve}

```
daemon off;
error_log stderr error;
pid @{HOME}/nginx/logs/nginx.pid;
```
Weitere Informationen dazu, wie die Standardkonfiguration für die Protokollierung geändert wird, finden Sie unter [error_log ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window}.
	

## Importieren der Python-Bibliothek eines Drittanbieters in {{site.data.keyword.Bluemix_notm}} nicht möglich
{: #ts_importpylib}

Möglicherweise können Sie die Python-Bibliothek eines Drittanbieters nicht in {{site.data.keyword.Bluemix_notm}} importieren. Fügen Sie zur Lösung des Problems Konfigurationsdateien zum Stammverzeichnis Ihrer Python-App hinzu.

Beim Versuch, die Python-Bibliothek eines Drittanbieters (beispielsweise die Bibliothek `web.py`) zu importieren, schlägt der Befehl `cf push` fehl.
{: tsSymptoms}

Konfigurationsinformationen für die Python-App fehlen.
{: tsCauses}

Fügen Sie eine Datei `requirements.txt` und eine Datei `Procfile` zum Stammverzeichnis Ihrer Python-App hinzu. In den folgenden Informationen wird davon ausgegangen, dass Sie die Bibliothek `web.py` importieren:
{: tsResolve}

 1. Fügen Sie eine Datei `requirements.txt` zum Stammverzeichnis Ihrer Python-App hinzu.
 
 Die Datei `requirements.txt` gibt die für Ihre Python-App erforderlichen Bibliothekspakete sowie die Version der Pakete an. Das folgende Beispiel zeigt den Inhalt der Datei `requirements.txt`, wobei `web.py==0.37` angibt, dass es sich bei der Version der Bibliothek `web.py` um '0.37' handelt, und `wsgiref==0.1.2` angibt, dass es sich bei der für die Bibliothek 'web.py' erforderliche Version der Gateway-Schnittstelle des Web-Servers um '0.1.2' handelt.
	 ```
	 web.py==0.37
     wsgiref==0.1.2
	 ```
	 Weitere Informationen zur Konfiguration der Datei `requirements.txt` finden Sie unter [Requirements files](https://pip.readthedocs.org/en/1.1/requirements.html). 
	 
 2. Fügen Sie eine Datei `Procfile` zum Stammverzeichnis Ihrer Python-App hinzu.
Die Datei `Procfile` muss den Starbefehl für Ihre Python-App enthalten. Im folgenden Befehl ist *NameIhrerApp* der Name Ihrer Python-Anwendung und *PORT* ist die Portnummer, die Ihre Python-Anwendung zum Empfangen von Anforderungen von Benutzern der App verwenden muss. Bei *$PORT* handelt es sich um ein optionales Element. Wenn Sie im Startbefehl PORT nicht angeben, wird die Portnummer unter der Umgebungsvariablen `VCAP_APP_PORT` verwendet, die sich innerhalb der App befindet. 
	```
	web: python <NameIhrerApp>.py $PORT
	```

Sie können nun die Python-Bibliothek eines Drittanbieters in {{site.data.keyword.Bluemix_notm}} importieren.	


## Schaltfläche 'Aktionen' auf Seite 'Instanzdetails' ist inaktiviert
{: #ts_actionsbutton}

Die Schaltfläche 'Aktionen' auf der Seite 'Instanzdetails' ist inaktiviert.
{: tsSymptoms} 

Dieses Problem tritt aufgrund folgender Ursachen auf:
{: tsCauses}

 * Die App ist keine Java&trade;-Web-App. Von Runtime Management Utilities (RMU) werden nur Web-Apps unterstützt, die mit Liberty-Buildpacks bereitgestellt werden.
 * Die App wurde nicht mit dem integrierten Liberty-Buildpack bereitgestellt.
 * Die App wurde mit einer älteren Version eines Liberty-Buildpacks bereitgestellt.

Wenn das Problem durch eine ältere Version des Liberty-Buildpacks verursacht wird, stellen Sie die App erneut in {{site.data.keyword.Bluemix_notm}} bereit. Andernfalls können Sie dem Support-Team die folgenden Protokolldateien der Clientanwendung zur Verfügung stellen:
{: tsResolve} 

  * logs/messages.log
  * logs/stdout.log
  * logs/stderr.log
 
  
## Berechtigungsnachweise zum Öffnen des Trace- oder Speicherauszugsfensters erforderlich
{: #ts_username}

Zum Öffnen des Trace- oder Speicherauszugsfenster sind ein Benutzername und ein Kennwort erforderlich.
{: tsSymptoms}

Dieses Problem tritt auf, weil das Zeitlimit für die Anmeldesitzung überschritten ist.
{: tsCauses}

Geben Sie den Benutzernamen und das Kennwort erneut ein.
{: tsResolve}


## Fehler treten während Ausführung von Trace- oder Speicherauszugsoperationen auf
{: #ts_target}

Während Trace- oder Speicherauszugsoperationen ausgeführt werden, wird eine Fehlernachricht angezeigt. Die Nachricht gibt an, dass sich eine Zielinstanz für eine App nicht im Status 'Aktiv' befindet:	
{: tsSymptoms}

```
Instance 0: Trace specification is set successfully
Instance 2: Trace specification is set successfully
Instance 1: Target instance 1 for app abcd is not in the running state.
Instance 3: Trace specification is set successfully
Instance 4: Trace specification is set successfully
```

Dieses Problem tritt aufgrund folgender Ursachen auf:
{: tsCauses} 

  * Die Funktionen für die Trace- und Speicherauszugsverwaltung stehen nur für Appinstanzen zur Verfügung, die aktiv sind. Trace- bzw. Speicherauszugsoperationen können nicht für Appinstanzen verwendet werden, die gestoppt wurden, derzeit gestartet werden oder ausgefallen sind.
  * Der Status der Appinstanz wird geändert, wenn der Trace- oder Speicherauszugsdialog geöffnet wird. 

Schließen Sie das Fenster und öffnen Sie es anschließend erneut.
{: tsResolve} 


## Instanzen verfügen über unterschiedliche Konfigurationen für Tracespezifikation
{: #ts_different_config}

Für unterschiedliche Instanzen einer App können unterschiedliche Konfigurationen für die Tracespezifikation angezeigt werden.
{: tsSymptoms}

Dieses Verhalten tritt aufgrund folgender Ursachen auf:
{: tsCauses}

  * Sie haben die Konfiguration zuvor für mindestens eine Instanz geändert. Falls Sie die Konfiguration für die Tracespezifikation für eine Instanz ändern, gilt die Änderung nicht für andere Instanzen derselben App. Beispiel: Ihre App verwendet 'log4j' und Sie haben 2 Instanzen für diese App. Sie können die Protokollebene für Instanz 0 von 'info' in 'debug' ändern, aber die Protokollebene von Instanz 1 verbleibt bei 'info'.
  
  * Für die App wird ein Scale-out durchgeführt und sie verfügt über neue Instanzen. Von Runtime Management Utilities (RMU) wird die Konfiguration der Tracespezifikation auf die neue Instanz angewendet, für die das Scale-out durchgeführt wird. Von der neuen Instanz wird die Standardkonfiguration verwendet. Beispiel: Von der App wird 'log4j' verwendet und sie verfügt über eine Instanz. Sie können die Protokollebene dieser Instanz 0 von 'info' in 'debug' ändern. Wenn Sie diese Änderung durchgeführt und für die App ein Scale-out in zwei Instanzen durchgeführt haben, lautet die Protokollebene der neuen Instanz 'info' und nicht 'debug'.

Es ist keine Aktion erforderlich. Hierbei handelt es sich um ein erwartetes Verhalten.
{: tsResolve} 


## Überschrittenes Datenträgerkontingent
{: #ts_diskquota}

Es kann vorkommen, dass im Anwendungsprotokoll angezeigt wird, dass das Datenträgerkontingent überschritten ist.

Die Fehlernachricht `Disk quota exceeded` (Datenträgerkontingent überschritten) wird im Protokoll der App angezeigt.
{: tsSymptoms}

Dieses Problem wird durch einen der folgenden Gründe verursacht: 
{: tsCauses} 

  * Die Speicherauszugsdateien werden mit aktiven Appinstanzen generiert und die Dateien belegen das zugeordnete Datenträgerkontingent. Das Datenträgerkontingent für eine Appinstanz beträgt standardmäßig 1 GB. Wenn Sie die Plattenbelegung überprüfen möchten, klicken Sie auf **Dashboard>Anwendung>Anwendungslaufzeit**. Im folgenden Beispiel werden die Laufzeitinformationen inklusive der Plattenbelegung für zwei Instanzen einer App aufgeführt:
    ```
    Instance	State	CPU	Memory Usage	Disk Usage

	0		Running	1.0%	344.8MB/512MB	236.8MB/1GB
	2		Running	2.3%	361.2MB/512MB	235.7MB/1GB
    ```
  * Das Datenträgerkontingent wird durch das aktuelle Organisationskontingent eingeschränkt.

Verwenden Sie eines der folgenden Verfahren:
{: tsResolve} 

  * Löschen der Speicherauszugsdateien, nachdem sie heruntergeladen wurden.
  * Erneute Bereitstellung der App mit einem größeren Datenträgerkontingent und dem folgenden Eintrag im Bereitstellungsmanifest:
    ```
	disk_quota: 2048
	```
	
