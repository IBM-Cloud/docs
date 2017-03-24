---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Node.js-Ressourcen schützen
{: #protecting-resources-nodejs}

Sie können das {{site.data.keyword.appid_short}}-Server-SDK verwenden, um Ressourcen in Ihrer Node.js-App zu schützen.
{:shortdesc}

## Vorbereitungen
{: #before-you-begin}

* Sie sollten mit der Entwicklung von Node.js-Anwendungen in {{site.data.keyword.Bluemix_notm}} vertraut sein.
* Das {{site.data.keyword.appid_short_notm}}-Server-SDK erfordert, dass Ihr Node.js-Server mit dem <a href="http://expressjs.com/" target="_blank">Express-Framework <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> implementiert ist.

**Hinweis**: Es gibt andere Frameworks, die `Express`-Frameworks verwenden, wie zum Beispiel LoopBack. Sie können das {{site.data.keyword.appid_short_notm}}-Server-SDK mit einem beliebigen dieser Frameworks verwenden.

## Informationen zum Server-SDK
{: #about}

Das {{site.data.keyword.appid_short_notm}}-Server-SDK stellt eine ApiStrategy-Passwort-Strategie zur Verfügung, die in Back-End-Anwendungen verwendet werden, die in {{site.data.keyword.Bluemix_notm}} bereitgestellt werden. Zum Schutz Ihrer App gegen unbefugten Zugriff müssen Sie Ihren Node.js-Server mit ApiStrategy instrumentieren. Das NPM-Modul `appid-serversdk-nodejs` stellt die Passport-Strategie 'ApiStrategy' und eine Verifizierungsmethode bereit, um das von {{site.data.keyword.appid_short_notm}} ausgegebene Zugriffstoken und ID-Token zu validieren.

Das {{site.data.keyword.appid_short_notm}}-Server-SDK verwendet das Passport-Framework, um die Berechtigung umzusetzen, siehe <a href="http://passportjs.org/" target="_blank">Passport-Framework <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.


## Server-SDK installieren
{: #protecting-resources-serversdk}

1. Öffnen Sie mithilfe der Befehlszeile das Verzeichnis mit Ihrer Node.js-App.
2. Führen Sie die folgenden Befehle aus:

  ```
  npm install -save express
  npm install -save passport
  npm install -save appid-serversdk-nodejs
  ```
  {:pre}

## Ressourcen in Node.js schützen
{: #protecting-resources-nodesdk}

Das folgende Snippet demonstriert, wie `ApiStrategy` in einer einfachen Express-Anwendung zum Schutz der GET-Methoden für den Endpunkt `/protected` verwendet wird.

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var ApiStrategy = require('appid-serversdk-nodejs').ApiStrategy;

  passport.use(new ApiStrategy());
  var app = express();
  app.use(passport.initialize());

  app.get('/protected', passport.authenticate('appid-api-strategy', {session: false }),
      function(request, response){
          console.log("Securty context", request.securityContext)    
          response.send(200, "Success!");
      }
  );

  app.listen(process.env.PORT);
  ```
  {:pre}

Sie können mit `WebAppStrategy` die Ressourcen von Webanwendungen schützen:

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var ApiStrategy = require('appid-serversdk-nodejs').WebStrategy;
  ```
  {:pre}

Weitere Informationen finden Sie in <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">GitHub-Repository <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.
