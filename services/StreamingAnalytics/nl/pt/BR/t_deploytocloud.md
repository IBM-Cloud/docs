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

#Implementando aplicativos {{site.data.keyword.streamsshort}} na nuvem
{: #t_deploytocloud}

É possível implementar os seus aplicativos {{site.data.keyword.streamsshort}} em uma instância do {{site.data.keyword.streaminganalyticsshort}}
que estiver em execução na nuvem do {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

Os aplicativos {{site.data.keyword.streamsshort}} são escritos em {{site.data.keyword.streamsshort}} Processing Language (SPL) em um
ambiente do {{site.data.keyword.streamsshort}}. O {{site.data.keyword.streamsshort}} também suporta vários Java™ Development Kits que podem ser usados
para desenvolver os seus aplicativos. Para obter mais informações sobre o suporte a Java no {{site.data.keyword.streamsshort}}, veja
[Java
Development Kits suportados para desenvolvimento de aplicativos](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-prerequisites-java-supported-sdks.html){:new_window}.
O {{site.data.keyword.streaminganalyticsshort}} não inclui um ambiente de desenvolvimento do {{site.data.keyword.streamsshort}} na nuvem, mas é
possível implementar localmente na nuvem os aplicativos que você desenvolve.

Antes de iniciar, desative o bloqueador de pop-up de seu navegador para exibir o console do Streaming Analytics.

Para implementar os seus aplicativos {{site.data.keyword.streamsshort}} na nuvem:

1. Configure um ambiente do {{site.data.keyword.streamsshort}} para desenvolver e testar o seu aplicativo. 

	Caso você não tenha um ambiente do {{site.data.keyword.streamsshort}}, é possível fazer download do {{site.data.keyword.streamsshort}} Quick
Start Edition, gratuitamente. Acesse a [página de produto IBM Streams](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window}
e clique em **Download da instalação de software nativo**.

2. Desenvolva o seu aplicativo SPL ou Java em seu ambiente do {{site.data.keyword.streamsshort}} usando o Streams Studio ou as ferramentas de linha
de comandos.
3. Verifique se o seu aplicativo SPL ou Java é executado adequadamente em seu ambiente de desenvolvimento.
4. Envie o pacote configurável do aplicativo (arquivo .sab) que está associado ao seu aplicativo SPL ou Java para a sua instância de serviço na nuvem usando um desses métodos:
	* Use o console do {{site.data.keyword.streaminganalyticsshort}} para enviar o pacote configurável do aplicativo.
    * Desenvolva um aplicativo {{site.data.keyword.Bluemix_short}} e inclua o aplicativo {{site.data.keyword.streamsshort}} nele. Controle-o usando a API REST do {{site.data.keyword.streaminganalyticsshort}}.

Agora seu aplicativo está implementado na nuvem. É possível monitorar seu aplicativo usando o serviço {{site.data.keyword.streaminganalyticsshort}}. Também é possível
enviar mais de um aplicativo SPL ou Java (arquivos .sab) para a sua instância de serviço. Quantas
você quiser.
