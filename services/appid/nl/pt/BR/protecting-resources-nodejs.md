---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Protegendo recursos de Node.js
{: #protecting-resources-nodejs}

É possível usar o {{site.data.keyword.appid_short}} server SDK para proteger recursos em seu app Node.js.
{:shortdesc}

## Antes de Começar
{: #before-you-begin}

* Familiarize-se com o desenvolvimento de aplicativos Node.js no {{site.data.keyword.Bluemix_notm}}.
* O SDK do servidor {{site.data.keyword.appid_short_notm}} requer que o seu servidor Node.js seja implementado com a
<a href="http://expressjs.com/" target="_blank">estrutura Express <img src="../../icons/launch-glyph.svg" alt="ícone de Link externo"></a>.

**Nota**: há outras estruturas que usam estruturas `Express`, como LoopBack. É possível usar o SDK do servidor
{{site.data.keyword.appid_short_notm}} com qualquer uma dessas estruturas.

## Sobre o SDK do servidor
{: #about}

O SDK do servidor {{site.data.keyword.appid_short_notm}} fornece uma estratégia de passaporte ApiStrategy que é usada em aplicativos backend que são
implementados no {{site.data.keyword.Bluemix_notm}}. Para proteger o seu app contra acesso não autorizado, deve-se instrumentar o seu servidor Node.js com a
ApiStrategy. O `appid-serversdk-nodejs npm module` fornece a estratégia de passaporte ApiStrategy e o método de verificação para validar o token de
acesso e o token de ID emitidos pelo {{site.data.keyword.appid_short_notm}}.

O SDK do servidor {{site.data.keyword.appid_short_notm}} usa a estrutura do Passport para reforçar a autorização. Veja
<a href="http://passportjs.org/" target="_blank">Estrutura do Passport <img src="../../icons/launch-glyph.svg" alt="ícone do Link externo"></a>.


## Instalando o SDK do servidor
{: #protecting-resources-serversdk}

1. Usando a linha de comandos, abra o diretório como seu app Node.js.
2. Execute os seguintes comandos:

  ```
  npm install -save express
  npm install -save passport
  npm install -save bluemix-appid
  ```
  {:pre}

## Protegendo recursos no Node.js
{: #protecting-resources-nodesdk}

O fragmento a seguir demonstra como usar `APIStrategy` em um aplicativo Express simples para proteger os métodos GET do terminal `/protected`.

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

É possível usar a `WebAppStrategy` para proteger recursos de aplicativo da web:

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var WebAppStrategy = require('bluemix-appid').WebAppStrategy;
  ```
  {:pre}

Para obter mais informações, consulte o <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}} repositório do GitHub Node.js <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
