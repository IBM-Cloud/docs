---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Acessando o painel do Kibana por meio de um navegador da web
{: #launch_Kibana_from_browser}

Ative o Kibana em um navegador se precisar analisar as entradas de log em um espaço do {{site.data.keyword.Bluemix}}.{:shortdesc}

A consulta que é usada para filtrar os dados que são exibidos no Kibana recupera entradas de log para um espaço na organização do {{site.data.keyword.Bluemix_notm}}. As informações de log que o Kibana exibe incluem registros para todos os recursos que estiverem implementados no espaço da organização do {{site.data.keyword.Bluemix_notm}} na qual você estiver com login efetuado.

Conclua as etapas a seguir para ativar o Kibana em um navegador:

1. Abra [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) para efetuar login na interface com o usuário do Kibana.

2. Selecione a versão do Kibana que deseja usar para analisar seus logs.
    * Selecione a guia **Kibana 4** para trabalhar com o Kibana 4. A página Descobrir se abre. Para obter mais informações, consulte [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).
    * Selecione a guia **Kibana 3** para trabalhar com o Kibana 3. O painel do Kibana padrão é aberto. Para obter mais informações sobre como customizar um painel do Kibana 3, consulte [essa postagem do blog](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/).
     
        **Nota**: o Kibana 3 foi descontinuado. 

    Se a página Descobrir não mostrar nenhuma entrada de log, ajuste o selecionador de tempo. Para obter mais informações, consulte [Configurando um filtro de tempo](logging_kibana_set_time_filter.html#set_time_filter).

Para obter mais informações sobre o Kibana, consulte o [Guia do Usuário do Kibana ![Ícone de Link externo](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.
