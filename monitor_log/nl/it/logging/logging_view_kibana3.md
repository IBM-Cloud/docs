---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-22"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analisi dei log in Kibana 3 (obsoleto)
{: #analyzing_logs_Kibana3}

In {{site.data.keyword.Bluemix}}, puoi utilizzare Kibana, una piattaforma di analisi e visualizzazione open source, per monitorare, ricercare, analizzare e visualizzare i tuoi dati in una varietà di grafici, ad esempio, diagrammi e tabelle. Utilizza Kibana per eseguire attività di analisi avanzate.
{:shortdesc}

Puoi avviare Kibana in uno dei seguenti modi:

* Dal dashboard dell'applicazione Cloud Foundry

    Puoi avviare i log della tua specifica applicazione CF in Kibana, nel contesto di quella specifica applicazione.
    
    La query che viene utilizzata per filtrare i dati visualizzati nel dashboard richiama le voci di log per l'applicazione Cloud Foundry. Le informazioni di log visualizzate dal dashboard Kibana per impostazione predefinita sono tutte correlate a un'unica applicazione Cloud Foundry e a tutte le sue istanze. Per ulteriori informazioni, vedi [Accesso al dashboard Kibana dal dashboard Bluemix](logging_view_kibana3.html#launch_Kibana_from_bluemix).

* Da un link diretto del browser

    Potresti voler avviare il dashboard Kibana personalizzato che aggrega i dati dai servizi all'interno di uno spazio {{site.data.keyword.Bluemix}} fornito.
    
    La query che viene utilizzata per filtrare i dati visualizzati nel dashboard richiama le voci di log per uno spazio nell'organizzazione {{site.data.keyword.Bluemix}}. Le informazioni di log visualizzate dal dashboard Kibana includono i record per tutte le risorse che vengono distribuite all'interno dello spazio dell'organizzazione {{site.data.keyword.Bluemix}} a cui sei connesso. Per ulteriori informazioni, vedi [Accesso al dashboard Kibana da un browser web](logging_view_kibana3.html#launch_Kibana_from_browser).
    
    Puoi anche modificare o rimuovere la query iniziale e aggiungere altre query. Per ulteriori informazioni, vedi [Filtraggio dei log dell'applicazione Cloud Foundry con le query in Kibana](kibana3/logging_kibana_query.html#logging_kibana_query).


Kibana è un'interfaccia basata su browser in cui puoi personalizzare i dashboard che potrai quindi utilizzare per analizzare i dati di log ed eseguire attività di gestione avanzate. 

In {{site.data.keyword.Bluemix}}, puoi analizzare i dati utilizzando il dashboard Kibana predefinito disponibile per ogni applicazione Cloud Foundry e per ogni spazio della tua organizzazione. Per impostazione predefinita, questi dashboard visualizzano tutti i dati disponibili durante le ultime 24 ore attraverso un pannello che include la riga Istogramma e una riga Tabella di eventi. 

Per limitare le informazioni visualizzate attraverso un qualsiasi dashboard predefinito, puoi aggiungere query e filtri al dashboard. Puoi quindi salvare il dashboard per riutilizzi futuri. 

I dati visualizzati da un dashboard Kibana sono controllati dalla query. Per modificare le informazioni visualizzate in un dashboard, puoi modificare la query, aggiungere altre query e poi salvare il dashboard. Puoi personalizzare, salvare e condividere più dashboard contemporaneamente. Questo è il modo in cui Kibana mostra le informazioni relative a una singola applicazione, ad esempio, nel tuo spazio.

Puoi anche configurare i filtri dai campi di log, ad esempio, message_type e instance_ID. Per ulteriori informazioni, vedi [Formato dei log Kibana](logging_view_kibana3.html#kibana_log_format_cf). Puoi abilitare o disabilitare dinamicamente questi filtri. Il dashboard visualizzerà le voci di log che soddisfano la query e i criteri di filtro da te abilitati. Per ulteriori informazioni, vedi [Filtraggio dei dati in un dashboard Kibana](logging_view_kibana3.html#filter_data_kibana_dashboard).

Per visualizzare i dati, puoi configurare i pannelli. Kibana include diversi pannelli, come tabella, tendenze e istogramma, che puoi utilizzare per analizzare le informazioni. Puoi aggiungere, rimuovere e riorganizzare i pannelli nel dashboard. Ogni pannello ha un obiettivo diverso. Alcuni pannelli sono organizzati in righe che forniscono i risultati di una o più query. Altri pannelli visualizzano documenti o informazioni personalizzate. Per ulteriori informazioni, vedi [Personalizzazione di un dashboard Kibana](logging_view_kibana3.html#customize_kibana_dashboard).

Dopo aver personalizzato un dashboard, puoi scegliere una delle seguenti azioni:

* Puoi salvare il dashboard per riutilizzi futuri. Per ulteriori informazioni, vedi [Salvataggio di un dashboard Kibana](logging_view_kibana3.html#save_Kibana_dashboard).

* Puoi esportare o condividere un link diretto a un dashboard Kibana con un altro utente. Per ulteriori informazioni, vedi [Esportazione e condivisione dei tuoi dashboard Kibana](kibana3/logging_kibana_export_share_dashboard.html#sexporting_sharing_kibana_dash).

* Puoi incorporare il tuo dashboard in una pagina web. Perché un utente possa visualizzare un dashboard incorporato, deve avere le autorizzazioni per accedere a Kibana.

Per ulteriori informazioni, consulta la documentazione [Kibana ![icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/current/index.html){: new_window}.

**Nota:** Kibana 4 e Kibana 3 sono supportati. Kibana 3 è obsoleto.


##  Accesso al dashboard Kibana dal dashboard Bluemix
{: #launch_Kibana_from_bluemix}

La query che viene utilizzata per filtrare i dati visualizzati nel dashboard richiama le voci di log per l'applicazione Cloud Foundry. Le informazioni di log visualizzate dal dashboard Kibana per impostazione predefinita sono tutte correlate a un'unica applicazione Cloud Foundry e a tutte le sue istanze.

Per visualizzare i log di un'applicazione Cloud Foundry in Kibana, completa la seguente procedura:

1. Accedi a {{site.data.keyword.Bluemix_notm}} e fai clic sul nome applicazione nel dashboard delle **Applicazioni** {{site.data.keyword.Bluemix_notm}}. Viene visualizzata la pagina dei dettagli dell'applicazione.
    
2. Nella barra di navigazione, fai clic su **Log**. Viene visualizzata la scheda Log. 
    
3. Fai clic su **Vista avanzata**. Si aprirà il dashboard **Kibana 3**.

Se non visualizzi alcun log, modifica il selezionatore di tempo nell'intestazione.

Per ulteriori informazioni sulla personalizzazione di un dashboard Kibana, consulta [questo post del blog ![icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/){: new_window} o la documentazione [Kibana ![icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/current/index.html){: new_window}.

##  Accesso al dashboard Kibana da un browser web
{: #launch_Kibana_from_browser}

La query che viene utilizzata per filtrare i dati visualizzati nel dashboard richiama le voci di log per uno spazio nell'organizzazione {{site.data.keyword.Bluemix}}. Le informazioni di log visualizzate dal dashboard Kibana includono i record per tutte le risorse che vengono distribuite all'interno dello spazio dell'organizzazione {{site.data.keyword.Bluemix}} a cui sei connesso.

Completa la seguente procedura per aprire un dashboard Kibana da un browser:

1. Apri [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) per accedere all'interfaccia utente Kibana.

2. Seleziona la scheda **Kibana 3** per lavorare con Kibana 3. Seleziona **Kibana 4** per lavorare con Kibana 4. Viene visualizzato il dashboard Kibana predefinito. 

Se non visualizzi alcun log, modifica il selezionatore di tempo nell'intestazione.

Per ulteriori informazioni sulla personalizzazione di un dashboard Kibana, consulta [questo post del blog ![icona link esterno](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/){: new_window} o la documentazione [Kibana ![icona link esterno](../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/current/index.html){: new_window}.



## Filtraggio dei dati in un dashboard Kibana
{: #filter_data_kibana_dashboard}

In {{site.data.keyword.Bluemix}}, puoi analizzare i dati utilizzando il dashboard Kibana predefinito fornito per ogni risorsa o in base allo spazio {{site.data.keyword.Bluemix}}. Per impostazione predefinita, questi dashboard visualizzano tutti i dati disponibili durante le ultime 24 ore. Tuttavia, puoi limitare le informazioni visualizzate tramite un dashboard. Puoi aggiungere query e filtri a un dashboard predefinito e quindi salvarlo per riutilizzi futuri.

In un dashboard, puoi aggiungere più query e filtri. Una query definisce un sottoinsieme di voci di log.  Un filtro ridefinisce la selezione dei dati includendo o escludendo informazioni. 

Per le applicazioni Cloud Foundry, il seguente elenco mostra degli esempi su come filtrare i dati:
* Se nei log stai cercando delle informazioni che includono termini chiave, puoi creare query per filtrare in base a questi termini. Con Kibana, puoi confrontare visivamente le query sul dashboard. Per ulteriori informazioni, vedi [Filtraggio dei log dell'applicazione Cloud Foundry con le query in Kibana](kibana3/logging_kibana_query.html#logging_kibana_query).

* Se stai cercando informazioni per uno specifico periodo di tempo, puoi filtrare i dati all'interno di un intervallo di tempo. Per ulteriori informazioni, vedi [Filtraggio dei log dell'applicazione Cloud Foundry in base all'ora in Kibana](kibana3/logging_kibana_filter_by_time_period.html#logging_kibana_time_filter).

* Se stai cercando informazioni per uno specifico ID istanza, puoi filtrare i dati per ID istanza. Per ulteriori informazioni, vedi [Filtraggio dei log dell'applicazione Cloud Foundry per ID istanza in Kibana](kibana3/logging_kibana_filter_by_instance_id.html#logging_kibana_instance_id) e [Filtraggio dei log dell'applicazione Cloud Foundry per ID applicazione noto in Kibana](kibana3/logging_kibana_filter_by_known_application_id.html#logging_kibana_known_application_id).

* Se stai cercando informazioni per uno specifico componente, puoi filtrare i dati per componente (tipo di log). Per ulteriori informazioni, vedi [Filtraggio dei log dell'applicazione Cloud Foundry per tipo di log in Kibana](kibana3/logging_kibana_filter_by_component.html#logging_kibana_component_filter).

* Se stai cercando informazioni come, ad esempio, messaggi di errore, puoi filtrare i dati per tipo di messaggio. Per ulteriori informazioni, vedi [Filtraggio dei log dell'applicazione Cloud Foundry per tipo di messaggio in Kibana](kibana3/logging_kibana_filter_by_message_type.html#logging_kibana_message_type_filter).

## Personalizzazione di un dashboard Kibana
{: #customize_kibana_dashboard}

Esistono diversi tipi di dashboard che puoi personalizzare per visualizzare e analizzare i dati, ad esempio:
* Dashboard a singola applicazione cf: questo dashboard mostra le informazioni per una singola applicazione Cloud Foundry.  
* Dashboard a più applicazioni cf: questo dashboard mostra informazioni per tutte le applicazioni Cloud Foundry distribuite nello stesso spazio {{site.data.keyword.Bluemix}}. 

Quando personalizzi un dashboard, puoi configurare query e filtri per selezionare un sottoinsieme di dati di log da visualizzare attraverso il dashboard.

Per visualizzare i dati, puoi configurare i pannelli. Kibana include diversi pannelli, come tabella, tendenze e istogramma, che puoi utilizzare per analizzare le informazioni. Puoi aggiungere, rimuovere e riorganizzare i pannelli nel dashboard. Ogni pannello ha un obiettivo diverso. Alcuni pannelli sono organizzati in righe che forniscono i risultati di una o più query. Altri pannelli visualizzano documenti o informazioni personalizzate. Ad esempio, puoi configurare un grafico a barre, un grafico a torta o una tabella per visualizzare i dati e analizzarli.  


## Salvataggio di un dashboard Kibana
{: #save_Kibana_dashboard}

Completa la seguente procedura per salvare un dashboard Kibana dopo averlo personalizzato:

1. Nella barra degli strumenti, fai clic sull'icona **Salva**.

2. Immetti un nome per il dashboard.

    **Nota:** un dashboard con un nome che contiene spazi vuoti non verrà salvato.

3. Accanto al nome campo, fai clic sull'icona **Salva**.



## Analisi dei log tramite un dashboard Kibana
{: #analyze_kibana_logs}

Dopo aver personalizzato un dashboard Kibana, puoi visualizzare e analizzare i dati attraverso i suoi pannelli. 

Per ricercare informazioni, puoi bloccare o sbloccare query. 

* Puoi bloccare una query nel dashboard e la ricerca viene attivata automaticamente.
* Per rimuovere il contenuto dal dashboard, puoi disattivare una query.

Per filtrare le informazioni, puoi abilitare o disabilitare i filtri. 

* Puoi selezionare la casella di spunta **Attiva/disattiva** ![Casella di attivazione per includere un filtro](images/logging_toggle_include_filter.jpg) in un filtro per abilitarlo.   
* Puoi deselezionare la casella di spunta **Attiva/disattiva** ![Casella di attivazione per includere un filtro](images/logging_toggle_exclude_filter.jpg) in un filtro per disabilitarlo. 

I grafici e diagrammi all'interno nel tuo dashboard visualizzano i dati. Puoi utilizzare i grafici e diagrammi nel tuo dashboard per monitorare i dati. 

Ad esempio, per un dashboard a singola applicazione cf, il dashboard include informazioni su una singola applicazione Cloud Foundry. I dati che puoi visualizzare e analizzare sono limitati a tale applicazione. Puoi utilizzare il dashboard per analizzare i dati di tutte le istanze dell'applicazione e puoi confrontare le istanze. Le informazioni possono essere filtrate in base all'ID istanza. 

Puoi definire e bloccare una query per ogni ID istanza nel dashboard. 

![Dashboard con query bloccate](images/logging_kibana_dash_activate_query.jpg)

Puoi quindi attivare o disattivare le singole query a seconda delle informazioni sull'istanza che vuoi visualizzare nel dashboard. 

La seguente figura mostra una query attivata e un'altra disattivata:

![Dashboard con query bloccate](images/logging_kibana_dash_deactivate_query.jpg)

Se vuoi confrontare 2 istanze in un istogramma, puoi definire due query nello stesso dashboard, una per ogni ID istanza. Puoi fornire loro un alias e un colore univoco per identificarle facilmente. Kibana gestisce più query unendole con un OR logico. 

La seguente figura mostra il pannello per configurare un alias e un colore per una query, per bloccarla nel dashboard e per disattivarla:

![Procedura guidata del dashboard per configurare la query](images/logging_kibana_query_def.jpg)



## Formato dei log Kibana per le applicazioni Cloud Foundry
{: #kibana_log_format_cf}

Puoi configurare un dashboard Kibana per visualizzare i seguenti campi per ogni voce di log:

<dl>
<dt><strong>@timestamp</strong></dt>
<dd>
<pre class="pre screen"><code>yyyy-MM-ddTHH:mm:ss:SS-0500</code></pre>
<p>L'ora dell'evento registrato. La data e ora è definita fino al millisecondo.</p>
</dd>

<dt><strong>@version</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>ALCH_TENANT_ID</strong></dt>
<dd>
<p>L'ID della risorsa {{site.data.keyword.Bluemix_notm}}.</p>
</dd>

<dt><strong>_id</strong></dt>
<dd>
<p>L'ID univoco per il tuo documento di log.</p>
</dd>

<dt><strong>_index</strong></dt>
<dd>
<p>L'indice per la voce di log.</p>
</dd>

<dt><strong>_type</strong></dt>
<dd>
<p>Il tipo di log, ad esempio <samp>syslog</samp>.</p>
</dd>

<dt><strong>app_name</strong></dt>
<dd>
<p>Il nome della tua applicazione {{site.data.keyword.Bluemix_notm}}.</p>
</dd>

<dt><strong>application_id</strong></dt>
<dd>
<p>L'ID univoco della tua applicazione {{site.data.keyword.Bluemix_notm}}.</p>
</dd>

<dt><strong>host</strong></dt>
<dd>
<p>Il nome della tua applicazione che ha prodotto i dati di log.</p>
</dd>

<dt><strong>instance_id</strong></dt>
<dd>
<p>L'ID dell'istanza della tua applicazione che ha prodotto i dati di log.</p>
</dd>

<dt><strong>module</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>loglevel</strong></dt>
<dd>
<p>La severità dell'evento registrato.</p>
</dd>

<dt><strong>message</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Messaggio</var>&gt;</code></pre>
<p>Il messaggio che viene emesso dal componente. Il messaggio varia a seconda dal contesto.</p>
</dd>

<dt><strong>message_type</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>Il flusso in cui viene scritto il messaggio di log. <samp class="ph codeph">OUT</samp> si riferisce al flusso <samp class="ph codeph">stdout</samp> e <samp class="ph codeph">ERR</samp> si riferisce al flusso <samp class="ph codeph">stderr</samp>.</p>
</dd>

<dt><strong>org_id</strong></dt>
<dd>
<p>L'ID univoco della tua organizzazione {{site.data.keyword.Bluemix_notm}}.</p>
</dd>

<dt><strong>org_name</strong></dt>
<dd>
<p>Il nome dell'organizzazione {{site.data.keyword.Bluemix_notm}} in cui viene preparata la tua applicazione.</p>
</dd>

<dt><strong>origin</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>source_id</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>Il componente che produce i log. Il seguente elenco descrive i log di ogni componente:</p>

<dl>
<dt><strong>API</strong></dt>
<dd>Le risposte registrate per le chiamate API che richiedono una modifica allo stato della tua applicazione.</dd>

<dt><strong>APP</strong></dt>
<dd>Risposte registrate dalla tua applicazione.</dd>

<dt><strong>CELL</strong></dt>
<dd>Risposte registrate dalla cella Diego che indicano quando un'applicazione viene avviata, interrotta o arrestata in modo anomalo.</dd>

<dt><strong>LGR</strong></dt>
<dd>Risposte registrate dal loggregator che indicano problemi con il processo di registrazione.</dd>

<dt><strong>RTR</strong></dt>
<dd>Risposte registrate dal Router quando istrada le richieste HTTP alla tua applicazione.</dd>

<dt><strong>SSH</strong></dt>
<dd>Risposte registrate dalla cella Diego quando un utente accede a un contenitore applicazioni utilizzando il comando **cf ssh**.</dd>

<dt><strong>STG</strong></dt>
<dd>Risposte registrate dalla cella Diego o dal DEA (Droplet Execution Agent) quando la tua applicazione viene preparata o ripreparata.</dd>
</dl>
</dd>

<dt><strong>space_name</strong></dt>
<dd>
<p>Il nome dello spazio {{site.data.keyword.Bluemix_notm}} in cui viene preparata la tua applicazione.</p>
</dd>

<dt><strong>timestamp</strong></dt>
<dd>
<p>L'ora dell'evento registrato. La data e ora è definita fino al millisecondo.</p>
</dd>

<dt><strong>_type</strong></dt>
<dd>
<p>Il tipo di log, ad esempio <samp>syslog</samp>.</p>
</dd>
</dl>




