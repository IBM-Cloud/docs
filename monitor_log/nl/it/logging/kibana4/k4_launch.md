---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Passaggio al dashboard Kibana
{: #k4_launch}

Puoi avviare Kibana dall'interfaccia utente {{site.data.keyword.Bluemix}} o direttamente da un browser web.
{:shortdesc}

Avvia Kibana da {{site.data.keyword.Bluemix_notm}} per visualizzare e analizzare i dati nel contesto della risorsa da cui avvii Kibana. Ad esempio, puoi avviare i log della tua specifica applicazione CF in Kibana, nel contesto di quella specifica applicazione oppure i log del tuo specifico contenitore Docker in Kibana, nel contesto di quello specifico contenitore. 
    
Avvia Kibana da un link diretto del browser se vuoi visualizzare i dati di log aggregati provenienti dai servizi all'interno di uno spazio {{site.data.keyword.Bluemix_notm}} specifico. La query che viene utilizzata per filtrare i dati visualizzati nel dashboard richiama le voci di log per uno spazio nell'organizzazione {{site.data.keyword.Bluemix_notm}}. Le informazioni di log visualizzate da Kibana includono i record per tutte le risorse che vengono distribuite all'interno dello spazio dell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui sei connesso. 

Per ulteriori informazioni su Kibana, consulta [Kibana User Guide ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.
    

##  Passaggio al dashboard Kibana dal dashboard Bluemix
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


##  Passaggio al dashboard Kibana da un browser web
{: #launch_Kibana_from_browser}

La query utilizzata per filtrare i dati visualizzati in Kibana richiama le voci di log per uno spazio nell'organizzazione {{site.data.keyword.Bluemix_notm}}. Le informazioni di log visualizzate da Kibana includono i record per tutte le risorse che vengono distribuite all'interno dello spazio dell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui sei connesso.

Completa la seguente procedura per avviare Kibana da un browser:

1. Apri [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) per accedere all'interfaccia utente Kibana.

2. Seleziona la versione di Kibana che desideri utilizzare per analizzare i tuoi log.
    * Seleziona **Kibana 4** per lavorare con Kibana 4. Viene aperta la pagina Rileva. Per ulteriori informazioni, consulta [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).
    * Seleziona la scheda **Kibana 3** per lavorare con Kibana 3. Viene aperto il dashboard Kibana predefinito. Per ulteriori informazioni sull'utilizzo di Kibana per analizzare i tuoi log, consulta [Analisi dei log in Kibana 3 (Obsoleto)](../logging_view_kibana3.html#analyzing_logs_Kibana3). Per ulteriori informazioni sulla personalizzazione di un dashboard Kibana 3, consulta [questo post del blog ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/).
     
        **Nota:** Kibana 3 è obsoleto.

    Se la pagina Rileva non mostra alcuna voce di log, modifica il selezionatore di tempo. Per ulteriori informazioni, consulta [Configurazione di un filtro temporale](logging_kibana_set_time_filter.html#set_time_filter).


