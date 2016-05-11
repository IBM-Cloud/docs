---

copyright:
  years: 2015, 2016

---

# Node.js-Ressourcen mit {{site.data.keyword.amashort}} schützen
{: #protecting-resources-nodejs}

Sie können das {{site.data.keyword.amashort}}-Server-SDK verwenden, um Ressourcen in Ihrer Node.js-App zu schützen.

### Vorbereitungen
{: #before-you-begin}

* Sie müssen mit der Entwicklung von Node.js-Anwendungen in {{site.data.keyword.Bluemix_notm}} vertraut sein. Weitere Informationen finden Sie im Abschnitt zum [Erstellen von Apps mit dem SDK für Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html#nodejs_runtime).
* Das {{site.data.keyword.amashort}}-Server-SDK erfordert, dass Ihr Node.js-Server mit dem `Express`-Framework implementiert ist. Beachten Sie, dass es mehrere andere Frameworks gibt, die `Express`-Frameworks verwenden, wie zum Beispiel LoopBack. Sie können das {{site.data.keyword.amashort}}-Server-SDK mit einem beliebigen dieser Frameworks verwenden. Weitere Informationen zum Express-Framework finden Sie unter [Expressjs.com](http://expressjs.com/).

### Informationen zum {{site.data.keyword.amashort}}-Server-SDK
{: #about}

Das {{site.data.keyword.amashort}}-Server-SDK stellt die Passport-Strategie `MCABackendStrategy` für die Verwendung in Back-End-Anwendungen zur Verfügung, die in IBM {{site.data.keyword.Bluemix_notm}} bereitgestellt werden. Zum Schutz Ihrer App gegen unbefugten Zugriff und zum Erfassen von Überwachungsdaten müssen Sie Ihren Node.js-Server mit `MCABackendStrategy` instrumentieren. Das NPM-Modul `bms-mca-token-validation-strategy` stellt die Passport-Strategie `MCABackendStrategy` und eine Verifizierungsmethode bereit, um das von {{site.data.keyword.amashort}} ausgegebene Zugriffstoken und ID-Token zu validieren. Dieses Modul stellt außerdem automatisch Überwachungsdaten zu Sicherheitsereignissen bereit.

Das {{site.data.keyword.amashort}}-Server-SDK verwendet das `Passport`-Framework, um die Berechtigung umzusetzen.  Weitere Informationen finden Sie in [Passportjs.org](http://passportjs.org/).

### {{site.data.keyword.amashort}}-Server-SDK installieren
{: #protecting-resources-serversdk}

Öffnen Sie das Verzeichnis mit Ihrer Node.js-Anwendung in einer Befehlszeile und führen Sie die folgenden Befehle aus:

```
npm install -save express
npm install -save passport
npm install -save bms-mca-token-validation-strategy
```

### Ressourcen in Node.js schützen
{: #protecting-resources-nodesdk}

Das folgende Snippet demonstriert, wie `MCABackendStrategy` in einer einfachen Express-Anwendung zum Schutz der GET-Methoden für den Endpunkt `/protected` verwendet werden.

```JavaScript
var express = require('express');
var passport = require('passport');
var MCABackendStrategy = require('bms-mca-token-validation-strategy').MCABackendStrategy;

passport.use(new MCABackendStrategy());

var app = express();
app.use(passport.initialize());

app.get('/protected', passport.authenticate('mca-backend-strategy', {session: false }),
    function(request, response){
		console.log("Securty context", request.securityContext)    
		response.send(200, "Success!");
    }
);

app.listen(process.env.PORT);
```
