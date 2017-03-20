---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Filtraggio dei log dell'applicazione Cloud Foundry per ID istanza in Kibana
<!-- for example, Uploading your data -->
{: #logging_kibana_instance_id}
<!-- Provide an appropriate ID above -->

Visualizza e filtra i log dell'istanza {{site.data.keyword.Bluemix_notm}} per ID istanza (instance_id) della tua applicazione nel dashboard Kibana. Puoi accedere al dashboard Kibana dalla scheda **Log** della tua applicazione Cloud Foundry.
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
Completa le seguenti attività per visualizzare e filtrare i log della tua applicazione Cloud Foundry per instance_id nel dashboard Kibana:

1. Accedi alla scheda **Log** della tua applicazione Cloud Foundry. 

    1. Fai clic sul nome dell'applicazione nel dashboard delle **Applicazioni** {{site.data.keyword.Bluemix_notm}}.
    2. Fai clic sulla scheda **Log**. 
    
    Vengono visualizzati i log della tua applicazione.

2. Accedi al dashboard Kibana per la tua applicazione. Fai clic su **Vista avanzata** ![link Vista avanzata](images/logging_advanced_view.jpg). Viene visualizzato il dashboard Kibana.

3. Nel dashboard Kibana, fai clic sull'icona **Vai a valore predefinito salvato**  ![icona Vai a valore predefinito salvato](images/logging_default_dash.jpg) per visualizzare tutti i log per un spazio. Nella finestra **TUTTI GLI EVENTI**, fai clic sull'icona Freccia destra per visualizzare tutti i campi. 

    ![Finestra Tutti gli eventi con l'icona Freccia destra](images/logging_all_events_no_fields.jpg)

4. Nel riquadro **Campi**, seleziona **application_id** e **instance_id** per visualizzare i campi  application_id e instance_id nella finestra **TUTTI GLI EVENTI**.

    ![Finestra Tutti gli eventi con i campi application_id e instance_id selezionati](images/logging_all_events_app_instance_select.jpg)

5. Nella finestra **TUTTI GLI EVENTI**, fai clic su una riga di evento di log per visualizzare i dettagli di tale evento. Scegli un evento che visualizzi l'instance_id che desideri filtrare.

    ![Finestra Tutti gli eventi che visualizza i dettagli di un evento di log selezionato](images/logging_selected_log_event.jpg)

6. Aggiungi un filtro per includere o escludere informazioni su un ID applicazione. 

    * Per aggiungere un filtro che includa informazioni relative a uno specifico ID applicazione, fai clic sull'icona **Lente di ingrandimento** ![icona Lente di ingrandimento](images/logging_magnifying_glass.jpg) nella riga application_id della tabella. 
    
           ![Condizione di filtro per il campo application_id](images/logging_application_id_filter.jpg)
    
    * Per aggiungere un filtro che escluda informazioni relative a uno specifico ID applicazione, fai clic sull'icona **Esclusione** ![icona Esclusione](images/logging_exclusion_icon.png) nella riga application_id della tabella. 
    
           ![Condizione di filtro per escludere un ID applicazione](images/logging_application_id_exclude_filter.jpg)
    
    Viene aggiunta una nuova condizione di filtro al dashboard Kibana.
 

7. Aggiungi un filtro per includere o escludere informazioni su un ID istanza dell'applicazione. 

    * Per aggiungere un filtro che includa informazioni relative a uno specifico ID istanza, fai clic sull'icona **Lente di ingrandimento** ![icona Lente di ingrandimento](images/logging_magnifying_glass.jpg) nella riga instance_id della tabella. 

    ![Condizione di filtro per il campo instance_id](images/logging_instance_id_filter.jpg)

     * Per aggiungere un filtro che escluda informazioni relative a uno specifico ID istanza, fai clic sull'icona **Esclusione** ![icona Esclusione](images/logging_exclusion_icon.png) nella riga instance_id della tabella. 
    
           ![Condizione di filtro per escludere un ID istanza](images/logging_application_instance_id_exclude_filter.jpg)
    
    Viene aggiunta una nuova condizione di filtro al dashboard Kibana.

9. Salva il dashboard. Una volta terminato di creare il filtro, fai clic sull'icona **Salva** ![icona Salva](images/logging_save.jpg) e immetti un nome per il tuo dashboard. 

    **Nota:** un dashboard con un nome che contiene spazi vuoti non verrà salvato. Immetti un nome senza spazi e fai clic sull'icona **Salva**.

    ![Salva nome del dashboard](images/logging_save_dashboard.jpg).

Hai creato un dashboard che filtra le voci di log per instance_id. Puoi caricare in qualsiasi momento il tuo dashboard salvato facendo clic sull'icona **Cartella** ![icona Cartella](images/logging_folder.jpg) e selezionando il tuo dashboard per nome. 
