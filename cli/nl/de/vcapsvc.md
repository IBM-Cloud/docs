
{:shortdesc: .shortdesc}

# VCAP-Services

*Letzte Aktualisierung: 9. November 2015*


Die Umgebungsvariable VCAP_SERVICES ist ein JSON-Objekt, das Informationen enthält,
die Sie für die Interaktion mit einer Serviceinstanz in {{site.data.keyword.Bluemix_notm}} verwenden können.
{:shortdesc}


## Wert der Umgebungsvariable VCAP_SERVICES abrufen
{:retrieving}

Die Umgebungsvariable VCAP_SERVICES ist ein JSON-Objekt, das Informationen enthält,
die Sie für die Interaktion mit einer Serviceinstanz in {{site.data.keyword.Bluemix_notm}} verwenden können.
Die Informationen umfassen den Namen der Serviceinstanz, den Berechtigungsnachweis und die URL für die Verbindung zu der Serviceinstanz.
Mit diesen Werten wird die Umgebungsvariable VCAP_SERVICES gefüllt, wenn Ihre Anwendung an eine Serviceinstanz in {{site.data.keyword.Bluemix_notm}} gebunden wird. 

Der Wert der Umgebungsvariable VCAP_SERVICES steht nur zur Verfügung, wenn Sie eine Serviceinstanz an Ihre Anwendung binden.
Sie können die Anwendungsumgebungsvariablen durch Verwendung des WebSocket-Konsolentreibers anzeigen. Im Folgenden wird ein Beispiel für die Verwendung des WebSocket-Konsolentreibers für die Anzeige von Umgebungsvariablen einer Node.js-Anwendung gezeigt. 

Führen Sie zuerst den Befehl aus, mit dem für Ihre Node.js-Anwendung eine erneute Push-Operation durchgeführt wird. ```
cf push -c "curl -s https://raw.githubusercontent.com/dmikusa-pivotal/cf-debug-tools/master/debug-console.sh | bash" yourapp```
Geben Sie als Nächstes die folgende URL ein: ```
https://yourapp.{APPDomain}/bash.sh
```
Klicken Sie auf der daraufhin angezeigten Seite auf das Häkchen, um das Tool zu verbinden. Setzen Sie anschließend den Befehl 'env' ab, um die Umgebungsvariablen Ihrer Anwendung anzuzeigen. Weitere Informationen zu den cf-Debug-Tools finden Sie unter [Debug
Tools for Cloud Foundry](https://github.com/dmikusa-pivotal/cf-debug-tools).## Bluemix-Infrastrukturebenen anzeigen
{:viewinfra}


{{site.data.keyword.Bluemix_notm}} abstrahiert und
verdeckt Betriebssystem- und Infrastrukturebenen, damit diese von Ihnen nicht verwaltet werden müssen. Gelegentlich
wünschen Sie aber möglicherweise mehr Informationen über das Betriebssystem und die Middleware für Ihre
App. 

Sie können den Befehl 'cf stacks' ausführen, um die verfügbaren Stacks bzw. Rootdateisysteme anzuzeigen, auf denen Ihre Apps bereitgestellt werden sollen. Sie können bei der Verwendung des Befehls 'cf push' mit der Option *-s* und dem Stacknamen in *stack_name* auch den Stack angeben; dabei ist der 'stack_name' das Stammdateisystem, zum Beispiel `lucid64` oder `cflinuxfs2`:
```
cf push appName -s stack_name
```
Mithilfe des Befehls `cf buildpacks` können Sie die Middlewarekomponenten anzeigen, z. B. WebSphere Liberty Profile und SDK for Node.js; diese sind als Laufzeiten für die Ausführung Ihrer App verfügbar. Des Weiteren können Sie mithilfe des folgenden Befehls
die Laufzeitumgebung für Ihre App angeben:
```
cf push appName -b buildpackname
```
