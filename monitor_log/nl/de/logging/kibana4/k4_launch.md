---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Zum Kibana-Dashboard navigieren
{: #k4_launch}

Sie können Kibana über die {{site.data.keyword.Bluemix}}-Benutzerschnittstelle oder direkt über einen Browser starten.
{:shortdesc}

Starten Sie Kibana über {{site.data.keyword.Bluemix_notm}}, um Daten im Kontext der Ressource, von der aus Sie Kibana starten, anzuzeigen und zu analysieren. Sie können Kibana zum Beispiel für bestimmte CF-App-Protokolle im Kontext einer bestimmten App oder für bestimmte Docker-Containerprotokolle im Kontext eines bestimmten Containers starten.  
    
Starten Sie Kibana über einen direkten Browser-Link, wenn Sie aggregierte Protokolldaten aus Services in einem angegebenen {{site.data.keyword.Bluemix_notm}}-Bereich anzeigen möchten. Die Abfrage, durch die die Daten gefiltert werden, die im Dashboard angezeigt werden, ruft Protokolleinträge für einen Bereich in der {{site.data.keyword.Bluemix_notm}}-Organisation ab. Die Protokollinformationen, die in Kibana angezeigt werden, umfassen Einträge für alle Ressourcen, die innerhalb des Bereichs der {{site.data.keyword.Bluemix_notm}}-Organisation bereitgestellt wurden, an der Sie angemeldet sind.  

Weitere Informationen zu Kibana finden Sie in der Veröffentlichung [Kibana User Guide ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.
    

##  Zum Kibana-Dashboard über das Bluemix-Dashboard navigieren
{: #launch_Kibana_from_bluemix}

Die Abfrage, durch die die Daten gefiltert werden, die in Kibana angezeigt werden, ruft Protokolleinträge für die {{site.data.keyword.Bluemix_notm}}-CF-App oder für den Container von der Position aus ab, an der Sie Kibana starten. 

Führen Sie die folgenden Schritte aus, um die Protokolle einer Cloud Foundry-Anwendung oder eines Docker-Containers in Kibana anzuzeigen:

1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an und klicken Sie auf den App-Namen oder den Container im {{site.data.keyword.Bluemix_notm}}-Dashboard. 
    
2. Öffnen Sie die Registerkarte für Protokolle in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle.

    * Klicken Sie für CF-Apps auf **Protokolle** in der Navigationsleiste. 
    * Wählen Sie für Container **Überwachung und Protokolle** in der Navigationsleiste aus und klicken Sie auf die Registerkarte **Protokollierung**. 
    
    Die Registerkarte für Protokolle wird geöffnet. 
    
3. Klicken Sie auf **Erweiterte Ansicht**. Das Dashboard von **Kibana 4** wird geöffnet.

    Die Seite **Discover** wird standardmäßig mit dem ausgewählten Standardindexmuster und einem Zeitfilter, der auf die letzten 30 Sekunden eingestellt ist, angezeigt. Die Suchabfrage ist so definiert, dass sie allen Einträgen für Ihre CF-App oder Ihren Docker-Container entspricht.

    Wenn die Seite 'Discover' keine Protokolleinträge anzeigt, passen Sie das Zeitauswahlfeld an. Weitere Informationen finden Sie unter [Zeitfilter festlegen](logging_kibana_set_time_filter.html#set_time_filter).


##  Zum Kibana-Dashboard über einen Web-Browser navigieren
{: #launch_Kibana_from_browser}

Die Abfrage, durch die die Daten gefiltert werden, die in Kibana angezeigt werden, ruft Protokolleinträge für einen Bereich in der {{site.data.keyword.Bluemix_notm}}-Organisation ab. Die Protokollinformationen, die in Kibana angezeigt werden, umfassen Einträge für alle Ressourcen, die innerhalb des Bereichs der {{site.data.keyword.Bluemix_notm}}-Organisation bereitgestellt wurden, an der Sie angemeldet sind.

Führen Sie die folgenden Schritte aus, um Kibana über einen Browser zu starten:

1. Öffnen Sie [https://logmet.<span class="keyword" data-hd-keyref="DomainName">Domänenname</span>](https://logmet.{DomainName}), um sich bei der Kibana-Benutzerschnittstelle anzumelden.

2. Wählen Sie die Version von Kibana aus, die Sie zur Analyse Ihrer Protokolle verwenden wollen.
    * Wählen Sie die Registerkarte **Kibana 4** aus, um mit Kibana 4 zu arbeiten. Die Seite 'Discover' wird geöffnet. Weitere Informationen finden Sie unter [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).
    * Wählen Sie die Registerkarte **Kibana 3** aus, um mit Kibana 3 zu arbeiten. Das Kibana-Standarddashboard wird geöffnet. Informationen zur Verwendung von Kibana 3 zur Analyse Ihrer Protokolle finden Sie unter [Protokolle in Kibana 3 analysieren (veraltet)](../logging_view_kibana3.html#analyzing_logs_Kibana3). Weitere Informationen zur Anpassung eines Kibana 3-Dashboards finden Sie [in diesem Blogbeitrag ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/). 
     
        **Hinweis:** Kibana 3 ist veraltet.

    Wenn die Seite 'Discover' keine Protokolleinträge anzeigt, passen Sie das Zeitauswahlfeld an. Weitere Informationen finden Sie unter [Zeitfilter festlegen](logging_kibana_set_time_filter.html#set_time_filter).


