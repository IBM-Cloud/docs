{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Monitoramento e criação de log
{: #monitoringandlogging}

*Última atualização: 8 de dezembro de 2015*

Ao monitorar seus apps e revisar logs, é possível seguir a execução do aplicativo e o fluxo de dados para obter um melhor entendimento de sua implementação. Além disso, é possível reduzir o tempo e o esforço necessários para localizar problemas e repará-los.
{:shortdesc}

Os aplicativos {{site.data.keyword.Bluemix}} podem ser amplamente distribuídos, aplicativos multi-instância, e a execução do aplicativo e seus dados pode ser compartilhada entre vários serviços. Nesse ambiente complexo, o monitoramento dos apps e a revisão dos logs é importante para o gerenciamento dos apps.

O {{site.data.keyword.Bluemix_notm}} possui um mecanismo de criação de log integrado para produzir arquivos de log para seus apps enquanto estão sendo executados. Nos logs, é possível visualizar os erros, os avisos e as mensagens informativas produzidas para o app. Além disso, também é possível configurar o app para gravar mensagens de log para o arquivo de log. Para obter mais informações sobre formatos de log e como visualizar os logs, consulte [Criação de log para apps {{site.data.keyword.Bluemix_notm}}](#logging_for_bluemix_apps).

Monitorar o app permite ver e controlar a implementação do app. Com o monitoramento, é possível realizar as tarefas a seguir:

* Coletar e monitorar informações de desempenho para instâncias do app e verificar se elas são funcionais.
* Obter insight sobre operações do aplicativo, por exemplo, detectar os gargalos em potencial ou quando há necessidade de upgrades.
* Estimar uso do recurso e encargos.

Para operações estáveis de suas implementações na plataforma {{site.data.keyword.Bluemix_notm}}, você deseja detectar problemas rapidamente e determinar as causas de forma eficiente. Para realizar esse objetivo, mantenha a resolução de problemas em mente ao projetar seus apps e use serviços ou ferramentas para monitoramento e criação de log quando seu app for implementado no {{site.data.keyword.Bluemix_notm}}.

##Monitorando apps em execução no Cloud Foundry
{: #monitoring_bluemix_apps}

Quando você estiver usando a infraestrutura do Cloud Foundry para executar seus apps no {{site.data.keyword.Bluemix_notm}}, você desejará manter informações de desempenho, como status de funcionamento, uso de recursos e métricas de tráfego. Com essas informações de desempenho, será possível, então, tomar decisões ou executar ações adequadamente.

Para monitorar apps {{site.data.keyword.Bluemix_notm}}, use um dos métodos a seguir:

* Serviços {{site.data.keyword.Bluemix_notm}}. O Monitoring and Analytics oferece um serviço que pode ser usado para monitorar o desempenho do aplicativo. Além disso, esse serviço também fornece recursos analíticos, como análise de log. Para obter mais informações, consulte [Monitoring and
Analytics](../services/monana/index.html).
* Opções de terceiros. Por exemplo, [New Relic](http://newrelic.com/){:new_window}.

##Criação de log para apps em execução no Cloud Foundry
{: #logging_for_bluemix_apps}

Os arquivos de log são criados automaticamente quando se está usando a infraestrutura do Cloud Foundry para executar seus apps no {{site.data.keyword.Bluemix_notm}}. É possível visualizar os logs a partir do Painel do {{site.data.keyword.Bluemix_notm}} ou da interface de linha de comandos cf. Também é possível filtrar os logs para ver as partes em que você está interessado.

###Formato do Log
{: #log_format}

Os logs para aplicativos {{site.data.keyword.Bluemix_notm}} são exibidos em um formato fixo, semelhante ao padrão a seguir:

```
         1         2         3         4         5
12345678901234567890123456789012345678901234567890
--------------------------------------------------
yyyy-MM-ddTHH:mm:ss:SS-0500 [App/0]      OUT <message>
```
{:screen}

Toda entrada de log contém quatro campos. Consulte a lista a seguir para obter uma breve descrição de cada campo:

<dl>
<dt><strong>Registro de data e hora</strong></dt>
<dd>
<pre class="pre screen"><code>yyyy-MM-ddTHH:mm:ss:SS-0500</code></pre>
<p>Colunas: 1 – 27</p>
<p>O tempo da instrução de log. O registro de data e hora é definido até o milissegundo.</p>
</dd>

<dt><strong>Componente</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>Colunas: 29 – 40</p>
<p>O componente que produz logs. A lista a seguir fornece a definição para todos os componentes:</p>

<dl>
<dt><strong>AP
</strong></dt>
<dd>Aplicativo. O componente APP é seguido por uma barra e um dígito que indica a instância do aplicativo. Em que 0 é a primeira instância, 1 é a segunda e assim por diante.</dd>

<dt><strong>API</strong></dt>
<dd>API do Cloud Foundry.</dd>

<dt><strong>DEA</strong></dt>
<dd>Droplet Execution Agent.</dd>

<dt><strong>LGR</strong></dt>
<dd>Loggregator.</dd>

<dt><strong>RTR</strong></dt>
<dd>Roteador.</dd>

<dt><strong>STG</strong></dt>
<dd>Preparação.</dd>
</dl>
</dd>

<dt><strong>Stream
</strong></dt>
<dd>
<pre class="pre screen"><code>OUT </code></pre>
<p>Colunas: 42 – 44</p>
<p>O fluxo para o qual a mensagem de log é gravada. <samp class="ph codeph">OUT</samp> refere-se ao fluxo <samp class="ph codeph">stdout</samp> e <samp class="ph codeph">ERR</samp> refere-se ao fluxo <samp class="ph codeph">stderr</samp>.</p>
</dd>

<dt><strong>Mensagem</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Mensagem</var>&gt;</code></pre>
<p>Colunas: 46 – término da linha</p>
<p>A mensagem que é emitida pelo componente. A mensagem varia, dependendo do contexto.</p>
</dd>

</dl>

###Visualizando logs
{: #viewing_logs}

É possível usar o Painel do {{site.data.keyword.Bluemix_notm}} ou a interface da linha de comandos para visualizar logs.

####VISUALIZANDO LOGS A PARTIR DO PAINEL DO {{site.data.keyword.Bluemix_notm}}

Para ver os logs de **Implementação** ou de **Tempo de execução**, conclua as etapas a seguir:
1. Clique no quadrado do app. A página de detalhes do app é exibida.
2. Na barra de navegação à esquerda, clique em **Logs**.

####VISUALIZANDO LOGS A PARTIR DA INTERFACE DA LINHA DE COMANDOS

Escolha entre as opções a seguir para visualizar logs a partir da interface da linha de comandos:

<ul>
<li>Ajustando logs ao implementar apps.
<p>Use o comando **cf logs** para exibir logs a partir de seu app e dos componentes do sistema que interagem com ele durante a implementação de apps no {{site.data.keyword.Bluemix_notm}}. É possível digitar os comandos a seguir na interface de linha de comandos cf. Para obter informações adicionais sobre logs cf, consulte [Tipos de log e suas mensagens em Cloud Foundry](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}.</p>
<dl>
<dt><strong>cf logs <var class="keyword varname">appname</var> --recent</strong></dt>
<dd>Exibir logs do passado recente.</dd>

<dt><strong>cf logs <var class="keyword varname">appname</var></strong></dt>
<dd>Exiba logs que são gerados a partir do momento em que você executa este
comando.</dd>
</dl>
<div class="note tip"><span class="tiptitle">Dica:</span> ao executar o comando <span class="keyword cmdname">cf push</span> ou <span class="keyword cmdname">cf
start</span> em uma janela de linha de comandos, é possível inserir <samp class="ph codeph">cf
logs appname --recent</samp> em outra janela de linha de comandos para ver
os logs em tempo real. </div>
</li>

<li>Visualizando logs após a implementação dos apps.

<p>Se a criação de log do aplicativo estiver ativada, será possível visualizar os logs de aplicativo a seguir se você encontrar problemas com o app no tempo de execução. Os logs do aplicativo podem ajudar a determinar a causa do erro.</p>

<dl><strong>buildpack.log</strong></dt>
<dd>
<p>Esse arquivo de log registra eventos informativos de baixa granularidade para
depuração. É possível usar esse log para solucionar problemas de
execução de buildpack.</p>
<p>Para gerar dados para o arquivo <span class="ph filepath">buildpack.log</span>, deve-se ativar o rastreio do buildpack usando o comando a seguir:
   <pre class="pre">cf set-env <var class="keyword varname">appname</var> JBP_LOG_LEVEL DEBUG</pre>
<p>
<p>Para visualizar esse log, insira o comando a seguir:
<pre class="pre">cf files <var class="keyword varname">appname</var> app/.buildpack-diagnostics/buildpack.log</pre>
</p>
</dd>

<dt><strong>staging_task.log</strong></dt>
<dd><p>Esse arquivo de log registra mensagens depois das principais etapas da
tarefa de preparação. É possível usar esse log para solucionar problemas de preparação.</p>
<p>Para visualizar esse log, insira o comando a seguir:
<pre class="pre">cf files <var class="keyword varname">appname</var> logs/staging_task.log</pre>
</p>
</dd>
</dl>
</li></ul>


**Nota:** para obter informações sobre como ativar a criação de log do aplicativo, consulte [Depurando erros de tempo de execução](../troubleshoot/debugging.html#debug_runtime).

###Filtrando logs
{: #filtering_logs}

Para visualizar logs em que você está interessado ou excluir o conteúdo que você não deseja visualizar, é possível usar o comando **cf logs** com opções de filtragem, como **cut** e **grep** na interface de linha de comandos cf.

* Para visualizar uma parte, em vez dos logs detalhados completos, use a opção **cut**. Por exemplo, para exibir as informações do componente e da mensagem, use o comando a seguir:
```
cf logs appname --recent | cut -c 29-40,46- 
```

Para obter mais informações sobre a opção **grep**, digite cut --help.
* Para exibir entradas de log que contêm determinadas palavras-chave, use a opção **grep**. Por exemplo, para exibir entradas de log que contêm a palavra-chave [APP, é possível usar o comando a seguir:
```
cf logs appname --recent | grep '\[App'
```
Para obter mais informações sobre a opção **grep**, digite `grep --help`.

###Configurando a criação de log de terceiro
{: #thirdparty_logging}

O {{site.data.keyword.Bluemix_notm}} mantém
uma quantia limitada de informação de log na memória. Quando as informações são
registradas, as informações antigas são substituídas pelas informações mais novas. Para manter todas as informações do log, é possível salvar os logs em um serviço de
gerenciamento de log de terceiro.

Para mover logs do aplicativo e do sistema para
um serviço de gerenciamento de log de terceiro, conclua as etapas a seguir:

1. Registre um serviço de gerenciamento de log de terceiro.
    
    É
possível usar qualquer serviço de gerenciamento de log de terceiro que suporte o [protocolo
syslog](http://tools.ietf.org/html/rfc5424){:new_window}, como Papertail, Splunk Storm, SumoLogic e Logentries. Registre um serviço de gerenciamento de log de terceiro e, em seguida, configure o
serviço para fornecer um destino para os logs no {{site.data.keyword.Bluemix_notm}}. Depois que a configuração é concluída, o serviço geralmente fornece uma URL do syslog como o destino para seus logs no {{site.data.keyword.Bluemix_notm}}. Para obter
informações sobre como configurar serviços de gerenciamento de log de terceiro,
consulte [Configurando serviços de gerenciamento de log de terceiro selecionados](http://docs.cloudfoundry.org/devguide/services/log-management-thirdparty-svc.html){:new_window}.

2. Crie uma instância de serviço fornecida pelo usuário.
	
	Para
mover logs no {{site.data.keyword.Bluemix_notm}} para
o serviço de gerenciamento de log de terceiro, deve-se primeiro criar uma instância de serviço
fornecida pelo usuário. Use o comando a seguir para criar uma instância de serviço fornecida pelo usuário, em que service_name é o nome da instância de serviço fornecida pelo usuário e syslog_URL é a URL obtida do serviço de criação de log de terceiros.
	
	```
	cf create-user-provided-service <service_name> -l <syslog_URL>
	```
	
3. Ligue a instância de serviço ao aplicativo.

	Use o comando a seguir para ligar a instância de serviço ao aplicativo, em que appname é o nome do aplicativo e service_name é o nome da instância de serviço fornecida pelo usuário.
	
	```
	cf bind-service appname <service_name>
	```
	
	Depois disso, você será solicitado a remontar o aplicativo digitando cf restage appname para que as mudanças entrem em vigor. Quando os logs forem gerados, você poderá visualizar mensagens semelhantes
no serviço de gerenciamento de log de terceiro depois de um breve atraso.

**Nota:** os logs visualizados na interface de linha de comandos não estão no formato syslog e podem não corresponder exatamente às mensagens exibidas nos serviços de gerenciamento de log de terceiros.
