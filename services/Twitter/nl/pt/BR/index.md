{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introdução ao Insights for Twitter {: #insights_twitter_overview}

*Última atualização: 13 de maio de 2016*
{: .last-updated}

Use {{site.data.keyword.twitterfull}} para incorporar o conteúdo do Twitter
a partir dos fluxos do Twitter [Decahose](http://support.gnip.com/apis/firehose/overview.html){: new_window} ou [PowerTrack](http://support.gnip.com/apis/powertrack/overview.html){: new_window} aos aplicativos {{site.data.keyword.Bluemix}}.
{:shortdesc}

Para iniciar a utilização do {{site.data.keyword.twittershort}}, crie primeiramente seu aplicativo da web do Bluemix com um tempo de execução do tipo Liberty for Java e, em seguida, inclua o serviço {{site.data.keyword.twittershort}} no app. Quando o serviço {{site.data.keyword.twittershort}} estiver ligado ao app, a instância de serviço será provisionada com credenciais exclusivas. Seu app usa essas credenciais com APIs REST para procurar e consumir conteúdo do Twitter. Siga estas etapas para recuperar as credenciais de VCAP_SERVICES e integrar a instância de serviço ao app.

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

<!--
## Adding Insights for Twitter to your application {: #adding_twitter}

The following instructions guide you through the process of creating an application, binding the application to the {{site.data.keyword.twittershort}} service, and retrieving the service credentials to interact with REST API operations in the provided API reference documentation.

### Create an application
For demonstration purposes, you'll create an application using the Liberty for Java&trade;  runtime, but the general process described below can be applied to other runtimes. If you don't have an existing application, click **CREATE AN APP** in the dashboard. When asked to confirm the type of app, click **WEB**.

1. Open the **Catalog** menu.
2. From the **Runtimes** section, click **Liberty for Java**.
3. Click **Create**.
4. In the **App Name** field, specify the name of your app.
5. Click **Finish**. Wait for your application to provision.

### Add the Insights for Twitter service
Follow these steps to add the {{site.data.keyword.twittershort}} service to your app.

1. Open the **Catalog** menu.
2. From the **Data & Analytics** section, click the {{site.data.keyword.twittershort}} tile.
3. In the **App** field, select the name of your app.
4. Click **Create**.
5. When prompted, click **Restage** to restart your application.
-->

# rellinks
## SAMPLEs
* [Demo de procura do decahose interativo](https://cdetestapp.mybluemix.net/){: new_window}
* [developerWorks: tutorial e código-fonte do demo de procura do decahose](http://www.ibm.com/developerworks/cloud/library/cl-twitter-search-insights-bluemix-trs/index.html){: new_window}
* [Analisando os dados de bilheteria de "Sniper americano" (YouTube)](https://www.youtube.com/watch?v=Gfk5quglXvI){: new_window}
* [Aulas práticas em laboratório do Places Insights](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}

## api
* [API REST
](https://cdeservice.{APPDomain}/rest-api/){: new_window}

## tempos de execução compatíveis {:id="buildpacks"}
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
* [O que há de novo nos serviços do {{site.data.keyword.Bluemix_notm}}](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){: new_window}
* [Incluindo um serviço em seu aplicativo](../reqnsi.html){: new_window}
* [Desenvolvimento de ponta a ponta](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [Folha de precificação do {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/pricing/){: new_window}
* [Pré-requisitos do {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}

