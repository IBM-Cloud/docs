---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Filtraggio dei log dell'applicazione Cloud Foundry con le query in Kibana
{: #logging_kibana_query}

Utilizza Kibana per creare delle query con cui cercare termini chiave nei log e filtrare in base a tali termini. Con Kibana, puoi confrontare visivamente le query sul dashboard. Puoi accedere al dashboard Kibana dalla scheda **Log** della tua applicazione Cloud Foundry. 
{:shortdesc}

Completa le seguenti attività per creare una query per i log della tua applicazione Cloud Foundry nel dashboard Kibana:

1. Accedi alla scheda **Log** della tua applicazione Cloud Foundry. 

    1. Fai clic sul nome dell'applicazione nel dashboard delle **Applicazioni** {{site.data.keyword.Bluemix_notm}}.
    2. Fai clic sulla scheda **Log**. 
    
    Vengono visualizzati i log della tua applicazione.

2. Accedi al dashboard Kibana per la tua applicazione. Fai clic su **Vista avanzata** ![link Vista avanzata](images/logging_advanced_view.jpg "Advanced view link"). Viene visualizzato il dashboard Kibana.

3. Nel dashboard Kibana, fai clic su **QUERY** ![icona Query](images/logging_query.jpg "Query icon") per visualizzare il campo. Quando accedi in Kibana per visualizzare i log della tua applicazione dalla scheda **Log**, viene creata una query per mostrare tutti i log per l'application_id della tua applicazione.
	
    Per modificare la tua query, fai clic sul campo **QUERY** e immetti un termine di ricerca.

    * Per cercare una parola chiave, o parte di una parola chiave, immetti una parola seguita da un simbolo jolly \*, ad esempio `Java*`. 
	* Per cercare una frase particolare, immetti tale frase tra virgolette doppie, ad esempio `"Java/1.8.0"`.
	* Per creare ricerche più complesse, puoi utilizzare i termini logici AND e OR, ad esempio `"Java/1.8.0" OR "Java/1.7.0"`.
	* Per cercare un valore all'interno di un determinato campo, immetti la ricerca nel seguente formato: *log_field_name:search_term*; ad esempio `instance_id:1`.
	* Per cercare un intervallo di valori per un determinato campo di log, immetti la ricerca nel seguente formato: *log_field_name:[start_of_range TO end_of_range]*, ad esempio `instance_id:[1 TO 2]`.

4. Se vuoi confrontare i risultati di due query separate, puoi aggiungere un altro termine di query al tuo dashboard. Per aggiungere un'altra query, fai clic sull'icona **+** alla fine del campo **QUERY**.

    ![Campo Query](images/logging_query_field.jpg "Query field")
	
    Viene visualizzato un nuovo campo **QUERY** che contiene il carattere jolly \*. Questa query indica a Kibana di includere tutte le voci.
	
    ![Campo query aggiuntivo](images/logging_additional_query_field.jpg "Additional Query field")
	
    Il dashboard viene aggiornato con i risultati della tua nuova query. Il riquadro **EVENTI PER ORA** visualizza una rappresentazione grafica per entrambe le query, insieme al numero di termini per ciascuna query tra parentesi. 
	
    ![Dashboard che visualizza un grafico per entrambe le query](images/logging_dashboard_queries.jpg "Dashboard displaying graph for both queries")
	
5. Fai clic sul nuovo campo **QUERY** per modificarne il contenuto e aggiungere una condizione di query, ad esempio `instance_id:1`. Utilizza il riquadro **EVENTI PER ORA** per confrontare i risultati delle tue query.

    ![Dashboard che visualizza un grafico per entrambe le query](images/logging_dashboard_queries2.jpg "Dashboard displaying graph for both queries")

6. Per eliminare una query, sposta il mouse sul campo **QUERY** che vuoi eliminare per visualizzare l'icona **Elimina**. Fai clic sull'icona **Elimina**.

    ![Campo Query con l'icona Elimina](images/logging_delete_query.jpg "Query field with delete icon")

7. Per salvare questo dashboard con un nome riconoscibile, fai clic sull'icona **Salva** ![icona Salva](images/logging_save.jpg "Save icon") e immetti un nome per il tuo dashboard. 

    **Nota:** un dashboard con un nome che contiene spazi vuoti non verrà salvato. Immetti un nome senza spazi e fai clic sull'icona **Salva**.

    ![Salva nome del dashboard ](images/logging_save_dashboard.jpg "Save dashboard name")


