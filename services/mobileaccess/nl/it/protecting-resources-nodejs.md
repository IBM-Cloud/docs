---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-10-27"

---

{:shortdesc: .shortdesc} 
{:codeblock:.codeblock}

# Protezione di risorse Node.js con {{site.data.keyword.amashort}}
{: #protecting-resources-nodejs}


Puoi utilizzare l'SDK server {{site.data.keyword.amashort}} per proteggere risorse nella tua applicazione Node.js.

## Prima di cominciare
{: #before-you-begin}

* Devi avere dimestichezza con lo sviluppo di applicazioni Node.js su {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni, vedi [Creazione di applicazioni con SDK for Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html#nodejs_runtime).
* l'SDK server {{site.data.keyword.amashort}} richiede che il tuo server Node.js sia implementato con il framework `Express`. Nota che ci sono altri framework che utilizzano i framework `Express`, come ad esempio LoopBack. Puoi utilizzare l'SDK server {{site.data.keyword.amashort}} con uno qualsiasi di questi framework. Per ulteriori informazioni sul framework Express, vedi [Expressjs.com ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://expressjs.com/ "Icona link esterno"){: new_window}.

## Informazioni sull'SDK server
{: #about}

L'SDK server {{site.data.keyword.amashort}} fornisce una strategia di passport `MCABackendStrategy` da utilizzare nelle applicazioni di back-end distribuite su IBM {{site.data.keyword.Bluemix_notm}}. Per proteggere la tua applicazione da accessi non autorizzati e ottenere le informazioni di monitoraggio, devi strumentare il tuo server Node.js con `MCABackendStrategy`. Il modulo npm `bms-mca-token-validation-strategy` fornisce il
metodo di verifica e la strategia passport `MCABackendStrategy` per convalidare il token di accesso e il token ID emessi da {{site.data.keyword.amashort}}. Questo modulo fornisce anche automaticamente le informazioni di monitoraggio relative agli eventi di sicurezza.

l'SDK server {{site.data.keyword.amashort}} utilizza il framework `Passport` per implementare l'autorizzazione.  Per ulteriori informazioni, vedi [Passportjs.org ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://passportjs.org/ "Icona link esterno"){: new_window}.

## Installazione dell'SDK server
{: #protecting-resources-serversdk}

Apri la directory con la tua applicazione Node.js su una riga di comando ed esegui questi comandi:

```
npm install -save express
npm install -save passport
npm install -save bms-mca-token-validation-strategy
```
{: codeblock}

## Protezione di risorse in Node.js
{: #protecting-resources-nodesdk}

Il seguente frammento di codice illustra come utilizzare `MCABackendStrategy` in una semplice applicazione Express per proteggere i metodi GET dell'endpoint `/protected`.

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
{: codeblock}
