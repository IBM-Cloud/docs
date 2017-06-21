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

# Implementando aplicativos {{site.data.keyword.streamsshort}} na nuvem
{: #t_deploytocloud}

É possível implementar os seus aplicativos {{site.data.keyword.streamsshort}} em uma instância do {{site.data.keyword.streaminganalyticsshort}} que estiver em execução na nuvem do {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

Os aplicativos {{site.data.keyword.streamsshort}} são gravados em {{site.data.keyword.streamsshort}} Processing Language (SPL), SPL, Java, Scala ou Python em um ambiente {{site.data.keyword.streamsshort}}. Agora é possível desenvolver aplicativos Streams Python sem um ambiente {{site.data.keyword.streamsshort}}. Consulte [Implementando aplicativos {{site.data.keyword.streamsshort}} Python para a nuvem](docs/services/StreamingAnalytics/t_deploytocloud.html#t_deploypython)


O {{site.data.keyword.streaminganalyticsshort}} não inclui um ambiente de desenvolvimento do {{site.data.keyword.streamsshort}} na nuvem, mas é possível implementar localmente na nuvem os aplicativos que você desenvolve.

Antes de iniciar, desative o bloqueador de pop-up de seu navegador para exibir o console do {{site.data.keyword.streaminganalyticsshort}}.

Para implementar os seus aplicativos {{site.data.keyword.streamsshort}} na nuvem:

1. Configure seu ambiente de desenvolvimento para desenvolver e testar seu aplicativo.

	Se você deseja usar um ambiente {{site.data.keyword.streamsshort}}, é possível fazer download gratuitamente do {{site.data.keyword.streamsshort}} Quick Start Edition. Acesse a [página de produto IBM Streams](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window}
e clique em **Download da instalação de software nativo**.

2. Desenvolva seu aplicativo de fluxo em seu ambiente de desenvolvimento. No ambiente de desenvolvimento do {{site.data.keyword.streamsshort}}, é possível usar o Streams Studio ou as ferramentas de linha de comandos para desenvolver seu aplicativo.

3. Verifique se o seu aplicativo de fluxo está sendo executado adequadamente em seu ambiente de desenvolvimento.
**Observação:** deve-se compilar seu aplicativo em um sistema operacional Red Hat Enterprise Linux (RHEL) 6.5 ou em uma versão equivalente do CentOS usando processadores Intel.

4. Envie o pacote configurável do aplicativo (arquivo .sab) que está associado ao seu aplicativo SPL, Java, Scala ou Python para sua instância de serviço na nuvem usando um destes métodos:
	* Use o console do {{site.data.keyword.streaminganalyticsshort}} para enviar o pacote configurável do aplicativo.
  * Crie um aplicativo {{site.data.keyword.Bluemix_short}} e inclua o aplicativo {{site.data.keyword.streamsshort}} nele. Controle-o usando a API REST do {{site.data.keyword.streaminganalyticsshort}}.

Agora seu aplicativo está implementado na nuvem. É possível monitorar seu aplicativo usando o serviço {{site.data.keyword.streaminganalyticsshort}}. Também é possível enviar mais de um aplicativo (arquivos .sab) para sua instância de serviço. Quantas você quiser.

O {{site.data.keyword.streamsshort}} também suporta vários Java™ Development Kits que podem ser usados para desenvolver os seus aplicativos. Para obter mais informações sobre o suporte a Java no {{site.data.keyword.streamsshort}}, veja [Java Development Kits suportados para desenvolvimento de aplicativos](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-prerequisites-java-supported-sdks.html){:new_window}.

## Implementando aplicativos {{site.data.keyword.streamsshort}} Python para a nuvem
{: #t_deploypython}

Implemente seus aplicativos {{site.data.keyword.streamsshort}} Python para um serviço {{site.data.keyword.streaminganalyticsshort}} que esteja em execução na nuvem do {{site.data.keyword.Bluemix_short}}. Não é necessário ter uma instalação do {{site.data.keyword.streamsshort}}.
{:shortdesc}

A [API do aplicativo {{site.data.keyword.streamsshort}} Python](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features), que está incluída no pacote streamsx, permite implementar aplicativos Python para o serviço {{site.data.keyword.streaminganalyticsshort}}. Confira o tutorial [Desenvolvendo para o serviço {{site.data.keyword.streaminganalyticsshort}}](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html) para obter um exemplo de como criar e implementar um aplicativo Python simples para o serviço {{site.data.keyword.streaminganalyticsshort}}.

O IBM Data Science Experience (DSX) também suporta o envio de aplicativos Python nos blocos de notas interativos do Jupyter. Para obter mais informações, consulte [Desenvolvendo aplicativos Python para o {{site.data.keyword.streaminganalyticsshort}}](/docs/services/StreamingAnalytics/t_develop_apps_python.html).
