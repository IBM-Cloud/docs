---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Acessando o painel do Kibana por meio do painel do Bluemix
{: #launch_Kibana_from_bluemix}

Ative o Kibana na IU do {{site.data.keyword.Bluemix}} para ver os logs específicos de um aplicativo Cloud Foundry ou contêiner do Docker.{:shortdesc}

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

Para obter mais informações sobre o Kibana, consulte o [Guia do Usuário do Kibana ![Ícone de Link externo](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.

