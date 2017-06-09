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

# Introduzione a DevOps Insights (Beta)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} applica le analisi dello sviluppatore, del team e di distribuzione ai tuoi progetti DevOps più impegnati. Utilizzalo per imparare quanto il tuo team è conforme con le procedure DevOps e dello sviluppatore, per gestire il rischio nei tuoi codici di base e per applicare automaticamente gli standard di qualità nei progetti di fornitura continua.
{:shortdesc}

{{site.data.keyword.DRA_short}} comprende molti gruppi di funzionalità:

   * Developer Insights fornisce un modo completo di esplorare la maturità dello sviluppo del tuo progetto. Puoi identificare i file con alta tendenza all'errore e ottenere una vista di conformità del progetto per le procedure dello sviluppatore.

   * Team Dynamics utilizza le analisi di codifica social per aiutarti a capire come il tuo team collabora e come può funzionare in modo migliore.

   * Deployment Risk è come una rete di sicurezza di fornitura continua. Analizza i risultati dagli strumenti di verifica di unità, di test funzionali, di scansioni dell'applicazione e di copertura del codice nei gate specificati nel tuo processo di distribuzione e previene il rilascio di modifiche rischiose.

   * Delivery Insights mostra le metriche, le statistiche di distribuzione e altre informazioni sulla tua installazione di IBM UrbanCode Deploy. Ad esempio, può mostrare i grafici della durata della distribuzione, degli esiti positivi e negativi, tutti elencati per ambienti raggruppati logicamente. Consulta [Integrazione di DevOps Insights con IBM UrbanCode Deploy](/docs/services/DevOpsInsights/uc_insights_overview.html).

{{site.data.keyword.DRA_short}} è un'integrazione nel catalogo delle toolchain aperte Bluemix. Per ulteriori informazioni sulle toolchain, vedi [Gestione delle toolchain](/docs/services/ContinuousDelivery/toolchains_working.html).

Per utilizzare {{site.data.keyword.DRA_short}}, devi aggiungerlo a una toolchain. Molti template toolchain già includono {{site.data.keyword.DRA_short}}. Assicurati anche di [aggiungerlo alla tua organizzazione {{site.data.keyword.Bluemix_notm}} come un servizio](/docs/services/reqnsi.html) in modo da poter visualizzare le informazioni su {{site.data.keyword.DRA_short}} e accedere ad alcuni template toolchain che lo includono dal tuo dashboard {{site.data.keyword.Bluemix_notm}}.  

## Aggiunta di DevOps Insights a una toolchain
{: #catalog}

{{site.data.keyword.DRA_short}} fa parte di {{site.data.keyword.contdelivery_short}}. Puoi aggiungere {{site.data.keyword.DRA_short}} a qualsiasi toolchain selezionandolo dal catalogo di integrazione dello strumento.

{{site.data.keyword.DRA_short}} fa anche parte di molti template toolchain. Se crei una toolchain da un template che include {{site.data.keyword.DRA_short}}, assicurati che {{site.data.keyword.DRA_short}} sia impostato su **Advanced**. Quindi, crea la toolchain e passa a [Utilizzo di Insights](/docs/services/DevOpsInsights/index.html#using).

Per aggiungere {{site.data.keyword.DRA_short}} a una toolchain:

1. Fai clic su **Add a Tool**.

2. Fai clic su **{{site.data.keyword.DRA_short}}**.

3. Fai clic su **Create Integration**.

{{site.data.keyword.DRA_short}} è ora disponibile nella pagina della panoramica della tua toolchain. Il tuo sistema di traccia dei problemi e quello di repository vengono scansionati automaticamente per rilevare se sono presenti eventuali dati. 

## Utilizzo di DevOps Insights
{: #using}

Se la tua toolchain include GitHub, GitLab o JIRA, {{site.data.keyword.DRA_short}} ti fornisce automaticamente le informazioni sul tuo codice di base e sul team dopo la raccolta e l'analisi di alcuni dati iniziali. Se la tua toolchain non include alcuna di queste integrazioni, aggiungine una e segui quindi questa procedura:

1. Dalla pagina della panoramica della tua toolchain, fai clic su **{{site.data.keyword.DRA_short}}**.

2. Fai clic su **Team Dynamics** o **Developer Insights** e scegli quindi una categoria di dati. 

3. Esplora i dati del tuo progetto visualizzando i dashboard nella categoria dei dati. Se desideri avere ulteriori informazioni su un grafico o su cosa puoi fare con queste informazioni, fai clic su **Information** o **Guidance**.

Dopo aver esplorato Team Dynamics e Developer Insights, [configura Deployment Risk](/docs/services/DevOpsInsights/insights_risk.html) per aiutarti nell'applicazione della qualità del codice. Deployment Risk è compatibile sia con {{site.data.keyword.contdelivery_short}} pipeline che con Jenkins.   
