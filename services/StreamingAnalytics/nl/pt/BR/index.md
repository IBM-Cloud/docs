---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Introdução ao {{site.data.keyword.streaminganalyticsshort}}
{: #gettingstarted}

O {{site.data.keyword.streaminganalyticsshort}} foi desenvolvido com o {{site.data.keyword.streamsshort}}, uma plataforma analítica avançada que pode ser usada para alimentar, analisar e correlacionar informações assim que chegam de diferentes tipos de origens de dados em tempo real. Ao criar uma instância do serviço {{site.data.keyword.streaminganalyticsshort}}, você obtém sua própria instância do {{site.data.keyword.streamsshort}} em execução na nuvem do {{site.data.keyword.Bluemix_short}}, pronta para executar seus aplicativos {{site.data.keyword.streamsshort}}.
{:shortdesc}

Inicie o {{site.data.keyword.streaminganalyticsshort}} imediatamente executando os [aplicativos iniciadores](/docs/services/StreamingAnalytics/c_starterapps.html){:new_window}.

Para iniciar o {{site.data.keyword.streaminganalyticsshort}}, use um dos métodos a seguir para enviar o pacote configurável do aplicativo (arquivo .sab) que está associado ao seu aplicativo SPL, Java™, Python ou Scala Streams:
* Use o botão **Enviar tarefa** no console do {{site.data.keyword.streaminganalyticsshort}}.
* Desenvolva um aplicativo {{site.data.keyword.Bluemix_short}} e inclua o aplicativo {{site.data.keyword.streamsshort}} nele. Controle-o usando
a API de REST do [{{site.data.keyword.streaminganalyticsshort}}](https://console.ng.bluemix.net/apidocs/220).


Use o {{site.data.keyword.streaminganalyticsshort}} com outros serviços do {{site.data.keyword.Bluemix_short}}, incluindo o {{site.data.keyword.cloudant}} e o {{site.data.keyword.messagehub}}. Veja os [Tutoriais para se integrar com outros serviços do {{site.data.keyword.Bluemix_short}}](/docs/services/StreamingAnalytics/r_integrating_cloudant_rest.html){:new_window} para obter exemplos de funcionamento.

Se você deseja ir além com seus próprios aplicativos, é possível obter um ambiente de desenvolvimento do {{site.data.keyword.streamsshort}} e deve-se deixar seu aplicativo pronto para a nuvem. Caso você não tenha um ambiente do {{site.data.keyword.streamsshort}}, é possível fazer download do {{site.data.keyword.streamsshort}} Quick Start Edition, gratuitamente, na página de produto do [{{site.data.keyword.streamsshort}}.](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)

Se você não estiver familiarizado com o desenvolvimento de aplicativo do {{site.data.keyword.streamsshort}}, haverá recursos para ajudá-lo a aprender. Para obter mais informações, veja o [{{site.data.keyword.streamsshort}} Knowledge Center.](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}

Se você já tiver um aplicativo SPL que será executado no local, deverá [deixar o seu aplicativo pronto para a nuvem.](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud/){:new_window}

**Observação:** deve-se compilar seus aplicativos no Red Hat Enterprise Linux (RHEL) 6.5 ou em uma versão equivalente do CentOS usando processadores Intel.

## Apps {{site.data.keyword.streamsshort}} Python para o {{site.data.keyword.streaminganalyticsshort}}
{: #gettingstarted_py notoc}

Agora é possível criar apps Streams em um ambiente Python, como o IBM Data Science Experience (DSX), e enviar esses aplicativos para a instância do {{site.data.keyword.streaminganalyticsshort}} para serem implementados na nuvem do Bluemix. Não é mais necessário instalar o {{site.data.keyword.streamsshort}} localmente para compilar e implementar um app Streams Python.

Inicie a criação de apps Streams Python de amostra usando blocos de notas do Jupyter em DSX e envie esses apps para a instância de serviço diretamente do DSX. Para obter mais informações, consulte [Desenvolvendo apps Streams Python no DSX](/docs/services/StreamingAnalytics/t_develop_apps_python.html#t_develop_python_dsx).

O {{site.data.keyword.streaminganalyticsshort}} também suporta a implementação de apps Streams de seu ambiente Python local. Deve-se usar a [API do aplicativo {{site.data.keyword.streamsshort}} Python](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features), que está incluída no pacote streamsx, para desenvolver seus apps Streams Python localmente e enviá-los à instância de serviço. Para iniciar, siga as etapas no tutorial [Desenvolvendo para o serviço {{site.data.keyword.streaminganalyticsshort}} ](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html).
