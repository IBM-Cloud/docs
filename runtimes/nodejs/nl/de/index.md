---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# SDK for Node.js
{: #nodejs_runtime}

Die Laufzeit von Node.js in {{site.data.keyword.Bluemix}} basiert auf dem Buildpack 'sdk-for-nodejs'.
Das Buildpack 'sdk-for-nodejs' bietet eine vollständige Laufzeitumgebung für Node.js-Apps.
{: shortdesc}

Das Buildpack 'sdk-for-nodejs' wird verwendet, wenn die Anwendung die Datei **package.json** im Stammverzeichnis enthält.

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix}} stellt eine Node.js-Starteranwendung bereit.  Die Node.js-Starteranwendung ist eine einfache Node.js-App, die Sie als Schablone für Ihre App verwenden können. Sie können mit der Starter-App experimentieren, Änderungen an der Bluemix-Umgebung vornehmen und diese mit einer Push-Operation übertragen. Lesen Sie als Hilfe für die Verwendung von Starteranwendungen [Starteranwendungen verwenden](/docs/cfapps/starter_app_usage.html).

## Startbefehl
{: #starup_commmand}

Für die Angabe eines Startbefehls für Ihre Bluemix Node.js-Anwendung wird empfohlen, dass Sie entweder das Element **Procfile** oder die Datei **package.json** verwenden.

Geben Sie im folgenden Format einen Startbefehl in Ihrem Element **Procfile** an. Dabei ist 'app.js' das js-Startscript für Ihre Anwendung.
```
web: node app.js
```
{: codeblock}

Speichern Sie das Element **Procfile** im Stammverzeichnis Ihrer Anwendung.

Wenn das Element **Procfile** nicht vorhanden ist, prüft das IBM Bluemix-Node.js-Buildpack, ob der Eintrag 'scripts.start' in der Datei **package.json** vorhanden ist. Im unten stehenden Beispiel ist 'app.js' wieder das js-Startscript für Ihre Anwendung.
```
{
    ...   
    "scripts": {
      "start": "node app.js"
    }
}
```
{: codeblock}

Wenn ein Eintrag für ein Startscript in der Datei **package.json** vorhanden ist, wird das Element **Procfile** automatisch erstellt. Der Inhalt des automatisch generierten Elements **Procfile** ist wie folgt:
```
    web: npm start
```
{: codeblock}

Weitere Informationen zum Element **Procfile** und zur Datei **package.json** finden Sie in [Tips for Node.js Applications](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html).

## Hinweise für die lokale Ausführung Ihrer Node.js-Anwendung
{: #hints}

Mithilfe dieser Informationen können Sie die Ausführung Ihrer Node.js-Anwendung lokal oder in Bluemix vereinfachen.

Im folgenden Beispiel wird ein Teil der Quelle für eine **js**-Datei gezeigt:
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

Wenn die Anwendung bei diesem Code in Bluemix ausgeführt wird, enthält die Umgebungsvariable PORT den internen Portwert von Bluemix , auf dem die App für eingehende Verbindungen empfangsbereit ist. Bei lokaler Ausführung der Anwendung ist die Umgebungsvariablen PORT nicht definiert, sodass **3000** als Portnummer verwendet wird. Durch diese Schreibung können Sie die Anwendung sowohl lokal für Testzwecke als auch in Bluemix ausführen, ohne Änderungen vornehmen zu müssen.

## Offlinemodus
{: #offline_mode}

Informationen zum Steuern des Buildpack-Zugriff auf externe Sites finden Sie unter [Offlinemodus](offlineMode.html). 

## App-Management
{{site.data.keyword.Bluemix}} stellt eine Anzahl Dienstprogramme für das Management und das Debugging Ihrer Node.js-App zur Verfügung.  Vollständige Details finden Sie in [App-Management](/docs/manageapps/app_mng.html).

## Verfügbare Versionen
{: #available_versions}

{{site.data.keyword.Bluemix}} stellt alle [zurzeit verfügbaren Node.js-Laufzeiten](http://nodejs.org/dist/) zur Verfügung. Davon stellt IBM Versionen zur Verfügung, die Erweiterungen und Fehlerkorrekturen enthalten. Weitere Informationen finden Sie in [Neueste Aktualisierungen für das Node.js-Buildpack](/docs/runtimes/nodejs/updates.html).

Das IBM Node.js-Buildpack stellt die IBM Laufzeitversionen in den Cache. Verwenden Sie die IBM SDK for Node.js-Laufzeit also in Ihrer Anwendung, erhalten Sie eine bessere Anwendungsleistung, wenn Ihre Anwendung mit einer Push-Operation an Bluemix übertragen wird.

Verwenden Sie den Parameter **node** im Abschnitt **engines** der Datei **package.json**, um die Version der Node.js-Laufzeit anzugeben, die Sie ausführen möchten.

Verwenden Sie den Parameter **npm** im Abschnitt **engines** der Datei **package.json**, wenn Sie eine andere als die mit Node.js im Paket vorhandene Version von 'npm' verwenden müssen.  

Lesen Sie folgendes Beispiel:

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "2.11.3"
  }
}
```
{: codeblock}

Für 'node' muss in der Datei **package.json** stets eine Version angegeben werden. Ist das nicht der Fall, wird die neueste Knotenversion verwendet.

## Konfigurationsoptionen
{: #configuration_options}

### NPM-Scripts
{: #npm_scripts}
NPM stellt eine Scripting-Funktion bereit, mit der Sie Scripts einschließlich der Scripts **preinstall** und **postinstall** ausführen können, die vor und nach der Installation Ihrer Knotenmodule (node_modules) installiert werden.  Vollständige Details finden Sie in [npm-scripts](https://docs.npmjs.com/misc/scripts).

### Caching-Verhalten
{: #cache_behavior}
{{site.data.keyword.Bluemix}} enthält pro Knotenanwendung ein Cacheverzeichnis, das von einem Build zum anderen erhalten bleibt. Der Cache speichert aufgelöste Abhängigkeiten, das heißt, sie werden nicht bei jeder Implementierung der App heruntergeladen und installiert.  Beispiel: Nehmen Sie an, die 'myapp' hängt von **express** ab.  Dann wird 'myapp' das erste Mal bereitgestellt, wenn das Modul **express** heruntergeladen wird.  Bei den nachfolgenden Implementierungen von 'myapp' wird die in den Cache gestellte Instanz von **express** verwendet. Das Standardverhalten sieht so aus, dass alle von NPM installierten Knotenmodule (node_modules) und alle von Bower installierten Bower-Komponenten (bower_components) in den Cache gestellt werden.

Legen Sie mithilfe der Variablen NODE_MODULES_CACHE fest, ob das Node-Buildpack den bei vorherigen Builds verwendeten Cache verwendet oder ignoriert. Der Standardwert ist 'true'.  Legen Sie zum Inaktivieren des Cachings für NODE_MODULES_CACHE den Wert 'false' fest, beispielsweise über die cf-Befehlszeile:
```
    $ cf set-env myapp NODE_MODULES_CACHE false
```
{: codeblock}

Beachten Sie, dass in Ihrer Anwendung enthaltene Knotenmodule (node_modules) nicht in den Cache gestellt werden.

Sie können das Array **cacheDirectories** im **package.json** der höchsten Ebene verwenden, um detailliert steuern zu können, welche Module in den Cache gestellt werden.  Wenn das Element **cacheDirectories** in der Datei **package.json** vorhanden ist, werden nur Module in den Cache gestellt, die sich im Array **cacheDirectories** befinden.  Im folgenden Beispiel werden nur Knotenmodule (node_modules) und Bower-Komponenten (bower_components) in den Cache gestellt.
```
{
  "cacheDirectories": ["node_modules","bower_components"],
  ...
}
```
{: codeblock}

### FIPS MODE
{: #fips_mode}

Die Node.js-Buildpackversionen v3.2-20160315-1257 sowie höhere Versionen unterstützen [FIPS](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards).  Setzen Sie die Umgebungsvariable FIPS_MODE auf 'true', wenn Sie eine FIPS-fähige Knotenengine verwenden möchten.
Beispiel:

```
    $ cf set-env myapp FIPS_MODE true
```
{: codeblock}

Beachten Sie, dass einige Knotenmodule möglicherweise nicht funktionieren, wenn FIPS_MODE auf 'true' gesetzt ist.  Beispiel: **Knotenmodule, die [MD5](https://en.wikipedia.org/wiki/MD5) nutzen, schlagen fehl**, wie beispielsweise [Express](http://expressjs.com/).  Im Falle von Express können Sie dieses Problem möglicherweise umgehen, indem Sie [etag](http://expressjs.com/en/api.html) in Ihrer
Expess-App auf 'false' setzen. Sie können Ihren Code beispielsweise wie folgt bearbeiten:
```
    app.set('etag', false);
```
{: codeblock}
Weitere Informationen finden Sie in diesem [stackoverflow-Post](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js).

**ANMERKUNG** [App-Management](/docs/manageapps/app_mng.html) und FIPS_MODE werden *NICHT* gleichzeitig unterstützt.  Wenn die Umgebungsvariable BLUEMIX_APP_MGMT_ENABLE eingestellt ist und die Umgebungsvariable FIPS_MODE auf 'true' gesetzt ist, kann für die App kein Staging durchgeführt werden.

Es gibt mehrere Möglichkeiten, den FIPS_MODE-Status zu überprüfen:
<ul>
<li> Sie können in der Datei 'staging_task.log' für Ihre Anwendung
nach einer Nachricht ähnlich der folgenden suchen:    

  <pre>
  Installing FIPS-enabled IBM SDK for Node.js (4.4.3) from cache
  </pre>
  {: codeblock}

Diese Nachricht teilt mit, dass eine FIPS-fähige node.js-Engine ausgeführt wird, aber nicht unbedingt, dass FIPS ausgeführt wird
</li>

<li> Sie können den Wert von **process.versions.openssl** prüfen. Beispiel:

  <pre>
  console.log('ssl version is [' +process.versions.openssl +']');
  </pre>
  {: codeblock}

Wenn die SSL-Version 'fips' enthält, unterstützt die verwendete SSL-Version FIPS.  
</li>

<li> Bei node.js Version 6 und höher können Sie den von crypto.fips zurückgegebenen Wert in Code wie dem folgenden prüfen:

  <pre>
  console.log('crypto.fips== [' +crypto.fips +']');
  </pre>
  {: codeblock}

Wenn der zurückgegebene Wert '1' ist, wird FIPS verwendet. Beachten Sie, dass crypto.fips für node.js-Versionen vor Version 6 den Wert *undefined* (nicht definiert) zurückgibt.
</li>
</ul>

#### Nodejs Version 4
{: #nodejs_v4_fips}

Die folgende Tabelle erläutert das Verhalten von node.js Version 4 bezüglich FIPS:

|                 | Ergebnis        |
| :-------------- | :------------ |
|FIPS_MODE=true   |Erfolg (1)    |
|FIPS_MODE !=true |Erfolg (2)    |

* Erfolg (1)
  * FIPS wird verwendet.
  * Die Datei staging_task.log enthält die Nachricht *Installing FIPS-enabled IBM SDK for Node.js*.
  * Der von process.versions.openssl zurückgegebene Wert enthält 'fips'.
* Erfolg (2)
  * FIPS wird *NICHT* verwendet.
  * Die Datei staging_task.log enthält *NICHT* die Nachricht *Installing FIPS-enabled IBM SDK for Node.js*.
  * Der von process.versions.openssl zurückgegebene Wert enthält *NICHT* 'fips'.

#### Nodejs Version 6
{: #nodejs_v6_fips}

Für die Ausführung im FIPS-Modus müssen Sie bei Node.js Version 6 neben der Einstellung von **FIPS_MODE=true** in Ihrem Startbefehl **--enable-fips** angeben, entsprechend dem folgenden Beispiel:
```
{
    ...   
    "scripts": {
      "start": "node --enable-fips app.js"
    }
}
```
{: codeblock}

Die folgende Tabelle erläutert das Verhalten von node.js Version 6 bezüglich FIPS.

|                 |--enable-fips  |KEIN --enable-fips |
| :-------------- | :------------ | :-------------- |
|FIPS_MODE=true   |Erfolg (1)    |Erfolg (2)      |
|FIPS_MODE !=true |Fehler (3)    |Erfolg (4)      |

* Erfolg (1)
  * FIPS wird verwendet.
  * Die Datei staging_task.log enthält die Nachricht *Installing FIPS-enabled IBM SDK for Node.js*.
  * Der von process.versions.openssl zurückgegebene Wert enthält 'fips'
  * crypto.fips gibt '1' zurück, was bedeutet, dass FIPS verwendet wird
* Erfolg (2)
  * FIPS wird *NICHT* verwendet.
  * Die Datei staging_task.log enthält die Nachricht *Installing FIPS-enabled IBM SDK for Node.js*.
  * Der von process.versions.openssl zurückgegebene Wert enthält 'fips'
  * crypto.fips gibt '0' zurück, was bedeutet, dass FIPS *NICHT* verwendet wird
* Fehler (3)
  * FIPS wird *NICHT* verwendet.
  * Die Datei staging_task.log enthält *NICHT* die Nachricht *Installing FIPS-enabled IBM SDK for Node.js*.
  * Das Staging schlägt mit der Nachricht 'ERR node: bad option: --enable-fips' fehl
* Erfolg (4)
  * FIPS wird *NICHT* verwendet.
  * Die Datei staging_task.log enthält *NICHT* die Nachricht *Installing FIPS-enabled IBM SDK for Node.js*.
  * Der von process.versions.openssl zurückgegebene Wert enthält *NICHT* 'fips'
  * crypto.fips gibt '0' zurück, was bedeutet, dass FIPS *NICHT* verwendet wird


## Node.js-Buildpacks

Bluemix stellt mehrere Versionen des Node.js-Buildpacks bereit.
* Das von IBM erstellte Buildpack **sdk-for-nodejs** ist das für Node.js-Anwendungen in Bluemix standardmäßig verwendete Buildpack.
* Das **nodejs_buildpack** ist ein Community-Buildpack, das von der Cloud Foundry-Community zur Verfügung gestellt wird.

Das Buildpack **sdk-for-nodejs** hat in Bluemix Vorrang vor dem Buildpack **nodejs_buildpack**. Wenn Sie mit Ihrer Anwendung das Buildpack **nodejs_buildpack** statt des Buildpacks **sdk-for-nodejs** verwenden wollen, müssen Sie Ihr Buildpack angeben, beispielsweise indem Sie mit dem Befehl **cf push** die Option Option '-b' angeben.

In der Regel stehen das aktuelle Buildpack **sdk-for-nodejs** und eine frühere Version zur Verfügung.  Mithilfe des Befehls **cf buildpacks** können Sie alle verfügbaren Buildpacks anzeigen.  Beispiel:
<pre>
      cf buildpacks
      Getting buildpacks...

      buildpack                         position   enabled   locked   filename   

      sdk_for_nodejs                    2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
      nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
      sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
</pre>
{: codeblock}

# Zugehörige Links
{: #rellinks}
## Allgemein
{: #general}
* [Neueste Aktualisierungen für das Node.js-Buildpack](/docs/runtimes/nodejs/updates.html)
* [App-Management](/docs/manageapps/app_mng.html)
* [Node.js](https://nodejs.org)
* [IBM API Connect](https://strongloop.com/)
