---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Integrazione OpenWhisk con Serverless Framework
{: #openwhisk_goserverless}

[Serverless Framework](https://serverless.com/) è un framework open-source per la creazione di applicazioni senza server. Utilizzando un file manifest singolo, gli sviluppatori possono definire le funzioni senza server, collegarle alle origini dell'evento e dichiarare i servizi cloud necessari alle loro applicazioni. Il framework gestisce la distribuzione di queste applicazioni senza server ai provider cloud. Consente inoltre agli sviluppatori di monitorare i servizi in produzione, eseguire il rollout degli aggiornamenti e fornire assistenza nel debug dei problemi. Dispone inoltre di un ecosistema vibrante di plugin di terze parti per estendere la funzionalità del framework. Qui è dove entra OpenWhisk.
{:shortdesc}

OpenWhisk ha [il proprio plugin del provider per Serverless Framework](https://github.com/serverless/serverless-openwhisk). Gli sviluppatori che utilizzano Serverless Framework possono scegliere di distribuire le loro applicazioni ad ogni istanza della piattaforma di OpenWhisk (ospitata in Bluemix o su altri cloud o in privato). Il supporto a più provider significa che lo spostare le applicazioni tra le piattaforme è più facile e gli sviluppatori possono sviluppare applicazioni senza server a più cloud.

## Introduzione
{: #openwhisk_goserverless_starting}

Questo è il Serverless Framework ufficiale [Getting Started Guide for OpenWhisk](https://serverless.com/framework/docs/providers/openwhisk/guide/intro/) - che copre l'installazione, lo sviluppo del flusso di lavoro, le procedure consigliate, la guida dettagliata per la creazione e la distribuzione di un applicazione OpenWhisk funzionante e altro.

[Questo video](https://youtu.be/GJY10W98Itc) illustra come utilizzare Serverless Framework con il plugin del provider OpenWhisk.
## Documentazione
{: #openwhisk_goserverless_docs}

L'ultima documentazione su come utilizzare OpenWhisk con Serverless Framework [può essere trovata qui](https://serverless.com/framework/docs/providers/openwhisk/).
## Esempi
{: #openwhisk_goserverless_samples}
[Serverless Framework examples GitHub repository](https://github.com/serverless/examples) ora le funzioni OpenWhisk ti mostrano come creare le API HTTP, le pianificazioni basate su cron, le funzioni di concatenamento e altro ancora.
