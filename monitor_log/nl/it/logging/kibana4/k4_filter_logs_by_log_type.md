---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtro dei tuoi log per tipo di log 
{:#k4_filter_logs_by_log_type}

Visualizza e filtra i log {{site.data.keyword.Bluemix}} per tipo di log.
{:shortdesc}

Completa la seguente procedura per ricercare le voci che includono un tipo di log specifico: 

1. Guarda nella pagina Rileva Kibana per visualizzare quale sottorete dei tuoi dati viene visualizzata. Per ulteriori informazioni, consulta [Identificazione dei dati visualizzati nella tua pagina Rileva Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. Nell'*Elenco campo*, seleziona il campo **tipo**.

    Ad esempio, nella seguente figura, è disponibile solo un tipo di log: *syslog*
    
    ![Elenco del filtro che mostra il tipo di log del campo](images/k4_filter_log_type_F1.jpg "Elenco del filtro che mostra il tipo di log del campo")
   
3. Per aggiungere un filtro che esegue la ricerca per un tipo di log specifico, scegli il pulsante di ingrandimento ![Pulsante della lente di ingrandimento nella modalità inclusiva](images/k4_include_field_icon.jpg "Pulsante della lente di ingrandimento nella modalità inclusiva") per il tipo di log che desideri analizzare.

    Ad esempio, per aggiungere un filtro che include le voci di log per *syslog*, seleziona il pulsante della lente di ingrandimento ![Pulsante della lente di ingrandimento nella modalità inclusiva](images/k4_include_field_icon.jpg "Pulsante della lente di ingrandimento nella modalità inclusiva") disponibile per il valore *syslog* nella sezione *Elenco campi*. La seguente figura mostra il filtro che include le voci per tipo di log *syslog*.

    ![Filtro che include le voci tipo di log per syslog](images/k4_filter_log_type_F2.jpg "Filtro che include le voci tipo di log per syslog")

    Per aggiungere un filtro che ricerca le voci che non includono un tipo di log specifico, scegli il pulsante di ingrandimento![Pulsante della lente di ingrandimento nella modalità esclusiva](images/k4_exclude_field_icon.jpg "Pulsante della lente di ingrandimento nella modalità esclusiva") per il valore.

     Ad esempio, per aggiungere un filtro che esclude le voci di log per *syslog*, seleziona il pulsante della lente di ingrandimento ![Pulsante della lente di ingrandimento nella modalità esclusiva](images/k4_exclude_field_icon.jpg "Pulsante della lente di ingrandimento nella modalità esclusiva") disponibile per il valore *syslog* nella sezione *Elenco campi*. La seguente figura mostra il filtro che esclude le voci per il tipo di log *syslog*.
     
     ![Filtro che esclude le voci tipo di log per syslog](images/k4_filter_log_type_F3.jpg "Filtro che esclude le voci tipo di log per syslog")



