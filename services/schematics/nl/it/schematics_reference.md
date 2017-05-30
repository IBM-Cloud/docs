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

# Plug-in CLI {{site.data.keyword.bpshort}} per la CLI {{site.data.keyword.Bluemix_notm}}
{: #cli}

Fai riferimento ai comandi {{site.data.keyword.bpshort}} per la CLI {{site.data.keyword.Bluemix}} per gestire i tuoi ambienti ed eseguire altre operazioni in {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Prima di utilizzare i comandi della CLI:

* Accedi a {{site.data.keyword.Bluemix_notm}} with `bx login [--sso]` per autenticare la tua sessione. Gli utenti con un ID federato devono utilizzare l'indicatore `--sso` per generare una passcode monouso.

Per visualizzare un elenco di comandi, puoi eseguire `bx schematics help`.

<table id="manage_environments" summary="Manage your environments with the bx schematics environment commands.">
<caption>Tabella 1. Comandi disponibili per gestire il tuo ambiente. I comandi seguono la sintassi <code>bx schematics environment</code>.
</caption>
 <thead>
 <th colspan="5">Gestione del tuo ambiente</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx schematics environment create](#environment-create)</td>
 <td>[bx schematics environment delete](#environment-delete)</td>
 <td>[bx schematics environment list](#environment-list)</td>
 <td>[bx schematics environment show](#environment-show)</td>
 <td>[bx schematics environment update](#environment-update)</td>
 </tr>
</tbody></table>
 
 <table id="update_resources" summary="Update the resources provisioned by your environment with the bx schematics action commands.">
 <caption>Tabella 2. Comandi disponibili per aggiornare le risorse nel tuo ambiente. I comandi seguono la sintassi <code>bx schematics action</code>.
 </caption>
  <thead>
  <th colspan="5">Aggiornamento delle tue risorse</th>
  </thead>
  <tbody>
  <td>[bx schematics action apply](#action-apply)</td>
  <td>[bx schematics action destroy](#action-destroy)</td>
  <td>[bx schematics action plan](#action-plan)</td>
  </tr></tbody></table>
  
  <table id="audit_environment" summary="Auditing activities that ran against your environment with the bx schematics activity commands.">
  <caption>Tabella 3. Comandi disponibili per controllare le attività eseguite nel tuo ambiente. I comandi seguono la sintassi <code>bx schematics activity</code>.
  </caption>
   <thead>
   <th colspan="5">Controllo del tuo ambiente</th>
   </thead>
   <tbody>
   <td>[bx schematics activity list](#activity-list)</td>
   <td>[bx schematics activity log](#activity-log)</td>
   <td>[bx schematics activity planfile](#activity-planfile)</td>
   <td>[bx schematics activity show](#activity-show)</td>
   </tr></tbody></table>

## bx schematics environment create
{: #environment-create notoc}

Crea un ambiente in {{site.data.keyword.Bluemix_notm}} dalla tua configurazione.

```
bx schematics environment create --file FILE_NAME [--json]
```
{: codeblock}

### Parametri

<dl>
<dt>--file FILE_NAME</dt>
<dd>Il file JSON utilizzato per passare i dettagli sul tuo ambiente.
<p>
<p>JSON di esempio con tutti i valori disponibili:
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
}</pre></dd>
<dt>--json</dt>
<dd>Stampa l'output in formato JSON.</dd>
</dl>

## bx schematics environment delete
{: #environment-delete notoc}

Rimuovi la configurazione del tuo ambiente da {{site.data.keyword.Bluemix_notm}}. Questo comando è consigliato solo per ambienti senza risorse in esecuzione. Se elimini un ambiente con delle risorse in esecuzione, devi gestire ogni risorsa nei singoli dashboard del servizio.

```
bx schematics environment delete --id ENVIRONMENT_ID [--force]
```
{: codeblock}

### Parametri

<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>L'identificativo univoco dell'ambiente. Puoi richiamare questo valore eseguendo <code>bx schematics environment list</code>.</dd>
<dt>--force</dt>
<dd>Forza l'avanzamento del comando senza una conferma sì/no.</dd>
</dl>

## bx schematics environment list
{: #environment-list notoc}

Richiama un elenco di tutti gli ambienti esistenti nel tuo account {{site.data.keyword.Bluemix_notm}}.

```
bx schematics environment list [--count VALUE] [--offset VALUE] [--json] 
```
{: codeblock}

### Parametri
<dl>
<dt>--count VALUE</dt>
<dd>Il numero di ambienti da limitare nella restituzione.</dd>
<dt>--offset VALUE</dt>
<dd>L'offset nell'elenco di ambienti.</dd>
<dt>--json</dt>
<dd>Stampa l'output in formato JSON.</dd>
</dl>

## bx schematics environment show
{: #environment-show notoc}

Richiama i dettagli su un ambiente esistente.

```
bx schematics environment show --id ENVIRONMENT_ID [--json]
```
{: codeblock}

### Parametri
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>L'identificativo univoco dell'ambiente. Puoi richiamare questo valore eseguendo <code>bx schematics environment list</code>.</dd>
<dt>--json</dt>
<dd>Stampa l'output in formato JSON.</dd>
</dl>
  
## bx schematics environment update
{: #environment-update notoc}

Aggiorna i dettagli su un ambiente esistente, come il nome ambiente o l'URL GitHub. Per aggiornare il numero di risorse assegnate nell'ambiente, vedi [bx schematics action plan](#action-plan).

```
bx schematics environment update --id ENVIRONMENT_ID --file FILE_NAME [--json]
```
{: codeblock}

### Parametri
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>L'identificativo univoco dell'ambiente. Puoi richiamare questo valore eseguendo <code>bx schematics environment list</code>.</dd>
<dt>--file FILE_NAME</dt>
<dd>Il file JSON utilizzato per passare i dettagli sul tuo ambiente. Vedi [bx schematics environment create](#environment-create) per un frammento JSON di esempio con i valori consentiti.</dd>
<dt>--json</dt>
<dd>Stampa l'output in formato JSON.</dd>
</dl>

## bx schematics action apply
{: #action-apply notoc}

Distribuisci la configurazione del tuo ambiente. Il comando `apply` scansiona ed esegue le configurazioni memorizzate nel tuo repository GitHub.

```
bx schematics action apply --id ENVIRONMENT_ID [--force] [--json]
```
{: codeblock}

### Parametri
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>L'identificativo univoco dell'ambiente. Puoi richiamare questo valore eseguendo <code>bx schematics environment list</code>.</dd>
<dt>--force</dt>
<dd>Forza l'avanzamento del comando senza una conferma sì/no.</dd>
<dt>--json</dt>
<dd>Salva l'output dell'applicazione in formato JSON.</dd>
</dl>

## bx schematics action destroy
{: #action-destroy notoc}

Elimina il tuo ambiente e le tue risorse. Il comando `destroy` elimina il tuo ambiente, incluse le risorse in esecuzione. Questa azione viene utilizzata tipicamente solo per gli ambienti temporanei, ad esempio un ambiente QA, con l'intento di supportare l'ambiente per un periodo limitato. Non è consigliata l'eliminazione degli ambienti di produzione. L'azione `destroy` non può essere annullata e deve essere utilizzata con cautela.

```
bx schematics action destroy --id ENVIRONMENT_ID [--force] [--json]
```
{: codeblock}

### Parametri
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>L'identificativo univoco dell'ambiente. Puoi richiamare questo valore eseguendo <code>bx schematics environment list</code>.</dd>
<dt>--force</dt>
<dd>Forza l'avanzamento del comando senza una conferma sì/no.</dd>
<dt>--json</dt>
<dd>Salva l'output dell'eliminazione in formato JSON.</dd>
</dl>
</dl>

## bx schematics action plan
{: #action-plan notoc}

Confronta la tua configurazione dell'ambiente con la configurazione distribuita. Il comando `plan` scansiona la configurazione nel tuo repository GitHub ed esegue un comando diff sul file di stato associato al tuo ambiente distribuito. L'output del piano mostra quali risorse verranno aggiunte o rimosse se hai distribuito la tua configurazione dell'ambiente con il comando `apply`. 

```
bx schematics action plan --id ENVIRONMENT_ID [--file FILE_NAME] [--json]
```
{: codeblock}

### Parametri
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>L'identificativo univoco dell'ambiente. Puoi richiamare questo valore eseguendo <code>bx schematics environment list</code>.</dd>
<dt>--file FILE_NAME</dt>
<dd>Il file JSON facoltativo utilizzato per passare i parametri per l'azione del piano. Puoi passare il parametro <code>sourcesha</code> per fare riferimento a uno specifico ramo Git per la configurazione Terraform dell'ambiente. Il ramo Git deve essere specificato come riferimento head, ad esempio <code>refs/heads/BRANCH_NAME</code>. Se nessun parametro viene specificato, il valore predefinito è l'intestazione del ramo master, ossia <code>refs/heads/master</code>.
<p>
<p>Frammento JSON di esempio con valore:
<pre>{
  "sourcesha": "refs/heads/BRANCH_NAME"
}</pre></dd>
<dt>--json</dt>
<dd>Salva l'output del piano in formato JSON.</dd>
</dl>

## bx schematics activity list
{: #activity-list notoc}

Elenca i dati provenienti dalle attività Terraform eseguite in un ambiente.

```
bx schematics activity list --id ENVIRONMENT_ID [--count VALUE] [--offset VALUE] [--json]
```
{: codeblock}

### Parametri
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>L'identificativo univoco dell'ambiente. Puoi richiamare questo valore eseguendo <code>bx schematics environment list</code>.</dd>
<dt>--count VALUE</dt>
<dd>Il numero di attività da restituire. </dd>
<dt>--offset VALUE</dt>
<dd>L'offset nell'elenco.</dd>
<dt>--json</dt>
<dd>Salva l'output del piano in formato JSON.</dd>
</dl>

## bx schematics activity log
{: #activity-log notoc}

Visualizza i log di attività dettagliati per le azioni eseguite in un ambiente.

```
bx schematics activity log --id ACTIVITY_ID
```
{: codeblock}

### Parametri
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>L'indicatore per restituire i dettagli su una specifica attività. Puoi richiamare un elenco di ID attività per ogni ambiente con il comando <code>bx schematics activity list --id ENVIRONMENT_ID</code>.</dd>
</dl>

## bx schematics activity planfile
{: #activity-planfile notoc}

Visualizza i file di piano per un ambiente.

```
bx schematics activity planfile --id ACTIVITY_ID
```
{: codeblock}

### Parametri
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>L'indicatore per restituire i dettagli su una specifica attività. Puoi richiamare un elenco di ID attività per ogni ambiente con il comando <code>bx schematics activity list --id ENVIRONMENT_ID</code>.</dd>
</dl>

## bx schematics activity show
{: #activity-show notoc}

Richiama i dettagli di una specifica attività eseguita in un ambiente.

```
bx schematics activity show --id ACTIVITY_ID [--json]
```
{: codeblock}

### Parametri
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>L'indicatore per restituire i dettagli su una specifica attività. Puoi richiamare un elenco di ID attività per ogni ambiente con il comando <code>bx schematics activity list --id ENVIRONMENT_ID</code>.</dd>
<dt>--json</dt>
<dd>Salva l'output del piano in formato JSON.</dd>
</dl>
