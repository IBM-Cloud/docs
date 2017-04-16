---

copyright:
  years: 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introdução ao Insights for Twitter {: #insights_twitter_overview}

Use {{site.data.keyword.twitterfull}} para incorporar o conteúdo do Twitter
a partir dos fluxos do Twitter [Decahose](http://support.gnip.com/gnip2.0/){: new_window} ou [PowerTrack](http://support.gnip.com/apis/powertrack2.0/){: new_window} aos aplicativos {{site.data.keyword.Bluemix}}.
{:shortdesc}

Para começar a usar o {{site.data.keyword.twittershort}}, primeiro crie seu aplicativo da Web do Bluemix com um tempo de execução como o Liberty for Java, em seguida, inclua o serviço {{site.data.keyword.twittershort}} em seu app. Quando o serviço {{site.data.keyword.twittershort}} estiver ligado ao seu app, a instância de serviço será provisionada com credenciais exclusivas. Seu app usa essas credenciais com APIs REST para procurar e consumir conteúdo do Twitter.  Siga estas etapas para recuperar as credenciais de VCAP_SERVICES e integrar a instância de serviço ao app.

1. Navegue para a página de visão geral do seu aplicativo.
2. Acesse a seção **Variáveis de Ambiente**. As informações de `VCAP_SERVICES` para cada um de seus serviços são exibidas.
3. Observe os valores username e password do serviço {{site.data.keyword.twittershort}}. Para testar operações na documentação de referência da API REST, será necessário inserir essas credenciais. Por exemplo, seus `VCAP_SERVICES` serão semelhantes ao fragmento a seguir:

```
{  
   "twitterinsights": [    
     {      
      "name": "IBM Insights for Twitter-x3",
      "label": "twitterinsights",
      "plan": "Free",
      "credentials": {
         "port": "443",
         "username": "fa7fed4b86baa0ec3e48e96b29cd2a03",
         "host": "cdeservice.mybluemix.net",
         "password": "7cunxw29",
         "url": "https://fa7fed4b86baa0ec3e48e96b29cd2a03:7cunxw29@cdeservice.mybluemix.net"
      }
     }  
   ]
}
```

# rellinks
{: #rellinks}
## SAMPLEs
{: #samples}
* [Demo de procura do decahose interativo](https://cdetestapp.mybluemix.net/){: new_window}
* [developerWorks: tutorial e código-fonte do demo de procura do decahose](http://www.ibm.com/developerworks/cloud/library/cl-twitter-search-insights-bluemix-trs/index.html){: new_window}
* [Analisando os dados de bilheteria de "Sniper americano" (YouTube)](https://www.youtube.com/watch?v=Gfk5quglXvI){: new_window}
* [Aulas práticas em laboratório do Places Insights](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}

## api
{: #api}
* [API REST
](https://cdeservice.{APPDomain}/rest-api/){: new_window}

## tempos de execução compatíveis
{: #buildpacks}
* [Ir](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Swift
](https://console.{DomainName}/docs/runtimes/swift/index.html){: new_window}
* [Tomcat ](https://console.{DomainName}/docs/runtimes/tomcat/index.html){: new_window}

## gerais
{: #general}
* [O que há de novo nos serviços do {{site.data.keyword.Bluemix_notm}}](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){: new_window}
* [Incluindo um serviço em seu aplicativo](../reqnsi.html){: new_window}
* [Desenvolvimento de ponta a ponta](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [Folha de precificação do {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/pricing/){: new_window}
* [Pré-requisitos do {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}

