---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Navegando para o painel do Kibana
{: #k4_launch}

É possível ativar o Kibana da UI do {{site.data.keyword.Bluemix}} ou diretamente de um navegador da web.
{:shortdesc}

Ative o Kibana do {{site.data.keyword.Bluemix_notm}} para visualizar e analisar os dados no contexto para o recurso por meio do qual você ativa o Kibana. Por exemplo, é possível ativar para seus logs específicos do app CF no Kibana, no contexto para esse app específico ou para seus logs específicos de contêiner do Docker no Kibana, no contexto para esse contêiner específico. 
    
Ative o Kibana por meio de um link direto do navegador se você deseja ver dados do log agregados de serviços dentro de um espaço do {{site.data.keyword.Bluemix_notm}} fornecido. A consulta que é usada para filtrar os dados que são exibidos no painel recupera entradas de log para um espaço na organização do
    {{site.data.keyword.Bluemix_notm}}. As informações de log que o Kibana
    exibe incluem registros para todos os recursos que estiverem implementados no espaço da organização do {{site.data.keyword.Bluemix_notm}} na qual você estiver com login efetuado. 

Para obter mais informações sobre o Kibana, consulte o [Guia do Usuário do Kibana ![Ícone de Link externo](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.
    

##  Navegando para o painel do Kibana por meio do painel do Bluemix
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


##  Navegando para o painel do Kibana por meio de um navegador da web
{: #launch_Kibana_from_browser}

A consulta que é usada para filtrar os dados que são exibidos no Kibana recupera entradas de log para um espaço na organização do {{site.data.keyword.Bluemix_notm}}. As informações de log que o Kibana exibe incluem registros para todos os recursos que estiverem implementados no espaço da organização do {{site.data.keyword.Bluemix_notm}} na qual você estiver com login efetuado.

Conclua as etapas a seguir para ativar o Kibana em um navegador:

1. Abra [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) para efetuar login na interface com o usuário do Kibana.

2. Selecione a versão do Kibana que deseja usar para analisar seus logs.
    * Selecione a guia **Kibana 4** para trabalhar com o Kibana 4. A página Descobrir se abre. Para obter mais informações, consulte [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).
    * Selecione a guia **Kibana 3** para trabalhar com o Kibana 3. O painel do Kibana padrão é aberto. Para obter informações sobre como usar o Kibana 3 para analisar seus logs, consulte [Analisando logs no Kibana 3 (descontinuado)](../logging_view_kibana3.html#analyzing_logs_Kibana3). Para obter mais informações sobre como customizar um painel do Kibana 3, veja [esta postagem do blog ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/).
     
        **Nota**: o Kibana 3 foi descontinuado.

    Se a página Descobrir não mostrar nenhuma entrada de log, ajuste o selecionador de tempo. Para obter mais informações, consulte [Configurando um filtro de tempo](logging_kibana_set_time_filter.html#set_time_filter).


