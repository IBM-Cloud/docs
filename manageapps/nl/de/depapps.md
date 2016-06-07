---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Anwendungen bereitstellen
{: #deployingapps}

*Letzte Aktualisierung: 9. Mai 2016*

Sie können Anwendungen anhand verschiedener Methoden für {{site.data.keyword.Bluemix}} bereitstellen, beispielsweise über die Befehlszeilenschnittstelle oder über integrierte Entwicklungsumgebungen (IDEs). Darüber hinaus können Anwendungen mithilfe von Anwendungsmanifesten bereitgestellt werden. Bei Verwendung eines Anwendungsmanifests wird die Anzahl der Bereitstellungsdetails reduziert, die Sie jedes Mal angeben müssen, wenn Sie die Anwendung in {{site.data.keyword.Bluemix_notm}} bereitstellen.
{:shortdesc}

##Anwendungsbereitstellung
{: #appdeploy}

Das Bereitstellen einer Anwendung in
{{site.data.keyword.Bluemix_notm}} umfasst zwei Phasen: Das Staging der Anwendung und das Starten der
Anwendung.

###Staging einer Anwendung

Während der Staging-Phase werden die Informationen, die Sie in der Befehlszeilenschnittstelle 'cf' oder in der Datei `manifest.yml` angeben, von einem Droplet Execution Agent (DEA) verwendet, um zu entscheiden, was für das Staging der Anwendung erstellt werden muss. Der DEA wählt ein geeignetes Buildpack für das Staging Ihrer Anwendung aus, und das Ergebnis des Staging-Prozesses ist ein Droplet. Weitere Informationen zur Bereitstellung einer Anwendung in {{site.data.keyword.Bluemix_notm}} finden Sie unter [{{site.data.keyword.Bluemix_notm}}-Architektur, Funktionsweise von {{site.data.keyword.Bluemix_notm}}](../public/index.html#publicarch).

Während des Staging-Prozesses überprüft der DEA, ob das Buildpack mit der Anwendung übereinstimmt, d. h. für diese geeignet ist. Beispiel: eine Liberty-Laufzeit für eine .war-Datei oder eine Node.js-Laufzeit für .js-Dateien. Anschließend erstellt der DEA einen isolierten Container, der das Buildpack und den Anwendungscode enthält. Der Container wird von der Komponente 'Warden'
verwaltet. Weitere Informationen finden Sie unter [How Applications Are Staged](http://docs.cloudfoundry.org/concepts/how-applications-are-staged.html){:new_window}.

###Starten einer Anwendung

Beim Starten einer Anwendung wird die Instanz des Warden-Containers erstellt. Gegebenenfalls werden auch
mehrere Instanzen erstellt. Mithilfe des Befehls **cf files** können Sie die Dateien (beispielsweise Protokolle) anzeigen, die im
Dateisystem des Warden-Containers gespeichert sind. Wenn der Start der Anwendung fehlschlägt, wird die Anwendung vom DEA gestoppt, und der gesamte Inhalt des
Warden-Containers wird entfernt. Daher stehen Ihnen keine Protokolldateien zur Verfügung, wenn eine Anwendung gestoppt wird oder wenn der Staging-Prozess einer
Anwendung fehlschlägt.

Wenn die Protokolle für Ihre Anwendung nicht mehr verfügbar sind, sodass auch der Befehl
**cf files** nicht mehr verwendet werden kann, um die Ursache der Staging-Fehler anzuzeigen, können Sie stattdessen den Befehl
**cf logs** verwenden. Der Befehl **cf logs** verwendet den Cloud Foundry-Protokollaggregator, um die
Details Ihrer Anwendungsprotokolle
und Systemprotokolle zu erfassen, und Sie können den im Protokollaggregator gepufferten Inhalt anzeigen. Weitere Informationen zum Protokollaggregator finden
Sie unter [Logging in Cloud Foundry](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}.

**Hinweis:** Die Puffergröße ist begrenzt. Wenn eine Anwendung über einen langen Zeitraum ausgeführt wird und nicht erneut gestartet wird,
kann es sein, dass nach Eingabe von `cf logs App-Name --recent` keine Protokolle angezeigt werden, weil der Inhalt des Protokollpuffers möglicherweise gelöscht worden
ist. Daher können Sie zur Behebung von Staging-Fehlern für eine große Anwendung `cf logs App-Name` in
eine von der Befehlszeilenschnittstelle 'cf' separate Befehlszeile eingeben, um die Protokolle zu verfolgen, wenn Sie die Anwendung
bereitstellen.

Wenn beim Staging Ihrer Anwendungen unter
{{site.data.keyword.Bluemix_notm}} Probleme auftreten, können Sie die Schritte im Thema
[Staging-Fehler beheben](../debug/index.html#debugging-staging-errors) befolgen, um diese Probleme zu beheben.

##Bereitstellung von Anwendungen mit dem Befehl 'cf'
{: #dep_apps}

Wenn Sie Ihre Anwendungen über die Befehlszeilenschnittstelle für
{{site.data.keyword.Bluemix_notm}} bereitstellen, muss ein Buildpack als Laufzeitumgebung
entsprechend Ihrer Anwendungssprache und Ihrem Framework angegeben
werden. Sie können auch den Service 'Delivery Pipeline' verwenden, um Anwendungen für {{site.data.keyword.Bluemix_notm}} bereitzustellen.

{{site.data.keyword.Bluemix_notm}} stellt integrierte Buildpacks
zur Verfügung, die Java und Node.js unterstützen. Wenn Sie diese Sprachen und Frameworks verwenden, brauchen Sie bei der
Bereitstellung Ihrer Anwendung über die Befehlszeilenschnittstelle kein Buildpack anzugeben. Da {{site.data.keyword.Bluemix_notm}} auf der Grundlage von Cloud Foundry erstellt ist, nimmt der
Befehl diese
Buildpacks standardmäßig als Wert an.

Wenn Sie ein externes Buildpack verwenden, müssen Sie die URL des Buildpacks mithilfe der Option
**-b** angeben, wenn Sie Ihre Anwendung über die Eingabeaufforderung
für {{site.data.keyword.Bluemix_notm}} bereitstellen.

  * Um Liberty-Serverpakete für {{site.data.keyword.Bluemix_notm}} bereitzustellen, verwenden Sie den folgenden Befehl in Ihrem Quellenverzeichnis:
  
  ```
  cf push
  ```
  
  Weitere Informationen zum Liberty-Buildpack finden Sie unter [Liberty for Java](../runtimes/liberty/index.html).
  
  * Um Java Tomcat-Anwendungen für {{site.data.keyword.Bluemix_notm}} bereitzustellen, verwenden Sie den folgenden Befehl:
  
  ```
  cf push appname -b https://github.com/cloudfoundry/java-buildpack.git -p app_path
  ```
  
  * Um WAR-Pakete in {{site.data.keyword.Bluemix_notm}} bereitzustellen, verwenden Sie den folgenden Befehl:
  
  ```
  cf push App-Name -p app.war
  ```
  Alternativ können Sie ein Verzeichnis angeben, in dem Ihre Anwendungsdateien enthalten sind. Verwenden Sie dazu den folgenden Befehl:
  
  ```
  cf push App-Name -p "./app"
  ```
  
  * Um Node.js-Anwendungen für {{site.data.keyword.Bluemix_notm}} bereitzustellen, verwenden Sie den folgenden Befehl:
  
  ```
  cf push appname -p app_path
  ```
  
Die Datei `package.json` muss sich in Ihrer Node.js-Anwendung befinden, damit die Anwendung vom Node.js-Buildpack erkannt werden kann. Die Datei `app.js` ist das Einstiegsscript für die Anwendung und kann in der Datei `package.json` angegeben werden. Das folgende Beispiel zeigt eine einfache `package.json`-Datei:

  ```
  {
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": ">=3.4.7 <4",
                "jade": ">=1.1.4"
        },
        "scripts": {
                "start": "node app.js"
        },
        "engines": {
                "node": ">=0.10.0"
        },
        "repository": {}
  }
  ```
    
  Weitere Informationen zur Datei `package.json` finden Sie unter [package.json](https://www.npmjs.org/doc/files/package.json.html){:new_window}.
  
  * Um PHP-, Ruby- oder Python-Anwendungen in {{site.data.keyword.Bluemix_notm}} bereitzustellen, verwenden Sie den folgenden Befehl in dem Verzeichnis, das die Anwendungsquelle enthält:
  
  ```
  cf push App-Name
  ```

###Bereitstellung einer App in mehreren Bereichen

Eine App ist für den Bereich, in dem sie bereitgestellt wird, spezifisch. Es ist nicht möglich, eine App von einem Bereich in {{site.data.keyword.Bluemix_notm}} in einen anderen zu verschieben oder zu kopieren. Um eine App in mehreren Bereichen bereitzustellen, müssen Sie Ihre App in den einzelnen Bereichen bereitstellen, in denen Sie die App verwenden möchten; gehen Sie hierfür wie folgt vor:

  1. Wechseln Sie in den Bereich, in dem Sie Ihre App bereitstellen möchten; verwenden Sie hierfür den Befehl **cf target** zusammen mit der Option **-s**:
  
  ```
  cf target -s <Bereichsname>
  ```
  
  2. Wechseln Sie in Ihr App-Verzeichnis und stellen Sie Ihre App mithilfe des Befehls **cf push** bereit; dabei muss der App-Name in Ihrer Domäne eindeutig sein.
  
  ```
  cf push App-Name
  ```
  
##Anwendungsmanifest
{: #appmanifest}

Anwendungsmanifeste enthalten Optionen, die auf den Befehl **cf push** angewendet werden. Durch die Verwendung eines
Anwendungsmanifests können Sie die Anzahl der Bereitstellungsdetails reduzieren, die Sie jedes Mal angeben müssen, wenn Sie für eine Anwendung eine
Push-Operation an {{site.data.keyword.Bluemix_notm}} durchführen.

In Anwendungsmanifesten können Sie Optionen wie beispielsweise die Anzahl der zu erstellenden Anwendungsinstanzen, die Speicherkapazität und
das Datenträgerkontingent, die bzw. das den Anwendungen zugeordnet werden soll, sowie weitere Umgebungsvariablen für die Anwendung angeben. Darüber hinaus
können Sie Anwendungsmanifeste verwenden, um Anwendungsbereitstellungen zu automatisieren. Der Standardname einer Manifestdatei lautet `manifest.yml`.

###Unterstützte Optionen in der Manifestdatei

Die nachstehende Tabelle zeigt die unterstützten Optionen, die Sie in einer Anwendungsmanifestdatei verwenden können. Wenn Sie einen anderen Dateinamen
als
`manifest.yml` verwenden wollen, müssen Sie die Option **-f** mit dem Befehl **cf push** verwenden. Im folgenden
Beispiel wird `appManifest.yml` als Dateiname verwendet:

```
cf push -f appManifest.yml
```

<p>  </p>


|Optionen	|Beschreibung	|Verwendung oder Beispiel|
|:----------|:--------------|:---------------|
|**buildpack**	|Die URL oder der Name des angepassten Buildpacks.	|`buildpack:` *Buildpack-URL*|
|**disk_quota**	|Das Datenträgerkontingent, das einer Anwendung zugeordnet wird. Der Standardwert ist 1 GB.	|`disk_quota: 500M`|
|**domain**	|Der Domänenname der Anwendung in {{site.data.keyword.Bluemix_notm}}.	|`domain:` ng.bluemix.net|
|**host**	|Der Hostname der Anwendung in {{site.data.keyword.Bluemix_notm}}. Dieser Wert muss in der {{site.data.keyword.Bluemix_notm}}-Umgebung eindeutig sein.	|`host:` *Hostname*|
|**name**	|Der Anwendungsname in {{site.data.keyword.Bluemix_notm}}. Dieser Wert muss in der {{site.data.keyword.Bluemix_notm}}-Umgebung eindeutig sein.	|`name:` *App-Name*|
|**path**	|Die Position Ihrer Anwendung. Dieser Wert kann entweder ein relativer Pfad oder ein absoluter Pfad sein.	|`path:` *Pfad zur Anwendung*|
|**command**	|Der angepasste Startbefehl für Ihre Anwendung oder der Befehl für die Ausführung von Scriptdateien.	|`command:` *Angepasster Befehl* `command:` *bash ./run.sh*|
|**memory**	|Die Speicherkapazität, die der Anwendung zugeordnet werden soll. Der Standardwert ist 1 GB.	|`memory: 512M`|
|**instances**	|Die Anzahl der Instanzen, die für Ihre Anwendung erstellt werden sollen.	|`instances: 2`|
|**timeout**	|Die für den Start der Anwendung zulässige Höchstdauer in Sekunden. Der Standardwert ist 60 Sekunden.	|`timeout: 80`|
|**no-route**	|Ein boolescher Wert, der verwendet wird, um zu verhindern, dass der Anwendung eine Route zugewiesen wird, wenn die Anwendung lediglich im Hintergrund ausgeführt wird. Der Standardwert ist **false**.	|`no-route: true`|
|**random-route**	|Ein boolescher Wert, der verwendet wird, um der Anwendung eine beliebige Route zuzuweisen. Der Standardwert ist **false**.	|`random-route: true`|
|**services**	|Die Services, die an die Anwendung gebunden werden sollen.	|`services: - mysql_maptest`|
|**env**	|Die angepassten Umgebungsvariablen für die Anwendung.|`env: DEV_ENV: production`|
*Tabelle 1. Unterstützte Optionen in der Datei 'manifest.yml'*

###Beispiel für eine Datei `manifest.yml`

Das folgende Beispiel zeigt eine Manifestdatei für eine Node.js-Anwendung, die das integrierte Node.js-Community-Buildpack in {{site.data.keyword.Bluemix_notm}} verwendet.

```
---
- name: myNodejsapp
  memory: 256M
  disk_quota: 512M
  path: /dev/myNodejsApp
  buildpack: nodejs_buildpack
  host: nodejs001
  domain: mybluemix.net
  command: node app.js
  timeout: 80
  services:
  - mongo_8917
  env:
    env_type: production
```
{:codeblock}

##Umgebungsvariablen
{: #app_env}

Umgebungsvariablen enthalten Informationen zur Umgebung einer in {{site.data.keyword.Bluemix_notm}} bereitgestellten Anwendung. Neben den Umgebungsvariablen, die von einem *Droplet Execution Agent (DEA)* und Buildpacks festgelegt werden, können Sie auch anwendungsspezifische Umgebungsvariablen für Anwendungen in {{site.data.keyword.Bluemix_notm}} festlegen.

Die folgenden Umgebungsvariablen einer aktiven {{site.data.keyword.Bluemix_notm}}-Anwendung können Sie mit dem Befehl **cf env** oder über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle anzeigen:
	
  * Benutzerdefinierte Variablen, die für eine Anwendung spezifisch sind. Informationen dazu, wie eine benutzerdefinierte Variable einer App hinzugefügt wird, finden Sie in [Benutzerdefinierte Umgebungsvariablen hinzufügen](#ud_env){:new_window}.
	 
  * Die Variable VCAP_SERVICES, die Verbindungsinformationen für den Zugriff auf eine Serviceinstanz enthält. Ist Ihre Anwendung an mehrere Services gebunden, so enthält die Variable VCAP_SERVICES die Verbindungsinformationen für jede einzelne Serviceinstanz. Beispiel:
  
  ```
  {
   "VCAP_SERVICES": {
    "AppScan Dynamic Analyzer": [
     {
      "credentials": {
       "bindingid": "0ab3162a-867e-4137-a2e7-39463a89472e",
       "password": "xE/jh/PlRj3ruuy8RCl8JNyEywaivRH1xXSZcbVExKg="
      },
      "label": "AppScan Dynamic Analyzer",
      "name": "AppScan Dynamic Analyzer-9q",
      "plan": "standard",
      "tags": [
       "Security",
       "security",
       "ibm_created"
      ]
     }
    ],
    "mysql-5.5": [
     {
      "credentials": {
       "host": "23.246.200.38",
       "hostname": "23.246.200.38",
       "name": "d296abcc06c9e418b94abcaafdf547620",
       "password": "peRiYCG4ZYqu3",
       "port": 3307,
       "uri": "mysql://uzpGf7eGJ7mtB:peRiYCG4ZYqu3@23.246.200.38:3307/d296abcc06c9e418b94abcaafdf547620",
       "user": "uzpGf7eGJ7mtB",
       "username": "uzpGf7eGJ7mtB"
      },
      "label": "mysql-5.5",
      "name": "mysql-ix",
      "plan": "300",
      "tags": [
       "mysql",
       "relational",
       "data_management",
       "ibm_experimental"
      ]
     }
    ]
   }
  }
  ```
        
Sie haben auch Zugriff auf die vom DEA und von den Buildpacks festgelegten Umgebungsvariablen.

Folgende Variablen werden vom DEA definiert:

<dl>
  <dt><strong>HOME</strong></dt>
  <dd>Das Stammverzeichnis der bereitgestellten Anwendung.</dd>
  <dt><strong>MEMORY_LIMIT</strong></dt>
  <dd>Die maximale Speicherkapazität, die jede Instanz Ihrer Anwendung jeweils nutzen kann. Sie können den Wert in einer <span class="ph filepath">manifest.yml</span>-Datei der Anwendung oder bei der Push-Operation für die Anwendung in der Befehlszeile angeben.</dd>
  <dt><strong>PORT</strong></dt>
  <dd>Der Port des DEA für die Kommunikation mit der Anwendung. Der Port wird der Anwendung zum Zeitpunkt des Staging vom DEA zugeordnet.</dd>
  <dt><strong>PWD</strong></dt>
  <dd>Das aktuelle Arbeitsverzeichnis, in dem das Buildpack ausgeführt wird.</dd>
  <dt><strong>TMPDIR</strong></dt>
  <dd>Das Verzeichnis, in dem temporäre Dateien und Staging-Dateien gespeichert werden.</dd>
  <dt><strong>USER</strong></dt>
  <dd>Die Benutzer-ID, unter der der DEA ausgeführt wird.</dd>
  <dt><strong>VCAP_APP_HOST</strong></dt>
  <dd>Die IP-Adresse des DEA-Hosts.</dd>
  <dt><strong>VCAP_APPLICATION</strong></dt>
  <dd>Eine JSON-Zeichenfolge, die Informationen zur bereitgestellten Anwendung enthält. Die Informationen umfassen den Anwendungsnamen, die URIs, die Speicherbegrenzungen, die Zeitmarke bei Erreichen des aktuellen Anwendungsstatus usw. Beispiel: 
  <pre class="pre codeblock"><code>
  {
    "limits": {
        "mem": 512,
        "disk": 1024,
        "fds": 16384
    },
    "application_version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "application_name": "testapp",
    "application_uris": [
        "testapp.AppDomainNameng.mybluemix.net"
    ],
    "version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "name": "testapp",
    "space_name": "dev",
    "space_id": "c6ed3a8e-436b-43ac-9f96-b676ee335000",
    "uris": [
        "testapp.AppDomainNameng.mybluemix.net"
    ],
    "users": null,
    "application_id": "e984bb73-4c4e-414b-84b7-c28c87f84003",
    "instance_id": "09f50e22848d4ec0b943e9e487c23569",
    "instance_index": 0,
    "host": "0.0.0.0",
    "port": 61399,
    "started_at": "2015-01-16 06:50:51 +0000",
    "started_at_timestamp": 1421391051,
    "start": "2015-01-16 06:50:51 +0000",
    "state_timestamp": 1421391051
}
</code></pre></dd>
  <dt><strong>VCAP_SERVICES</strong></dt>
  <dd>Eine JSON-Zeichenfolge, die Informationen des Service enthält, der an die bereitgestellte Anwendung gebunden ist. Beispiel:
  <pre class="pre codeblock"><code>
  {
    "mysql-5.5": [
        {
            "name": "mysql-ix",
            "label": "mysql-5.5",
            "tags": [
                "mysql",
                "relational",
                "data_management",
                "ibm_experimental"
            ],
            "plan": "300",
            "credentials": {
                "name": "d296abcc06c9e418b94abcaafdf547620",
                "hostname": "23.246.200.38",
                "host": "23.246.200.38",
                "port": 3307,
                "user": "uzpGf7eGJ7mtB",
                "username": "uzpGf7eGJ7mtB",
                "password": "peRiYCG4ZYqu3",
                "uri": "mysql://uzpGf7eGJ7mtB:peRiYCG4ZYqu3@23.246.200.38:3307/d296abcc06c9e418b94abcaafdf547620"
            }
        }
    ]
}
</code></pre></dd>

</dl>

Von Buildpacks definierte Variablen sind für jedes Buildpack unterschiedlich. Informationen zu weiteren kompatiblen Buildpacks finden Sie unter [Buildpacks](https://github.com/cloudfoundry-community/cf-docs-contrib/wiki/Buildpacks){:new_window}.

<ul>
    <li>Folgende Variablen werden vom Liberty-Buildpack definiert:
	
	  <dl>
	  <dt><strong>JAVA_HOME</strong></dt>
	  <dd>Die Position des Java-SDK, das die Anwendung ausführt.</dd>
	  <dt><strong>IBM_JAVA_OPTIONS</strong></dt>
	  <dd>Die Java-SDK-Optionen, die bei Ausführung der Anwendung verwendet werden sollen.</dd>
	  <dt><strong>IBM_JAVA_COMMAND_LINE</strong></dt>
	  <dd>Der Java-Befehl zum Starten einer Liberty-Profil-Serverinstanz im DEA.</dd>
	  <dt><strong>WLP_USR_DIR</strong></dt>
	  <dd>Die Position der gemeinsam genutzten Ressourcen und Serverdefinitionen beim Starten einer Liberty-Profil-Serverinstanz im DEA.</dd>
	  <dt><strong>WLP_OUTPUT_DIR</strong></dt>
	  <dd>Die Position der generierten Ausgabe, z. B. Protokolldateien oder das Arbeitsverzeichnis einer aktiven Liberty-Profil-Serverinstanz.</dd>
	  </dl>
</li>   
<li>Folgende Variablen werden vom Node.js-Buildpack definiert:
	<dl>
	<dt><strong>BUILD_DIR</strong></dt>
	<dd>Das Verzeichnis der Node.js-Laufzeitumgebung.</dd>
	<dt><strong>CACHE_DIR</strong></dt>
	<dd>Das Verzeichnis, das die Node.js-Laufzeitumgebung für das Caching verwendet.</dd>
	<dt><strong>PATH</strong></dt>
	<dd>Der Systempfad, der von der Node.js-Laufzeitumgebung verwendet wird.</dd>
	</dl>
</li>
</li>
</ul>	

Sie können den folgenden Node.js-Beispielcode zum Abrufen des Werts der Umgebungsvariablen VCAP_SERVICES verwenden:

```
if (process.env.VCAP_SERVICES) {
    var env = JSON.parse (process.env.VCAP_SERVICES);
    myvar = env.foo[bar].foo;
}
```

Weitere Informationen zu den einzelnen Umgebungsvariablen finden Sie unter [Cloud Foundry-Umgebungsvariablen](http://docs.cloudfoundry.org/devguide/deploy-apps/environment-variable.html){:new_window}.

## Anwendungsbereitstellungen anpassen
{: #customize_dep}

Sie können Bereitstellungstasks für Ihre Anwendungen anpassen. So können Sie beispielsweise die Startbefehle für ihre Anwendungen angeben und Ihre Anwendungsstartumgebung konfigurieren.
{:shortdesc}

### Startbefehle angeben

Zum Angeben von Startbefehlen für Ihre Anwendung können Sie eine der nachstehenden Methoden verwenden. Die vom Buildpack bereitgestellten standardmäßigen Startbefehle werden durch die von Ihnen angegebenen Startbefehle überschrieben.

**Hinweis:** Wenn die Startbefehle des Buildpacks Vorrang haben sollen, geben Sie **null** als Startbefehl an.

  * Verwenden Sie den Befehl **cf push** und geben Sie den Parameter '-c' an. Wenn Sie beispielsweise eine Node.js-Anwendung bereitstellen, können Sie den Startbefehl **node app.js** im Parameter '-c' angeben:
  
  ```
  cf push appname -p app_path -c "node app.js"
  ```
  
  * Verwenden Sie den Parameter 'command' in der Datei `manifest.yml`. Wenn Sie beispielsweise eine Node.js-Anwendung bereitstellen, können Sie den Startbefehl **node app.js** in der Manifestdatei angeben:
  
  ```
  command: node app.js
  ```
  

### Benutzerdefinierte Umgebungsvariablen hinzufügen
{: #ud_env}

Benutzerdefinierte Umgebungsvariablen sind für eine Anwendung spezifisch. Sie haben die folgenden Möglichkeiten, einer aktiven App eine benutzerdefinierte Umgebungsvariable hinzuzufügen:

  * Verwenden Sie die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle. Führen Sie die folgenden Schritte aus:
    1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf die Kachel Ihrer App. Die Detailseite für die App wird angezeigt.
	2. Klicken Sie im linken Navigationsbereich auf **Umgebungsvariablen**.
	3. Klicken Sie auf **USER-DEFINED** (Benutzerdefiniert) und anschließend auf **ADD** (Hinzufügen).
	4. Füllen Sie die erforderlichen Felder aus und klicken Sie auf **SAVE** (Speichern).
  * Verwenden Sie die Befehlszeilenschnittstelle 'cf'. Fügen Sie eine benutzerdefinierte Variable mit dem Befehl `cf set-env` hinzu. Beispiel: 
    ```
    cf set-env appname Umgebungsvariablenname Umgebungsvariablenwert
    ```
	
  * Mithilfe der Datei `manifest.yml`. Fügen Sie Wertepaare in der Datei hinzu. Beispiel: 
    ```
	env:
      VAR1:wert1
      VAR2:wert2
    ```
	
Wenn Sie eine benutzerdefinierte Umgebungsvariable hinzugefügt haben, können Sie den folgenden Node.js-Beispielcode verwenden, um den Wert der Variablen abzurufen, die Sie definiert haben:

```
var myEnv = process.env.env_var_name;
console.log("My user defined = " + myEnv);
```
	
### Startumgebung konfigurieren

Zur Konfiguration der Startumgebung für Ihre Anwendung können Sie Shell-Scripts zum Verzeichnis `/.profile.d` hinzufügen. Das Verzeichnis `/.profile.d` befindet sich unter dem Buildverzeichnis Ihrer Anwendung. Scripts im Verzeichnis `/.profile.d` werden von {{site.data.keyword.Bluemix_notm}} ausgeführt, bevor die Anwendung ausgeführt wird. So können Sie beispielsweise die Umgebungsvariable NODE_ENV auf **production** setzen, indem Sie eine Datei `node_env.sh` mit dem folgenden Inhalt unter dem Verzeichnis `/.profile.d` einreihen:

```
export NODE_ENV=production;
```

###Hochladen von Dateien und Verzeichnissen verhindern

Bei der Verwendung der Befehlszeilenschnittstelle 'cf' für die Bereitstellung einer Anwendung können Sie Zeit für das Hochladen sparen, wenn Sie bestimmte Dateien und Verzeichnisse auslassen, die {{site.data.keyword.Bluemix_notm}} an anderer Stelle abrufen kann. Damit diese Dateien und Verzeichnisse nicht nach {{site.data.keyword.Bluemix_notm}} hochgeladen werden, können Sie im Stammverzeichnis Ihrer Anwendung eine Datei vom Typ `.cfignore` erstellen.

**Hinweis:** Die Datei `.cfignore` muss das UTF-8-Format aufweisen.

Die Datei mit der Endung `.cfignore` enthält die Namen der Dateien und Verzeichnisse, die Sie ignorieren möchten; dabei steht jeder Name in einer einzelnen Zeile. Sie können einen Stern (*) als Platzhalterzeichen verwenden. Wenn Sie ein Verzeichnis angeben, werden zudem alle Dateien und Unterverzeichnisse in diesem Verzeichnis ignoriert. Der folgende Inhalt der Datei mit der Endung `.cfignore` gibt z. B. an, dass alle Dateien mit der Endung `.swp` und alle Dateien und Unterverzeichnisse des Verzeichnisses `tmp/` nicht nach {{site.data.keyword.Bluemix_notm}} hochgeladen werden.

```
*.swp
tmp/
```

# Zugehörige Links
{: #rellinks}

## Zugehörige Links
{: #general}

* [Bereitstellung mit Anwendungsmanifesten](http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){:new_window}
* [CF-Manifestgenerator](http://cfmanigen.mybluemix.net/){:new_window}
* [Einführung in CF Version 6](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html){:new_window}
* [Einführung in IBM Continuous Delivery Pipeline for Bluemix](../services/DeliveryPipeline/index.html#getstartwithCD)
