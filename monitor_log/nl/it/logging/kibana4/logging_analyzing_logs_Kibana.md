---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analisi log avanzata con Kibana
{:#analyzing_logs_Kibana}

In {{site.data.keyword.Bluemix}}, puoi utilizzare Kibana, una piattaforma di analisi e visualizzazione open source, per monitorare, ricercare, analizzare e visualizzare i tuoi dati in una varietà di grafici, ad esempio, diagrammi e tabelle. Utilizza Kibana per eseguire attività di analisi avanzate.
{:shortdesc}

Puoi avviare Kibana in uno dei seguenti modi:

* Da {{site.data.keyword.Bluemix_notm}}

    Puoi avviare i log della tua specifica applicazione CF in Kibana, nel contesto di quella specifica applicazione. 
    
    Puoi avviare i log del tuo specifico contenitore Docker in Kibana, nel contesto di quello specifico contenitore.  
    
    Per le applicazioni CF, la query che viene utilizzata per filtrare i dati disponibili per l'analisi in Kibana richiama le voci di log per l'applicazione Cloud Foundry. Le informazioni di log visualizzate da Kibana per impostazione predefinita sono tutte correlate a un'unica applicazione Cloud Foundry e a tutte le sue istanze. 
    
    Per i contenitori, la query che viene utilizzata per filtrare i dati disponibili per l'analisi in Kibana richiama le voci di log per tutte le istanze del contenitore. Le informazioni di log visualizzate da Kibana per impostazione predefinita sono tutte correlate a un solo contenitore o a un gruppo di contenitori e a tutte le relative istanze.  
    
    Per ulteriori informazioni, vedi [Accesso al dashboard Kibana dal dashboard Bluemix](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix).

* Da un link diretto del browser

    Potresti voler avviare Kibana in modo che i dati che visualizzi aggreghino i log dai servizi all'interno di uno spazio {{site.data.keyword.Bluemix_notm}} fornito.
    
    La query che viene utilizzata per filtrare i dati visualizzati nel dashboard richiama le voci di log per uno spazio nell'organizzazione {{site.data.keyword.Bluemix_notm}}. Le informazioni di log visualizzate da Kibana includono i record per tutte le risorse che vengono distribuite all'interno dello spazio dell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui sei connesso. 
    
    Per ulteriori informazioni, vedi [Accesso al dashboard Kibana da un browser web](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser).
    
    Quando avvii Kibana da un browser, puoi scegliere di utilizzare Kibana 4 o Kibana 3. **Nota:** Kibana 3 è obsoleto. Per ulteriori informazioni sull'utilizzo di Kibana per analizzare i tuoi log, consulta [Analisi dei log in Kibana 3 (Obsoleto)](../logging_view_kibana3.html#analyzing_logs_Kibana3).

<br>    

Kibana è un'interfaccia basata su browser in cui puoi analizzare i dati interattivamente e personalizzare i dashboard che potrai quindi utilizzare per analizzare i dati di log ed eseguire attività di gestione avanzate.  

I dati visualizzati da una pagina Kibana sono vincolati da una ricerca. La serie di dati predefinita è definita dal modello di indice preconfigurato. Per filtrare le informazioni, puoi aggiungere nuove query di ricerca e applicare i filtri alla serie di dati predefinita. Puoi quindi salvare la ricerca per riutilizzi futuri.  

Kibana include diverse pagine che puoi utilizzare per analizzare i tuoi log:

| Pagina Kibana | Descrizione |
|-------------|-------------|
| Ricerca | Utilizza questa pagina per definire le ricerche e per analizzare i tuoi log interattivamente tramite una tabella e un istogramma. |
| Visualizza  | Utilizza questa pagina per creare visualizzazioni come grafici e tabelle che puoi utilizzare per analizzare i tuoi dati di log e confrontare i risultati.  |
| Dashboard | Utilizza questa pagina per analizzare i tuoi log tramite le raccolte di ricerche e visualizzazioni salvate.  |

**Nota:** puoi analizzare soltanto 1 giorno completo alla volta tramite le pagine Visualizza o Dashboard, anche se puoi tornare indietro di 7 giorni. I dati di log sono archiviati per 7 giorni per impostazione predefinita. 

| Pagina Kibana | Informazioni periodo di tempo |
|-------------|-------------------------|
| Ricerca | Analizza i dati per un massimo di 7 giorni. |
| Visualizza  | Analizza i dati per un periodo di 24 ore. <br> Puoi filtrare i dati di log per un periodo personalizzato che passi le 24 ore.  |
| Dashboard | Analizza i dati per un periodo di 24 ore. <br> Puoi filtrare i dati di log per un periodo personalizzato che passi le 24 ore.<br> Il selezionatore di tempo che imposti, viene applicato a tutte le visualizzazioni incluse nel dashboard. |


Ad esempio, questo è un modo di utilizzare Kibana per visualizzare le informazioni su un contenitore o un'applicazione CF nel tuo spazio tramite pagine differenti:

* Nella pagina Rileva, puoi definire nuove query di ricerca e applicare i filtri alle query. I dati di log sono visualizzati tramite una tabella e un istogramma. Puoi utilizzare queste visualizzazioni per analizzare i dati interattivamente. Per ulteriori informazioni, vedi [Analisi dei log interattiva in Kibana](logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).

    Puoi configurare i filtri dai campi di log, ad esempio, message_type e instance_ID e impostare un periodo di tempo. Puoi abilitare o disabilitare dinamicamente questi filtri. La tabella e l'istogramma visualizzeranno le voci di log che soddisfano la query e i criteri di filtro da te abilitati. Per ulteriori informazioni, vedi [Filtro dei log in Kibana](logging_kibana_filtering_logs.html#kibana_filtering_logs).
    
* Nella pagina Visualizza, puoi definire nuove visualizzazioni e query di ricerca. 

    Per analizzare i dati, puoi creare visualizzazioni basate su una ricerca esistente o una nuova ricerca. Kibana include diversi tipi di visualizzazioni, come tabella, tendenze e istogramma, che puoi utilizzare per analizzare le informazioni. Ogni visualizzazione ha un obiettivo diverso. Alcune visualizzazioni sono organizzate in righe che forniscono i risultati di una o più query. Altre visualizzazioni mostrano documenti o informazioni personalizzate. I dati in una visualizzazione possono essere corretti o modificati se viene aggiornata una query di ricerca. Puoi incorporare la tua visualizzazione in una pagina web o condividerla. Per ulteriori informazioni, vedi [Analisi dei log utilizzando le visualizzazioni](logging_kibana_visualizations.html#logging_kibana_visualizations).

* Nella pagina Dashboard, puoi personalizzare, salvare e condividere più visualizzazioni e ricerche contemporaneamente. 

    Puoi aggiungere, rimuovere e riorganizzare le visualizzazioni nel dashboard. Per ulteriori informazioni, vedi [Analisi dei log in Kibana tramite un dashboard](logging_kibana_analize_logs_dashboard.html#kibana_analize_logs_dashboard).
    
    Dopo aver personalizzato un dashboard Kibana, puoi analizzare i dati tramite le relative visualizzazioni e salvarli per un utilizzo successivo. Per ulteriori informazioni, vedi [Salvataggio di un dashboard Kibana](logging_kibana_analize_logs_dashboard.html#save_Kibana_dashboard).

In Kibana, è anche presente una pagina *Impostazioni* che puoi utilizzare per configurare Kibana e per salvare, eliminare, esportare e importare ricerche, visualizzazioni e dashboard.

Per ulteriori informazioni su Kibana, consulta [Kibana User Guide ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.

**Nota:** Kibana 4 e Kibana 3 sono supportati. Kibana 3 è obsoleto.


##  Accesso al dashboard Kibana dal dashboard Bluemix
{: #launch_Kibana_from_bluemix}

La query che viene utilizzata per filtrare i dati visualizzati in Kibana richiama le voci di log per l'applicazione CF o il contenitore {{site.data.keyword.Bluemix_notm}} da cui è stato avviato Kibana. 

Per visualizzare i log di un'applicazione Cloud Foundry o un contenitore Docker in Kibana, completa la seguente procedura:

1. Accedi a {{site.data.keyword.Bluemix_notm}} e fai clic sul nome applicazione o sul contenitore dal dashboard {{site.data.keyword.Bluemix_notm}}. 
    
2. Apri la scheda del log nella IU {{site.data.keyword.Bluemix_notm}}.

    * Per le applicazioni CF, fai clic su **Log** nella barra di navigazione. 
    * Per i contenitori, seleziona **Monitoraggio e log** nella barra di navigazione e fai quindi clic sulla scheda **Registrazione**. 
    
    Viene visualizzata la scheda Log. 
    
3. Fai clic su **Vista avanzata**. Si aprirà il dashboard **Kibana 4**.

    Per impostazione predefinita, la pagina **Ricerca** viene caricata con il modello di indice predefinito selezionato e un filtro temporale impostato sugli ultimi 30 secondi. La query di ricerca è configurata per corrispondere a tutte le voci per la tua applicazione CF o contenitore Docker.

    Se la pagina Rileva non mostra alcuna voce di log, modifica il selezionatore di tempo. Per ulteriori informazioni, consulta [Configurazione di un filtro temporale](logging_kibana_set_time_filter.html#set_time_filter).

Per ulteriori informazioni su Kibana, consulta [Kibana User Guide](https://www.elastic.co/guide/en/kibana/current/index.html).

##  Accesso al dashboard Kibana da un browser web
{: #launch_Kibana_from_browser}

La query utilizzata per filtrare i dati visualizzati in Kibana richiama le voci di log per uno spazio nell'organizzazione {{site.data.keyword.Bluemix_notm}}. Le informazioni di log visualizzate da Kibana includono i record per tutte le risorse che vengono distribuite all'interno dello spazio dell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui sei connesso.

Completa la seguente procedura per avviare Kibana da un browser:

1. Apri [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) per accedere all'interfaccia utente Kibana.

2. Seleziona la versione di Kibana che desideri utilizzare per analizzare i tuoi log.
    * Seleziona **Kibana 4** per lavorare con Kibana 4. Viene aperta la pagina Rileva. Per ulteriori informazioni, consulta [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).
    * Seleziona la scheda **Kibana 3** per lavorare con Kibana 3. Viene aperto il dashboard Kibana predefinito. Per ulteriori informazioni sulla personalizzazione di un dashboard Kibana 3, consulta [questo post del blog](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/).
     
        **Nota:** Kibana 3 è obsoleto.

    Se la pagina Rileva non mostra alcuna voce di log, modifica il selezionatore di tempo. Per ulteriori informazioni, consulta [Configurazione di un filtro temporale](logging_kibana_set_time_filter.html#set_time_filter).

Per ulteriori informazioni su Kibana, consulta [Kibana User Guide ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.

