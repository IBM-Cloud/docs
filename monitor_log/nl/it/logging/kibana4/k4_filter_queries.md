---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtro dei log definendo le query di ricerca personalizzate
{:#k4_filter_queries}

Nella barra di ricerca della pagina Rileva, puoi definire e salvare le query di ricerca utilizzando il linguaggio di query Lucene. Per ogni ricerca, puoi applicare i filtri per restringere le voci disponibili per l'analisi.
{:shortdesc}

Completa le seguenti attività per filtrare i tuoi log utilizzando una ricerca personalizzata:

1. Accedi alla scheda **Log** della tua applicazione o contenitore Cloud Foundry (CF). 

    1. Fai clic sul nome dell'applicazione o sul contenitore nel dashboard {{site.data.keyword.Bluemix}}.
    2. Per le applicazioni CF, fai clic sulla scheda **Log**. Per i contenitori, fai clic su **Monitoraggio e log** e seleziona quindi la scheda **Registrazione**.
    
    Vengono visualizzati i log.

2. Accedi a Kibana. Fai clic su **Vista avanzata** ![Link Vista avanzata](images/logging_advanced_view.jpg). Viene visualizzato il dashboard Kibana.

    Quando accedi a Kibana, viene applicata la ricerca predefinita. Puoi visualizzare i log per l'elenco di istanze delle risorse per cui hai avviato Kibana. Puoi filtrare i log per ognuna delle risorse {{site.data.keyword.Bluemix_notm}} in tale spazio.

Anziché "keyword", il termine corretto in Lucene è "term".

3. Guarda nella pagina Rileva per visualizzare quale sottorete dei tuoi dati viene visualizzata. Per ulteriori informazioni, consulta [Identificazione dei dati visualizzati nella tua pagina Rileva Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data). Quindi, modifica la query predefinita per filtrare le voci.

    **Nota:** utilizza il linguaggio di query Lucene per definire la tua query personalizzata. Per ulteriori informazioni, consulta [Apache Lucene - Query Parser Syntax  ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html){: new_window}
    
    Quando viene avviato Kibana da {{site.data.keyword.Bluemix_notm}}, per modificare la query e per definire più criteri di ricerca, puoi utilizzare i termini logici **AND** e **OR**. Questi operatori devono essere maiuscoli.    
    
    * Per cercare una parola chiave, o parte di una parola chiave, immetti una parola seguita da un simbolo jolly \*, ad esempio `Java*`. 
    * Per cercare una frase particolare, immetti tale frase tra virgolette doppie, ad esempio `"Java/1.8.0"`.
    * Per creare ricerche più complesse, puoi utilizzare i termini logici AND e OR, ad esempio `"Java/1.8.0" OR "Java/1.7.0"`.
    * Per cercare un valore all'interno di un determinato campo, immetti la ricerca nel seguente formato: *log_field_name:search_term*; ad esempio, `instance_id:"1"`.
    * Per cercare un intervallo di valori per un determinato campo di log, immetti la ricerca nel seguente formato: *log_field_name:[start_of_range TO end_of_range]*, ad esempio, `instance_id:["1" TO "2"]`.

     Ad esempio, per un'applicazione CF, puoi creare una query `application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:["0" TO "1"]` che elenca solo le voci per le istanze *0* e *1*. 

4. Salva la query in modo da poterla riutilizzare successivamente. Per ulteriori informazioni, vedi [Salvataggio di una ricerca](logging_kibana_filtering_logs.html#k4_save_search). 

**Nota:** se hai bisogno di eliminare una query, consulta [Eliminazione di una ricerca](logging_kibana_filtering_logs.html#k4_delete_search).



