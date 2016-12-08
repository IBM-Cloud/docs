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
Ultimo aggiornamento: 17 novembre 2016
{: .last-updated}

Puoi gestire, configurare e estendere le integrazioni di IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}}.
{:shortdesc}

Completa le seguenti attività per gestire, configurare e estendere una pipeline.

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

Puoi estendere le funzionalità della pipeline configurando i tuoi lavori per l'utilizzo dei servizi supportati. Ad esempio, i lavori di verifica possono eseguire delle scansioni di codice statico e i lavori di creazione possono globalizzare le stringhe.

Per ulteriori informazioni sull'estensione delle funzionalità della pipeline, consulta [Estensione delle funzionalità del servizio {{site.data.keyword.deliverypipeline}}](./deliverypipeline_extension.html).

