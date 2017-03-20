---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Filtraggio dei log dell'applicazione Cloud Foundry in base all'ora in Kibana
<!-- for example, Uploading your data -->
{: #logging_kibana_time_filter}


Visualizza e filtra i log dell'applicazione {{site.data.keyword.Bluemix_notm}} in base all'ora sul dashboard Kibana. Puoi accedere al dashboard Kibana dalla scheda **Log** della tua applicazione Cloud Foundry.
{:shortdesc}

Completa le seguenti attività per visualizzare e filtrare i log della tua applicazione Cloud Foundry in base all'ora nel dashboard Kibana:

1. Accedi alla scheda **Log** della tua applicazione Cloud Foundry. 

    1. Fai clic sul nome dell'applicazione nel dashboard delle **Applicazioni** {{site.data.keyword.Bluemix_notm}}.
    2. Fai clic sulla scheda **Log**. 
    
    Vengono visualizzati i log della tua applicazione.

2. Accedi al dashboard Kibana per la tua applicazione. Fai clic su **Vista avanzata** ![link Vista avanzata](images/logging_advanced_view.jpg). Viene visualizzato il dashboard Kibana.


3. Nel dashboard Kibana, fai clic sull'icona **Filtro temporale**; ![Filtro temporale Kibana](images/logging_kibana_time_filter.jpg) e seleziona **Personalizzato** dal menu a discesa. Viene visualizzata la seguente finestra:

    ![Filtro temporale personalizzato sul dashboard Kibana](images/logging_custom_time_filter.jpg)

4. Fai clic sui campi **Da** e **A** per modificare l'ora di inizio e di fine per il tuo filtro. 
    
    Per includere i log fino al momento attuale, fai clic sul link **adesso**.
    Quando hai finito di selezionare l'intervallo di tempo desiderato, fai clic su **Applica**. 

Il dashboard Kibana visualizza ora gli eventi registrati in base al tuo filtro temporale personalizzato.
