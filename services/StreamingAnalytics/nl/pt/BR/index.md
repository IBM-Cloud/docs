---

copyright:
  years: 2015, 2017 lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Introdução ao {{site.data.keyword.streaminganalyticsshort}}
{: #gettingstarted}

O {{site.data.keyword.streaminganalyticsshort}} foi desenvolvido com o {{site.data.keyword.streamsshort}}, uma plataforma analítica avançada que
pode ser usada para alimentar, analisar e correlacionar informações assim que chegam de diferentes tipos de origens de dados em tempo real. Ao criar uma instância do
serviço {{site.data.keyword.streaminganalyticsshort}}, você obtém sua própria instância do {{site.data.keyword.streamsshort}} em execução na nuvem do
{{site.data.keyword.Bluemix_short}}, pronta para executar seus aplicativos {{site.data.keyword.streamsshort}}.{:shortdesc}

É possível implementar seus aplicativos em uma instância do {{site.data.keyword.streaminganalyticsshort}} que está em execução na nuvem do
{{site.data.keyword.Bluemix_short}}.

É possível iniciar o {{site.data.keyword.streaminganalyticsshort}} imediatamente executando os
[aplicativos iniciadores](/docs/services/StreamingAnalytics/c_starterapps.html){:new_window}. Se você desejar ir além com os seus próprios aplicativos, precisará de um ambiente de desenvolvimento do {{site.data.keyword.streamsshort}} e deverá deixar o seu SPL pronto para a nuvem.

Para a introdução ao {{site.data.keyword.streaminganalyticsshort}}, use um dos métodos a seguir para enviar o pacote configurável do aplicativo
(arquivo .sab) que está associado ao seu aplicativo SPL ou Java™:
* Use o console do {{site.data.keyword.streaminganalyticsshort}}.
* Desenvolva um aplicativo {{site.data.keyword.Bluemix_short}} e inclua o aplicativo {{site.data.keyword.streamsshort}} nele. Controle-o usando
a API de REST do [{{site.data.keyword.streaminganalyticsshort}}](https://console.ng.bluemix.net/apidocs/220). Verifique se o seu aplicativo
SPL ou Java é executado adequadamente em seu ambiente de desenvolvimento.

Agora é possível usar o {{site.data.keyword.streaminganalyticsshort}} com outros serviços do {{site.data.keyword.Bluemix_short}},
incluindo o {{site.data.keyword.cloudant}} e o {{site.data.keyword.messagehub}}. Veja os [Tutoriais para se integrar com outros serviços do {{site.data.keyword.Bluemix_short}}](/docs/services/StreamingAnalytics/r_integrating_cloudant_rest.html){:new_window} para obter exemplos de funcionamento.

Para desenvolver um aplicativo {{site.data.keyword.streamsshort}}, deve-se ter um ambiente de desenvolvimento do {{site.data.keyword.streamsshort}}. Caso
você não tenha um ambiente do {{site.data.keyword.streamsshort}}, é possível fazer download do {{site.data.keyword.streamsshort}} Quick Start Edition, gratuitamente, na página de produto do [{{site.data.keyword.streamsshort}}.](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)

Se você não estiver familiarizado com o desenvolvimento de
aplicativo do
{{site.data.keyword.streamsshort}},
haverá recursos para ajudá-lo a aprender. Para obter mais informações, veja o
[{{site.data.keyword.streamsshort}} Knowledge Center.](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}

Se você já tiver um aplicativo SPL que será executado no local, deverá
[deixar
o seu aplicativo pronto para a nuvem.](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud/){:new_window}

# Links Relacionados
{: #rellinks}

## Tutoriais e amostras
{: #samples}
* [Introdução ao {{site.data.keyword.streaminganalyticsshort}}](https://developer.ibm.com/streamsdev/docs/streaming-analytics-now-available-bluemix){:new_window}
* [{{site.data.keyword.streaminganalyticsshort}}Aplicativo iniciador SDK for Node.js™](http://bit.ly/1iR1bzu){:new_window}
* [{{site.data.keyword.streaminganalyticsshort}}Aplicativo iniciador Liberty for Java™](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-starter-application/){:new_window}
* [Aprontando seu aplicativo SPL para a nuvem](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud){:new_window}
* [Bluemix {{site.data.keyword.streaminganalyticsshort}}: Guia de Desenvolvimento](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-development-guide/){:new_window}
* [Mais tutoriais](StreamingAnalytics.html#r_integrating_cloudant_rest){:new_window}


## Referência de API
{: #api}
* [{{site.data.keyword.streaminganalyticsshort}} API REST](https://console.ng.bluemix.net/apidocs/220){:new_window}
* Métricas do [{{site.data.keyword.streaminganalyticsshort}} usando a API de REST do {{site.data.keyword.streamsshort}}](https://developer.ibm.com/bluemix/2016/07/25/streaming-analytics-metrics-using-rest-api/){:new_window}

## Tempos de Execução Compatíveis
{: #buildpacks}
* [Liberty para Java](/docs/runtimes/liberty/index.html#liberty)
* [Node.js](/docs/runtimes/nodejs/index.html#nodejs)

## Links Relacionados
{: #general}
* Documentação do
[{{site.data.keyword.streamsshort}}](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}
* [{{site.data.keyword.streamsshort}} Quick Start Edition](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window}
