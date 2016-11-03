---

copyright:
  years: 2016

---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be surrounded by 3 dashes.
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Gestione delle pipeline
{: #deliverypipeline_managing}
Ultimo aggiornamento: 30 agosto 2016
{: .last-updated}

Puoi gestire, configurare e estendere le integrazioni di IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}}.
{:shortdesc}

Completa le seguenti attività per gestire, configurare e estendere una pipeline.

## Controllo dell'accesso
{: #deliverypipeline_access}

Puoi limitare gli utenti che possono eseguire le fasi o modificare una pipeline. A tal fine, vai alla pagina delle impostazioni della pipeline, che puoi raggiungere facendo clic sull'icona **Configurazione fase** nella pipeline: nella pagina Tutte le fasi.

![L'icona ingranaggio delle impostazioni della pipeline](./images/pipeline_settings.png)

## Risorse e proprietà dell'ambiente
{: #deliverypipeline_envprop}

Puoi utilizzare le proprietà dell'ambiente e le risorse preinstallate per interagire con il servizio {{site.data.keyword.deliverypipeline}}. Ad esempio, puoi incorporarle in uno script del lavoro o in un comando di verifica. Per ulteriori informazioni, consulta [Risorse e proprietà dell'ambiente per il servizio {{site.data.keyword.deliverypipeline}}](./deploy_var.html).

Puoi aggiungere le tue proprie proprietà dell'ambiente a una fase dalla relativa scheda **PROPRIETÀ AMBIENTE**. Le proprietà dell'ambiente sono disponibili per ogni lavoro in una fase.

Puoi aggiungere quattro tipi di proprietà dalla scheda Proprietà ambiente:
* **Testo**: una chiave della proprietà con un valore a singola riga.
* **Area di testo**: una chiave della proprietà con un valore a più righe.
* **Sicurezza**: una chiave della proprietà con un valore a singola riga. Il valore viene visualizzato come degli asterischi.
* **Proprietà**: un file nel repository del progetto. Questo file può contenere più proprietà. Ogni proprietà deve essere sulla propria riga. Per coppie di valore-chiave separate, utilizzare il segno uguale (=).

## Estensione delle funzionalità della tua pipeline
{: #deliverypipeline_extend}

Puoi estendere le funzionalità della pipeline Distribuisci & build configurando i tuoi lavori in modo che utilizzino i servizi supportati. Ad esempio, i lavori di verifica possono eseguire delle scansioni di codice statico e i lavori di creazione possono globalizzare le stringhe.

Per ulteriori informazioni sull'estensione delle funzionalità della pipeline, consulta [Estensione delle funzionalità del servizio {{site.data.keyword.deliverypipeline}}](./deliverypipeline_extension.html).

<!-- [1]: https://www.ng.bluemix.net/docs/manageapps/deployingapps.html#appmanifest
[2]: https://www.ng.bluemix.net/docs/#services/DeliveryPipeline/index.html#getstartwithCD
[3]: http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html#push
[4]: https://console.ng.bluemix.net/?ace_base=true/#/pricing/cloudOEPaneId=pricing
[5]: ./images/open_logs.png
[6]: #manifests
[7]: ./images/runbar-annotated-dark.png
[8]: ./images/input_tab_only_execute.png
[9]: ./images/deploy_to.png
[10]: ./images/view_logs_and_history.png
[11]: ./images/play_button.png
[12]: ./images/basicAnimate.gif
[13]: ./images/AddStage.png
[14]: ./images/AddJob.png
[15]: ./images/jobs.png
[16]: ./images/RunStage.png
[17]: https://www.ng.bluemix.net/docs/starters/container_pipeline.html#container_pipeline
[18]: ../../../tutorials/basicbuild
[19]: #add_stage
[20]: #add_job
[21]: ../deploy_ext
[22]: ./images/pipeline_settings_icon.png
[23]: ./images/pipeline_settings.png
[24]: https://www.ng.bluemix.net/docs/services/reqnsi.html#add_service
[25]: ../deploy_var
[26]: ./images/click_stage_run_number.png
[27]: ./images/diagram.jpg -->
