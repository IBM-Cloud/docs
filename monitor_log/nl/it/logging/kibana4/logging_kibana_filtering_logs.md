---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtro dei log in Kibana
{:#kibana_filtering_logs}

Nella pagina Rileva, puoi creare le query di ricerca e applicare i filtri per vincolare le informazioni visualizzate per l'analisi.
{:shortdesc}

* Puoi definire una o più query di ricerca nella barra di ricerca della pagina Rileva. Una query di ricerca definisce un sottoinsieme di voci di log. Utilizza il linguaggio di query Lucene per definire la query di ricerca. 

* Puoi aggiungere filtri dall'*Elenco campi* o dalle voci della tabella. Un filtro ridefinisce la selezione dei dati includendo o escludendo informazioni. Puoi abilitare o disabilitare un filtro, invertire l'azione di filtro, attivare/disattivare il filtro o rimuoverlo completamente. 

Dopo aver definito una nuova ricerca, salvala in modo da poterla riutilizzare per analisi future nella pagina Rileva o per creare le visualizzazioni che puoi utilizzare nei dashboard personalizzati. Per ulteriori informazioni, vedi [Salvataggio di una ricerca](logging_kibana_filtering_logs.html#k4_save_search).

Quando esegui una nuova ricerca, l'istogramma, la tabella e l'elenco dei campi vengono automaticamente aggiornati per visualizzare i risultati della ricerca. Per scoprire quali dati vengono visualizzati, consulta [Identificazione dei dati visualizzati nella pagina Rileva](k4_identify_data.html#k4_identify_data).

Il seguente elenco mostra gli scenari su come filtrare i dati nei tuoi log:

* Puoi creare delle ricerche personalizzate per filtrare i tuoi log. Per ulteriori informazioni, vedi [Filtro dei log definendo query personalizzate](k4_filter_queries.html#k4_filter_queries).

* Puoi eseguire la ricerca nel tuo log per le voci che includono un testo specifico nel valore di un campo. Per ulteriori informazioni, consulta [Filtro dei tuoi log per un testo specifico in un valore del campo](k4_filter_logs_spec_text.html#k4_filter_logs_spec_text).
 
* Puoi eseguire la ricerca nel tuo log per un valore del campo specifico o escludere voci dal log per un valore del campo specifico. Per ulteriori informazioni, consulta [Filtro dei tuoi log per un valore del campo specifico](k4_filter_logs_spec_field.html#k4_filter_logs_spec_field).

    * Puoi filtrare i log per tipo di log. Per ulteriori informazioni, vedi [Filtro dei tuoi log per tipo di log](k4_filter_logs_by_log_type.html#k4_filter_logs_by_log_type).
    * Puoi filtrare la tua applicazione CF per origine. Per ulteriori informazioni, consulta [Filtro dei tuoi log dell'applicazione CF per origine](k4_filter_logs_by_source.html#k4_filter_logs_by_source).
    * Puoi filtrare i log per ID istanza. Per ulteriori informazioni, vedi [Filtro dei tuoi log per ID istanza](k4_filter_logs_by_instance_id.html#k4_filter_logs_by_instance_id).   
    * Puoi filtrare i log per tipo di messaggio. Per ulteriori informazioni, vedi [Filtro dei tuoi log per ID tipo messaggio](k4_filter_cf_logs_by_msg_type.html#k4_filter_cf_logs_by_msg_type).  
 
* Puoi filtrare i tuoi log per visualizzare le voci in un periodo di tempo. Per ulteriori informazioni, consulta [Configurazione di un filtro temporale](logging_kibana_set_time_filter.html#set_time_filter).
     

## Avvio di una nuova ricerca
{: #k4_new_search}

Per avviare una nuova ricerca, fai clic sul pulsante **Nuova ricerca** ![Nuova ricerca](images/k4_new_search_icon.jpg "Nuova ricerca") nella barra degli strumenti della pagina Rileva.

## Salvataggio di una ricerca 
{: #k4_save_search}

Quando salvi una ricerca, la stringa della query di ricerca e il modello di indice selezionato correntemente, vengono salvati.

Completa la seguente procedura per salvare la ricerca corrente nella pagina Rileva: 

1. Nella barra degli strumenti della pagina Rileva, fai clic sul pulsante **Salva ricerca** ![Salva ricerca](images/k4_save_search_icon.jpg "Salva ricerca").

2. Immetti un nome per la ricerca.

3. Fai clic su Salva. 

## Eliminazione di una ricerca
{: #k4_delete_search}

Per eliminare una ricerca, completa la seguente procedura nella pagina Impostazioni: 

1. Nella pagina Impostazioni, seleziona la scheda **Oggetti**.

2. Nella scheda **Ricerche**, seleziona la ricerca che desideri eliminare. 

3. Fai clic su **Elimina**.


## Esportazione di una ricerca
{: #k4_export_search}

Per esportare una ricerca, completa la seguente procedura nella pagina Impostazioni: 

1. Nella pagina Impostazioni, seleziona la scheda **Oggetti**.

2. Nella scheda **Ricerche**, seleziona la ricerca che desideri esportare. 

3. Fai clic su **Esporta**.

4. Salva il file.

## Importazione di una ricerca
{: #k4_import_search}

Per importare una ricerca, completa la seguente procedura nella pagina Impostazioni: 

1. Nella pagina Impostazioni, seleziona la scheda **Oggetti**.

2. Nella scheda **Ricerche**, seleziona **Importa**. 

3. Seleziona un file e fai clic su **Apri**.

La ricerca viene aggiunta all'elenco delle ricerche.


## Ricaricamento di una ricerca 
{: #k4_reload_search}

Completa la seguente procedura per caricare una ricerca salvata: 

1. Nella barra degli strumenti della pagina Rileva, fai clic sul pulsante **Carica ricerca** ![Carica ricerca](images/k4_load_icon.jpg "Carica ricerca").

2. Seleziona la ricerca che desideri caricare.  


## Aggiornamento del contenuto di una ricerca 
{: #k4_refresh_search}

Per aggiornare manualmente il contenuto di una ricerca, puoi fare clic sulla lente di ingrandimento disponibile nella barra di ricerca. 

Per aggiornare automaticamente i dati visualizzati nella pagina Rileva, puoi configurare un intervallo di aggiornamento. Il valore corrente dell'intervallo di aggiornamento viene visualizzato nella barra del menu nella pagine Rileva. Per impostazione predefinita, l'aggiornamento automatico è impostato su **DISATTIVO**.

Completa la seguente procedura per impostare un intervallo di aggiornamento: 

1. Nella pagina Rileva, fai clic sul **Filtro temporale** disponibile nella barra del menu.

2. Fai clic su **Aggiornamento automatico** ![Aggiornamento automatico](images/k4_auto_refresh_icon.jpg "Aggiornamento automatico").

3. Scegli un intervallo di aggiornamento dall'elenco. 

    ![Opzioni intervallo di aggiornamento](images/k4_change_autorefresh.jpg "Opzioni intervallo di aggiornamento")


**Nota**: dopo aver abilitato un intervallo di aggiornamento, puoi sospenderlo facendo clic sul pulsante di pausa ![Pausa](images/k4_auto_refresh_pause_icon.jpg "Pausa").




