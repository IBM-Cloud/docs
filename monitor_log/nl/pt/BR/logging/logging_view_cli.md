---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analisando logs do app CF na CLI
{: #analyzing_logs_cli}

No {{site.data.keyword.Bluemix}}, é possível visualizar, filtrar e analisar logs por meio da interface da linha de comandos usando o comando **cf logs**. Use a linha de comandos para gerenciar logs programaticamente.
{:shortdesc}

Use o comando **cf logs** para exibir logs de um app Cloud Foundry e dos componentes do sistema que interagem com ele durante a implementação do app no {{site.data.keyword.Bluemix_notm}}. O comando **cf logs** exibe os fluxos de logs STDOUT e STDERR de um aplicativo Cloud Foundry.

Para visualizar os logs de seu interesse ou excluir o conteúdo que você não deseja visualizar, é possível usar o comando **cf logs** com opções de filtragem, como **cut** e **grep**, na interface da linha de comandos cf.

* Para visualizar os logs para um app Cloud Foundry, veja [Visualizando o log para um app Cloud Foundry](logging_view_cli.html#full_log_cli).
* Para visualizar os registros de log mais recentes para um app Cloud Foundry, veja [Visualizando as entradas de log mais recentes para um app Cloud Foundry](logging_view_cli.html#tailing_log_cli).
* Para visualizar os registros de log para um app Cloud Foundry em um intervalo de tempo específico, veja [Visualizando uma seção dos logs](logging_view_cli.html#partial_log_cli).
* Para visualizar as entradas nos logs para um app Cloud Foundry que contenham palavras-chave específicas, veja [Visualizando entradas de log que contenham determinadas palavras-chave](logging_view_cli.html#partial_by_keyword_log_cli).


## Visualizando o log para um app Cloud Foundry
{: #full_log_cli}

Para ver todos os logs disponíveis para um app Cloud Foundry, conclua as etapas a seguir:

1. Abra um terminal e efetue login no {{site.data.keyword.Bluemix}}.

2. Na linha de comandos, execute o comando a seguir para exibir todos os logs:

   <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var></code></pre>
   
   
## Visualizando as entradas de log mais recentes para um app Cloud Foundry
{: #tailing_log_cli}

Para ver os logs mais recentes que estão disponíveis para um app Cloud Foundry, conclua as etapas a seguir:

1. Abra um terminal e efetue login no {{site.data.keyword.Bluemix}}.

2. Na linha de comandos, execute o comando a seguir para exibir todos os logs:

     <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent</code></pre>

<div class="note tip"><span class="tiptitle">Dica:</span> ao executar o comando <span class="keyword cmdname">cf push</span> ou <span class="keyword cmdname">cf
start</span> em uma janela de linha de comandos, é possível inserir <samp class="ph codeph">cf
logs appname --recent</samp> em outra janela de linha de comandos para ver
os logs em tempo real. </div>


## Visualizando uma seção de um log do Cloud Foundry
{: #partial_log_cli}

Para visualizar uma parte dos logs que estão disponíveis para um app Cloud Foundry dentro de um intervalo de tempo, conclua as etapas a seguir:

1. Abra um terminal e efetue login no {{site.data.keyword.Bluemix}}.

2. Na linha de comandos, execute o comando a seguir para exibir todos os logs:

    <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent  | cut -c 29-40,46-</code></pre>
    
    Para obter mais informações sobre a opção **cut**, insira **cut --help**.


## Visualizando entradas de log que contêm determinadas palavras-chave
{: #partial_by_keyword_log_cli}

Para exibir entradas de log que contenham determinadas palavras-chave para um app Cloud Foundry, conclua as etapas a seguir:

1. Abra um terminal e efetue login no {{site.data.keyword.Bluemix}}.

2. Na linha de comandos, execute o comando a seguir para exibir todos os logs:

    <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent | grep '<var class="keyword varname">keyword</var>'</code></pre>
    

Por exemplo, para exibir entradas de log que contenham a palavra-chave **APP**, é possível usar o comando a seguir:


<pre class="pre screen"><code>cf logs appname --recent | grep '\[App'</code></pre>

Para obter mais informações sobre a opção **grep**, digite **grep --help**.


## Logs do aplicativo Cloud Foundry
{: #cf_app_logs_cli}

Os logs a seguir estão disponíveis para um aplicativo Cloud Foundry depois de implementá-lo no {{site.data.keyword.Bluemix}}:

<dl><dt><strong>buildpack.log</strong></dt>
<dd>
<p>Esse arquivo de log registra eventos informativos de baixa granularidade para
depuração. É possível usar esse log para solucionar problemas de
execução de buildpack.</p>

<p>Para gerar dados para o arquivo <span class="ph filepath">buildpack.log</span>, deve-se ativar o rastreio do buildpack usando o comando a seguir:</p>

   <pre class="pre">cf set-env <var class="keyword varname">appname</var> JBP_LOG_LEVEL DEBUG</pre>
   
<p>Para visualizar esse log, insira o comando a seguir:</p>

    <pre class="pre">cf files <var class="keyword varname">appname</var> app/.buildpack-diagnostics/buildpack.log</pre>

</dd>

<dt><strong>staging_task.log</strong></dt>
<dd><p>Esse arquivo de log registra mensagens depois das principais etapas da
tarefa de preparação. É possível usar esse log para solucionar problemas de preparação.</p>

<p>Para visualizar esse log, insira o comando a seguir:</p>

    <pre class="pre">cf files <var class="keyword varname">appname</var> logs/staging_task.log</pre>
</dd>
</dl>

**Nota:** para obter informações sobre como ativar a criação de log do aplicativo, consulte [Depurando erros de tempo de execução](/docs/debug/index.html#debugging-runtime-errors).

