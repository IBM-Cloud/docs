---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integrazione con Continuous Delivery pipeline

Dopo aver aggiunto {{site.data.keyword.DRA_short}} a una toolchain e aver definito le politiche che monitora, integralo con {{site.data.keyword.deliverypipeline}}. Per ulteriori informazioni sulle pipeline, consulta [la documentazione ufficiale](/docs/services/ContinuousDelivery/pipeline_working.html).

## Preparazione delle fasi della pipeline
{: #integrate_pipeline}

Per far analizzare a Deployment Risk il tuo progetto, devi definire le fasi di produzione e di preparazione nella tua pipeline. Definisci le fasi utilizzando le proprietà di ambiente di testo, che puoi trovare in ogni menu di configurazione della fase ![Icona configurazione fase pipeline](images/pipeline-stage-configuration-icon.png) in **Environment Properties**.

1. Nella fase di preparazione, imposta la proprietà `LOGICAL_ENV_NAME` su `STAGING`. 

2. Nella fase di produzione, imposta la proprietà `LOGICAL_ENV_NAME` su `PRODUCTION`. 

Puoi anche aggiungere le seguenti proprietà alle fasi che creano o distribuiscono la tua applicazione:

* `LOGICAL_APP_NAME`, che definisce il nome dell'applicazione nel dashboard.
* `BUILD_PREFIX`, che definisce il testo che precede le build della fase. Questo testo viene anche visualizzato nel dashboard. 

## Aggiunta di lavori di verifica
{: #configure_pipeline_jobs}

Integra {{site.data.keyword.DRA_short}} nella tua pipeline utilizzando due tipi di lavori di verifica: uno che carica i risultati in {{site.data.keyword.DRA_short}} per l'analisi e i gate che utilizzano questa analisi. 

Per prima cosa, aggiungi i lavori di tester avanzato alla tua pipeline per eseguire i test e caricare i risultati. 

**Nota:** se desideri aggiornare un lavoro di verifica per caricare i risultati in {{site.data.keyword.DRA_short}}, salvane la configurazione in un luogo apposito prima di procedere. Quindi, apri il menu di configurazione del lavoro e passa ala passo 3. 

1. Nella fase in cui desideri aggiungere il lavoro che carica i risultati, fai clic sull'icona **Configurazione fase** ![Icona configurazione fase della pipeline](images/pipeline-stage-configuration-icon.png). Fai clic su **Configura fase**.
2. Crea un lavoro di verifica ed immetti un nome per esso. 
3. Per il tipo di lavoro, seleziona **Advanced Tester**.
4. Riempi i campi **Test Command** e **Working Directory** come preferisci per una lavoro di verifica di una pipeline normale. 
5. Riempi i campi rimanenti per caricare i risultati del test per un tipo di test particolare. 

 1. Scegli il tipo di metrica che corrisponde a quella definita nella politica {{site.data.keyword.DRA_short}} che desideri utilizzare.
 2. Immetti un'ubicazione del file del risultato. Questa ubicazione è relativa alla directory di lavoro. 

6. Se desideri caricare i risultati per un secondo tipo di test, riempi i campi con il prefisso *Ulteriori*.
7. Fai clic su **Salva** per ritornare alla pipeline.

I valori per i campi **Tipo di metrica** e **Ubicazione del File di risultato** devono corrispondere al formato corretto:

<table><thead>
<tr>
<th>Tipo di metrica</th>
<th>Formati supportati</th>
</tr>
</thead><tbody>
<tr>
<td>Test di verifica funzionale</td>
<td>Mocha, xUnit</td>
</tr>
<tr>
<td>Verifica di unità</td>
<td>Mocha, xUnit, Karma/Mocha</td>
</tr>
<tr>
<td>Copertura del codice</td>
<td>Istanbul, Blanket.js</td>
</tr>
</tbody></table>

La figura 1 mostra un lavoro di test configurato per eseguire le verifiche di unità, per caricare i risultati nel formato Mocha e per caricare i risultati della copertura del codice nel formato Istanbul.

![Lavoro di caricamento DevOps Insights](images/insights_upload_job.png)
*Figura 1. Carica i risultati in DevOps Insights*

## Definizione dei gate
{: #configure_pipeline_gates}

I gate {{site.data.keyword.DRA_short}} verificano se i tuoi risultati di test soddisfano una politica definita. Se la politica non viene soddisfatta, il gate {{site.data.keyword.DRA_short}} ha un malfunzionamento per impostazione predefinita. Puoi inoltre configurare i gate per funzionare nella modalità advisory per consentire l'avanzamento della pipeline anche dopo un malfunzionamento.

Il dashboard Deployment Risk si basa sulla presenza di un gate dopo un lavoro di distribuzione di preparazione. Se desideri utilizzare il dashboard, assicurati di avere un gate dopo aver distribuito l'ambiente in fase di preparazione, ma prima di distribuire un ambiente di produzione.

Di solito, i gate sono posizionati prima della promozione della build nella tua pipeline. Queste ubicazioni sono ideali per controllare la qualità della build nelle tue politiche per assicurati che siano sicure da promuovere da un ambiente a un altro. Tuttavia, puoi posizionare i gate ovunque nella pipeline in cui desideri che venga controllato un criterio specifico. I gate che sono posizionati prima di distribuire un ambiente in fase di preparazione ancora utilizzeranno le politiche, ma non compariranno nel dashboard Deployment Risk.

1. Nella fase, fai clic sull'icona **Configurazione fase** ![Icona configurazione fase della pipeline](images/pipeline-stage-configuration-icon.png) e fai clic su **Configura fase**.
2. Fai clic su **Aggiungi lavoro**. Per il tipo di lavoro, seleziona **Test**.
3. Per il tipo di tester, seleziona **Gate {{site.data.keyword.DRA_short}}**.
4. Specifica il nome dell'ambiente. Assicurati che questo valore corrisponda al valore che è stato definito nelle tue [proprietà di ambiente](#toolchain_pipeline_props).
5. Immetti il nome della politica da controllare in questo gate.

 Questo nome deve corrispondere esattamente a uno dei nomi della politica che hai definito. Puoi specificare solo politiche definite nella stessa organizzazione {{site.data.keyword.Bluemix_notm}} della tua toolchain.

6. Facoltativo: per passare una funzione gate ella modalità advisory, annulla la spunta della casella **Arrestare l'esecuzione di questa fase se il lavoro non riesce**. Nella modalità advisory, {{site.data.keyword.DRA_short}} completa le stesse analisi della politica nel gate e genera i report, ma se incontra un malfunzionamento, la pipeline non viene arrestata.
7. Fai clic su **Salva** per ritornare alla pipeline.
8. Configura i gate per tutte le politiche {{site.data.keyword.DRA_short}} ripetendo questi passi.

![Lavoro Deployment Risk Mocha](images/insights_gate_job.png)
*Figura 2. Gate DevOps Insights*

Dopo aver configurato la tua pipeline, inizia ad utilizzare {{site.data.keyword.DRA_short}}. 
