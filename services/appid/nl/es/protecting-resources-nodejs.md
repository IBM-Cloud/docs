---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Protección de recursos Node.js
{: #protecting-resources-nodejs}

Puede utilizar el SDK del servidor de {{site.data.keyword.appid_short}} para proteger recursos en la app Node.js.
{:shortdesc}

## Antes de empezar
{: #before-you-begin}

* Familiarícese con el desarrollo de aplicaciones Node.js en {{site.data.keyword.Bluemix_notm}}.
* El SDK del servidor de {{site.data.keyword.appid_short_notm}} necesita que se implemente el servidor de Node.js con la <a href="http://expressjs.com/" target="_blank">infraestructura Express <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.

**Nota**: hay otras infraestructuras que utilizan infraestructuras `Express`, como LoopBack. Puede utilizar el SDK del servidor de {{site.data.keyword.appid_short_notm}} con cualquiera de estas infraestructuras.


## Instalación del SDK del servidor
{: #protecting-resources-serversdk}

1. Desde la línea de mandatos, abra el directorio con su app Node.js.
2. Ejecute los siguientes mandatos:

  ```
  npm install -save express
  npm install -save passport
  npm install -save bluemix-appid
  ```
  {:pre}

## Protección de recursos en Node.js
{: #protecting-resources-nodesdk}

El SDK del servidor de {{site.data.keyword.appid_short_notm}} proporciona una estrategia de pasaporte de ApiStrategy que se utiliza en aplicaciones de fondo que se despliegan en {{site.data.keyword.Bluemix_notm}}. Para proteger la app de accesos no autorizados, debe instrumentar el servidor Node.js con ApiStrategy. El `módulo appid-serversdk-nodejs npm` proporciona la estrategia de pasaporte ApiStrategy y el método de verificación para validar la señal de acceso y la señal de identidad que emite {{site.data.keyword.appid_short_notm}}.

El SDK del servidor de {{site.data.keyword.appid_short_notm}} utiliza la <a href="http://passportjs.org/" target="_blank">infraestructura Passport <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para imponer la autorización.

El siguiente fragmento de código muestra cómo utilizar `APIStrategy` en una aplicación Express sencilla para proteger los métodos GET del punto final `/protected`.

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

Puede utilizar `WebAppStrategy` para proteger los recursos de aplicaciones web:

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var WebAppStrategy = require('bluemix-appid').WebAppStrategy;
  ```
  {:pre}

Para obtener más información, consulte el <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">Repositorio GitHub de Node.js de {{site.data.keyword.appid_short_notm}}<img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
