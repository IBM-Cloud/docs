---



copyright:

  years: 2015，2017

lastupdated: "2017-04-19"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:prereq: .prereq}
{:download: .download}
{:pre: .pre}
{:app_name: data-hd-keyref="app_name"}
{:app_key: data-hd-keyref="app_key"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:host: data-hd-keyref="host"}
{:org_name: data-hd-keyref="org_name"}
{:route: data-hd-keyref="route"}
{:space_name: data-hd-keyref="space_name"}
{:service_name: data-hd-keyref="service_name"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:user_ID: data-hd-keyref="user_ID"}

# Faça download, modifique e reimplemente seu app Cloud Foundry com a interface da linha de comandos

Use a interface da linha de comandos do {{site.data.keyword.Bluemix_notm}} para fazer download, modificar e reimplementar os aplicativos e as instâncias de serviço do Cloud Foundry.
{:shortdesc}

Antes de iniciar, faça download e instale a interface da linha de comandos do {{site.data.keyword.Bluemix_notm}}. 

<p>
<a class="xref" href="https://clis.ng.bluemix.net" target="_blank" title="(Abre em uma nova guia ou janela)"><img class="image" src="images/btn_bx_commandline.svg" alt="Fazer download da interface da linha de comandos do Bluemix" /> </a>
</p>

**Restrição:** a ferramenta de linha de comandos não é suportada por Cygwin. Use a ferramenta em uma janela de linha de comandos diferente da janela de linha de comandos do Cygwin.
{:prereq}

Após a instalação da interface da linha de comandos, é possível iniciar:

  1. {: download} Faça download do código do app em um novo diretório para configurar seu ambiente de desenvolvimento.
  
    <a class="xref" href="http://bluemix.net" target="_blank" title="(Abre em uma nova guia ou janela)"><img class="image" src="images/btn_starter-code.svg" alt="Fazer download do código do aplicativo" /> </a>

  2. Mude para o diretório no qual o seu código está localizado.

  <pre class="pre"><code class="hljs">cd <var class="keyword varname">your_new_directory</var></code></pre>

  3.  Faça mudanças no código de seu app conforme necessário. Por exemplo, se você estiver usando um aplicativo de amostra do {{site.data.keyword.Bluemix}} e seu app contiver o arquivo `src/main/webapp/index.html`, será possível modificá-lo e editar "Obrigado por criar..." para dizer algo novo. Assegure-se de que o app seja executado localmente antes de implementá-lo de volta no {{site.data.keyword.Bluemix_notm}}.

    Anote o arquivo `manifest.yml`. Ao implementar seu app de volta no {{site.data.keyword.Bluemix_notm}}, esse arquivo será usado para determinar a URL de seu aplicativo, a alocação de memória, o número de instâncias e outros parâmetros essenciais. É possível [ler mais sobre o arquivo manifest](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){: new_window} na documentação do Cloud Foundry.

    Preste atenção também no arquivo `README.md`, que contém detalhes como instruções de construção, se aplicável.

    Nota: caso seu aplicativo seja um app Liberty, deve-se construí-lo antes da reimplementação.

  4. Conecte e efetue login no {{site.data.keyword.Bluemix_notm}}.

  <pre class="pre"><code class="hljs">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></code></pre>

  <pre class="pre"><code class="hljs">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></code></pre>

  Se você estiver usando um ID federado, use a opção `-sso`.

  <pre class="pre"><code class="hljs">bluemix login  -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var> -sso</code></pre>

  5. Em <var class="keyword varname">your_new_directory</var>, reimplemente seu app no {{site.data.keyword.Bluemix_notm}} usando o comando `bluemix app push`. Para obter mais informações sobre o comando `bx app push`, veja [Fazendo upload de seu aplicativo](/docs/starters/upload_app.html).

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var></code></pre>

  6. Acesse seu app procurando https://<var class="keyword varname" data-hd-keyref="app_url">app_url</var>.<span class="keyword" data-hd-keyref="APPDomain">AppDomainName</span>.
