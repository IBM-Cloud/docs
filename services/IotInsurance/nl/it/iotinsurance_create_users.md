---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Creazione di utenti e associazioni scudo
{: #gettingstartedtemplate}
Ultimo aggiornamento: 15 settembre 2016
{: .last-updated}

Dopo aver creato il servizio {{site.data.keyword.iotinsurance_short}} e distribuito i servizi e le applicazioni di supporto richiesti, puoi verificare il servizio creando un utente autorizzato e un'associazione scudo.
{:shortdesc}

**Prerequisiti:** prima di iniziare, assicurati che siano implementati i seguenti prerequisiti:

- [Node.js](https://nodejs.org/en/) installato sul tuo computer.  
- Un ambiente di runtime abilitato con Node.js come Eclipse.
- Software Git e accesso a [GitHub source code repository for the API examples](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs).   In alternativa, puoi scaricare l'[archivio con i file del codice di origine](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/archive/master.zip).
- Codice di origine pronto.  
  Per preparare il codice di origine, completa la seguente procedura:
  1. Clona o scarica il [GitHub source code repository](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs) sul tuo computer.
  2. Installa i prerequisiti open source del progetto utilizzando un prompt dei comandi per andare alla cartella che contiene i file del codice di origine clonati ed esegui il comando `npm install`.

Crea un utente che puoi utilizzare per verificare le funzioni del dashboard e l'applicazione mobile di esempio.

1. Crea un utente nel sistema {{site.data.keyword.iotinsurance_short}}.
  1. Modifica il file createUser.js per sostituire i valori nella variabile **user** con informazioni utente univoche.
  2. Salva il file.
  3. Esegui `node createUser.js`. Il processo necessità di alcuni minuti per essere completato.
  4. Prendi nota del nome utente; è necessario nel prossimo passo.
2. Crea un'associazione scudo per l'utente.
  1. Modifica il file createUserShieldAssociation.js per aggiungere il nome utente dal passo precedente nella variabile **username**.
  2. Salva il file.
  3. Esegui `node createUserShieldAssociation.js`. Per ulteriori informazioni sugli scudi, consulta [Componenti](iotinsurance_overview.html#components).
3. (facoltativo) Il motore di analisi viene aggiornato automaticamente; tuttavia, se non vengono visualizzati i dati corretti, puoi aggiornare il motore di analisi eseguendo `node updateAnalyticsEngine.js`.
4. (facoltativo) Simula un evento pericoloso per l'utente.
  1. Modifica il file simulateHazard.js per aggiungere il nome utente dai passi precedenti nella variabile **usr**.
  2. Salva il file.
  3. Esegui `node simulateHazard.js`.
5. (facoltativo) Crea una serie di dati cronologici simulati eseguendo `node createHistoricalData.js`.


# Link correlati
{: #rellinks}

## Riferimento API
{: #api}
* [Esempi API {{site.data.keyword.iotinsurance_short}}](https://iot4i-docs-api.mybluemix.net/dist/){:new_window}

## Link correlati
{: #general}
* [Developer support forum](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Stack overflow support forum](http://stackoverflow.com/questions/tagged/ibm-bluemix)
