---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analisando as métricas no Grafana
{:#analyzing_metrics_grafana}

No {{site.data.keyword.Bluemix}}, é possível usar o Grafana, uma plataforma de análise de dados e de visualização de software livre para monitorar, procurar, analisar e visualizar suas métricas em uma variedade de gráficos, por exemplo, diagramas e tabelas. Use o Grafana para executar tarefas analíticas avançadas.
{:shortdesc}

É possível ativar o Grafana de qualquer uma das maneiras a seguir:

* No {{site.data.keyword.Bluemix_notm}}

    É possível ativar para suas métricas de contêiner do Docker específicas no Grafana, no contexto para esse contêiner específico. 
    
    Para obter mais informações veja [Navegando para o painel do Grafana por meio do painel do
    {{site.data.keyword.Bluemix_notm}}](monitoring_analyzing_metrics_grafana.html#launch_grafana_from_bluemix).

* Em um link direto do navegador

    É possível ativar o Grafana para que os dados que são exibidos agreguem logs de serviços em um espaço fornecido do {{site.data.keyword.Bluemix_notm}}.
    
    Para obter mais informações, veja [Navegando para o painel do Kibana de um navegador da web](monitoring_analyzing_metrics_grafana.html#launch_grafana_from_browser).
    
Para obter mais informações sobre o Grafana, consulte o [Guia do Usuário do Grafana ![Ícone de Link externo](../../../icons/launch-glyph.svg "External link icon")](http://docs.grafana.org/guides/getting_started/){: new_window}.


##  Navegando para o painel do Grafana por meio do painel do Bluemix
{: #launch_grafana_from_bluemix}

A consulta que é usada para filtrar os dados que são exibidos no Grafana recupera dados para o contêiner do {{site.data.keyword.Bluemix_notm}} no local em que o Kibana é ativado. 

Para ver as métricas de um contêiner do Docker no Grafana, conclua as etapas a seguir:

1. Efetue login no {{site.data.keyword.Bluemix_notm}} e, em seguida, clique no contêiner por meio do painel do {{site.data.keyword.Bluemix_notm}}. 
    
2. Na barra de navegação, clique em **Monitoramento e logs**. A guia de monitoramento é aberta. 
    
3. Clique em **Visualização avançada**. O painel do **Grafana** é aberto.


##  Navegando para o painel do Grafana por meio de um navegador da web
{: #launch_grafana_from_browser}

A consulta que é usada para filtrar os dados que são exibidos no Grafana recupera dados para um espaço na organização do {{site.data.keyword.Bluemix_notm}}. As informações de métricas que o Grafana exibe incluem registros para todos os recursos que estiverem implementados no espaço da organização do {{site.data.keyword.Bluemix_notm}} na qual você estiver com login efetuado.

Conclua as etapas a seguir para ativar o Grafana em um navegador:

1. Abra [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) para efetuar login na interface com o usuário do Grafana.

2. Selecione **Grafana**.
     

