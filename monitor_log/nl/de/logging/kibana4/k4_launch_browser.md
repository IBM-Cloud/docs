---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Kibana-Dashboard im Web-Browser aufrufen
{: #launch_Kibana_from_browser}

Starten Sie Kibana über einen Browser, wenn Sie Protokolleinträge in einem {{site.data.keyword.Bluemix}}-Bereich analysieren müssen.
{:shortdesc}

Die Abfrage, durch die die Daten gefiltert werden, die in Kibana angezeigt werden, ruft Protokolleinträge für einen Bereich in der {{site.data.keyword.Bluemix_notm}}-Organisation ab. Die Protokollinformationen, die in Kibana angezeigt werden, umfassen Einträge für alle Ressourcen, die innerhalb des Bereichs der {{site.data.keyword.Bluemix_notm}}-Organisation bereitgestellt wurden, an der Sie angemeldet sind.

Führen Sie die folgenden Schritte aus, um Kibana über einen Browser zu starten: 

1. Öffnen Sie [https://logmet.<span class="keyword" data-hd-keyref="DomainName">Domänenname</span>](https://logmet.{DomainName}), um sich bei der Kibana-Benutzerschnittstelle anzumelden.

2. Wählen Sie die Version von Kibana aus, die Sie zur Analyse Ihrer Protokolle verwenden wollen. 
    * Wählen Sie die Registerkarte **Kibana 4** aus, um mit Kibana 4 zu arbeiten. Die Seite 'Discover' wird geöffnet. Weitere Informationen finden Sie unter [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively). 
    * Wählen Sie die Registerkarte **Kibana 3** aus, um mit Kibana 3 zu arbeiten. Das Kibana-Standarddashboard wird geöffnet. Weitere Informationen zur Anpassung eines Kibana 3-Dashboards finden Sie [in diesem Blogbeitrag](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/). 
     
        **Hinweis:** Kibana 3 ist veraltet. 

    Wenn die Seite 'Discover' keine Protokolleinträge anzeigt, passen Sie das Zeitauswahlfeld an. Weitere Informationen finden Sie unter [Zeitfilter festlegen](logging_kibana_set_time_filter.html#set_time_filter).

Weitere Informationen zu Kibana finden Sie in der Veröffentlichung [Kibana User Guide ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.
