---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtro dei tuoi log dell'applicazione CF per origine 
{:#k4_filter_logs_by_source}

Visualizza e filtra i log dell'applicazione Cloud Foundry per il tipo di origine tramite il dashboard Kibana.
{:shortdesc}

Completa la seguente procedura per ricercare le voci che includono un'origine del log specifica: 

1. Guarda nella pagina Rileva Kibana per visualizzare quale sottorete dei tuoi dati viene visualizzata. Per ulteriori informazioni, consulta [Identificazione dei dati visualizzati nella tua pagina Rileva Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. Nell'*Elenco campo*, seleziona il campo **ID_origine**.

    ![Elenco del filtro che mostra l'ID origine del campo](images/k4_filter_sourceid_F1.jpg "Elenco del filtro che mostra l'ID origine del campo")     

3. Per aggiungere un filtro che ricerca le voci che includono un ID_origine specifico, scegli il pulsante di ingrandimento ![Pulsante della lente di ingrandimento nella modalità inclusiva](images/k4_include_field_icon.jpg "Pulsante della lente di ingrandimento nella modalità inclusiva") per tale valore.

    Per un elenco delle origini del log disponibili per le applicazioni CF, consulta [Origini del log per le applicazioni CF](../logging_cf_apps.html#logging_bluemix_cf_apps_log_sources).

    Ad esempio, per aggiungere un filtro che include le voci di log per l'avvio, l'arresto o l'arresto anomalo di un'applicazione CF, seleziona il pulsante della lente di ingrandimento ![Pulsante della lente di ingrandimento nella modalità inclusiva](images/k4_include_field_icon.jpg "Pulsante della lente di ingrandimento nella modalità  inclusiva") disponibile per il valore *CELL* nella sezione *Elenco campi*. La seguente figura mostra il filtro per il valore ID_origine *CELL* abilitato. 
    
    ![Filtro che include il valore del campo](images/k4_filter_sourceid_F2.jpg "Filtro che include il valore del campo")

    Per aggiungere un filtro che ricerca le voci che non includono un ID_origine specifico, scegli il pulsante di ingrandimento ![Pulsante della lente di ingrandimento nella modalità esclusiva](images/k4_exclude_field_icon.jpg "Pulsante della lente di ingrandimento nella modalità esclusiva") per il valore.
    
    Ad esempio, per aggiungere un filtro che esclude le voci di log per l'avvio, l'arresto o l'arresto anomalo di un'applicazione CF, seleziona il pulsante della lente di ingrandimento ![Pulsante della lente di ingrandimento nella modalità inclusiva](images/k4_exclude_field_icon.jpg "Pulsante della lente di ingrandimento nella modalità  inclusiva") disponibile per il valore *CELL* nella sezione *Elenco campi*. La seguente figura mostra il filtro che esclude le voci per il valore ID_origine*CELL*. 

    ![Filtro che esclude il valore del campo](images/k4_filter_sourceid_F3.jpg "Filtro che esclude il valore del campo")




