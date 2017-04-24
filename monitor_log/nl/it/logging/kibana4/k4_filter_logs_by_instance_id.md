---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtro dei tuoi log per ID istanza
{:#k4_filter_logs_by_instance_id}

Visualizza e filtra i log {{site.data.keyword.Bluemix}} per ID istanza.
{:shortdesc}

Completa le seguenti attività per visualizzare e filtrare i tuoi log per ID istanza nel dashboard Kibana:

1. Guarda nella pagina Rileva Kibana per visualizzare quale sottorete dei tuoi dati viene visualizzata. Per ulteriori informazioni, consulta [Identificazione dei dati visualizzati nella tua pagina Rileva Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. Nell'*Elenco campo*, seleziona uno dei seguenti campi per la ricerca per un ID istanza specifico:

    * **ID_istanza**: questo campo elenca i vari ID istanza disponibili nel log per un'applicazione Cloud Foundry. 
    * **istanza**: questo campo elenca i vari GUID di tutte le istanze per un gruppo di contenitori. 

    Ad esempio, la seguente figura mostra i valori differenti di istanze per un'applicazione CF: 
    
    ![Elenco del filtro che mostra il campo ID_istanza](images/k4_filter_instanceid_f1.jpg "Elenco del filtro che mostra il campo ID_istanza")
   
3. Per aggiungere un filtro che esegue la ricerca per un tipo di log specifico, scegli il pulsante di ingrandimento ![Pulsante della lente di ingrandimento nella modalità inclusiva](images/k4_include_field_icon.jpg "Pulsante della lente di ingrandimento nella modalità inclusiva") per il tipo di log che desideri analizzare.

   Ad esempio, per aggiungere un filtro che include le voci per l'istanza dell'applicazione CF *2*, seleziona il pulsante della lente di ingrandimento ![Pulsante della lente di ingrandimento nella modalità inclusiva](images/k4_include_field_icon.jpg "Pulsante della lente di ingrandimento nella modalità inclusiva") disponibile per il valore *2* nella sezione Elenco campi. La seguente figura mostra il filtro che include le voci per l'istanza *2*.
    
    ![Filtro che include le voci ID_istanza per l'istanza 2](images/k4_filter_instanceid_f2.jpg "Filtro che include le voci ID_istanza per l'istanza 2")

    Per aggiungere un filtro che ricerca le voci che non includono un ID istanza specifico, scegli il pulsante di ingrandimento ![Pulsante della lente di ingrandimento nella modalità esclusiva](images/k4_exclude_field_icon.jpg "Pulsante della lente di ingrandimento nella modalità esclusiva") per il valore.

     Ad esempio, per aggiungere un filtro che esclude le voci per l'istanza dell'applicazione CF *2*, seleziona il pulsante della lente di ingrandimento ![Pulsante della lente di ingrandimento nella modalità esclusiva](images/k4_exclude_field_icon.jpg "Pulsante della lente di ingrandimento nella modalità esclusiva") disponibile per il valore *2* nella sezione Elenco campi. La seguente figura mostra il filtro che esclude le voci per l'istanza *2*.
     
      ![Filtro che esclude le voci ID_istanza per l'istanza 2](images/k4_filter_instanceid_f3.jpg "Filtro che esclude le voci ID_istanza per l'istanza 2")

