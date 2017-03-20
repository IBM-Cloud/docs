---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-16"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Filtraggio dei log dell'applicazione Cloud Foundry per tipo di messaggio in Kibana
<!-- for example, Uploading your data -->
{: #logging_kibana_message_type_filter}
<!-- Provide an appropriate ID above -->

Visualizza e filtra i log dell'applicazione {{site.data.keyword.Bluemix_notm}} in base al tipo di messaggio sul dashboard Kibana. Puoi accedere al dashboard Kibana dalla scheda **Log** della tua applicazione Cloud Foundry.
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
Completa le seguenti attività per visualizzare e filtrare i log della tua applicazione Cloud Foundry per tipo di messaggio nel dashboard Kibana:

1. Accedi alla scheda **Log** della tua applicazione Cloud Foundry. 

    1. Fai clic sul nome dell'applicazione nel dashboard delle **Applicazioni** {{site.data.keyword.Bluemix_notm}}.
    2. Fai clic sulla scheda **Log**. 
    
    Vengono visualizzati i log della tua applicazione.

2. Accedi al dashboard Kibana per la tua applicazione. Fai clic su **Vista avanzata** ![link Vista avanzata](images/logging_advanced_view.jpg). Viene visualizzato il dashboard Kibana.

3. Nella finestra **TUTTI GLI EVENTI**, fai clic sull'icona Freccia destra per visualizzare tutti i campi. 

    ![Finestra Tutti gli eventi con l'icona Freccia destra](images/logging_all_events_no_fields.jpg)

4. Nel riquadro **Campi**, seleziona **message_type** per visualizzare il componente che ha generato ogni voce di log nella finestra **TUTTI GLI EVENTI**.

    ![Finestra Tutti gli eventi con il campo message_type selezionato](images/logging_message_type.png)

5. Nella finestra **TUTTI GLI EVENTI**, fai clic su una riga di evento di log per visualizzare i dettagli di tale evento. Scegli un evento che visualizzi il **message_type** che desideri filtrare.

    ![Finestra Tutti gli eventi che visualizza i dettagli di un evento di log selezionato](images/logging_message_type_add_filter.png)

6. Aggiungi un filtro per includere o escludere informazioni su un tipo di messaggio. 

    * Per aggiungere un filtro che includa informazioni relative a un tipo di messaggio, fai clic sull'icona **Lente di ingrandimento** ![icona Lente di ingrandimento](images/logging_magnifying_glass.jpg) nella riga message_type della tabella. 
    
           ![Condizione di filtro per il campo message_type](images/logging_message_type_filter.png)
    
    * Per aggiungere un filtro che escluda informazioni relative a un tipo di messaggio, fai clic sull'icona **Esclusione** ![icona Esclusione](images/logging_exclusion_icon.png) nella riga message_type della tabella. 
    
    Viene aggiunta una nuova condizione di filtro al dashboard Kibana.

7. Facoltativamente, ripeti il passo precedente per aggiungere un filtro per altri tipi di messaggio. Per visualizzare l'elenco completo dei tipi di messaggio, vedi [Formato del log](../logging_view_kibana3.html#kibana_log_format_cf).

9. Salva il dashboard.    
        
    Una volta terminato di creare i filtri, fai clic sull'icona **Salva** ![icona Salva](images/logging_save.jpg) e immetti un nome per il tuo dashboard. 
      
    **Nota:** un dashboard con un nome che contiene spazi vuoti non verrà salvato. Immetti un nome senza spazi e fai clic sull'icona **Salva**.
    
    ![Salva nome del dashboard](images/logging_save_dashboard.jpg).

Hai creato un dashboard che filtra le voci di log per tipo di messaggio. Puoi caricare in qualsiasi momento il tuo dashboard salvato facendo clic sull'icona **Cartella** ![icona Cartella](images/logging_folder.jpg) e selezionando il tuo dashboard per nome.
