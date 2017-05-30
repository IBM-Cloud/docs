---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gestione delle risorse nei tuoi ambienti
{: #managing}

{{site.data.keyword.bplong}} semplifica la gestione dei tuoi ambienti. Puoi modificare le risorse distribuite e ridistribuire ripetutamente le modifiche su richiesta.

{:shortdesc}

Le modifiche al tuo ambiente possono essere distribuite con un processo leggero. Se vuoi modificare quali risorse vengono assegnate, codifichi le modifiche alla tua configurazione nella sintassi dichiarativa, vale a dire che indichi solo il risultato desiderato. Con {{site.data.keyword.bpshort}}, puoi visualizzare in anteprima le modifiche prima della distribuzione.


## Aggiornamento delle risorse con la GUI
{: #gui}

Se preferisci una vista grafica per gestire le risorse nel tuo ambiente, puoi utilizzare il dashboard {{site.data.keyword.bpshort}}.
{:shortdesc}

Dopo aver pubblicato le modifiche di codice nella tua configurazione in GitHub o modificato le variabili nella GUI, completa la seguente procedura per distribuire gli aggiornamenti al tuo ambiente:

1. Nel dashboard **{{site.data.keyword.bpshort}}**, seleziona **Ambienti**.

2. Fai clic sulla riga dell'ambiente specifico che desideri aggiornare.

3. Fai clic su **Piano** e controlla il tuo log del piano per rilevare la presenza di eventuali errori. L'ambiente rimane bloccato finché il piano non viene applicato o annullato da te o da altri collaboratori nel tuo account {{site.data.keyword.Bluemix_notm}}. 

4. Fai clic su **Applica** per distribuire gli aggiornamenti. 


## Aggiornamento delle risorse con la CLI
{: #cli}

Puoi aggiornare le risorse nel tuo ambiente a livello di programmazione con la CLI {{site.data.keyword.bpshort}}.
{:shortdesc}

Dopo aver pubblicato le modifiche di codice nella tua configurazione in GitHub, completa la seguente procedura per distribuire gli aggiornamenti al tuo ambiente:

1. Esegui il comando `plan`. La CLI {{site.data.keyword.bpshort}} estrae la configurazione aggiornata dell'ambiente da GitHub e fornisce un'anteprima di come differiscano le risorse rispetto alla distribuzione corrente.

  ```
  bx schematics action plan --id ENVIRONMENT_ID
  ```
  {: codeblock}

2. Visualizza l'output del piano nel log di attività.

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

3. Distribuisci il tuo piano eseguendo il comando `apply`. 

  ```
  bx schematics action apply --id ENVIRONMENT_ID
  ```
  {: codeblock}


## Aggiornamento delle risorse con l'API
{: #api}

Puoi gestire le risorse nel tuo ambiente a livello di programmazione con l'API {{site.data.keyword.bpshort}}.
{:shortdesc}

Dopo aver pubblicato le modifiche di codice nella tua configurazione in GitHub, completa la seguente procedura per distribuire gli aggiornamenti al tuo ambiente:

1. Esegui la chiamata `POST v1/environments/<environment_ID>/plan`. L'API {{site.data.keyword.bpshort}} estrae la configurazione aggiornata dell'ambiente da GitHub e la confronta con il file di stato Terraform per mostrare come differiscano le risorse rispetto alla distribuzione corrente.

  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/plan \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}

  Risposta di esempio:
  ```
  {
    "activityid": "<activity_ID>"
  }
  ```
  {: screen}

2. Visualizza l'output del piano nel log di attività.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

3. Distribuisci il tuo piano eseguendo la chiamata `PUT /v1/environments/<environment_ID>/apply`. 

  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/apply \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json' \
  ```
  {: codeblock}


## Controllo delle modifiche ai tuoi ambienti
{: #auditing}

Le configurazioni possono essere controllate nella cronologia delle versioni del tuo repository di controllo sorgente. Per monitorare le distribuzioni al tuo ambiente o per visualizzare i log delle distribuzioni precedenti, {{site.data.keyword.bpshort}} offre le seguenti opzioni per visualizzare i log di controllo.

### Dal dashboard {{site.data.keyword.bpshort}}
{: #auditing-gui}

1. Seleziona la riga dell'ambiente per accedere alla pagina dei dettagli dell'ambiente.

2. Monitora la sezione **Attività recenti**. Puoi anche visualizzare i log cronologici dei piani e delle distribuzioni precedenti.

### Con la CLI {{site.data.keyword.bpshort}}
{: #auditing-cli}

1. Richiama il tuo ID ambiente.

  ```
  bx schematics environment list
  ```
  {: codeblock}

2. Richiama gli ID attività per il tuo ambiente. Gli ID attività vengono assegnati alle azioni plan, apply, destroy e delete. Il seguente comando elenca tutte le attività che sono state eseguite nel tuo ambiente.

  ```
  bx schematics activity list --id ENVIRONMENT_ID
  ```
  {: codeblock}

3. Richiama i dati su una specifica attività, ad esempio chi e quando ha apportato modifiche a un ambiente.

  ```
  bx schematics activity show --id ACTIVITY_ID
  ```
  {: codeblock}

4. Facoltativo: per visualizzare un log dettagliato, come l'output del piano o dell'applicazione, esegui il comando `log`. 

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

### Con l'API {{site.data.keyword.bpshort}}
{: #auditing-api}

1. Richiama il tuo ID ambiente.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
  
  Il corpo della risposta contiene tutti gli ambienti esistenti nel tuo account {{site.data.keyword.Bluemix_notm}}. Individua il valore `id` dello specifico ambiente che vuoi controllare.

2. Richiama gli ID attività per le azioni eseguite nel tuo ambiente.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

3. Richiama una specifica attività per un ambiente. 

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID> \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

4. Controlla un log dettagliato dell'output Terraform.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
