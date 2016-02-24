{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*Letzte Aktualisierung: 12. Januar 2016*

# Node.js-Laufzeit
{: #nodejs_runtime}

Die Node.js-Laufzeit in {{site.data.keyword.Bluemix}} basiert auf dem Buildpack sdk-for-nodejs.
Das Buildpack sdk-for-nodejs stellt eine vollständige Laufzeitumgebung für Node.js-Apps bereit.
{: shortdesc}

Das Node.js-Buildpack wird verwendet, wenn sich die Datei **package.json** im Stammverzeichnis der Anwendung befindet.

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix}} stellt eine Node.js-Starteranwendung zur Verfügung.  Die Node.js-Starteranwendung ist eine einfache Node.js-App, die eine Vorlage bereitstellt, die Sie für Ihre App nutzen können. Sie können die Starter-App ausprobieren und Änderungen vornehmen und diese dann per Push-Operation an die Bluemix-Umgebung übertragen. Hilfeinformationen zur Verwendung der Starteranwendung finden Sie im Thema zur [Verwendung der Starteranwendungen](../../cfapps/starter_app_usage.html).

## Startbefehl
{: #starup_commmand}

Es wird empfohlen, zum Angeben eines Startbefehls für Ihre Bluemix-Node.js-Anwendung die Datei **Procfile** oder die Datei **package.json** zu verwenden.

Geben Sie in der Datei **Procfile** im Formular, das im Anschluss folgt, einen Startbefehl an. Dabei ist 'app.js' das js-Startscript für die Anwendung.
```
web: node app.js```
{: codeblock}

Speichern Sie die Datei **Procfile** im Stammverzeichnis Ihrer Anwendung. 

Wenn keine Datei des Typs **Procfile** vorhanden ist, sucht das IBM Bluemix-Node.js-Buildpack in der Datei **package.json** nach dem Eintrag 'scripts.start'. Im unten stehenden Beispiel ist 'app.js' ebenfalls das js-Startscript für die Anwendung.
```
{
  ...   
"scripts": {

    "start": "node app.js"
}
}
```
{: codeblock}

Wenn ein solcher Eintrag in der Datei **package.json** vorhanden ist, wird die Datei **Procfile** automatisch generiert. Der Inhalt der automatisch generierten Datei **Procfile** sieht wie folgt aus:
```
web: npm start```
{: codeblock}

Weitere Informationen zu den Dateien **Procfile** und **package.json** finden Sie unter
[Tips for Node.js Applications](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html). 

## Hinweise zur lokalen Ausführung Ihrer Node.js-Anwendung
{: #hints}

Mit diesen Angaben vereinfachen Sie sowohl die lokale Ausführung der Node.js-Anwendung als auch deren Ausführung in Bluemix.

Das folgende Beispiel zeigt einen Teil der Quelle für eine **js**-Datei:
```
var port = (process.env.VCAP_APP_PORT || 3000);
var host = (process.env.VCAP_APP_HOST || 'localhost');
```
{: codeblock}

Wenn die Anwendung mit diesem Code in Bluemix ausgeführt wird, enthalten die Umgebungsvariablen VCAP_APP_HOST und VCAP_APP_PORT die Bluemix-internen Werte für Host und Port, bei denen die App für eingehende Verbindungen empfangsbereit ist. Bei einer lokalen Ausführung der Anwendung sind VCAP_APP_HOST und VCAP_APP_PORT nicht definiert; somit wird **localhost** als Host und **3000** als Portnummer verwendet. Bei dieser Konfiguration kann die Anwendung ohne weitere Änderungen lokal zu Testzwecken und in Bluemix ausgeführt werden.

## App-Management
{{site.data.keyword.Bluemix}} stellt eine Reihe von Dienstprogrammen für Verwaltung und Debugging Ihrer Node.js-App bereit.  Ausführliche Details hierzu finden Sie unter [App-Management](../../manageapps/app_mng.html).

## Verfügbare Versionen
{: #available_versions}

In {{site.data.keyword.Bluemix}} werden alle [derzeit verfügbaren Node.js-Laufzeiten](http://nodejs.org/dist/) bereitgestellt. IBM stellt dafür Versionen bereit, die funktionale Erweiterungen und Fehlerkorrekturen enthalten. Informationen hierzu finden Sie unter [Neueste Aktualisierungen für das Node.js-Buildpack](updates.html).

Das IBM Node.js-Buildpack stellt alle IBM Laufzeitversionen in den Cache. Daher erzielen Sie bei Verwendung der IBM SDK for Node.js-Laufzeit in Ihrer Anwendung eine bessere Anwendungsleistung, wenn die Anwendung per Push-Operation an Bluemix übertragen wird.

Geben Sie mithilfe des Parameters **node** im Abschnitt **engines** der Datei **package.json** die Version der Node.js-Laufzeit an, die Sie ausführen möchten.

Verwenden Sie den Parameter **npm** im Abschnitt **engines** der Datei **package.json**, wenn Sie eine Version von npm angeben müssen, die sich von der Version unterscheidet, die im Lieferumfang von Node.js enthalten ist.  

Beispiel:

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4"
     "npm": "2.11.3"
  }
}
```
{: codeblock}

Eine Knotenversion muss stets in der Datei **package.json** angegeben werden. Wenn keine Angabe erfolgt, wird die neueste Knotenversion verwendet.

## Konfigurationsoptionen
{: #configuration_options}

### NPM-Scripts
{: #npm_scripts}
NPM stellt eine Scripting-Funktion bereit, mit deren Hilfe Sie Scripts ausführen können, einschließlich der Scripts **preinstall** und **postinstall**, die vor und nach der Installation Ihrer Knotenmodule (node_modules) angewendet werden.  Ausführliche Details hierzu finden Sie unter [npm-scripts](https://docs.npmjs.com/misc/scripts).

### Caching-Verhalten
{: #cache_behavior}
{{site.data.keyword.Bluemix}} pflegt pro Knotenanwendung ein Cacheverzeichnis, das zwischen den Builds erhalten bleibt. Im Cache werden aufgelöste Abhängigkeiten gespeichert; sie werden also nicht jedes Mal, wenn die App bereitgestellt wird, heruntergeladen und installiert.  Beispiel: Angenommen, 'myapp' ist von **express** abhängig.  Wenn dann 'myapp' das erste Mal bereitgestellt wird, wird das Modul **expess** heruntergeladen.  Bei nachfolgenden Bereitstellungen von 'myapp' wird die im Cache stehende Instanz von **express** verwendet.

Verwenden Sie die Variable NODE_MODULES_CACHE, um festzustellen, ob das Node-Buildpack den Cache früherer Builds verwendet oder nicht. Der Standardwert ist true.  Zur Inaktivierung des Caching müssen Sie NODE_MODULES_CACHE auf 'false' setzen, beispielsweise über die Befehlszeile 'cf':
```
cf set-env myapp NODE_MODULES_CACHE false
```
{: codeblock}

Beachten Sie, dass Knotenmodule (node_modules), die in Ihrer Anwendung integriert sind, nicht in den Cache gestellt werden.

Für eine differenziertere Kontrolle über die im Cache gespeicherten Module können Sie in der übergeordneten Datei **package.json** ein Array des Typs **cacheDirectories** verwenden.  Ist das Element **cacheDirectories** in der Datei **package.json** enthalten, werden nur die Module, die sich um Array **cacheDirectories** befinden, im Cache gespeichert.  Im folgenden Beispiel werden nur Knotenmodule (node_modules) und Bower-Komponenten (bower_components) im Cache gespeichert.
```
{
  "cacheDirectories": ["node_modules","bower_components"],
  ...
}
```
{: codeblock}

## Node.js-Buildpacks

Bluemix stellt mehrere Versionen des Node.js-Buildpacks bereit.
* Das von IBM erstellte Buildpack **sdk-for-nodejs** ist das für Node.js-Anwendungen in Bluemix verwendete Standard-Buildpack.
* Das Buildpack **nodejs_buildpack** ist das externe Buildpack, das von der Cloud Foundry-Community bereitgestellt wird.

Das Buildpack **sdk-for-nodejs** hat in Bluemix Vorrang vor dem Buildpack **nodejs_buildpack**. Wenn Sie anstelle von **sdk-for-nodejs** das Buildpack **nodejs_buildpack** für Ihre Anwendung verwenden möchten, müssen Sie das Buildpack z. B. mit der Option -b im Befehl **cf push** angeben.

Standardmäßig sind das aktuelle Buildpack **sdk-for-nodejs** und eine frühere Version verfügbar.  Verwenden Sie den Befehl **cf buildpacks**, um alle verfügbaren Buildpacks anzuzeigen.  Beispiel:
```
cf buildpacks
Getting buildpacks...

buildpack                      position          enabled          locked          filename	
   
...
sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
```
{: codeblock}


## ZUGEHÖRIGE LINKS
{: #related_links}
* [Neueste Aktualisierungen für das Node.js-Buildpack](updates.html)
* [App-Management](../../manageapps/app_mng.html)
* [Node.js](https://nodejs.org)
* [StrongLoop](https://strongloop.com)
