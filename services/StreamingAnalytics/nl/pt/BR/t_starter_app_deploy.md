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

# Implementando os aplicativos iniciadores no {{site.data.keyword.Bluemix_short}}
{: #starterapps_deploy}

É possível enviar por push e implementar um dos aplicativos iniciadores do {{site.data.keyword.streaminganalyticsshort}} na nuvem do
{{site.data.keyword.Bluemix_short}}.
{:shortdesc}

Antes de iniciar, apronte o {{site.data.keyword.Bluemix_short}} para implementar os aplicativos iniciadores do
{{site.data.keyword.streaminganalyticsshort}}:

* [Instale a ferramenta de linha de comandos cf](https://github.com/cloudfoundry/cli/releases).
* Crie um aplicativo no {{site.data.keyword.Bluemix_short}}, inclua o serviço {{site.data.keyword.streaminganalyticsshort}} em seu aplicativo e
remonte o aplicativo:
	* Para implementar o app iniciador Event Detection, crie um aplicativo com o tempo de execução do {{site.data.keyword.sdk4node}}.
	* Para implementar o app iniciador NYC Traffic, crie um aplicativo com o tempo de execução do Liberty for Java™.

Lembre-se do nome que você deu ao aplicativo; você precisará dele posteriormente.

O {{site.data.keyword.streaminganalyticsshort}} fornece dois aplicativos de amostra para você iniciar o serviço.

O aplicativo iniciador Event Detection
analisa dados relacionados ao clima em um fluxo em tempo real e exibe o status e os resultados da
análise. O aplicativo é gravado no {{site.data.keyword.sdk4node}}. Para obter mais detalhes sobre como usar o app iniciador Event Detection, veja [Detectar eventos complexos em um fluxo de dados em tempo real](https://www.ibm.com/developerworks/library/ba-bluemix-detect-complex-events-from-data-stream-trs/index.html).

O aplicativo iniciador NYC Traffic lê e analisa dados de tráfego de um website público. O aplicativo é gravado no Liberty for Java™. Para obter mais detalhes sobre como usar o app iniciador NYC Traffic, veja [Aplicativo iniciador {{site.data.keyword.streaminganalyticsfull}}](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-starter-application/).

Para fazer download e implementar o aplicativo iniciador no {{site.data.keyword.Bluemix_short}}:

1. Faça download do aplicativo iniciador [Event Detection](https://hub.jazz.net/project/streamscloud/EventDetection/overview) ou [NYC Traffic](https://hub.jazz.net/project/streamscloud/NYCTraffic/overview).
2. Na linha de comandos, acesse o diretório de projeto.
  <pre><code>cd myapp</code></pre>
  {:pre}

3. Renomeie o diretório de projeto para que corresponda ao nome fornecido ao aplicativo no {{site.data.keyword.Bluemix_short}}.
4. Conecte ao {{site.data.keyword.Bluemix_short}}:
  <pre><code>cf api https://api.DomainName</code></pre>
  {:pre}

5. Efetue login no {{site.data.keyword.Bluemix_short}} e configure a sua organização de destino quando solicitado:
  <pre><code>cf login</code></pre>
  {:pre}

6. Implemente seu aplicativo:
  <pre><code>cf push myapp</code></pre>
  {:pre}

7. Acesse a página de visão geral do aplicativo, acessível por meio do painel do {{site.data.keyword.Bluemix_short}}, para verificar se o seu
aplicativo foi iniciado com êxito.
8. Ative seu aplicativo para vê-lo em seu navegador. É possível localizar (ou "rotear") a URL do aplicativo
            na página de visão geral do aplicativo.

Agora que o seu app está em execução, será possível acessar o painel de serviços para ver o status de sua instância do {{site.data.keyword.streaminganalyticsshort}} e obter informações para resolução de problemas. Para acessar o painel de serviços, acesse
o painel do {{site.data.keyword.Bluemix_short}} e clique no tile do {{site.data.keyword.streaminganalyticsshort}} em sua página de visão geral do
aplicativo.
