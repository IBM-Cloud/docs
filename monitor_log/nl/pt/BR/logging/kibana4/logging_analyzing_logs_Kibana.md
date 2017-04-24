---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Análise de log avançada com o Kibana
{:#analyzing_logs_Kibana}

No {{site.data.keyword.Bluemix}}, é possível usar o Kibana, uma plataforma de software livre para análise de dados e visualização, para monitorar, procurar, analisar e visualizar seus dados em uma variedade de gráficos, por exemplo, diagramas e tabelas. Use o Kibana para executar tarefas analíticas avançadas.
{:shortdesc}

É possível ativar o Kibana de qualquer uma das maneiras a seguir:

* No {{site.data.keyword.Bluemix_notm}}

    É possível ativar para seus logs específicos do app CF no Kibana, no contexto para esse app específico.
    
    É possível ativar para seus logs de contêiner do Docker específicos no Kibana, no contexto para esse contêiner específico. 
    
    Para apps CF, a consulta que é usada para filtrar os dados que estão disponíveis para análise no Kibana recupera entradas de log para o aplicativo Cloud Foundry. As informações de log que o Kibana exibe estão todas relacionadas a um único aplicativo Cloud Foundry e a todas as suas instâncias. 
    
    Para contêineres, a consulta que é usada para filtrar os dados que estão disponíveis para análise no Kibana recupera entradas de log para todas as instâncias do contêiner. As informações de log que o Kibana exibe por padrão estão todas relacionadas a um único contêiner ou a um grupo de contêiner e a todas as suas instâncias. 
    
    Para obter mais informações, consulte [Acessando o painel do Kibana por meio do painel do Bluemix](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix).

* Em um link direto do navegador

    Talvez você deseja ativar o Kibana para que os dados que são exibidos agreguem logs de serviços em um espaço fornecido do {{site.data.keyword.Bluemix_notm}}.
    
    A consulta que é usada para filtrar os dados que são exibidos no painel recupera entradas de log para um espaço na organização do
    {{site.data.keyword.Bluemix_notm}}. As informações de log que o Kibana
    exibe incluem registros para todos os recursos que estiverem implementados no espaço da organização do {{site.data.keyword.Bluemix_notm}} na qual você estiver com login efetuado. 
    
    Para obter mais informações, veja [Acessando o painel do Kibana em um navegador da web](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser).
    
    Ao ativar o Kibana por meio de um navegador, é possível optar por trabalhar com o Kibana 4 ou com o Kibana 3. **Nota:** o Kibana 3 foi descontinuado. Para obter informações sobre como usar o Kibana 3 para analisar seus logs, consulte [Analisando logs no Kibana 3 (descontinuado)](../logging_view_kibana3.html#analyzing_logs_Kibana3).

<br>    

O Kibana é uma interface baseada em navegador na qual é possível analisar dados interativamente e customizar painéis que podem ser usados para analisar dados do log e executar tarefas de gerenciamento avançado. 

Os dados que a página do Kibana exibe são restritos por uma procura. O conjunto de dados padrão é definido pelo padrão de índice pré-configurado. Para filtrar as informações, é possível incluir novas consultas de procura e aplicar filtros no conjunto de dados padrão. Em seguida, é possível salvar a procura para reutilização futura. 

O Kibana inclui páginas diferentes que podem ser usadas para analisar seus logs:

| Página do Kibana | Descrição |
|-------------|-------------|
| Descobrir | Use essa página para definir procuras e analisar seus logs interativamente por meio de uma tabela e um histograma. |
| Visualizar | Use esta página para criar visualizações, como gráficos e tabelas, que podem ser usadas para analisar seus dados do log e comparar resultados.  |
| Painel | Use essa página para analisar seus logs por meio de coleções de visualizações e procuras salvas.  |

**Nota:** é possível analisar somente 1 dia completo por vez por meio da página Visualizar ou da página Painel, mesmo que seja possível voltar 7 dias. Os dados do log são armazenados por 7 dias, por padrão. 

| Página do Kibana | Informações de período de tempo |
|-------------|-------------------------|
| Descobrir | Analisa dados para um máximo de 7 dias. |
| Visualizar | Analisa dados para um período de 24 horas.<br> É possível filtrar dados do log para um período customizado que decorra 24 horas.  |
| Painel | Analisa dados para um período de 24 horas.<br> É possível filtrar dados do log para um período customizado que decorra 24 horas.<br> O selecionador de tempo que você configurar é aplicado a todas as visualizações que estiverem incluídas no painel. |


Por exemplo, é desse modo que o Kibana pode ser usado para mostrar informações sobre um aplicativo ou contêiner CF em seu espaço por meio de diferentes páginas:

* Na página Descobrir, é possível definir novas consultas de procura e aplicar filtros por consulta. Os dados do log são exibidos por meio de uma tabela e de um histograma. É possível usar essas visualizações para analisar os dados interativamente. Para obter mais informações, consulte [Analisando logs interativamente no Kibana](logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).

    Também é possível configurar filtros de campos de log, por exemplo, message_type e instance_ID, e configurar um período de tempo. É possível ativar ou desativar dinamicamente esses filtros. A tabela e o histograma exibirão as entradas de log que atenderem aos critérios de consulta e de filtragem que você ativar. Para obter mais informações, consulte [Filtrando logs no Kibana](logging_kibana_filtering_logs.html#kibana_filtering_logs).
    
* Na página Visualizar, é possível definir novas consultas de procura e visualizações. 

    Para analisar os dados, é possível criar visualizações com base em uma procura nova ou existente.
O Kibana inclui diferentes tipos de visualizações, como tabela, tendências e histograma, que podem ser usados para analisar as informações. O objetivo de cada visualização varia. Algumas visualizações são organizadas em linhas que fornecem os resultados de uma ou mais consultas. Outras visualizações exibem documentos ou informações customizadas. Os dados em uma visualização poderão ser corrigidos ou mudados, se uma consulta de procura for atualizada. É possível integrar a visualização em uma página da web ou compartilhá-la. Para obter mais informações, consulte [Analisando logs usando visualizações](logging_kibana_visualizations.html#logging_kibana_visualizations).

* Na página Painel, é possível customizar, salvar e compartilhar múltiplas visualizações e procuras simultaneamente.  

    É possível incluir, remover e reorganizar as visualizações no painel. Para obter mais informações, consulte [Analisando logs no Kibana por meio de um painel](logging_kibana_analize_logs_dashboard.html#kibana_analize_logs_dashboard).
    
    Depois de customizar um painel do Kibana, é possível analisar os dados por meio de suas visualizações e salvá-los para reutilização futura. Para obter mais informações, veja [Salvando um painel do Kibana](logging_kibana_analize_logs_dashboard.html#save_Kibana_dashboard).

No Kibana, há também uma página *Configurações* que pode ser usada para configurar o Kibana e salvar, excluir, exportar e importar procuras, visualizações e painéis.

Para obter mais informações, consulte o [Guia do Usuário do Kibana ![Ícone de Link externo](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.

**Nota:** o Kibana 4 e o Kibana 3 são suportados. O Kibana 3 foi descontinuado.


##  Acessando o painel do Kibana por meio do painel do Bluemix
{: #launch_Kibana_from_bluemix}

A consulta que é usada para filtrar os dados que são exibidos no Kibana recupera entradas de log para o app ou contêiner CF do {{site.data.keyword.Bluemix_notm}} no local em que o Kibana é ativado.  

Para ver os logs de um aplicativo Cloud Foundry ou contêiner do Docker no Kibana, conclua as etapas a seguir:

1. Efetue login no {{site.data.keyword.Bluemix_notm}} e, em seguida, clique no nome ou no contêiner do app no painel do {{site.data.keyword.Bluemix_notm}}.  
    
2. Abra a guia de log na IU do {{site.data.keyword.Bluemix_notm}}.

    * Para apps CF, clique em **Logs** na barra de navegação. 
    * Para contêineres, selecione **Monitoramento e logs** na barra de navegação e, em seguida, clique na guia **Criação de log**. 
    
    A guia de logs é aberta. 
    
3. Clique em **Visualização avançada**. O painel **Kibana 4** é aberto.

    Por padrão, a página **Descobrir** é carregada com o modelo de índice padrão selecionado e com um filtro de tempo configurado para os últimos 30 segundos. A consulta de procura é configurada para corresponder todas as entradas para o seu app CF ou contêiner do Docker.

    Se a página Descobrir não mostrar nenhuma entrada de log, ajuste o selecionador de tempo. Para obter mais informações, consulte [Configurando um filtro de tempo](logging_kibana_set_time_filter.html#set_time_filter).

Para obter mais informações sobre o Kibana, consulte o [Guia do Usuário do Kibana](https://www.elastic.co/guide/en/kibana/current/index.html).

##  Acessando o painel do Kibana por meio de um navegador da web
{: #launch_Kibana_from_browser}

A consulta que é usada para filtrar os dados que são exibidos no Kibana recupera entradas de log para um espaço na organização do {{site.data.keyword.Bluemix_notm}}. As informações de log que o Kibana exibe incluem registros para todos os recursos que estiverem implementados no espaço da organização do {{site.data.keyword.Bluemix_notm}} na qual você estiver com login efetuado.

Conclua as etapas a seguir para ativar o Kibana em um navegador:

1. Abra [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) para efetuar login na interface com o usuário do Kibana.

2. Selecione a versão do Kibana que deseja usar para analisar seus logs.
    * Selecione a guia **Kibana 4** para trabalhar com o Kibana 4. A página Descobrir se abre. Para obter mais informações, consulte [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).
    * Selecione a guia **Kibana 3** para trabalhar com o Kibana 3. O painel do Kibana padrão é aberto. Para obter mais informações sobre como customizar um painel do Kibana 3, consulte [essa postagem do blog](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/).
     
        **Nota**: o Kibana 3 foi descontinuado. 

    Se a página Descobrir não mostrar nenhuma entrada de log, ajuste o selecionador de tempo. Para obter mais informações, consulte [Configurando um filtro de tempo](logging_kibana_set_time_filter.html#set_time_filter).

Para obter mais informações sobre o Kibana, consulte o [Guia do Usuário do Kibana ![Ícone de Link externo](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.

