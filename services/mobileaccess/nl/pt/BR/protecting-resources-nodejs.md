---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---

{:shortdesc: .shortdesc}
{:codeblock:.codeblock}

**Importante: o serviço {{site.data.keyword.amafull}} foi substituído pelo serviço {{site.data.keyword.appid_full}}.**

# Protegendo recursos Node.js com o {{site.data.keyword.amashort}}
{: #protecting-resources-nodejs}


É possível usar o {{site.data.keyword.amashort}} server SDK para proteger recursos em seu app Node.js.

## Antes de iniciar
{: #before-you-begin}

* Deve-se estar familiarizado com o desenvolvimento de aplicativos Node.js no {{site.data.keyword.Bluemix_notm}}. Para obter
informações adicionais, consulte [Criando apps com SDK para
Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html#nodejs_runtime).
* O {{site.data.keyword.amashort}} server SDK requer que seu servidor Node.js seja implementado com a estrutura `Express`. Observe
que há outras estruturas que usam estruturas `Express`, como LoopBack. É possível usar o SDK do servidor
{{site.data.keyword.amashort}} com qualquer uma dessas estruturas. Para obter mais informações
sobre a estrutura Express, veja [Expressjs.com ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](http://expressjs.com/){: new_window}.

## Sobre o SDK do servidor
{: #about}

O SDK do servidor {{site.data.keyword.amashort}} fornece uma estratégia de passaporte `MCABackendStrategy`
para ser usada em aplicativos backend implementados no IBM {{site.data.keyword.Bluemix_notm}}. Para proteger seu app contra acesso não autorizado e obter informações de monitoramento, deve-se instrumentar seu servidor Node.js com o `MCABackendStrategy`. O módulo npm `bms-mca-token-validation-strategy` fornece a estratégia de passaporte `MCABackendStrategy` e o método de verificação para validar o token de acesso e o token de ID emitidos pelo {{site.data.keyword.amashort}}. Esse módulo também fornece automaticamente informações de monitoramento sobre eventos de segurança.

O {{site.data.keyword.amashort}} server SDK usa a estrutura `Passport` para impor a autorização.  Para obter mais informações, veja [Passportjs.org ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](http://passportjs.org/){: new_window}.

## Instalando o SDK do servidor
{: #protecting-resources-serversdk}

Abra o diretório com seu aplicativo Node.js em uma linha de comandos e execute os comandos a seguir:

```
npm install -save express
npm install -save passport
npm install -save bms-mca-token-validation-strategy
```
{: codeblock}

## Protegendo recursos no Node.js
{: #protecting-resources-nodesdk}

O fragmento a seguir demonstra como usar `MCABackendStrategy` em um aplicativo Express simples, para proteger os métodos GET do terminal `/protected`.

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
