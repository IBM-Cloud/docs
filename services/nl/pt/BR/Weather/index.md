---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introdução ao Insights for Weather
{: #insights_weather_overview}

*Última atualização: 19 maio de 2016*

Use o
{{site.data.keyword.weatherfull}}
para incorporar dados de clima da The Weather Company (TWC) para seus
aplicativos do
{{site.data.keyword.Bluemix}}.
{:shortdesc}

**Nota:** o serviço Insights for Weather não está disponível atualmente no Japão.

Antes de começar, crie um aplicativo da web do {{site.data.keyword.Bluemix_notm}} no painel com um tempo de execução como Liberty for Java. Espere
o seu aplicativo ser provisionado e inclua o serviço Insights for Weather ao seu aplicativo.

Ao ligar seu aplicativo ao Insights for
Weather, você está provisionando uma instância de serviço com
credenciais exclusivas. Seu aplicativo usa essas credenciais com
o [REST
APIs](https://twcservice.{APPDomain}/rest-api/){:new_window} para recuperar dados de clima.

Siga essas etapas para recuperar as credenciais do
`VCAP_SERVICES` e integre a instância de serviço
com seu aplicativo.

1. Navegue para a página de visão geral do seu aplicativo.
2. Acesse a seção **Variáveis de Ambiente**. As informações de `VCAP_SERVICES` para cada um de seus serviços são exibidas.
3. Anote os valores de nome do usuário e senha do serviço Insights for Weather.
Para tentar as [APIs REST](https://twcservice.{APPDomain}/rest-api/){:new_window},
deve-se inserir essas credenciais quando for solicitado a efetuar login.
Seu `VCAP_SERVICES` é semelhante ao exemplo a seguir:

```
{
   "weatherinsights": [
     {
      "name": "Insights for Weather",
      "label": "weatherinsights",
      "plan": "Free",
      "credentials": {
         "port": "443",
         "username": "fa7fed4b86baa0ec3e48e96b29cd2a03",
         "host": "twcservice.mybluemix.net",
         "password": "7abcxw29",
         "url": "https://fa7fed4b86baa0ec3e48e96b29cd2a03:7cunxw29@cdeservice.mybluemix.net"
      }
     }
   ]
}
```

**Nota:** cada região é independente. Não é possível usar credenciais de serviço
fornecidas a você em uma região para se autenticar em um serviço em outra região.
A falha ao inserir credenciais adequadas resultará em uma mensagem "Desautorizado" no corpo da resposta. 

# rellinks
{: #rellinks}
## amostras
{: #samples}
* [Demo do Insights for Weather](http://insights-for-weather-demo.mybluemix.net/){: new_window}
* [Aulas práticas em laboratório do Places Insights](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [Como está o clima no Bluemix?](https://developer.ibm.com/bluemix/2015/12/08/insights-weather-sample-overview){: new_window}

## API
{: #api}
* [API REST](https://twcservice.{APPDomain}/rest-api/){: new_window}

## tempos de execução compatíveis
{: #buildpacks}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## gerais
{: #general}
* [Incluindo um serviço em seu aplicativo](../reqnsi.html){: new_window}
* [Desenvolvimento de ponta a ponta](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [Folha de precificação do {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/pricing/){: new_window}
* [Pré-requisitos do {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
