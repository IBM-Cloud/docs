---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-27"

---

# Protecting Node.js resources with {{site.data.keyword.amashort}}
{: #protecting-resources-nodejs}


You can use the {{site.data.keyword.amashort}} server SDK to protect resources in your Node.js app.

## Before you begin
{: #before-you-begin}

* You must be familiar with developing Node.js applications on {{site.data.keyword.Bluemix_notm}}. For more information, see [Creating apps with SDK for Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html#nodejs_runtime).
* The {{site.data.keyword.amashort}} server SDK requires that your Node.js server is implemented with the `Express` framework. Note that there are other frameworks that use `Express` frameworks, such as LoopBack. You can use the {{site.data.keyword.amashort}} server SDK with any of these frameworks. For more information about the Express framework, see [Expressjs.com](http://expressjs.com/).

## About the  server SDK
{: #about}

The {{site.data.keyword.amashort}} server SDK provides a `MCABackendStrategy` passport strategy, to be used in back-end applications deployed on IBM {{site.data.keyword.Bluemix_notm}}. To protect your app from unauthorized access and get monitoring information, you must instrument your Node.js server with the `MCABackendStrategy`. The `bms-mca-token-validation-strategy` npm module provides the `MCABackendStrategy` passport strategy and verification method to validate the access token and ID token that was issued by {{site.data.keyword.amashort}}. This module also automatically supplies monitoring information about security events.

The {{site.data.keyword.amashort}} server SDK uses the `Passport` framework to enforce authorization.  For more information, see [Passportjs.org](http://passportjs.org/).

## Installing the  server SDK
{: #protecting-resources-serversdk}

Open the directory with your Node.js application on a command line and run the following commands:

```
npm install -save express
npm install -save passport
npm install -save bms-mca-token-validation-strategy
```

## Protecting resources in Node.js
{: #protecting-resources-nodesdk}

The following snippet demonstrates how to use `MCABackendStrategy` in a simple Express application, to protect the `/protected` endpoint GET methods.

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
