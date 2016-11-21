---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introdução ao {{site.data.keyword.weather_short}}
{: #insights_weather_overview}

Use o
{{site.data.keyword.weatherfull}}
para incorporar dados de clima da The Weather Company (TWC) para seus
aplicativos do
{{site.data.keyword.Bluemix}}.
{:shortdesc}

**Atenção:** atualmente, o serviço {{site.data.keyword.weather_short}} **não pode** ser comprado
ou usado nos países ou nas regiões a seguir: Afeganistão, Armênia, Azerbaijão,
Bahrein, Bangladesh, Butão, Brunei, Camboja, China, Chipre, Geórgia,
Indonésia, Irã, Iraque, Japão, Jordânia, Cazaquistão, Kuwait, Quirguistão, Laos,
Líbano, Malásia, Maldivas, Mongólia, Myanmar, Nepal, Omã, Paquistão, Filipinas,
Catar, Rússia, Arábia Saudita, Singapura, Coreia do Sul, Sri Lanka, Síria,
Tajiquistão, Timor-Leste, Turquia, Turquemenistão, Emirados Árabes Unidos,
Uzbequistão, Vietnã, Iêmen. Essa lista é atualizada quando informações adicionais estão disponíveis.

Se você tiver um aplicativo existente que usa o
[serviço Insights for Weather](https://console.{DomainName}/docs/services/InsightsWeather/index.html){: new_window},
o seu aplicativo continuará a funcionar sem nenhuma modificação por 90 dias após a introdução do
{{site.data.keyword.weather_short}}. Para aproveitar as APIs recém-incluídas
e o modelo de precificação melhorado, é possível migrar o aplicativo para o novo serviço.

Antes de começar, crie um aplicativo da web do {{site.data.keyword.Bluemix_notm}} no painel com um tempo de execução como Liberty for Java. Espere
o seu aplicativo ser provisionado e, em seguida, inclua o serviço
{{site.data.keyword.weather_short}} em seu aplicativo.

Ao ligar o seu aplicativo ao {{site.data.keyword.weather_short}}, você está fornecendo uma
instância de serviço com credenciais exclusivas. Seu aplicativo usa essas credenciais com
as [APIs REST](https://twcservice.{APPDomain}/rest-api/){:new_window} para recuperar dados de clima.

Siga essas etapas para recuperar as credenciais de serviço a partir de `VCAP_SERVICES`
e integre a instância de serviço com o seu aplicativo.

1. Navegue para a página de visão geral do seu aplicativo.
2. Acesse a seção **Variáveis de Ambiente**. As informações de `VCAP_SERVICES` para cada um de seus serviços são exibidas.
3. Anote os valores de nome do usuário e senha a partir do serviço {{site.data.keyword.weather_short}}.
Para tentar as [APIs REST](https://twcservice.{APPDomain}/rest-api/){:new_window},
deve-se inserir essas credenciais quando for solicitado a efetuar login.
Seu `VCAP_SERVICES` é semelhante ao exemplo a seguir:

```
{
{
   "weatherinsights": [
      {
         "name": "Weather Company Data for IBM Bluemix",
         "label": "weatherinsights",
         "plan": "Free",
         "credentials": {
            "username": "d40845df-8125-441f-8e7c-e650726ce721",
            "password": "tDV0HGZz3O",
            "host": "twcservice.mybluemix.net",
            "port": 443,
            "url": "https://d40845df-8125-441f-8e7c-e650726ce721:tDV0HGZz3O@twcservice.mybluemix.net"
         }
      }
   ]
}
```

**Nota:** cada região é independente. Não é possível usar credenciais de serviço
fornecidas a você em uma região para se autenticar em um serviço em outra região.
A falha ao inserir credenciais adequadas resulta em uma mensagem *Não autorizado* no corpo da resposta.

# rellinks
{: #rellinks}
## amostras
{: #samples}
* [Aplicativo de demo de {{site.data.keyword.weather_short}}](http://weather-company-data-demo.{APPDomain}){: new_window}
* [Vídeo de Detalhamento de {{site.data.keyword.weather_short}}](https://youtu.be/pZHXIibziUo){: new_window}
* [Aulas práticas em laboratório do Places Insights](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [{{site.data.keyword.Bluemix_notm}} + aplicativo de amostra de Clima](https://github.com/IBM-Bluemix/insights-weather){: new_window}
* [IBM Cloud - Bare Metal, NYC Taxi Data e Insights for Weather (tutorial do YouTube)](https://www.youtube.com/watch?v=Uwmzpx9DZ5c){: new_window}

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
* [Incluindo um serviço em seu aplicativo](/docs/services/reqnsi.html){: new_window}
* [Desenvolvimento de ponta a ponta](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [Folha de precificação do {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/pricing/){: new_window}
* [Pré-requisitos do {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
