---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Protokolle für Cloud Foundry-Apps nach Zeit in Kibana filtern
<!-- for example, Uploading your data -->
{: #logging_kibana_time_filter}


Sie können Protokolle für {{site.data.keyword.Bluemix_notm}}-Anwendungen nach Zeit im Kibana-Dashboard anzeigen und filtern. Sie können über die Registerkarte **Protokolle** für Ihre Cloud Foundry-App auf das Kibana-Dashboard zugreifen.
{:shortdesc}

Führen Sie die folgenden Tasks aus, um Ihre Cloud Foundry-App-Protokolle nach Zeit im Kibana-Dashboard anzuzeigen und zu filtern:

1. Greifen Sie auf die Registerkarte **Protokolle** Ihrer Cloud Foundry-App zu. 

    1. Klicken Sie auf den App-Namen im {{site.data.keyword.Bluemix_notm}}-Dashboard **Apps**.
    2. Klicken Sie auf die Registerkarte **Protokolle**. 
    
    Die Protokolle für Ihre App werden angezeigt.

2. Greifen Sie auf das Kibana-Dashboard für Ihre App zu. Klicken Sie auf **Erweiterte Ansicht** ![Link für erweiterte Ansicht](images/logging_advanced_view.jpg). Das Kibana-Dashboard wird angezeigt.


3. Klicken Sie im Kibana-Dashboard auf den **Zeitfilter** ![Kibana-Zeitfilter](images/logging_kibana_time_filter.jpg) und wählen Sie anschließend die Option **Custom** im Dropdown-Menü aus. Das folgende Fenster wird angezeigt:

    ![Angepasster Zeitfilter im Kibana-Dashboard](images/logging_custom_time_filter.jpg)

4. Klicken Sie auf Felder **From** und **To**, um die Anfangszeit und die Endzeit für Ihren Filter zu bearbeiten. 
    
    Zum Einschließen von Protokollen bis zum gegenwärtigen Augenblick, klicken Sie auf den Link **now**.
    Wenn der Zeitbereich Ihren Vorstellungen entspricht, klicken Sie auf **Apply**. 

Das Kibana-Dashboard zeigt jetzt protokollierte Ereignisse für Ihren angepassten Zeitfilter an.
