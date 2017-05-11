---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-22"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analisando logs no Kibana 3 (descontinuado)
{: #analyzing_logs_Kibana3}

No {{site.data.keyword.Bluemix}}, é possível usar o Kibana, uma plataforma de software livre para análise de dados e visualização, para monitorar, procurar, analisar e visualizar seus dados em uma variedade de gráficos, por exemplo, diagramas e tabelas. Use o Kibana para executar tarefas analíticas avançadas.
{:shortdesc}

É possível ativar o Kibana de qualquer uma das maneiras a seguir:

* No painel do app Cloud Foundary

    É possível ativar para seus logs específicos do app CF no Kibana, no contexto para esse app específico.
    
    A consulta que é usada para filtrar os dados que são exibidos no painel recupera entradas de log para o aplicativo Cloud Foundry. As informações de log exibidas por padrão pelo painel do Kibana estão todas relacionadas a um único aplicativo Cloud Foundry e todas as suas instâncias. Para obter mais informações, consulte [Acessando o painel do Kibana por meio do painel do Bluemix](logging_view_kibana3.html#launch_Kibana_from_bluemix).

* Em um link direto do navegador

    Você pode desejar ativar para o painel customizado do Kibana que agrega dados de serviços dentro de um espaço do {{site.data.keyword.Bluemix}} fornecido.
    
    A consulta que é usada para filtrar os dados que são exibidos no painel recupera entradas de log para um espaço na organização do {{site.data.keyword.Bluemix}}. As informações de log exibidas pelo painel do Kibana incluem registros para todos os recursos que são implementados no espaço da organização do {{site.data.keyword.Bluemix}} em que você efetuou login. Para obter mais informações, veja [Acessando o painel do Kibana em um navegador da web](logging_view_kibana3.html#launch_Kibana_from_browser).
    
    Também é possível mudar ou remover a consulta inicial e incluir mais consultas. Para obter mais informações, veja [Filtrando seus logs do app Cloud Foundry com consultas no Kibana](kibana3/logging_kibana_query.html#logging_kibana_query).


Kibana é uma interface baseada em navegador na qual é possível customizar painéis que podem ser usados para analisar dados do log e executar tarefas de gerenciamento avançado. 

No {{site.data.keyword.Bluemix}}, é possível analisar dados usando o painel do Kibana padrão que está disponível para cada app Cloud Foundry e para cada espaço de sua organização. Por padrão, esses painéis exibem todos os dados que estão disponíveis para as últimas 24 horas por meio de um painel que inclui uma linha Histograma e uma linha Tabela de eventos. 

Para restringir as informações exibidas por meio de qualquer painel padrão, é possível incluir consultas e filtros em um painel padrão. Em seguida, é possível salvar o painel para reutilização futura. 

Os dados exibidos por um painel do Kibana são controlados pela consulta. Para modificar as informações que são exibidas em um painel, é possível mudar a consulta, incluir múltiplas consultas e, em seguida, salve o painel. É possível customizar, salvar e compartilhar múltiplos painéis simultaneamente. É dessa maneira que o Kibana mostra informações sobre um único app em seu espaço, por exemplo.

Também é possível configurar filtros de campos de log, por exemplo, message_type e instance_ID. Para obter mais informações, veja [Formato de log do Kibana](logging_view_kibana3.html#kibana_log_format_cf). É possível ativar ou desativar dinamicamente esses filtros. O painel exibirá as entradas de log que atenderem aos critérios de consulta e filtragem que você ativar. Para obter mais informações, veja [Filtrando dados em um painel do Kibana](logging_view_kibana3.html#filter_data_kibana_dashboard).

Para visualizar os dados, é possível configurar painéis. O Kibana inclui diferentes painéis, como tabela, tendências e histograma, que podem ser usados para analisar as informações. É possível incluir, remover e reorganizar os painéis no painel. O objetivo de cada painel varia. Alguns painéis são organizados em linhas que fornecem os resultados de uma ou mais consultas. Outros painéis exibem documentos ou informações customizadas. Para obter mais informações, veja [Customizando um painel do Kibana](logging_view_kibana3.html#customize_kibana_dashboard).

Depois de customizar um painel, é possível escolher qualquer uma das ações a seguir:

* É possível salvar o painel para reutilização futura. Para obter mais informações, veja [Salvando um painel do Kibana](logging_view_kibana3.html#save_Kibana_dashboard).

* É possível exportar ou compartilhar um link direto para um painel do Kibana com outro usuário. Para obter mais informações, veja [Exportando e compartilhando seus painéis do Kibana](kibana3/logging_kibana_export_share_dashboard.html#sexporting_sharing_kibana_dash).

* É possível integrar o painel em uma página da web. Para um usuário ver um painel integrado, esse usuário deve ter permissões para acessar o Kibana.

Para obter mais informações, veja a documentação do [Kibana ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.elastic.co/guide/en/kibana/current/index.html){: new_window}.

**Nota:** o Kibana 4 e o Kibana 3 são suportados. O Kibana 3 foi descontinuado.


##  Acessando o painel do Kibana por meio do painel do Bluemix
{: #launch_Kibana_from_bluemix}

A consulta que é usada para filtrar os dados que são exibidos no painel recupera entradas de log para o aplicativo Cloud Foundry. As informações de log exibidas por padrão pelo painel do Kibana estão todas relacionadas a um único aplicativo Cloud Foundry e todas as suas instâncias.

Para ver os logs de um aplicativo Cloud Foundry no Kibana, conclua as etapas a seguir:

1. Efetue login no {{site.data.keyword.Bluemix_notm}} e, em seguida, clique no nome do app no painel **Apps** do {{site.data.keyword.Bluemix_notm}}. A página de detalhes do app é aberta.
    
2. Na barra de navegação, clique em **Logs**. A guia de logs é aberta. 
    
3. Clique em **Visualização avançada**. O painel **Kibana 3** é aberto.

Se você não vir nenhum log, ajuste o selecionador de horário no cabeçalho.

Para obter mais informações sobre como customizar um painel do Kibana, veja [esta postagem do blog ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/){: new_window} ou a documentação do [Kibana ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.elastic.co/guide/en/kibana/current/index.html){: new_window}.

##  Acessando o painel do Kibana por meio de um navegador da web
{: #launch_Kibana_from_browser}

A consulta que é usada para filtrar os dados que são exibidos no painel recupera entradas de log para um espaço na organização do {{site.data.keyword.Bluemix}}. As informações de log exibidas pelo painel do Kibana incluem registros para todos os recursos que são implementados no espaço da organização do {{site.data.keyword.Bluemix}} em que você efetuou login.

Conclua as etapas a seguir para abrir um painel do Kibana em um navegador:

1. Abra [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) para efetuar login na interface com o usuário do Kibana.

2. Selecione a guia **Kibana 3** para trabalhar com o Kibana 3. Selecione a guia **Kibana 4** para trabalhar com o Kibana 4. O painel do Kibana padrão é aberto. 

Se você não vir nenhum log, ajuste o selecionador de horário no cabeçalho.

Para obter mais informações sobre como customizar um painel do Kibana, veja [esta postagem do blog ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/){: new_window} ou a documentação do [Kibana ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.elastic.co/guide/en/kibana/current/index.html){: new_window}.



## Filtrando dados em um painel do Kibana
{: #filter_data_kibana_dashboard}

No {{site.data.keyword.Bluemix}}, é possível analisar dados usando o painel do Kibana padrão que é fornecido por recurso ou por espaço do {{site.data.keyword.Bluemix}}. Por padrão, esses painéis exibem todos os dados que estão disponíveis para as últimas 24 horas. No entanto, é possível restringir as informações exibidas por meio de um painel. É possível incluir consultas e filtros em um painel padrão e, em seguida, salvá-lo para reutilização futura.

Em um painel, é possível incluir múltiplas consultas e filtros. Uma consulta define um subconjunto de entradas de log.  Um filtro define a seleção de dados incluindo ou excluindo informações. 

Para apps Cloud Foundry, a lista a seguir descreve exemplos de como filtrar dados:
* Se estiver procurando informações nos logs que incluam termos chave, será possível criar consultas para filtrar por esses termos. Com o Kibana, é possível comparar as consultas visualmente no painel. Para obter mais informações, veja [Filtrando seus logs do app Cloud Foundry com consultas no Kibana](kibana3/logging_kibana_query.html#logging_kibana_query).

* Se estiver procurando informações dentro de um período de tempo específico, será possível filtrar dados dentro de um intervalo de tempo. Para obter mais informações, veja [Filtrando seus logs do app Cloud Foundry por horário no Kibana](kibana3/logging_kibana_filter_by_time_period.html#logging_kibana_time_filter).

* Se estiver procurando informações para um ID da instância específico, será possível filtrar dados por ID da instância. Para obter mais informações, veja [Filtrando seus logs do app Cloud Foundry por ID da instância no Kibana](kibana3/logging_kibana_filter_by_instance_id.html#logging_kibana_instance_id) e [Filtrando seus logs do app Cloud Foundry por ID do aplicativo conhecido no Kibana](kibana3/logging_kibana_filter_by_known_application_id.html#logging_kibana_known_application_id).

* Se estiver procurando informações para um componente específico, será possível filtrar dados por componente (tipo de log). Para obter mais informações, veja [Filtrando seus logs do app Cloud Foundry por tipo de log no Kibana](kibana3/logging_kibana_filter_by_component.html#logging_kibana_component_filter).

* Se estiver procurando informações, por exemplo, mensagens de erro, será possível filtrar dados por tipo de mensagem. Para obter mais informações, veja [Filtrando seus logs do app Cloud Foundry por tipo de mensagem no Kibana](kibana3/logging_kibana_filter_by_message_type.html#logging_kibana_message_type_filter).

## Customizando um painel de Kibana
{: #customize_kibana_dashboard}

É possível customizar diferentes tipos de painéis para visualizar e analisar os dados, por exemplo:
* Painel Single-cf-app: esse é um painel que mostra informações para um único aplicativo Cloud Foundry.  
* Painel Multi-cf-app: esse é um painel que mostra informações para todos os aplicativos Cloud Foundry implementados no mesmo espaço do {{site.data.keyword.Bluemix}}. 

Ao customizar um painel, é possível configurar consultas e filtros para selecionar um subconjunto dos dados do log para mostrar por meio do painel.

Para visualizar os dados, é possível configurar painéis. O Kibana inclui diferentes painéis, como tabela, tendências e histograma, que podem ser usados para analisar as informações. É possível incluir, remover e reorganizar os painéis no painel. O objetivo de cada painel varia. Alguns painéis são organizados em linhas que fornecem os resultados de uma ou mais consultas. Outros painéis exibem documentos ou informações customizadas. Por exemplo, é possível configurar um gráfico de barras, gráfico de pizza ou tabela para visualizar os dados e analisá-los.  


## Salvando um painel do Kibana
{: #save_Kibana_dashboard}

Conclua as etapas a seguir para salvar um painel do Kibana após sua customização:

1. Na barra de ferramentas, clique no ícone **Salvar**.

2. Insira um nome para o painel.

    **Nota:** se você tentar salvar um painel com um nome contendo espaços em branco, ele não será salvo.

3. Próximo ao campo de nome, clique no ícone **Salvar**.



## Analisando logs por meio de um painel do Kibana
{: #analyze_kibana_logs}

Depois de customizar um painel do Kibana, é possível visualizar e analisar os dados por meio de seus painéis. 

Para procurar informações, é possível fixar ou desafixar as consultas. 

* É possível fixar uma consulta no painel e automaticamente a procura será ativada.
* Para remover conteúdo do painel, é possível desativar uma consulta.

Para filtrar informações, é possível ativar ou desativar filtros. 

* É possível marcar a caixa de seleção **Alternar** ![Alternar caixa para incluir um filtro](images/logging_toggle_include_filter.jpg) em um filtro para ativá-lo.   
* É possível desmarcar a caixa de seleção **Alternar** ![Alternar caixa para incluir um filtro](images/logging_toggle_exclude_filter.jpg) em um filtro para desativá-lo. 

Os gráficos e diagramas em seu painel exibem os dados. É possível usar os gráficos e diagramas em seu painel para monitorar os dados. 

Por exemplo, para um painel single-cf-app, o painel inclui informações sobre um aplicativo Cloud Foundry. Os dados que podem ser visualizados e analisados são limitados a esse app. É possível usar o painel para analisar os dados para todas as instâncias do app. É possível comparar instâncias. É possível filtrar as informações por ID da instância. 

É possível definir e fixar uma consulta para cada ID da instância no painel. 

![Painel com consultas fixadas](images/logging_kibana_dash_activate_query.jpg)

Em seguida, é possível ativar ou desativar consultas individuais, dependendo das informações da instância que você deseja ver no painel. 

A figura a seguir mostra uma consulta ativada e a outra desativada:

![Painel com consultas fixadas](images/logging_kibana_dash_deactivate_query.jpg)

Se você desejar comparar 2 instâncias em um Histograma, será possível definir duas consultas no mesmo painel, uma para cada ID da instância. É possível conceder a elas um alias e uma cor exclusiva para identificá-las facilmente. O Kibana manipula múltiplas consultas associando-as a um OR lógico. 

A figura a seguir mostra o painel para configurar um alias e uma cor para uma consulta, para fixá-la no painel e para desativá-la:

![Assistente de painel para configurar consulta](images/logging_kibana_query_def.jpg)



## Formato de log do Kibana para aplicativos Cloud Foundry
{: #kibana_log_format_cf}

É possível configurar um painel do Kibana para exibir os campos a seguir para cada entrada de log:

<dl>
<dt><strong>@timestamp</strong></dt>
<dd>
<pre class="pre screen"><code>yyyy-MM-ddTHH:mm:ss:SS-0500</code></pre>
<p>O horário do evento registrado. O registro de data e hora é definido até o milissegundo.</p>
</dd>

<dt><strong>@version</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>ALCH_TENANT_ID</strong></dt>
<dd>
<p>O ID do recurso do {{site.data.keyword.Bluemix_notm}}.</p>
</dd>

<dt><strong>_id</strong></dt>
<dd>
<p>O ID exclusivo para seu documento de log.</p>
</dd>

<dt><strong>_index</strong></dt>
<dd>
<p>O índice para sua entrada de log.</p>
</dd>

<dt><strong>_type</strong></dt>
<dd>
<p>O tipo de log; por exemplo, <samp>syslog</samp>.</p>
</dd>

<dt><strong>app_name</strong></dt>
<dd>
<p>O nome de seu aplicativo {{site.data.keyword.Bluemix_notm}}.</p>
</dd>

<dt><strong>application_id</strong></dt>
<dd>
<p>O ID exclusivo de seu aplicativo {{site.data.keyword.Bluemix_notm}}.</p>
</dd>

<dt><strong>host</strong></dt>
<dd>
<p>O nome de seu aplicativo que produziu os dados do log.</p>
</dd>

<dt><strong>instance_id</strong></dt>
<dd>
<p>O ID da instância de sua instância do aplicativo que produziu os dados do log.</p>
</dd>

<dt><strong>module</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>loglevel</strong></dt>
<dd>
<p>A severidade do evento registrado.</p>
</dd>

<dt><strong>mensagem</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Mensagem</var>&gt;</code></pre>
<p>A mensagem que é emitida pelo componente. A mensagem varia, dependendo do contexto.</p>
</dd>

<dt><strong>message_type</strong></dt>
<dd>
<pre class="pre screen"><code>OUT </code></pre>
<p>O fluxo para o qual a mensagem de log é gravada. <samp class="ph codeph">OUT</samp> refere-se ao fluxo <samp class="ph codeph">stdout</samp> e <samp class="ph codeph">ERR</samp> refere-se ao fluxo <samp class="ph codeph">stderr</samp>.</p>
</dd>

<dt><strong>org_id</strong></dt>
<dd>
<p>O ID exclusivo de sua organização do {{site.data.keyword.Bluemix_notm}}.</p>
</dd>

<dt><strong>org_name</strong></dt>
<dd>
<p>O nome da organização do {{site.data.keyword.Bluemix_notm}} na qual seu app está montado.</p>
</dd>

<dt><strong>origin</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>source_id</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>O componente que produz logs. A lista a seguir descreve os logs de cada componente:</p>

<dl>
<dt><strong>API</strong></dt>
<dd>Respostas registradas em chamadas API que solicitam uma mudança no estado do app.</dd>

<dt><strong>AP
</strong></dt>
<dd>Respostas registradas de seu app.</dd>

<dt><strong>CELL</strong></dt>
<dd>Respostas registradas da célula Diego que indicam quando um aplicativo é iniciado, parado ou travado.</dd>

<dt><strong>LGR</strong></dt>
<dd>Respostas registradas do loggregator que indicam problemas com o processo de criação de log.</dd>

<dt><strong>RTR</strong></dt>
<dd>Respostas registradas do Roteador quando ele roteia solicitações de HTTP para seu app.</dd>

<dt><strong>SSH</strong></dt>
<dd>Respostas registradas da célula Diego quando um usuário acessa um contêiner de app usando o comando **cf ssh**.</dd>

<dt><strong>STG</strong></dt>
<dd>Respostas registradas da célula Diego ou do Droplet Execution Agent quando seu app é montado ou remontado.</dd>
</dl>
</dd>

<dt><strong>space_name</strong></dt>
<dd>
<p>O nome do espaço do {{site.data.keyword.Bluemix_notm}} no qual seu app é montado.</p>
</dd>

<dt><strong>timestamp</strong></dt>
<dd>
<p>O horário do evento registrado. O registro de data e hora é definido até o milissegundo.</p>
</dd>

<dt><strong>_type</strong></dt>
<dd>
<p>O tipo de log, por exemplo, <samp>syslog</samp>.</p>
</dd>
</dl>




