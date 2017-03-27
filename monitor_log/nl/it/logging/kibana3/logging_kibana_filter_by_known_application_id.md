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


# Filtraggio dei log dell'applicazione Cloud Foundry per ID applicazione noto in Kibana
<!-- for example, Uploading your data -->
{: #logging_kibana_known_application_id}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

Se conosci l'ID della tua applicazione Cloud Foundry, puoi visualizzare e filtrare rapidamente i log in base all'ID applicazione (application_id) nel dashboard Kibana. Puoi accedere al dashboard Kibana dalla scheda **Log** della tua applicazione Cloud Foundry. 
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
Completa le seguenti attività per visualizzare e filtrare i log della tua applicazione Cloud Foundry per ID applicazione noto nel dashboard Kibana:

1. Accedi alla scheda **Log** della tua applicazione Cloud Foundry. 

    1. Fai clic sul nome dell'applicazione nel dashboard delle **Applicazioni** {{site.data.keyword.Bluemix_notm}}.
    2. Fai clic sulla scheda **Log**. 
    
    Vengono visualizzati i log della tua applicazione.

2. Accedi al dashboard Kibana per la tua applicazione. Fai clic su **Vista avanzata** ![link Vista avanzata](images/logging_advanced_view.jpg). Viene visualizzato il dashboard Kibana.

3. Nel dashboard Kibana, fai clic sull'icona **Cartella** ![icona Cartella](images/logging_folder.jpg) per visualizzare un menu che elenca tutti i dashboard recenti. 

    **Nota:** oltre ai dashboard che hai salvato per nome, il menu elenca i dashboard senza nome in base al seguente formato: *ALCH_TENANT_ID_application_id*. 

    ![Elenco di dashboard](images/logging_list_of_dashboards.jpg)

4. Seleziona il dashboard con un nome contenente il tuo application_id noto. 

    Il dashboard viene caricato e visualizza le informazioni filtrate per il tuo application_id.

5. Facoltativamente, puoi aggiungere altri campi alla tua sezione di filtro, ad esempio **instance_id** per abilitare o disabilitare il filtro di record per ID istanza. 
  
    1. Nella finestra **TUTTI GLI EVENTI**, fai clic su una riga di evento di log per visualizzare i dettagli di tale evento. 
	
        ![Finestra Tutti gli eventi che visualizza i dettagli di un evento di log selezionato](images/logging_selected_log_event.jpg)
	
    2. Scegli un evento che visualizzi il valore di campo che desideri filtrare.
	
    3. Aggiungi un filtro.
    
        Per aggiungere un filtro che includa informazioni su quello specifico valore di campo, fai clic sull'icona **Lente di ingrandimento** ![icona Lente di ingrandimento](images/logging_magnifying_glass.jpg) nella riga della tabella che contiene il campo che vuoi filtrare. 
	
        Per aggiungere un filtro che escluda informazioni su quello specifico valore di campo, fai clic sull'icona **Esclusione** ![icona Esclusione](images/logging_exclusion_icon.png) nella riga della tabella che contiene il campo che vuoi filtrare.  

        Viene aggiunta una nuova condizione di filtro al dashboard Kibana.
	
	    ![Condizione di filtro per il campo instance_id](images/logging_instance_id_filter.jpg)
	
6. Salva questo dashboard con un nome riconoscibile. 

    Fai clic sull'icona **Salva** ![icona Salva](images/logging_save.jpg) e immetti un nome per il tuo dashboard. 

    **Nota:** un dashboard con un nome che contiene spazi vuoti non verrà salvato. Immetti un nome senza spazi e fai clic sull'icona **Salva**.

    ![Salva nome del dashboard](images/logging_save_dashboard.jpg).


Hai creato un dashboard che filtra le voci di log per ID applicazione e ID istanza. Puoi caricare in qualsiasi momento il tuo dashboard salvato facendo clic sull'icona **Cartella** ![icona Cartella](images/logging_folder.jpg) e selezionando il tuo dashboard per nome.
