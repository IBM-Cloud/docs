---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Filtraggio dei log dell'applicazione Cloud Foundry per tipo di log in Kibana
<!-- for example, Uploading your data -->
{: #logging_kibana_component_filter}
<!-- Provide an appropriate ID above -->

Visualizza e filtra i log dell'applicazione {{site.data.keyword.Bluemix_notm}} in base al componente (tipo di log) sul dashboard Kibana. Puoi accedere al dashboard Kibana dalla scheda **Log** della tua applicazione Cloud Foundry. 
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
Completa le seguenti attività per visualizzare e filtrare i log della tua applicazione Cloud Foundry per tipo di log nel dashboard Kibana:

1. Accedi alla scheda **Log** della tua applicazione Cloud Foundry. 

    1. Fai clic sul nome dell'applicazione nel dashboard delle **Applicazioni** {{site.data.keyword.Bluemix_notm}}.
    2. Fai clic sulla scheda **Log**. 
    
    Vengono visualizzati i log della tua applicazione.

2. Accedi al dashboard Kibana per la tua applicazione. Fai clic su **Vista avanzata** ![link Vista avanzata](images/logging_advanced_view.jpg). Viene visualizzato il dashboard Kibana.

3. Nella finestra **TUTTI GLI EVENTI**, fai clic sull'icona Freccia destra per visualizzare tutti i campi. 

    ![Finestra Tutti gli eventi con l'icona Freccia destra](images/logging_all_events_no_fields.jpg)

4. Nel riquadro **Campi**, seleziona **source_id** per visualizzare il componente che ha generato ogni voce di log nella finestra **TUTTI GLI EVENTI**.

    ![Finestra Tutti gli eventi con il campo source_id selezionato](images/logging_component.png)

5. Nella finestra **TUTTI GLI EVENTI**, fai clic su una riga di evento di log per visualizzare i dettagli di tale evento. Scegli un evento che visualizzi il source_id che desideri filtrare.

    ![Finestra Tutti gli eventi che visualizza i dettagli di un evento di log selezionato](images/logging_component_add_filter.png)

6. Aggiungi un filtro per includere o escludere informazioni per un componente (tipo di log). 

    * Per aggiungere un filtro che includa un valore del componente, fai clic sull'icona **Lente di ingrandimento** ![icona Lente di ingrandimento](images/logging_magnifying_glass.jpg) nella riga source_id della tabella. 

        ![Condizione di filtro per il campo source_id](images/logging_component_filter.png) 

    * Per aggiungere un filtro che escluda un valore del componente, fai clic sull'icona **Esclusione** ![icona Esclusione](images/logging_exclusion_icon.png) nella riga source_id della tabella. 
    
         ![Condizione di filtro per escludere il campo source_id](images/logging_component_add_exclusion_filter.png) 
     
     Viene aggiunta una nuova condizione di filtro al dashboard Kibana.

7. Facoltativamente, puoi ripetere il passo precedente e aggiungere filtri per ogni componente. Per visualizzare l'elenco completo dei componenti, vedi [Formato del log](../logging_view_kibana3.html#kibana_log_format_cf).

    La seguente immagine mostra il dashboard con più filtri per i diversi componenti:
    
    ![Più condizioni di filtro per il campo source_id](images/logging_component_multiple_filters.png)

8. Salva il dashboard. 

    Una volta terminato di aggiungere i filtri e personalizzare il dashboard, fai clic sull'icona **Salva** ![icona Salva](images/logging_save.jpg) e immetti un nome per il tuo dashboard. 
      
    **Nota:** un dashboard con un nome che contiene spazi vuoti non verrà salvato. Immetti un nome senza spazi e fai clic sull'icona **Salva**.
    
    ![Salva nome del dashboard](images/logging_save_dashboard.jpg)

Hai creato un dashboard che filtra le voci di log per componente (tipo di log). Puoi caricare in qualsiasi momento il tuo dashboard salvato facendo clic sull'icona **Cartella** ![icona Cartella](images/logging_folder.jpg) e selezionando il tuo dashboard per nome.


