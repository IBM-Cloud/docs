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

# Informazioni su Deployment Risk

{{site.data.keyword.DRA_short}} fornisce un gran numero di informazioni sulle tue distribuzioni, particolarmente a rischio. Puoi utilizzarlo per automatizzare la protezione della qualità nella tua delivery pipeline utilizzando politiche e gate. 
{:shortdesc}

Dopo aver aperto {{site.data.keyword.DRA_short}} dalla tua toolchain, fai clic su **Deployment Risk**. Da lì, puoi ottenere una panoramica delle applicazioni nei tuoi ambienti di produzione e di preparazione ed eseguire il drill down per comprendere la copertura del codice, le prestazioni del test e i report di sicurezza. I dashboard sono automaticamente popolati con le informazioni più recenti dai test {{site.data.keyword.DRA_short}} della tua pipeline.

Puoi utilizzare Deployment Risk per applicare gli standard di qualità nella tua toolchain tramite politiche e gate. Le politiche comprendono le serie di regole; i gate applicano e politiche. Ad esempio, potresti creare una politica "Unit Testing and Test Coverage" che richiede che le le build rispettino gli standard di verifica dell'unità e di copertura del test. Successivamente aggiungi un gate che fa riferimento alla politica al tuo processo di fornitura continua. Le build che non soddisfano la politica vengono arrestate da questo gate. 

## Informazioni sull'integrazione

Deployment Risk si integra con {{site.data.keyword.deliverypipeline}}, che è parte di {{site.data.keyword.contdelivery_full}} e con i progetti Jenkins. Ad alto livello, le istruzioni per l'utilizzo di entrambi sono simili.  

Se si sta utilizzando {{site.data.keyword.deliverypipeline}}, procedi come segue:

1. [Crea le politiche e le regole](risk_policies.html) per {{site.data.keyword.DRA_short}} da gestire.
2. [Prepara le fasi della tua pipeline](risk_cd.html) per l'integrazione con {{site.data.keyword.DRA_short}}.
3. [Crea o modifica i lavori di verifica](risk_cd.html) nella pipeline che carica i risultati in {{site.data.keyword.DRA_short}}.
4. [Aggiungi i gate](risk_cd.html) alla pipeline che effettua le decisioni di promozione basate su quei risultati e sulle tue politiche.
5. Esegui la pipeline e [visualizza i risultati](results.html).

Se stai utilizzando Jenkins, segui questa procedura:

1. [Crea le politiche e le regole](risk_policies.html) per {{site.data.keyword.DRA_short}} da gestire.
2. [Installa e configura il plugin Jenkins](risk_jenkins.html).
3. [Crea i gate e i lavori di verifica come descritto nelle istruzioni del plugin](risk_jenkins.html). I test caricano i risultati in {{site.data.keyword.DRA_short}} per le analisi e i gate utilizzano questi risultati per effettuare decisioni di promozione.
4. Esegui il progetto e [visualizza i risultati](results.html). 

Non importa come crei e distribuisci il tuo codice, i risultati sono gli stessi: le build che soddisfano gli standard saranno spostate oltre i gate Deployment Risk, mentre quelle che non li soddisfano saranno arrestate. 

## Prerequisiti
{: #prerequisites}

Deployment Risk richiede alcune configurazioni oltre a quelle descritte in [Introduzione a {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html).

Per utilizzare Deployment Risk, hai bisogno di due cose:

* Una istanza di {{site.data.keyword.deliverypipeline}} o un progetto Jenkins
* I test che desideri utilizzare per valutare il tuo progetto
