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

*Última atualização: 06 de abril de 2016*

Use o
{{site.data.keyword.weatherfull}}
para incorporar dados de clima da The Weather Company (TWC) para seus
aplicativos do
{{site.data.keyword.Bluemix}}.
{:shortdesc}

As instruções a seguir fornecem orientação durante o processo de criação de um aplicativo,
ligando o aplicativo ao serviço Insights for Weather e recuperando as
credenciais de serviço para interagir com as [APIs REST](https://twcservice.{APPDomain}/rest-api/).

### Criar um aplicativo
{: #create_an_app}

Para propósitos de demonstração, você criará um aplicativo usando o tempo de execução do
Liberty for Java, mas o processo geral a seguir poderá ser aplicado a outros tempos de execução.

1. Se você não tiver um aplicativo existente, no painel, clique em **CREATE
APP**.
2. Ao ser solicitado a escolher seu modelo de aplicativo, clique
em **WEB**.
3. Ao ser solicitado a escolher um iniciador, clique em **Liberty for Java**.
4. Clique em **Continue**.
5. No campo **Nome do aplicativo**,
insira o nome de seu
aplicativo.
6. Clique em **Concluir (Finish)**. Aguarde seu aplicativo para provisão.

### Incluir o serviço Insights for Weather
{: #add_insights_for_weather_service}

Siga estas etapas para incluir o serviço Insights for Weather em seu app.
1. Abra o menu **Catálogo**.
2. Na seção **Dados e Analítica**, clique no quadro **Insights for Weather**.
3. Na lista suspensa **Aplicativo**, selecione seu
aplicativo.
4. Clique em **USE**.
5. Quando solicitado, clique em **Preparar novamente**
para reiniciar seu aplicativo.

### Recuperar credenciais do Insights for Weather
{: #retrieve_weather_credentials}

Ao ligar seu aplicativo ao Insights for Weather, você está fornecendo uma
instância de serviço com credenciais exclusivas. Essas credenciais são armazenadas no
`VCAP_SERVICES` do aplicativo e são essenciais para suportar a interação entre os serviços.

1. Navegue para a página de visão geral do seu aplicativo.
2. Acesse a seção **Variáveis de Ambiente**. As informações de `VCAP_SERVICES` para cada um de seus serviços são exibidas.
3. Anote os valores username e password do serviço Insights for Weather.
Para experimentar as [APIs REST](https://twcservice.{APPDomain}/rest-api/){:new_window},
deve-se inserir essas credenciais quando for solicitado para fazer login.
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

# rellinks
## amostras
* [Demo do Insights for Weather](http://insights-for-weather-demo.mybluemix.net/){: new_window}
* [Aulas práticas em laboratório do Places Insights](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [Como está o clima no Bluemix?](https://developer.ibm.com/bluemix/2015/12/08/insights-weather-sample-overview){: new_window}

## API
* [API REST](https://twcservice.{APPDomain}/rest-api/){: new_window}

## tempos de execução compatíveis {:id="buildpacks"}
* [Liberty for Java](https://console.{DomainName}/docs/starters/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## gerais
* [Sobre o Insights for Weather](https://console.{DomainName}/docs/services/Weather/weather_overview.html){: new_window}
* [Incluindo um serviço em seu aplicativo](https://console.{DomainName}/docs/services/reqnsi.html#add_service){: new_window}
* [Desenvolvimento de ponta a ponta](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [Folha de precificação do {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/pricing/){: new_window}
* [Pré-requisitos do {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
