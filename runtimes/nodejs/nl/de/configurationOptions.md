---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Konfigurationsoptionen
{: #configuration_options}
{: shortdesc}

Für die Konfiguration des sdk-for-nodejs-Buildpacks stehen eine Reihe von Optionen zur Verfügung.

## NPM-Scripts
{: #npm_scripts}
NPM stellt eine Scripting-Funktion bereit, mit der Sie Scripts einschließlich der Scripts **preinstall** und **postinstall** ausführen können, die vor und nach der Installation Ihrer Knotenmodule (node_modules) installiert werden.  Alle Einzelheiten dazu finden Sie unter [npm-scripts ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://docs.npmjs.com/misc/scripts).

## Caching-Verhalten
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
