---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Protezione di risorse Node.js
{: #protecting-resources-nodejs}

Puoi utilizzare l'SDK server {{site.data.keyword.appid_short}} per proteggere risorse nella tua applicazione Node.js.
{:shortdesc}

## Prima di cominciare
{: #before-you-begin}

* Devi avere dimestichezza con lo sviluppo di applicazioni Node.js su {{site.data.keyword.Bluemix_notm}}.
* L'SDK server {{site.data.keyword.appid_short_notm}} richiede che il tuo server Node.js sia implementato con il <a href="http://expressjs.com/" target="_blank">framework Express <img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a>.

**Nota**: ci sono altri framework che utilizzano i framework `Express`, come ad esempio LoopBack. Puoi utilizzare l'SDK server {{site.data.keyword.appid_short_notm}} con uno qualsiasi di questi framework.


## Installazione dell'SDK server
{: #protecting-resources-serversdk}

1. Utilizzando la riga di comando, apri la directory con la tua applicazione Node.js.
2. Emettere i seguenti comandi:

  ```
  npm install -save express
  npm install -save passport
  npm install -save bluemix-appid
  ```
  {:pre}

## Protezione di risorse in Node.js
{: #protecting-resources-nodesdk}

L'SDK server {{site.data.keyword.appid_short_notm}} fornisce una strategia passport ApiStrategy utilizzata nella applicazioni di back-end distribuite in {{site.data.keyword.Bluemix_notm}}. Per proteggere la tua applicazione da accessi non autorizzati devi strumentare il tuo server Node.js con ApiStrategy. Il `modulo npm appid-serversdk-nodejs` fornisce la strategia passport ApiStrategy e il metodo di verifica per convalidare il token di accesso e il token ID emessi da {{site.data.keyword.appid_short_notm}}.

L'SDK server {{site.data.keyword.appid_short_notm}} utilizza il framework <a href="http://passportjs.org/" target="_blank">Passport <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per implementare l'autorizzazione.

Il seguente frammento di codice illustra come utilizzare `APIStrategy` in un'applicazione Express semplice per proteggere i metodi GET dell'endpoint `/protected`.

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var APIStrategy = require('bluemix-appid').APIStrategy;

  passport.use(new APIStrategy());
  var app = express();
  app.use(passport.initialize());

  app.get('/protected', passport.authenticate('APIStrategy.STRATEGY_NAME', {session: false }),
      function(request, response){
          console.log("Securty context", request.securityContext)    
          response.send(200, "Success!");
      }
  );

  app.listen(process.env.PORT);
  ```
  {:pre}

Puoi utilizzare `WebAppStrategy` per proteggere le risorse dell'applicazione web:

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var WebAppStrategy = require('bluemix-appid').WebAppStrategy;
  ```
  {:pre}

Per ulteriori informazioni, visita il <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}} Node.js GitHub repository <img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a>.
