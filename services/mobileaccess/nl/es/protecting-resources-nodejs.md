---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-10-27"

---

{:shortdesc: .shortdesc} 
{:codeblock:.codeblock}

# Protección de recursos Node.js con {{site.data.keyword.amashort}}
{: #protecting-resources-nodejs}


Puede utilizar el SDK del servidor de {{site.data.keyword.amashort}} para proteger recursos en la app Node.js.

## Antes de empezar
{: #before-you-begin}

* Debe estar familiarizado con el desarrollo de aplicaciones Node.js en {{site.data.keyword.Bluemix_notm}}. Para obtener más información, consulte [Creación de apps con SDK for Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html#nodejs_runtime).
* El SDK del servidor de {{site.data.keyword.amashort}} necesita que se implemente el servidor de Node.js con la infraestructura `Express`. Tenga en cuenta que hay otras infraestructuras que utilizan infraestructuras `Express`, como LoopBack. Puede utilizar el SDK del servidor de {{site.data.keyword.amashort}} con cualquiera de estas infraestructuras. Para obtener más información sobre la infraestructura de Express, consulte [Expressjs.com ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://expressjs.com/ "Icono de enlace externo"){: new_window}.

## Acerca del SDK del servidor
{: #about}

El SDK del servidor de {{site.data.keyword.amashort}} proporciona la estrategia de pasaporte `MCABackendStrategy` para su uso en las aplicaciones de fondo desplegadas en IBM {{site.data.keyword.Bluemix_notm}}. Para proteger la app de accesos no autorizados y obtener información de supervisión, debe instrumentar el servidor Node.js con `MCABackendStrategy`. El módulo npm `bms-mca-token-validation-strategy` proporciona la estrategia de pasaporte `MCABackendStrategy` y el método de verificación para validar la señal de acceso y la señal de ID que ha emitido {{site.data.keyword.amashort}}. Este módulo también suministra automáticamente información de supervisión sobre sucesos de seguridad.

El SDK del servidor de {{site.data.keyword.amashort}} utiliza la infraestructura `Passport` para imponer la autorización. Para obtener más información, consulte [Passportjs.org ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://passportjs.org/ "Icono de enlace externo"){: new_window}.

## Instalación del SDK del servidor
{: #protecting-resources-serversdk}

Abra el directorio con la aplicación Node.js en una línea de mandatos y ejecute los mandatos siguientes:

```
npm install -save express
npm install -save passport
npm install -save bms-mca-token-validation-strategy
```
{: codeblock}

## Protección de recursos en Node.js
{: #protecting-resources-nodesdk}

El siguiente fragmento de código muestra cómo utilizar `MCABackendStrategy` en una aplicación Express sencilla para proteger los métodos GET del punto final `/protected`.

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
