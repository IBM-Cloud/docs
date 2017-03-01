---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Enviando por push o aplicativo iniciador para {{site.data.keyword.Bluemix_short}}
{: #pushing_starter_app}


 
Implemente o aplicativo iniciador e aprenda rapidamente como usar o serviço {{site.data.keyword.geospatialshort_Geospatial}}:
{:shortdesc}

1. [Instale a ferramenta de linha de comandos cf](docs/starters/install_cli.html) se ainda não tiver feito isso.
2. [Obtenha o código](https://hub.jazz.net/project/streamscloud/geo-starter/overview) do app iniciador do {{site.data.keyword.geospatialshort_Geospatial}}. 
3. Renomeie o diretório que contém os arquivos de aplicativo para corresponder ao nome que você deu a seu aplicativo no {{site.data.keyword.Bluemix_short}}. Por exemplo, se seu aplicativo for denominado myapp, renomeie o diretório para myapp.
4. Na linha de comandos, mude para o diretório renomeado.
<pre><code>cd myapp</code></pre>
5. Conecte ao {{site.data.keyword.Bluemix_short}}:
<pre><code>cf api https://api.DomainName</code></pre>
6. Efetue login no {{site.data.keyword.Bluemix_short}} e configure a organização de destino quando solicitado e implemente seu aplicativo.
<pre><code>
cf login
cf push myapp
</code></pre>

##O que fazer em seguida

* Acesse a página de visão geral do aplicativo, acessível a partir do painel do {{site.data.keyword.Bluemix_short}}, para verificar se
            seu aplicativo foi iniciado com êxito.
* Ative seu aplicativo para vê-lo em seu navegador. É possível localizar (ou "rotear") a URL do aplicativo
            na página de visão geral do aplicativo. A página da web do aplicativo de amostra exibe informações
            sobre o status das chamadas da API REST no código do aplicativo e os eventos
            que o {{site.data.keyword.geospatialshort_Geospatial}}
            detecta.
