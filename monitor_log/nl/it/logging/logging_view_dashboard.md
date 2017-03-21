---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analisi dei log dell'applicazione CF dal dashboard Bluemix
{: #analyzing_logs_bmx_ui}

In {{site.data.keyword.Bluemix}}, puoi visualizzare, filtrare e analizzare i log attraverso la scheda **Log** disponibile per ogni applicazione Cloud Foundry. Utilizza il dashboard {{site.data.keyword.Bluemix}} per visualizzare l'ultima attività dell'applicazione.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} pubblico offre un servizio di registrazione integrato. Quando esegui le tue applicazioni in Cloud Foundry,
il servizio di registrazione acquisisce i dati di log relativi alla tua applicazione dai componenti di sistema che interagiscono con l'applicazione e anche i dati di log dall'interno dell'applicazione quando utilizzi stdout e stderr.

I log per le applicazioni {{site.data.keyword.Bluemix_notm}} vengono visualizzati in un formato fisso, simile al seguente modello:

<code><var class="keyword varname">Component</var>/<var class="keyword varname">instanceID</var>     <var class="keyword varname">message</var>     <var class="keyword varname">timestamp</var></code>
   
Per ulteriori informazioni sul formato dei log, vedi [Formato dei log dell'applicazione Cloud Foundry](logging_view_dashboard.html#log_format_cf).

**Nota:** in {{site.data.keyword.Bluemix_notm}} pubblico, i dati dei log vengono memorizzati per 7 giorni per impostazione predefinita. Puoi ricercare fino a 1 GB di dati al giorno.



##  Accesso alla scheda Log Bluemix
{: #launch_logs_tab_bmx_ui}

Per visualizzare i log di distribuzione o di runtime di un'applicazione Cloud Foundry, completa la seguente procedura:

1. Accedi a {{site.data.keyword.Bluemix_notm}} e fai clic sul nome applicazione nel dashboard delle **Applicazioni** {{site.data.keyword.Bluemix_notm}}.  

    Viene visualizzata la pagina dei dettagli dell'applicazione.
    
2. Nella barra di navigazione, fai clic su **Log**.

    Viene visualizzata la scheda Log. 
    
    Nella scheda **Log**, puoi visualizzare in tempo reale i log recenti riguardanti la tua applicazione o le parti finali dei log. Inoltre, puoi filtrare i log in base al componente (tipo di log), all'ID istanza dell'applicazione e all'errore.



## Formato dei log dell'applicazione Cloud Foundry 
{: #log_format_cf}

Ogni voce di log contiene i seguenti campi:

<dl>
<dt><strong>Data/ora</strong></dt>
<dd>
<p>L'ora dell'istruzione di log. La data e ora è definita fino al millisecondo.</p>
</dd>

<dt><strong>Componente</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>Il componente che produce il log. </p>
<p>Ogni tipo di componente è seguito da una barra e da un numero che indica l'istanza dell'applicazione. 0 è il numero assegnato alla prima istanza, 1 è il numero assegnato alla seconda e così via. Puoi utilizzare il filtro per vedere una sola istanza dell'applicazione nel dashboard.</p>
<p>Il seguente elenco descrive i diversi tipi di componente:</p>

<dl>
<dt><strong>LGR</strong></dt>
<dd>Loggregator: il componente LGR fornisce informazioni relative al Loggregator Cloud Foundry, che inoltra i log dall'interno di Cloud Foundry.</dd>

<dt><strong>RTR</strong></dt>
<dd>Router: il componente RTR fornisce informazioni sulle richieste HTTP a un'applicazione.</dd>

<dt><strong>STG</strong></dt>
<dd>Preparazione: il componente STG fornisce informazioni su come viene preparata o ripreparata un'applicazione.</dd>

<dt><strong>APP</strong></dt>
<dd>Applicazione: il componente APP fornisce i log dall'applicazione. Qui è dove vengono mostrati i stderr e stdout nel tuo codice.
</dd>

<dt><strong>API</strong></dt>
<dd>API Cloud Foundry: il componente API fornisce informazioni sulle azioni interne che derivano dalla richiesta di un utente di modificare lo stato di un'applicazione.</dd>

<dt><strong>DEA</strong></dt>
<dd>Droplet Execution Agent: il componente DEA fornisce informazioni sull'avvio, l'interruzione o l'arresto anomalo di un'applicazione.
<p>Questo componente è disponibile solo se la tua applicazione viene distribuita nell'architettura Cloud Foundry basata su DEA.</p></dd>

<dt><strong>CELL</strong></dt>
<dd>Cella Diego: il componente CELL fornisce informazioni sull'avvio, l'interruzione o l'arresto anomalo di un'applicazione.
<p>Questo componente è disponibile solo se la tua applicazione viene distribuita nell'architettura Cloud Foundry basata su Diego.</p></dd>

<dt><strong>SSH</strong></dt>
<dd>SSH: il componente SSH fornisce informazioni ogni volta che un utente accede a un'applicazione utilizzando il comando **cf ssh**.
<p>Questo componente è disponibile solo se la tua applicazione viene distribuita nell'architettura Cloud Foundry basata su Diego.</p></dd>

</dl>
</dd>

<dt><strong>Messaggio</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Messaggio</var>&gt;</code></pre>
<p>Il messaggio che viene emesso dal componente. Il messaggio varia a seconda dal contesto.</p>
</dd>
</dl>

La seguente figura mostra i diversi componenti (tipi di log) in un'architettura Cloud Foundry basata su DEA (Droplet Execution Agent):
![Tipi di log in un'architettura DEA.](images/logging_F1.png "Componenti (tipi di log") in un'architettura Cloud Foundry basata su DEA (Droplet Execution Agent).")



