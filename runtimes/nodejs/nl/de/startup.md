---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Startbefehl
{: #startup_commmand}

Für die Angabe eines Startbefehls für Ihre Bluemix Node.js-Anwendung wird empfohlen, dass Sie entweder das Element **Procfile** oder die Datei **package.json** verwenden.{: shortdesc}

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

Weitere Informationen zum Element **Procfile** und zur Datei **package.json** finden Sie in [Tips for Node.js Applications ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html).
