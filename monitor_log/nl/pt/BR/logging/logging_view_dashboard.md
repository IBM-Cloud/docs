---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analisando logs de apps CF no painel do Bluemix
{: #analyzing_logs_bmx_ui}

No {{site.data.keyword.Bluemix}}, é possível visualizar, filtrar e analisar logs por meio do painel da guia **Log** que está disponível para cada aplicativo Cloud Foundry. Use o painel do {{site.data.keyword.Bluemix}} para visualizar a atividade mais recente do aplicativo.{:shortdesc}

O {{site.data.keyword.Bluemix_notm}} Public oferece um serviço de Criação de log integrado. Quando você executa seus aplicativos no Cloud Foundry,
o serviço de Criação de log captura dados do log de componentes do sistema que interagem com seu aplicativo, sobre seu aplicativo e até mesmo dados do log de dentro de seu aplicativo ao usar stdout e stderr.

Os logs para aplicativos {{site.data.keyword.Bluemix_notm}} são exibidos em um formato fixo, semelhante ao padrão a seguir:

<code><var class="keyword varname">Component</var>/<var class="keyword varname">instanceID</var>     <var class="keyword varname">message</var>     <var class="keyword varname">timestamp</var></code>
   
Para obter mais informações sobre o formato de log, veja [Formato de log para logs do app Cloud Foundry](logging_view_dashboard.html#log_format_cf).

**Nota:** no {{site.data.keyword.Bluemix_notm}} Public, os dados do log são armazenados durante 7 dias por padrão. É possível procurar até 1 GB de dados por dia.



##  Acessando a guia de log do Bluemix
{: #launch_logs_tab_bmx_ui}

Para ver os logs de implementação ou de tempo de execução de um aplicativo Cloud Foundry, conclua as etapas a seguir:

1. Efetue login no {{site.data.keyword.Bluemix_notm}} e, em seguida, clique no nome do app no painel **Apps** do {{site.data.keyword.Bluemix_notm}}. 

    A página de detalhes do app é exibida.
    
2. Na barra de navegação, clique em **Logs**.

    A guia de logs é aberta. 
    
    Na guia **Logs**, é possível visualizar os logs recentes para seu app ou acompanhar os logs em tempo real. Além disso, é possível filtrar logs por componente (tipo de log), por ID da instância do app e por erro.



## Formato de log para logs do app Cloud Foundry
{: #log_format_cf}

Toda entrada de log contém os campos a seguir:

<dl>
<dt><strong>Registro de data e hora</strong></dt>
<dd>
<p>O tempo da instrução de log. O registro de data e hora é definido até o milissegundo.</p>
</dd>

<dt><strong>Componente</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>O componente que produz o log. </p>
<p>Cada tipo de componente é seguido por uma barra e um dígito que indica a instância do aplicativo. 0 é o dígito alocado para a primeira instância, 1 é o dígito alocado para a segunda e assim por diante. Observe que é possível filtrar para ver somente uma instância do App no painel.</p>
<p>A lista a seguir descreve os diferentes tipos de componentes:</p>

<dl>
<dt><strong>LGR</strong></dt>
<dd>Loggregator: o componente LGR fornece informações sobre o Cloud Foundry Loggregator, que encaminha os logs de dentro do Cloud Foundry.</dd>

<dt><strong>RTR</strong></dt>
<dd>Roteador: o componente RTR fornece informações sobre solicitações de HTTP para um aplicativo.</dd>

<dt><strong>STG</strong></dt>
<dd>Preparação: o componente STG fornece informações sobre como um aplicativo é montado ou remontado.</dd>

<dt><strong>AP
</strong></dt>
<dd>Aplicativo: o componente APP fornece logs do aplicativo. É neste local que o stderr e o stdout aparecerão em seu código.
</dd>

<dt><strong>API</strong></dt>
<dd>Cloud Foundry API: o componente API fornece informações sobre as ações internas que resultam da solicitação de um usuário para mudar o estado de um aplicativo.</dd>

<dt><strong>DEA</strong></dt>
<dd>Droplet Execution Agent: o componente DEA fornece informações sobre o início, a parada ou o travamento de um aplicativo.
<p>Esse componente estará disponível somente se seu aplicativo for implementado na arquitetura Cloud Foundry que é baseada no DEA.</p></dd>

<dt><strong>CELL</strong></dt>
<dd>Célula Diego: o componente CELL fornece informações sobre o início, a parada ou o travamento de um aplicativo.
<p>Esse componente estará disponível somente se seu aplicativo for implementado na arquitetura Cloud Foundry que é baseada no Diego.</p></dd>

<dt><strong>SSH</strong></dt>
<dd>SSH: o componente SSH fornece informações cada vez que um usuário acessa um aplicativo usando o comando **cf ssh**.
<p>Esse componente estará disponível somente se seu aplicativo for implementado na arquitetura Cloud Foundry que é baseada no Diego.</p></dd>

</dl>
</dd>

<dt><strong>Mensagem</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Mensagem</var>&gt;</code></pre>
<p>A mensagem que é emitida pelo componente. A mensagem varia, dependendo do contexto.</p>
</dd>
</dl>

A figura a seguir mostra os diferentes componentes (tipos de log) em uma arquitetura Cloud Foundry que é baseada no Droplet Execution Agent (DEA):
![Tipos de log em uma arquitetura DEA.](images/logging_F1.png "Componentes (tipos de log") em uma arquitetura Cloud Foundry que é baseada no Droplet Execution Agent (DEA).")



