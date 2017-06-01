---



copyright:

  years: 2015, 2017

lastupdated: "2017-04-19"



---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Fazendo upload do seu aplicativo

Depois de ter efetuado login no {{site.data.keyword.Bluemix}}, é possível fazer upload de seu aplicativo com o comando `bluemix app push`.
{:shortdesc}

Antes de iniciar, deve-se:
  1. Instalar a interface da linha de comandos do {{site.data.keyword.Bluemix}}.

  <a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="(Abre em uma nova guia ou janela)"><img class="image" src="images/btn_bx_commandline.svg" alt="Fazer download {{site.data.keyword.Bluemix}} da interface da linha de comandos" /> </a>

  2. Conecte-se ao {{site.data.keyword.Bluemix}}.

  <pre class="pre"><code class="hljs">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></code></pre>

  3. Efetue login no {{site.data.keyword.Bluemix_notm}}.

  <pre class="pre"><code class="hljs">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></code></pre>

Quando um comando **bluemix app push** é emitido, a interface da linha de comandos fornece o diretório ativo para o ambiente do {{site.data.keyword.Bluemix_notm}} que usa um buildpack para construir e executar o aplicativo.

  1. De seu diretório de aplicativo, insira o comando **bluemix app push** com o nome do aplicativo. O nome do
app deve ser exclusivo no ambiente do {{site.data.keyword.Bluemix_notm}}.

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -m 512m</code></pre>

  O {{site.data.keyword.Bluemix_notm}} inclui buildpacks integrados. Em alguns casos, mesmo para os buildpacks integrados, deve-se também fornecer uma opção -c para especificar o comando que é usado para iniciar o aplicativo. Por exemplo, é necessário usar a opção -c para enviar por push o aplicativo Node.js:

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -c start_command</code></pre>

  Além disso, o aplicativo Node.js deve conter um arquivo package.json válido.

  Todos os outros buildpacks externos devem ser enviados por push usando a opção -b. Por
exemplo:

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -b buildpack_URL</code></pre>

  **Dica:** quando você usa o comando **bluemix app push**, o comando copia todos os arquivos e diretórios de seu diretório atual para o Bluemix. Assegure-se
de que você tenha apenas os arquivos necessários em seu diretório de aplicativo.


  2. Se você mudar seu aplicativo, será possível fazer upload dessas mudanças inserindo o comando `bluemix app push` novamente. O comando usa suas opções anteriores e suas respostas aos prompts para atualizar quaisquer instâncias em execução de seu aplicativo com novos bits de código.

A CLI do {{site.data.keyword.Bluemix}} empacotou um cf cli em sua instalação. O comando `bluemix app push` chama, na realidade, `cf push` para fazer upload e implementar seu aplicativo no {{site.data.keyword.Bluemix_notm}}. Consulte [Comandos cf](/docs/cli/reference/cfcommands/index.html) para obter mais informações sobre cf push. Veja [Usando buildpacks de comunidade](/docs/cfapps/byob.html) para obter informações sobre buildpacks.
