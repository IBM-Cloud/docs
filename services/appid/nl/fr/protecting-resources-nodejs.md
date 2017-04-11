---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Protection des ressources Node.js
{: #protecting-resources-nodejs}

Vous pouvez utiliser le SDK serveur de {{site.data.keyword.appid_short}} pour protéger les ressources dans votre appli Node.js.
{:shortdesc}

## Avant de commencer
{: #before-you-begin}

* Familiarisez-vous avec le développement d'applications Node.js sur {{site.data.keyword.Bluemix_notm}}.
* Le SDK serveur d'{{site.data.keyword.appid_short_notm}} exige que votre serveur Node.js soit implémenté avec l'<a href="http://expressjs.com/" target="_blank">infrastructure Express<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

**Remarque** : d'autres infrastructure, notamment LoopBack, utilisent également `Express`. Vous pouvez utiliser le SDK serveur de
{{site.data.keyword.appid_short_notm}} avec toutes ces infrastructures.

## A propos du SDK serveur
{: #about}

Le SDK serveur d'{{site.data.keyword.appid_short_notm}} fournit une stratégie de passeport ApiStrategy qui est utilisée dans les applications de back-end déployées sur {{site.data.keyword.Bluemix_notm}}. Pour protéger votre application contre des accès non autorisés, vous devez instrumenter votre serveur Node.js avec la stratégie ApiStrategy. Le module `appid-serversdk-nodejs npm module` fournit la stratégie de passeport ApiStrategy et la méthode de vérification servant à valider le jeton d'accès et le jeton d'identité émis par {{site.data.keyword.appid_short_notm}}.

Le SDK serveur d'{{site.data.keyword.appid_short_notm}} utilise l'infrastructure Passport pour mettre en oeuvre l'autorisation. Voir <a href="http://passportjs.org/" target="_blank">Passport framework <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.


## Installation du SDK serveur
{: #protecting-resources-serversdk}

1. Depuis la ligne de commande, ouvrez le répertoire où réside votre application Node.js.
2. Exécutez les commandes suivantes :

  ```
  npm install -save express
  npm install -save passport
  npm install -save bluemix-appid
  ```
  {:pre}

## Protection des ressources dans Node.js
{: #protecting-resources-nodesdk}

Le fragment de code suivant illustre comment utiliser la stratégie `APIStrategy` dans une application Express simple pour protéger les méthodes GET de noeud final `/protected`.

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

Vous pouvez utiliser la stratégie `WebAppStrategy` pour protéger vos ressources d'application Web :

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var WebAppStrategy = require('bluemix-appid').WebAppStrategy;
  ```
  {:pre}

Pour plus d'informations, reportez-vous à la section <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}} Node.js dans le référentiel GitHub<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
