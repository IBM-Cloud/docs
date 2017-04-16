---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-10-27"

---

{:shortdesc: .shortdesc} 
{:codeblock:.codeblock}

# Protection des ressources Node.js à l'aide de {{site.data.keyword.amashort}}
{: #protecting-resources-nodejs}


Vous pouvez utiliser le SDK serveur de {{site.data.keyword.amashort}} pour protéger les ressources dans votre appli Node.js.

## Avant de commencer
{: #before-you-begin}

* Vous devez savoir développer des applications Node.js sur {{site.data.keyword.Bluemix_notm}}. Pour plus d'informations, voir
[Création d'applications à l'aide du SDK pour Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html#nodejs_runtime).
* Le SDK serveur de {{site.data.keyword.amashort}} nécessite que le serveur Node.js soit implémenté avec l'infrastructure `Express`. Notez
que d'autres infrastructures, telle que LoopBack, utilisent les structures `Express`. Vous pouvez utiliser le SDK serveur de
{{site.data.keyword.amashort}} avec toutes ces infrastructures. Pour plus d'informations sur la structure Express, accédez au site [Expressjs.com ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://expressjs.com/ "Icône de lien externe"){: new_window}.

## A propos du SDK serveur
{: #about}

Le SDK serveur de {{site.data.keyword.amashort}} fournit une stratégie de passeport `MCABackendStrategy` pour son utilisation
dans les applications de back end déployées sur IBM {{site.data.keyword.Bluemix_notm}}. Pour protéger votre appli des accès non autorisés et obtenir des informations de surveillance, vous devez instrumenter votre serveur Node.js avec `MCABackendStrategy`. Le
module npm `bms-mca-token-validation-strategy` fournit la stratégie de passeport `MCABackendStrategy` et la méthode de
vérification pour valider le jeton d'accès et le jeton d'ID émis par {{site.data.keyword.amashort}}. Ce module fournit aussi automatiquement les informations de surveillance relatives aux événements de sécurité.

Le SDK serveur de {{site.data.keyword.amashort}} utilise l'infrastructure `Passport` pour mettre en oeuvre l'autorisation.  Pour plus d'informations, accédez au site [Passportjs.org ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://passportjs.org/ "Icône de lien externe"){: new_window}.

## Installation du SDK serveur
{: #protecting-resources-serversdk}

Sur une ligne de commande, ouvrez le répertoire contenant votre application Node.js set exécutez les commandes suivantes :

```
npm install -save express
npm install -save passport
npm install -save bms-mca-token-validation-strategy
```
{: codeblock}

## Protection des ressources dans Node.js
{: #protecting-resources-nodesdk}

Le fragment de code suivant illustre la manière d'utiliser `MCABackendStrategy` dans une application Express simple pour protéger les méthodes
GET du noeud final `/protected`.

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
