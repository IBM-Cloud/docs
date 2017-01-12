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

# Introduzione a {{site.data.keyword.DRA_short}} (sperimentale)
{: #gettingstarted}

Utilizza {{site.data.keyword.DRA_full}} per identificare i rischi per le tue build e distribuzioni.
{:shortdesc}

{{site.data.keyword.DRA_short}} aggrega e analizza i risultati dagli strumenti di verifica di unità, di test funzionali e di copertura del codice per determinare se il tuo codice soddisfa le politiche predefinite nei gate specificati nel tuo processo di distribuzione. Se il tuo codice non soddisfa o supera una politica, la distribuzione viene arrestata, per prevenire che vengano rilasciati dei rischi. Puoi utilizzare {{site.data.keyword.DRA_short}} come una rete di sicurezza per il tuo ambiente di fornitura continua, come un modo per implementare e migliorare gli standard nel tempo e come uno strumento di visualizzazione dei dati per aiutarti nella comprensione dello stato del tuo progetto.

{{site.data.keyword.DRA_short}} è un'offerta sperimentale e viene fornita nello stato in cui è soltanto per scopi di sperimentazione e sviluppo. Per utilizzare {{site.data.keyword.DRA_short}}, aggiungilo a una qualsiasi toolchain che utilizza la {{site.data.keyword.deliverypipeline}}.

{: #catalog}
Per accedere alla IU {{site.data.keyword.DRA_short}}, completa le seguenti istruzioni da una toolchain esistente:

1. Fai clic sul pulsante **Add a Tool**.

2. Fai clic su **{{site.data.keyword.DRA_short}}**.

3. Fai clic su **Create Integration**.

4. Fai clic sul tile **{{site.data.keyword.DRA_short}}**.

5. Completa la tua configurazione con le rimanenti attività:

	1. [Configura la tua integrazione {{site.data.keyword.deliverypipeline}}](./pipeline_integration.html).
	2. Avvia la pipeline e [controlla i dashboard {{site.data.keyword.deliverypipeline}}](./pipeline_decision_reports.html).
	3. [Definisci le politiche](./create_criteria.html) per {{site.data.keyword.DRA_short}} da gestire.
	4. Esegui di nuovo la pipeline per verificare che il tuo progetto superi le tue politiche.


# Link correlati
{: #rellinks}

## Esercitazioni ed esempi
{: #samples}

* [Utilizzo delle analisi per essere avvisati sulle probabilità di distribuzioni con esito positivo](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){:new_window}

## Link correlati
{: #general}

* [Introduzione alle toolchain](https://new-console.ng.bluemix.net/docs/toolchains/toolchains_overview.html){:new_window}
* [Introduzione a Delivery Pipeline](https://new-console.ng.bluemix.net/docs/services/DeliveryPipeline/index.html){:new_window}
* [Listino prezzi di IBM Bluemix](https://new-console.ng.bluemix.net/pricing/){:new_window}
* [Prerequisiti IBM Bluemix](https://developer.ibm.com/bluemix/support/?cm_mc_uid=96503159749414585876298&cm_mc_sid_50200000=1462802909#prereqs){:new_window}
