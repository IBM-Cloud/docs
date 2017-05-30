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

# Introduzione a {{site.data.keyword.bpfull_notm}} (Beta)
{: #gettingstarted}

{{site.data.keyword.bplong}} è uno strumento di automazione che puoi utilizzare per definire e distribuire l'infrastruttura cloud come una singola unità e per riutilizzare tali definizioni delle risorse cloud in qualsiasi numero di ambienti.
{:shortdesc}

{{site.data.keyword.bpshort}} utilizza Terraform, di HashiCorp, per codificare l'infrastruttura. I componenti della tua infrastruttura sono suddivisi in singole risorse, che possono essere qualsiasi cosa dall'hardware fisico agli account utente. Astraendo le risorse di alto livello e di basso livello, puoi trattare la tua infrastruttura come tratti il tuo software, ossia come codice.  

Quando lavori con {{site.data.keyword.bpshort}}, scrivi le configurazioni per l'ambiente utilizzando la sintassi dichiarativa. Indichi come vuoi che appaia il tuo ambiente, ad esempio che abbia {{site.data.keyword.virtualmachinesshort}} in produzione. Il servizio confronta la tua configurazione con ciò che Terraform ha creato in precedenza e aggiunge o rimuove le risorse secondo necessità.

{{site.data.keyword.bpshort}} è uno strumento DevOps di collaborazione che fornisce un'unica fonte di verità per l'infrastruttura. Puoi memorizzare le configurazioni dell'ambiente nel controllo del codice sorgente, consentendo al tuo team di condurre revisioni di codice, aggiornare le proprie infrastrutture, tenere traccia delle modifiche tramite la cronologia dei commit e di ripristinare le modifiche più facilmente.

{{site.data.keyword.bpshort}} è disponibile automaticamente a tutti gli utenti nel tuo account {{site.data.keyword.Bluemix_notm}}.


## Creazione di una configurazione
{: #configuration}

Quando crei una configurazione, codifichi le risorse cloud che compongono il tuo ambiente.
{:shortdesc}


Se vuoi provare una configurazione di esempio con {{site.data.keyword.bpshort}}, completa la seguente procedura. Nell'esempio, puoi eseguire il provisioning di una chiave SSH da utilizzare in {{site.data.keyword.BluSoftlayer}}. 

**Nota:** la configurazione di esempio richiede un account {{site.data.keyword.BluSoftlayer}}. Consulta la documentazione sul [collegamento dei tuoi account {{site.data.keyword.Bluemix_notm}} e SoftLayer](../../pricing/linking_accounts.html#unifyingaccounts) se hai un account esistente oppure puoi [registrare un account](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts).

1. Genera una coppia di chiavi SSH in locale.
  ```
  ssh-keygen -t rsa
  ```
  {:codeblock}

2. Suddividi la configurazione di esempio in <a href="https://github.com/IBM-Bluemix/tf-bluemix-ssh-key" target="_blank">GitHub <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>. 

  I seguenti esempi mostrano i diversi tipi di blocchi che si trovano nella configurazione di esempio. Puoi vedere la configurazione completa nel file `main.tf` del repository GitHub.
  
  * Il blocco provider imposta il provider {{site.data.keyword.IBM_notm}} Cloud e le credenziali di accesso.

    ```
    provider "ibmcloud" {
      ibmid                    = "${var.ibmid}"
      ibmid_password           = "${var.ibmidpw}"
      softlayer_account_number = "${var.slaccountnum}"
    }
    ```
    {:screen}
  
  * Il blocco risorsa definisce un componente della tua infrastruttura che, in questo esempio, è una chiave SSH.
  
    ```
    resource "ibmcloud_infra_ssh_key" "ssh_key" {
      label = "${var.key_label}"
      notes = "${var.key_note}"
      public_key = "${var.public_key}"
    }
    ```
    {:screen}
  
  * Il blocco variabile definisce le tue variabili, che per questo esempio puoi immettere nella GUI {{site.data.keyword.bpshort}}.
  
    ```
    variable ibmid {
      type = "string"
      description = "Your IBM-ID."
    }
    ```
    {:screen}
  
  * Il blocco output definisce ciò che viene visualizzato nell'output Terraform dopo che la configurazione viene utilizzata per creare il tuo ambiente e che la risorsa (chiave SSH) viene creata.
  
    ```
    output "ssh_key_id" {
      value = "${ibmcloud_infra_ssh_key.ssh_key.id}"
    }
    ```
    {:screen}
  
Puoi ora creare un ambiente dalla tua configurazione. 

{:codeblock}

## Creazione di un ambiente
{: #environment}

Quando crei un ambiente, punti il servizio alla tua configurazione in modo che il servizio possa estrarre le modifiche del codice più recenti.
{:shortdesc}

Utilizzando la configurazione di esempio, completa la seguente procedura per creare un ambiente.

1. Nel menu, seleziona **Servizi** e quindi **{{site.data.keyword.bpshort}}**. Viene visualizzato il dashboard {{site.data.keyword.bpshort}}.

2. Nel menu di navigazione a sinistra, seleziona **Ambienti** e fai clic su **Crea ambiente** per descrivere le proprietà della tua configurazione. La creazione di un ambiente definisce il modo in cui {{site.data.keyword.bpshort}} esegue il provisioning e l'aggiornamento delle risorse cloud, ma non crea ancora le risorse.

3. Immetti i dettagli relativi al tuo ambiente. La configurazione di esempio richiede i valori elencati nella seguente tabella.

  <table summary="The values that are required so that you can use the sample configuration as the source of your environment.">
  <caption>Tabella 1. I valori che sono richiesti in modo da utilizzare la configurazione di esempio come origine del tuo ambiente.
  </caption>
  <thead>
  <th colspan="1">Impostazione</th>
  <th colspan="1">Descrizione</th>
  </thead>
  <tbody>
  <tr>
  <td>URL controllo sorgente</td>
  <td>Immetti l'URL GitHub in cui hai suddiviso la configurazione di esempio.</td>
  </tr>
  <tr>
  <td>Nome</td>
  <td>Immetti un nome univoco da assegnare al tuo ambiente.</td>
  </tr>
  <td>Versione Terraform</td>
  <td>Immetti la versione di Terraform per garantire che nel tuo ambiente sia eseguita una versione compatibile di Terraform. Per la configurazione di esempio, utilizza la versione <code>0.9.1</code>.</td>
  </tr>
  <tr>
  <td>Variabili</td>
  <td>Puoi definire le variabili nel servizio o sovrascrivere le variabili di ambiente che si trovano nel file <code>.tf</code>. Puoi mascherare le variabili sensibili quando fai clic sull'icona di blocco. Il mascheramento delle variabili impedisce agli altri utenti di visualizzare i valori nascosti nella pagina dei dettagli dell'ambiente.
  <p>
  <p>Aggiungi le variabili e i valori che seguono per lavorare con la configurazione di esempio:
  <ul>
  <li><code>ibmid</code> - Immetti il tuo {{site.data.keyword.ibmid}} completo come valore.</li>
  <li><code>ibmidpw</code> - Immetti la password associata al tuo {{site.data.keyword.ibmid}} e fai clic sull'icona di blocco per mascherare il valore.</li>
  <li><code>slaccountnum</code> - Immetti il tuo numero di account {{site.data.keyword.BluSoftlayer}}.
   <li><code>datacenter</code> - Immetti il data center a cui vuoi distribuire la risorsa chiave SSH. Consulta il <a href="https://github.com/IBM-Bluemix/tf-bluemix-ssh-key/blob/master/README.md" target="_blank">file readme <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per un elenco completo di valori disponibili.</li> 
   <li><code>public_key</code> - Immetti la chiave SSH pubblica. Per copiare la chiave pubblica nei tuoi appunti, puoi eseguire il comando <code>pbcopy < ~/.ssh/id_rsa.pub</code>.
   <li><code>key_label</code> - Identifica la chiave con un nome univoco.
   <li><code>key_note</code> - Facoltativo: aggiungi un testo descrittivo sulla chiave SSH.</ul></td>
   </tr></tbody></table>

4. Quando hai finito di compilare i dettagli dell'ambiente, fare clic su **Crea**. L'ambiente appena creato viene visualizzato. 
5. Per visualizzare un'anteprima delle risorse che vengono fornite o rimosse quando distribuisci il tuo ambiente, fai clic su **Piano**. 
6. Visualizza il log del piano per verificare la presenza di eventuali errori nell'output.  
7. Quando sei pronto a distribuire il tuo ambiente, fai clic su **Applica**. Puoi monitorare il log di applicazione per verificare se la chiave viene distribuita correttamente. Una distribuzione corretta mostra la seguente riga verso la fine dell'output:

  ```
  Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
  ```
  {: screen}

  Puoi anche visualizzare la chiave SSH in [{{site.data.keyword.slportal}}](https://control.bluemix.net/devices/sshkeys).
8. Facoltativo: per rimuovere la chiave SSH e l'ambiente da {{site.data.keyword.Bluemix_notm}}, seleziona **Elimina risorse** dal menu di azioni.

### Operazioni successive
{: #next}

* Per trovare ulteriori informazioni sulla distribuzione dei tuoi ambienti a livello di programmazione, [controlla la CLI o l'API](schematics_deploying.html).
* Per creare le tue proprie configurazioni da zero, controlla <a href="https://ibm-bluemix.github.io/tf-ibm-docs/">{{site.data.keyword.IBM_notm}} Cloud resources <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>. Le risorse {{site.data.keyword.IBM_notm}} Cloud sono disponibili come provider di plug-in Terraform.
