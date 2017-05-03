---

copyright:
  years: 2017
lastupdated: "2017-02-06"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Risoluzione dei problemi per SDK for Nodejs
{: #ts}


Sono qui riportate le risposte alle domande comuni di risoluzione dei problemi sull'utilizzo di SDK for Nodejs su {{site.data.keyword.Bluemix}}.
{:shortdesc}

## Impossibile avviare l'applicazione con un errore “Mancanza di spazio sul dispositivo”
{: #no_space_left_on_device}


Impossibile avviare un'applicazione Nodejs  con un errore “Mancanza di spazio sul dispositivo”. Ad esempio, l'errore nei log può essere simile al seguente:
{: tsSymptoms}

```
   2017-01-16T14:25:14.61-0500 [CELL/0]     ERR tar: ./app/node_modules/pm2/node_modules/cron/node_modules/moment-timezone/LICENSE: Cannot write: No space left on device

```
{: #codeblock}

Le applicazioni Nodejs che utilizzano le versioni di NPM precedenti alla 3 utilizzano più spazio per lo scaricamento delle dipendenze.
{: tsCauses}

Modifica il file package.json della tua applicazione per utilizzare la versione 3 di NPM o una superiore.
{: tsResolve}

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "3.10.10"
  }
}
```
{: codeblock}
