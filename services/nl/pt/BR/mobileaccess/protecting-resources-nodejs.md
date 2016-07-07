---

copyright:
  years: 2015, 2016

---

# Protegendo recursos Node.js com o {{site.data.keyword.amashort}}
{: #protecting-resources-nodejs}

*Última atualização: 15 de abril de 2016*
{: .last-updated}

É possível usar o {{site.data.keyword.amashort}} server SDK para proteger recursos em seu app Node.js.

### Antes de iniciar
{: #before-you-begin}

* Deve-se estar familiarizado com o desenvolvimento de aplicativos Node.js no {{site.data.keyword.Bluemix_notm}}. Para obter mais informações, consulte [Criando apps com o SDK for Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html#nodejs_runtime)
* O {{site.data.keyword.amashort}} server SDK requer que seu servidor Node.js seja implementado com a estrutura `Express`. Observe que há várias outras estruturas que usam estruturas `Express`, como LoopBack. É possível usar o {{site.data.keyword.amashort}} server SDK com qualquer uma dessas estruturas. Para obter mais informações sobre a estrutura do Express, consulte [Expressjs.com](http://expressjs.com/).

### Sobre o {{site.data.keyword.amashort}} server SDK
{: #about}

O {{site.data.keyword.amashort}} server SDK fornece uma estratégia de passaporte `MCABackendStrategy` para ser usada em aplicativos backend implementados no IBM {{site.data.keyword.Bluemix_notm}}. Para proteger seu app contra acesso não autorizado e obter informações de monitoramento, deve-se instrumentar seu servidor Node.js com o `MCABackendStrategy`. O módulo npm `bms-mca-token-validation-strategy` fornece a estratégia de passaporte `MCABackendStrategy` e o método de verificação para validar o token de acesso e o token de ID emitidos pelo {{site.data.keyword.amashort}}. Esse módulo também fornece automaticamente informações de monitoramento sobre eventos de segurança.

O {{site.data.keyword.amashort}} server SDK usa a estrutura `Passport` para impor a autorização.  Para obter mais informações, consulte [Passportjs.org](http://passportjs.org/).

### Instalando o {{site.data.keyword.amashort}} server SDK
{: #protecting-resources-serversdk}

Abra o diretório com seu aplicativo Node.js em uma linha de comandos e execute os comandos a seguir:

```
npm install -save express
npm install -save passport
npm install -save bms-mca-token-validation-strategy
```

### Protegendo recursos no Node.js
{: #protecting-resources-nodesdk}

O fragmento a seguir demonstra como usar `MCABackendStrategy` em um aplicativo Express simples para proteger os métodos GET do terminal `/protected`.

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
