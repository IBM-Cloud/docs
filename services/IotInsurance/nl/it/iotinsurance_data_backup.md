---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-22"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->

# Backup dei dati
Puoi eseguire il backup dei tuoi dati {{site.data.keyword.iotinsurance_full}} replicando il database {{site.data.keyword.cloudantfull}}.
{:shortdesc}

La seguente tabella mostra i database {{site.data.keyword.iotinsurance_short}} archiviati in {{site.data.keyword.iotinsurance_full}}.

*Tabella 1: Database {{site.data.keyword.iotinsurance_short}}*

Nomi database| Frequenza di modifica| Motivo della modifica | Richiede il backup | Commenti
------------- | -------------| -------------| -------------| -------------
favorites|Gestione|Nuova azione dell'amministratore|SÍ|-
Devices|Gestione|Aggiunti o rimossi nuovi dispositivi o utenti|SÍ| Il trasformatore genera dinamicamente una tabella nella memoria e la compila con i dati dal provider del dispositivo. Per i gateway collegati direttamente, questa tabella archivia i dispositivi.
hazardevents|Casuale|Individuato nuovo evento scudo|SÍ|-
Jscode|Gestione|Distribuito nuovo codice JS per gli scudi|SÍ*| L'amministratore può facoltativamente saltare il backup e distribuire una nuova versione del codice JS.
Promotions|Gestione|Aggiunta nuova promozione|SÍ|-
shieldassociations|Gestione|Aggiunto nuovo utente o scudo|SÍ|-
Shields|Gestione|Aggiunto nuovo scudo|SÍ|-
Users|Gestione|Aggiunto nuovo utente|SÍ|-
aggregation|-|-|NO|Può essere ricompilato.
aggregationschedule|-|-| NO|Può essere ricompilato.

Per eseguire il backup dei dati {{site.data.keyword.iotinsurance_short}} esegui la seguente procedura:

## Creazione di un'istanza {{site.data.keyword.cloudant_short_notm}} di replica
{: #createinstance}
Crea un'istanza {{site.data.keyword.cloudant}} di replica utilizzando le [{{site.data.keyword.cloudant}}Istruzioni per la replica ![icona link esterno](../../icons/launch-glyph.svg)](https://docs.cloudant.com/replication.html). Per scopi di ripristino di emergenza, crea la replica in una posizione differente rispetto al servizio {{site.data.keyword.iotinsurance_short}} originale. Ad esempio, se la tua istanza originale è a Dallas, la replica potrebbe essere a Londra.

## Individua le credenziali e gli URL
{: #locate_credentials}
Individua le credenziali e gli URL per la tua istanza {{site.data.keyword.cloudant}} originale e per la tua istanza replicata.
1. Apri il servizio {{site.data.keyword.cloudant}}.
2. Fai clic sulla scheda **Credenziali del servizio** ubicata al di sotto del nome del servizio.
3. Fai clic su **Visualizza credenziali**.
4. Prendi nota dell'ID utente e della password.

## Creazione di nuove attività di replica
{: #create_replication}
Crea un'attività di replica per ogni database di cui si deve eseguire il backup. I database che richiedono il backup sono elencati nella Tabella 1 nella precedente sezione.

1. Apri la tua console {{site.data.keyword.Bluemix_notm}}.

2. Apri il servizio {{site.data.keyword.cloudant}} originale.

3. Fai clic su **Avvia** per aprire il dashboard {{site.data.keyword.cloudant}}.

4. Nel menu, seleziona **Replica**.

5. Immetti l'URL del database originale nella sezione Database di origine. Ogni URL del database è nel formato https://<CloudantbaseURL>/<database_name>.  Ad esempio, l'URL del database hazardevents è https://<CloudantbaseURL>/hazardevents.

6. Immetti l'URL del nuovo database nella sezione Database di destinazione.

7. **Importante:** non selezionare **Rendi questa replica continua**.  La replica continua spesso influenza le prestazioni.

8. Fai clic su **Replica i dati**.  

9. (facoltativo) Poiché le attività di replica successive sovrascrivono i dati precedenti, considera di esportare i dati in un file CSV.  Per le istruzioni, consulta [Esporta Cloudant JSON come CSV, RSS o iCal ![icona link esterno](../../icons/launch-glyph.svg)](https://developer.ibm.com/clouddataservices/2015/09/22/export-cloudant-json-as-csv-rss-or-ical/){: new_window}.

10. Ripeti questi passi per ogni database.

## Esecuzione di un backup
{: #run_backup}
Dopo aver creato le attività di replica, puoi rieseguire i backup in qualsiasi momento.
1. Apri la tua console {{site.data.keyword.Bluemix_notm}}.
2. Apri il tuo servizio {{site.data.keyword.cloudant}} originale.
3. Fai clic su **Avvia** per aprire il dashboard {{site.data.keyword.cloudant}}.
4. Nel menu, fai clic su **Replica** e seleziona quindi **Tutte le repliche**.
5. Seleziona tutti i database e riesegui ogni replica. Puoi controllare lo stato dei lavori in corso facendo clic su **Repliche attive**.
6. Quando tutte le repliche sono complete, puoi esportare i dati in un file semplice CSV.

## Ripristino dei dati
{: #restore_data}
Puoi ripristinare i dati da un database replicato o caricando un file CSV salvato.
1. Apri la tua console {{site.data.keyword.Bluemix_notm}}.
2. Arresta il servizio {{site.data.keyword.iotinsurance_short}}.
3. Ripristina i dati in uno dei seguenti modi:
  - Carica direttamente i dati da un file di backup CSV nell'istanza Cloudant principale
  - Crea un'attività di replica che dispone di un database replicato come l'origine e il database originale come la destinazione. Questa attività sposta i dati replicati nel database originale.
4. Esegui i seguenti script per ricreare i documenti di progettazione e ripristinare l'integrità di riferimento.  Gli script sono ubicati in [{{site.data.keyword.iotinsurance_short}} API examples GitHub site ![icona link esterno](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/){: new_window}.
  - iot4i-api/wearable-framework/auto-create/create.sh - Questo script ricrea i documenti di progettazioni all'interno di {{site.data.keyword.cloudant}}.
  - iot4i-api/wearable-framework/health/check-relations - Questo script ristabilisce l'integrità di riferimento. Ad esempio, lo script correggere un caso in cui uno scudo viene eliminato ma l'associazione a un utente ancora esiste.
