---

copyright:
  years: 2017
lastupdated: "2017-03-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Protecting Node.js resources
{: #protecting-resources-nodejs}

You can use the {{site.data.keyword.appid_short}} server SDK to protect resources in your Node.js app.
{:shortdesc}

## Before you begin
{: #before-you-begin}

* You should be familiar with developing Node.js applications on {{site.data.keyword.Bluemix_notm}}, see [Creating apps with SDK for Node.js](/docs/runtimes/nodejs/index.html#nodejs_runtime).
* The {{site.data.keyword.appid_short_notm}} server SDK requires that your Node.js server is implemented with the <a href="http://expressjs.com/" target="_blank">Express framework <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

**Note**: There are other frameworks that use `Express` frameworks, such as LoopBack. You can use the {{site.data.keyword.appid_short_notm}} server SDK with any of these frameworks.

## About the server SDK
{: #about}

The {{site.data.keyword.appid_short_notm}} server SDK provides an ApiStrategy passport strategy that is used in back-end applications that are deployed on {{site.data.keyword.Bluemix_notm}}. To protect your app from unauthorized access, you must instrument your Node.js server with the ApiStrategy. The appid-serversdk-nodejs npm module provides the ApiStrategy passport strategy and the verification method to validate the access token and ID token that are issued by {{site.data.keyword.appid_short_notm}}.

The {{site.data.keyword.appid_short_notm}} server SDK uses the Passport framework to enforce authorization, see <a href="http://passportjs.org/" target="_blank">Passport framework <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.


## Installing the server SDK
{: #protecting-resources-serversdk}

1. Using the command line, open the directory with your Node.js app.
2. Run the following commands:

    ```
    npm install -save express
    npm install -save passport
    npm install -save appid-serversdk-nodejs
    ```
    {:pre}

## Protecting resources in Node.js
{: #protecting-resources-nodesdk}

The following snippet demonstrates how to use `ApiStrategy` in a simple Express application, to protect the `/protected` endpoint GET methods.

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

You can use `WebAppStrategy` to protect web application resources:

    ```JavaScript

    var express = require('express');
    var passport = require('passport');
    var ApiStrategy = require('appid-serversdk-nodejs').WebStrategy;

    ```
    {:pre}

For more information, see the <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">GitHub repository <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
