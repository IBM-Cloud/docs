---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Aggiunta di un filtro a un valore non elencato nell'*Elenco campi*
{:#k4_add_filter_out_value}

Per aggiungere un filtro a un valore non visualizzato nell'*Elenco campi*, ricerca i record che includono tale valore tramite una query. Poi. aggiungi il filtro dalla voce della tabella disponibile nella pagina Rileva.
{:shortdesc}

Completa la seguente procedura per aggiungere un filtro al valore che non è disponibile nell'elenco visualizzato nella sezione *Elenco campi*:

1. Guarda nella pagina Rileva Kibana per visualizzare quale sottorete dei tuoi dati viene visualizzata. Per ulteriori informazioni, consulta [Identificazione dei dati visualizzati nella tua pagina Rileva Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).

    Ad esempio, la seguente figura mostra i valori delle istanze di un'applicazione CF nell'*Elenco campi*. 
    
    ![Mostra valori in Elenco campi](images/k4_add_filter_f1.jpg "Mostra valori in Elenco campi")
    
    Ti interessa il numero di istanza *3*, ma non è disponibile nell'elenco che puoi visualizzare.

2. Nella pagina Rileva, modifica la query per ricercare un valore di campo specifico.

    Ad esempio, per ricerca l'istanza *3*, la query che immetti è la seguente:
   `application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:"3"`
    
    ![Modifica query](images/k4_add_filter_f2.jpg "Modifica query")
    
    Nella tabella, puoi visualizzare tutti i record che corrispondono alla tua query. 
    
 3. Espandi un record e seleziona il pulsante della lente di ingrandimento ![Pulsante della lente di ingrandimento nella modalità inclusiva](images/k4_include_field_icon.jpg "Pulsante della lente di ingrandimento nella modalità inclusiva") per aggiungere un filtro.
 
     Ad esempio, per aggiungere un filtro all'ID dell'istanza con valore *3*, fai clic sul pulsante della lente di ingrandimento ![Pulsante della lente di ingrandimento nella modalità inclusiva](images/k4_include_field_icon.jpg "Pulsante della lente di ingrandimento nella modalità inclusiva") dal campo *ID_istanza*.
     
     ![Mostra tabella](images/k4_add_filter_f3.jpg "Mostra tabella")
     
4. Controlla che il filtro sia stato aggiunto.

    Ad esempio, la seguente figura mostra il filtro abilitato dopo che l'hai aggiunto dalla tabella. 
    
    ![Mostra filtro](images/k4_add_filter_f4.jpg "Mostra filtro")
    
    
