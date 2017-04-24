---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Kibana-Dashboard über das Bluemix-Dashboard aufrufen
{: #launch_Kibana_from_bluemix}

Sie können Kibana über die {{site.data.keyword.Bluemix}}-Benutzerschnittstelle (UI) starten, um die bestimmten Protokolle einer Cloud Foundry-Anwendung oder eines Docker-Containers anzuzeigen.
{:shortdesc}

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

Weitere Informationen zu Kibana finden Sie in der Veröffentlichung [Kibana User Guide ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.

