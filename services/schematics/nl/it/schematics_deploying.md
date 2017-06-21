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

# Distribuzione delle risorse ai tuoi ambienti
{: #deploying}

Con {{site.data.keyword.bplong}}, puoi distribuire le tue ultime modifiche del codice dal tuo codice sorgente. Quando distribuisci l'ambiente, stai distribuendo le risorse definite dai tuoi file di configurazione. Puoi quindi gestire il provisioning, le orchestrazioni e il ciclo di vita dell'ambiente dall'interno di  {{site.data.keyword.bpshort}}.
{:shortdesc}

## Distribuzione ai tuoi ambienti con la GUI
{: #gui}

Se preferisci una vista grafica per distribuire il tuo ambiente, puoi utilizzare il dashboard {{site.data.keyword.bpshort}}.
{:shortdesc}


### Prerequisito
{: #gui-prereq}

* Memorizza una configurazione Terraform nel controllo sorgente. Le configurazioni possono essere scritte in sintassi HCL (HashiCorp Configuration Language) o JSON. Consulta la <a href="https://www.terraform.io/docs/configuration/index.html">documentazione sulla configurazione Terraform <img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a> per la sintassi HCL e le linee guida su come scrivere le configurazioni. Consulta <a href="https://ibm-bluemix.github.io/tf-ibm-docs/">Provider {{site.data.keyword.IBM_notm}} Cloud <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per le risorse disponibili.

Dopo aver memorizzato la tua configurazione:

1. Nel dashboard **{{site.data.keyword.bpshort}}**, seleziona **Ambienti**.

2. Fai clic su **Crea ambiente** per aggiungere un ambiente o seleziona la riga di un ambiente esistente che vuoi distribuire.

3. Fai clic su **Piano** per visualizzare un'anteprima delle risorse che vengono fornite quando distribuisci il tuo ambiente. Quando esegui il piano, {{site.data.keyword.bpshort}} estrae le variabili nei dettagli del tuo ambiente e l'ultima versione della tua configurazione dal controllo sorgente. L'output del piano mostra come la configurazione viene confrontata con quello che viene distribuito in base al file di stato di Terraform. Nel tuo ambiente vengono bloccate ulteriori modifiche finché il piano non viene applicato all'ambiente o annullato. 

4. Visualizza il log nella sezione **Attività recente** per esaminare l'output del piano. L'output del piano mostra se esistono errori e quali risorse il servizio sta progettando di creare, modificare o eliminare.

5. Quando sei pronto ad avviare il tuo piano, fai clic su **Applica**. Puoi monitorare il log di attività per garantire che il piano sia stato applicato correttamente nell'ultima esecuzione. 


## Distribuzione ai tuoi ambienti con la CLI
{: #cli}

Puoi utilizzare il plug-in {{site.data.keyword.bpshort}} per la CLI {{site.data.keyword.Bluemix_notm}} per distribuire gli aggiornamenti al tuo ambiente.
{:shortdesc}

### Prerequisiti
{: #cli-prereq}

* Memorizza una configurazione Terraform nel controllo sorgente. 
* Se non lo hai già fatto, installa la CLI {{site.data.keyword.Bluemix_notm}} per il tuo sistema operativo dal [Repository CLI {{site.data.keyword.Bluemix_notm}}](http://clis.ng.bluemix.net/ui/home.html).

Dopo aver eseguito l'accesso alla CLI {{site.data.keyword.Bluemix_notm}}:

1. Installa il plug-in della CLI {{site.data.keyword.bpshort}} immettendo il seguente comando.
  
  ```
  bx plugin install schematics -r Bluemix
  ```
  {: codeblock}

  Se l'installazione ha esito positivo, il plug-in {{site.data.keyword.bpshort}} viene visualizzato sotto `bx plugin list`. 

2. Crea un ambiente dalla tua configurazione. Quando crei il tuo ambiente, punti il servizio al tuo controllo sorgente in modo che possa estrarre il codice più recente. 
  
  ```
  bx schematics environment create --file FILE_NAME
  ```
  {: codeblock}
  
  <table summary="Description of the environment create command.">
  <caption>Tabella 1. Descrizione del comando di creazione dell'ambiente.
  </caption>
  <thead>
  <th colspan="1">Comando</th>
  <th colspan="1">Cosa stai facendo</th>
  </thead>
  <tbody>
  <tr>
  <td>--file FILE_NAME</td>
  <td>Il file JSON in cui vengono memorizzati i dettagli sul tuo ambiente.
  <p>
  <p>JSON di esempio:
  <pre>{
      "description": "(Facoltativo) Descrizione dell'ambiente",
      "frozen": false,
      "name": "Nome dell'ambiente",
      "sourceurl": "L'URL GitHub che punta alla configurazione Terraform",
      "tags": ["(Optional) metadata_tag_1", "(Optional) metadata_tag_2"],
      "terraformversion": "0.9",
      "variablestore": [{
          "name": "(Facoltativo) variable_1",
          "secure": false,
          "value": "Valore visibile"
      },
      {
          "name": "(Facoltativo) variable_2_secret",
          "secure": true,
          "value": "Valore protetto"
      }]
  }</pre>
  </td>
  </tr>
  </tbody></table>
  
  Nota il valore `ID` che viene restituito. L'`ID` è un identificativo univoco che viene assegnato al tuo ambiente e viene utilizzato nei comandi successivi.
  
3. Esegui il comando `plan` per visualizzare l'anteprima del modo in cui può cambiare l'ambiente. Il comando plan mostra quali risorse possono cambiare e con quale quantità rispetto a quanto viene distribuito, ma le modifiche non hanno effetto finché non esegui il comando `apply`.
  
  ```
  bx schematics action plan --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
  <table summary="Description of the plan command.">
  <caption>Tabella 2. Descrizione del comando plan.
  </caption>
  <thead>
  <th colspan="1">Comando</th>
  <th colspan="1">Cosa stai facendo</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ENVIRONMENT_ID</td>
  <td>L'ambiente specifico per cui vuoi eseguire un piano di esecuzione. Puoi eseguire <code>bx schematics list</code> se hai bisogno di richiamare il valore per l'ID ambiente.
  </td>
  </tbody></table>
  
  Un `activity_id` viene assegnato al piano e registrato nel log di attività. 

4. Richiama il log di attività per visualizzare l'output del piano Terraform.

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

  <table summary="Description of the log command.">
  <caption>Tabella 3. Descrizione del comando log.
  </caption>
  <thead>
  <th colspan="1">Comando</th>
  <th colspan="1">Cosa stai facendo</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ACTIVITY_ID</td>
  <td>L'attività specifica per cui vuoi visualizzare il log. Puoi eseguire <code>bx schematics activity list --id ENVIRONMENT_ID</code> se hai bisogno di richiamare il valore per l'ID attività.
  </td>
  </tbody></table>
  
5. Esegui il comando `apply` per distribuire le risorse al tuo ambiente.
  
  ```
  bx schematics action apply --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
  <table summary="Description of the apply command.">
  <caption>Tabella 4. Descrizione del comando apply.
  </caption>
  <thead>
  <th colspan="1">Comando</th>
  <th colspan="1">Cosa stai facendo</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ENVIRONMENT_ID</td>
  <td>L'ambiente specifico a cui vuoi distribuire gli aggiornamenti. Puoi eseguire <code>bx schematics list</code> se hai bisogno di richiamare il valore per l'ID ambiente.
  </td>
  </tbody></table>
  
6. Monitora l'output di applicazione per garantire che la distribuzione sia riuscita. 

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

  Una distribuzione corretta restituisce la seguente riga verso la fine dell'output.
  
  ```
  Apply complete! Resources: N added, N changed, N destroyed.
  ```
  {: screen}
  
## Distribuzione ai tuoi ambienti con l'API
{: #api}

Puoi distribuire il tuo ambiente a livello di programmazione con l'API {{site.data.keyword.bpshort}}.
{:shortdesc}

Richiama l'<a href="https://us-south.schematics.bluemix.net/swagger-api/">API {{site.data.keyword.bpshort}} <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per puntare al seguente endpoint di base:

```
https://us-south.schematics.bluemix.net
```
{: codeblock}

### Prerequisito
{: #api-prereq}

* Memorizza una configurazione Terraform nel controllo sorgente. 

Completa la seguente procedura per distribuire le risorse al tuo ambiente:

1. Genera un token IAM OAuth da utilizzare nella tua intestazione di autenticazione. Il comando restituisce un token UAA e un token IAM.
  
  ```
  bx iam oauth-tokens
  ```
  {: codeblock}
  
  Output di esempio:
  ```
  IAM token:  Bearer eyJraWQ...
  ```
  {: screen}
    
  L'output `Bearer eyJraWQ...` è un esempio troncato del token IAM. Includi il token completo nell'intestazione delle tue chiamate API.
  
2. Crea un ambiente eseguendo una chiamata `POST v1/environments`.

  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments \
    -H 'accept: text/plain' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json' \
    -d '{
    "description": "(Facoltativo) Descrizione dell'ambiente",
    "frozen": false,
    "name": "Nome dell'ambiente",
    "sourceurl": "L'URL GitHub che punta alla configurazione Terraform",
    "tags": [
      "(Facoltativo) metadata_tag_1",
      "(Facoltativo) metadata_tag_2"
    ],
    "terraformversion": "0.9",
    "variablestore": [{
        "name": "(Facoltativo) variable_1",
        "secure": false,
        "value": "Valore visibile"
    },
    {
        "name": "(Facoltativo) variable_2_secret",
        "secure": true,
        "value": "Valore protetto"
    }]
  }'
  ```
  {: codeblock}
    
  Una risposta positiva restituisce il seguente output.
  ```
  {
    "id": "ID ambiente",
    "name": "Nome ambiente",
    "description": "Descrizione dell'ambiente",
    "account": "GUID account {{site.data.keyword.Bluemix_notm}}",
    "owner": "L'ID IBM dell'utente che ha creato l'ambiente",
    "creationtime": "AAAA-MM-GGTHH:MM:SSZ",
    "status": "CREATO",
    "frozen": false,
    "sourceurl": "L'URL GitHub che punta alla configurazione",
    "statefile": "Il riferimento al file di stato Terraform",
    "terraformversion": "0.9",
    "tags": [
      "metadata_tag_1",
      "metadata_tag_2"
    ],
    "variablestore": [
      {
        "name": "(Facoltativo) variable_1",
        "value": "Valore visibile"
      }
    ]
  }
  ```
  {: screen}
    
  Nota il valore `id` che viene restituito. L'`id` è un identificativo univoco che viene assegnato al tuo ambiente e viene utilizzato nelle chiamate successive.
  
3. Esegui la chiamata `POST v1/environments/<environment_ID>/plan` per visualizzare in anteprima quali risorse saranno distribuite al tuo ambiente quando applichi la configurazione. I piani estraggono le configurazioni di ambiente nel ramo master del tuo repository.
  
  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/plan \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}
  
  Una risposta positiva restituisce un `activityid`. Il valore ID attività è necessario per visualizzare i log, come ad esempio l'output del piano e dell'applicazione.
  ```
  {
    "activityid": "<activity_ID>"
  }
  ```
  {: screen}

4. Esegui la chiamata `GET v1/environments/<environment_ID>/activities/<activity_ID>/log` per visualizzare l'output del piano.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

5. Distribuisci il tuo ambiente eseguendo la chiamata `PUT v1/environments/<environment_ID>/apply/`.
  
  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/apply \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}
  
6. Monitora la distribuzione eseguendo la chiamata `GET v1/environments/<environment_ID>/activities/<activity_ID>/log` per visualizzare l'output di applicazione.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

  Una distribuzione corretta restituisce la seguente riga verso la fine dell'output.
  
  ```
  Apply complete! Resources: N added, N changed, N destroyed.
  ```
  {: screen}
