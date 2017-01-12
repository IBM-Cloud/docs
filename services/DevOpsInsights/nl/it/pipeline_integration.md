---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integrazione di {{site.data.keyword.DRA_short}} con {{site.data.keyword.deliverypipeline}}
{: #toolchain_configure_pipeline}

Dopo aver aggiunto {{site.data.keyword.DRA_full}} a una toolchain e aver definito le politiche da monitorare, devi integrare {{site.data.keyword.DRA_short}} con la tua pipeline.
{:shortdesc}

<!--##Configuring the {{site.data.keyword.deliverypipeline}}

{: #toolchain_integration}
To use {{site.data.keyword.DRA_short}}, add it to any toolchain that uses the {{site.data.keyword.deliverypipeline}}.

1. In {{site.data.keyword.Bluemix_notm}}, on the **Toolchains** tab, open a toolchain.

2. On the toolchain's Overview page, click the add (+) button.

3. In the Tool Integrations section, select **{{site.data.keyword.DRA_short}}**.

4. Click **Create Integration**.

5. In your toolchain, click the {{site.data.keyword.deliverypipeline}} tile. You can configure {{site.data.keyword.DRA_short}} in any number of pipelines.-->

## Preparazione delle fasi della pipeline per {{site.data.keyword.DRA_short}}
{: #toolchain_pipeline_props}

Devi creare diverse proprietà di ambiente in ogni fase della pipeline che contiene i lavori di distribuzione o di build:

1. Fai clic su **Configurazione fase** e quindi su **Configura fase**.

2. Fai clic su **PROPRIETÀ AMBIENTE**.

3. Aggiungi le seguenti tre proprietà e quindi salva le modifiche nella fase:

<table><thead>
<tr>
<th>Proprietà ambiente</th>
<th>Descrizione</th>
</tr>
</thead><tbody>
<tr>
<td><code>LOGICAL_APP_NAME</code></td>
<td>Il nome dell'applicazione come visualizzato nei dashboard {{site.data.keyword.DRA_short}}. </td>
</tr>
<tr>
<td><code>LOGICAL_ENV_NAME</code></td>
<td>Il nome dell'ambiente in cui è in esecuzione l'applicazione. Questa proprietà viene utilizzata per categorizzare l'applicazione nei dashboard {{site.data.keyword.DRA_short}}.</td>
</tr>
<tr>
<td><code>BUILD_PREFIX</code></td>
<td>Un prefisso che viene aggiunto per la build come mostrato nei dashboard {{site.data.keyword.DRA_short}}.</td>
</tr>
</tbody></table>


## Aggiornamento dei lavori di test per {{site.data.keyword.DRA_short}}
{: #toolchain_pipeline_upload}

Per iniziare, richiama le informazioni di configurazione da un lavoro di test.

1. Nella fase che contiene un lavoro di test, fai clic sull'icona **Configurazione fase** ![Icona configurazione fase della pipeline](images/pipeline-stage-configuration-icon.png). Fai clic su **Configura fase**.
2. Crea un lavoro. Per il tipo di lavoro, seleziona **Test**.
3. Seleziona un lavoro di test che utilizza il tipo di tester semplice e copia le informazioni in esso nei campi **Verifica comando** e **Directory di lavoro** in un editor. Avrai bisogno di queste informazioni successivamente.
4. Dallo stesso lavoro di test semplice, modifica il tipo di tester selezionando **Tester avanzato**.
5. Nel campo **Verifica comando**, incolla i comandi che hai copiato dal campo **Verifica comando** del lavoro di test semplice.
6. Nel campo **Directory di lavoro**, incolla il percorso che hai copiato dal campo **Directory di lavoro** del lavoro di test semplice.
7. Riempi i campi rimanenti per caricare i risultati del test per un tipo di test particolare. Se desideri caricare i risultati per un secondo tipo di test, riempi anche i campi con il prefisso *Ulteriori*.

 * Tipo di metrica
 * Formato
 * Ubicazione del File di risultato
8. Fai clic su **Salva** per ritornare alla pipeline.

I valori per i campi **Tipo di metrica** e **Ubicazione del File di risultato** devono corrispondere al formato corretto:

<table><thead>
<tr>
<th>Tipo di metrica</th>
<th>Formati supportati</th>
</tr>
</thead><tbody>
<tr>
<td>Test di verifica funzionale</td>
<td>Mocha, JUnit</td>
</tr>
<tr>
<td>Verifica di unità</td>
<td>Mocha, JUnit, Karma/Mocha</td>
</tr>
<tr>
<td>Copertura del codice</td>
<td>Istanbul, Blanket.js</td>
</tr>
</tbody></table>

*Figura 1* mostra un lavoro di test configurato per eseguire le verifiche di unità, per caricare i risultati nel formato Mocha e per caricare i risultati della copertura del codice nel formato Istanbul.

![Lavoro di caricamento Deployment Risk Analytics](images/DRA_upload_job.png)
*Figura 1. Carica i risultati in DevOps Analytics*

## Definizione dei gate {{site.data.keyword.DRA_short}} nella pipeline
{: #toolchain_pipeline_gates}

I gate {{site.data.keyword.DRA_short}} verificano se i tuoi risultati di test soddisfano la politica definita. Se la politica non viene soddisfatta, il gate {{site.data.keyword.DRA_short}} ha un malfunzionamento. Normalmente, i gate sono posizionati alla fine di ogni fase della tua pipeline. Questa ubicazione è ideale per controllare la qualità della build nella tua politica per assicurati che sia sicura da promuovere da un ambiente a un altro. Tuttavia, puoi posizionare i gate ovunque nella pipeline in cui desideri che venga controllato un criterio specifico.

1. Nella fase, fai clic sull'icona **Configurazione fase** ![Icona configurazione fase della pipeline](images/pipeline-stage-configuration-icon.png) e fai clic su **Configura fase**.
2. Fai clic su **Aggiungi lavoro**. Per il tipo di lavoro, seleziona **Test**.
3. Immetti un nome per il nuovo lavoro, come ad esempio *Gate (Unit Test)*.
4. Per il tipo di tester, seleziona **Gate {{site.data.keyword.DRA_short}}**.
5. Specifica il nome dell'ambiente. Assicurati che questo valore corrisponda al valore che è stato definito nelle tue [proprietà di ambiente](#toolchain_pipeline_props).
6. Definisci il nome della politica che deve essere verificata in questo gate.

 Questo nome deve corrispondere esattamente a uno dei nomi della politica che hai definito. Puoi specificare solo politiche definite nella stessa organizzazione {{site.data.keyword.Bluemix_notm}} della tua toolchain.

7. Facoltativo: per passare una funzione gate ella modalità advisory, annulla la spunta della casella **Arrestare l'esecuzione di questa fase se il lavoro non riesce**. Nella modalità advisory, {{site.data.keyword.DRA_short}} completa le stesse analisi della politica nel gate e genera i report, ma se incontra un malfunzionamento, la pipeline non viene arrestata.
8. Fai clic su **Salva** per ritornare alla pipeline.
9. Configura i gate per tutte le politiche {{site.data.keyword.DRA_short}} ripetendo questi passi.

![Lavoro Mocha Deployment Risk Analytics](images/DRA_gate_job.png)
*Figura 2. Gate DevOps Analytics*

Dopo aver configurato la tua pipeline, inizia ad utilizzare {{site.data.keyword.DRA_short}}. Per le istruzioni, consulta [Esecuzione della Delivery Pipeline](./pipeline_decision_reports.html#toolchain_reports).
