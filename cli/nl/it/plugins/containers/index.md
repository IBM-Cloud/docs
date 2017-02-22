---



copyright:

  years: 2015, 2017

lastupdated: "2017-01-12"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# CLI IBM Containers
{: #containercli}

*Versione:* 1.0.0

La CLI IBM Containers è un plug-in della CLI {{site.data.keyword.Bluemix_notm}} per gestire i contenitori e gruppi di contenitori in Bluemix.
{: shortdesc}

**Nota:** i *Prerequisiti* elencano quali azioni sono richieste prima di utilizzare il comando. I comandi che non hanno azioni prerequisite elencano **Nessuno**. Altrimenti, i prerequisiti possono includere una o più delle seguenti azioni:
<dl>
<dt>Endpoint</dt>
<dd>Un endpoint API deve essere impostato mediante <code>bluemix api</code> prima di utilizzare il comando.</dd>
<dt>Accedi</dt>
<dd>L'accesso utilizzando il comando <code>bluemix login</code> è richiesto prima di utilizzare questo comando. Se stai eseguendo l'accesso con l'ID federato, utilizza l'opzione '--sso' per autenticarti con il passcode temporale.</dd>
<dt>Destinazione</dt>
<dd>Il comando <code>bluemix target</code> deve essere utilizzato per impostare un'organizzazione e uno spazio prima di utilizzare questo comando.</dd>
<dt>Docker</dt>
<dd>La CLI Docker (docker) è richiesta per eseguire i comandi nel plug-in della CLI IBM Containers.</dd>
</dl>

<table summary="Comandi bluemix che puoi utilizzare per la gestione dei contenitori in Bluemix.">
<caption>Tabella 1. Comandi per la gestione dei contenitori in Bluemix</caption>
 <thead>
 <th colspan="5">Comandi per la gestione dei contenitori in Bluemix</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix ic attach](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_build)</td>
 <td>[bluemix ic cp](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_cp)</td>
 <td>[bluemix ic cpi](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_cpi)</td>
 <td>[bluemix ic exec](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_exec)</td>
 </tr>
 <tr>
 <td>[bluemix ic group-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_create)</td>
 <td>[bluemix ic group-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_instances)</td>
 <td>[bluemix ic group-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic group-update](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_update)</td>
 </tr>
 <tr>
  <td>[bluemix ic groups](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_groups)</td>
  <td>[bluemix ic info](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_info)</td>
  <td>[bluemix ic init](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_init)</td>
  <td>[bluemix ic images](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_images)</td>
  <td>[bluemix ic inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_inspect)</td>
 </tr>
 <tr>
 <td>[bluemix ic ip-bind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_bind)</td>
 <td>[bluemix ic ip-release](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-request](/docs/cli/reference/bluemix_cli/index.html#ip_request)</td>
 <td>[bluemix ic ip-unbind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_unbind)</td>
 <td>[bluemix ic ips](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ips)</td>
 </tr>
 <tr>
 <td>[bluemix ic kill](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_kill)</td>
 <td>[bluemix ic logs](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_logs)</td>
 <td>[bluemix ic namespace-get](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](/docs/cli/reference/bluemix_cli/index.html#pause)</td>
 </tr>
 <tr>
 <td>[bluemix ic port](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_port)</td>
 <td>[bluemix ic ps](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic rename](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rename)</td>
 <td>[bluemix ic reprovision](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_reprovision)</td>
 <td>[bluemix ic restart](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_restart)</td>
 </tr>
 <tr>
 <td>[bluemix ic rm](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rm)</td>
 <td>[bluemix ic rmi](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rmi)</td>
 <td>[bluemix ic route-map](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic run](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_run)</td>
 </tr>
 <tr>
 <td>[bluemix ic service-bind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_service_bind)</td>
 <td>[bluemix ic service-unbind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_service_unbind)</td>
 <td>[bluemix ic start](/docs/cli/reference/bluemix_cli/index.html#ic_start)</td>
 <td>[bluemix ic stats](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_stats)</td>
 <td>[bluemix ic stop](/docs/cli/reference/bluemix_cli/index.html#ic_stop)</td>
 </tr>
 <tr>
 <td>[bluemix ic top](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_top)</td>
 <td>[bluemix ic unpause](/docs/cli/reference/bluemix_cli/index.html#unpause)</td>
 <td>[bluemix ic unprovision](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_unprovision)</td>
 <td>[bluemix ic volume-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_inspect)</td>
 <td>[bluemix ic volume-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_create)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-fs
](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs)</td>
 <td>[bluemix ic volume-fs-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_create)</td>
 <td>[bluemix ic volume-fs-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_remove)</td>
 <td>[bluemix ic volume-fs-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors
](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_flavors)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_remove)</td>
 <td>[bluemix ic volumes](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic wait](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic wait-status](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_wait_status)</td>
 <td>[bluemix ic version
](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_version)</td>
 </tr>
  </tbody>
 </table>


## bluemix ic attach
{: #bluemix_ic_attach}

Controllare un contenitore in esecuzione o visualizzarne l'output. Utilizza `CTRL+C` per uscire e arrestare il contenitore. Questo comando richiama la CLI Docker. Per ulteriori informazioni, vedi il comando [attach ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/attach/){: new_window} nella guida di Docker.

```
bluemix ic attach [--no-stdin] [--sig-proxy] CONTAINER
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>--no-stdin (facoltativo)</dt>
   <dd>Non includere l'input standard.</dd>
   <dt>--sig-proxy (facoltativo)</dt>
   <dd>Eseguire il proxy di tutti i segnali ricevuti nel processo. Il
valore predefinito è <i>true</i>.</dd>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
    </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di collegamento al contenitore `my_container`:
```
bluemix ic attach my_container
```



## bluemix ic build
{: #bluemix_ic_build}

Richiamare il servizio di build IBM Containers per creare un'immagine Docker in locale o nel tuo repository {{site.data.keyword.Bluemix_notm}} privato. Questo comando richiama la CLI Docker. Per ulteriori informazioni, vedi il comando [build ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/build/){: new_window} nella guida di Docker.

```
bluemix ic build -t TAG|--tag TAG [--no-cache] [-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:
   <dl>
   <dt>-t <i>TAG</i>|--tag <i>TAG</i> (obbligatorio)</dt>
   <dd>Il nome repository da applicare all'immagine in fase di creazione.</dd>
   <dt>--no-cache (facoltativo)</dt>
   <dd>Non utilizzare la cache quando viene creata l'immagine. Il valore predefinito è <i>false</i>.</dd>
   <dt>--pull (facoltativo)</dt>
   <dd>Provare a estrarre l'immagine di base dal registro anche se è memorizzata nella cache.</dd>
   <dt>-q|--quiet (facoltativo)</dt>
   <dd>Sopprimere l'output dettagliato generato dai contenitori. Il valore predefinito è <i>false</i>.</dd>
   <dt><i>DOCKERFILE_LOCATION</i> (obbligatorio)</dt>
   <dd>Il percorso verso Dockerfile e contesto sull'host locale.</dd>
    </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di creazione di un'immagine denominata *myimage*. Il Dockerfile e altre risorse utente da utilizzare nella creazione si trovano nella stessa directory da cui viene eseguito il comando. Poiché il registro e lo spazio dei nomi sono inclusi nel nome dell'immagine, l'immagine viene creata nel repository {{site.data.keyword.Bluemix_notm}} privato della tua organizzazione.
```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage .
```


## bluemix ic cp
{: #bluemix_ic_cp}
Copia file o cartelle tra un contenitore e il file system locale. Questo comando richiama la CLI Docker. Per ulteriori informazioni, vedi il comando [cp ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/cp/){: new_window} nella guida di Docker.


## bluemix ic cpi
{: #bluemix_ic_cpi}

Accedere a un'immagine Docker Hub o a un'immagine dal tuo registro locale e copiarla nel tuo repository {{site.data.keyword.Bluemix_notm}} privato.

```
bluemix ic cpi IMMAGINE_DI_ORIGINE IMMAGINE_DI_DESTINAZIONE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
   <dl>
   <dt><i>IMMAGINE_DI_ORIGINE</i> (obbligatorio)</dt>
   <dd>Il nome del repository e dell'immagine di origine.</dd>
   <dt><i>IMMAGINE_DI_DESTINAZIONE</i> (obbligatorio)</dt>
   <dd>L'URL del repository {{site.data.keyword.Bluemix_notm}} privato, che include lo spazio dei nomi e il nome dell'immagine di destinazione. Una tag per l'immagine è facoltativa.</dd>
   </dl>

<strong>Esempi</strong>:

Copiare un'immagine dal repository di origine nel repository privato ed aggiungere una tag per l'immagine:

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

Copiare l'immagine `sinatra` dal repository `training` nel repository privato `registry.ng.bluemix.net/mynamespace` e il nome dell'immagine `mysinatra`. Aggiungere una tag `v1` per l'immagine `mysinatra`.

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


## bluemix ic exec
{: #bluemix_ic_exec}

Eseguire un comando all'interno di un contenitore. Per ulteriori informazioni, vedi il comando [exec ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/exec/){: new_window} nella guida di Docker.

```
bluemix ic exec [-d|--detach] [-it] [-u USER|--user USER] CONTAINER [CMD]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-d|--detach (facoltativo)</dt>
   <dd>Eseguire il comando specificato in background.</dd>
   <dt>-it (facoltativo)</dt>
   <dd>Modalità interattiva. L'input standard rimane visualizzato. Immetti <i>exit</i> per uscire.</dd>
   <dt>-u <i>UTENTE</i>|--user <i>UTENTE</i> (facoltativo)</dt>
   <dd>Il nome utente.</dd>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   <dt><i>CMD</i> (facoltativo)</dt>
   <dd>Il comando da eseguire all'interno del contenitore o dei contenitori specificati.</dd>
   </dl>

<strong>Esempi</strong>:

Eseguire il comando `bash` all'interno del contenitore `my_container` nella modalità interattiva:

```
bluemix ic exec -it my_container bash
```

Eseguire il comando `date` all'interno del contenitore `my_container`:

```
bluemix ic exec my_container date
```


## bluemix ic group-create
{: #bluemix_ic_group_create}

Creare un gruppo di contenitori scalabile.

```
bluemix ic group-create [--publish,-p PORT] --name GROUP_NAME [--memory,-m MEMORY_SIZE] [-n,--hostname HOSTNAME] [-d,--domain DOMAIN] [--env,-e ENV_KEY=ENV_VAL] [--env-file ENVIRO

NMENT_VARIABLE_FILE] [-P false|true] [--volume] [--min MIN_INSTANCE_COUNT] [--max MAX_INSTANCE_COUNT] [--desired DESIRED_INSTANCE_COUNT] [--anti false|true] [--auto false|true] IMAGE_NAME [CMD [CMD ...]]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
   <dl>
    <dt><i>IMAGE_NAME</i> (obbligatorio)</dt>
   <dd>L'immagine da includere in ciascuna istanza del contenitore del gruppo di contenitori. L'immagine può essere seguita da un elenco di comandi, ma non da opzioni. Includi tutte le opzioni prima di specificare l'immagine. <br><br>Se utilizzi un'immagine nel repository {{site.data.keyword.Bluemix_notm}} privato della tua organizzazione, specificala con il seguente formato: <i>registry.ng.bluemix.net/SPAZIO_NOMI/IMMAGINE</i>. <br><br>Se utilizzi un'immagine fornita da IBM Containers, non includere lo spazio dei nomi della tua organizzazione. Specifica l'immagine con il seguente formato: <i>registry.ng.bluemix.net/IMMAGINE</i>. </dd>
   <dt>--name <i>GROUP_NAME</i> (obbligatorio)</dt>
   <dd>Assegnare un nome al gruppo. <i>-n</i> è stato dichiarato obsoleto.<br>
   <strong>Suggerimento:</strong> il nome del contenitore deve iniziare con una lettera. Il nome può includere lettere maiuscole, lettere minuscole, numeri, punti., caratteri di sottolineatura _, o trattini -.</dd>
   <dt>-m <i>MEMORY_SIZE</i>|--memory <i>MEMORY_SIZE</i> (facoltativo)</dt>
   <dd>Assegnare un limite di memoria al gruppo in MB. Quando crei un gruppo di contenitori dalla CLI, il valore predefinito per ogni istanza del contenitore è <i>64</i> MB. Quando crei un gruppo di contenitori dal Dashboard {{site.data.keyword.Bluemix_notm}}, il valore predefinito per ogni istanza del contenitore è <i>256</i> MB. I valori accettati sono <i>64</i>, <i>256</i>, <i>512</i>, <i>1024</i> e <i>2048</i>. Una volta assegnato, il limite di memoria non può essere modificato.</dd>
   <dt>-n <i>HOSTNAME</i>|--hostname <i>HOSTNAME</i> (facoltativo)</dt>
   <dd>Il nome host, quale ad esempio <i>mycontainerhost</i>. L'host e il dominio si combinano per formare l'URL completo della rotta pubblica, quale ad esempio <i>http://mycontainerhost.mybluemix.net</i>. Quando esamini i dettagli di un gruppo di contenitori con il comando <i>bluemix ic group-inspect</i>, l'host e il dominio vengono elencati insieme come rotta.</dd>
   <dt>-d <i>DOMINIO</i>|--domain <i>DOMINIO</i> (facoltativo)</dt>
   <dd>Di solito, il dominio è <i>.mybluemix.net</i>. L'host e il dominio vengono combinati per formare l'URL completo della rotta pubblica, quale ad esempio <i>http://mycontainerhost.mybluemix.net</i>. Quando esamini i dettagli di un gruppo di contenitori con il comando <i>bluemix ic group-inspect</i>, l'host e il dominio vengono elencati insieme come rotta.</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>|--env <i>ENV_KEY=ENV_VAL</i> (facoltativo)</dt>
   <dd>Imposta la variabile di ambiente. In caso di più chiavi, elencale separatamente. Se sono incluse virgolette, includile racchiudendo sia il valore che il nome della variabile di ambiente. Ad esempio: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`.  La seguente tabella mostra alcune variabili di ambiente comunemente utilizzate che puoi specificare:</dd>
    </dl>


|  Variabile di ambiente                              |     Descrizione                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;nome_applicazione&gt;*       | Eseguire il bind di un servizio a un contenitore. Utilizza la variabile di ambiente `CCS_BIND_APP` per eseguire il bind di un'applicazione al contenitore. L'applicazione viene associata tramite bind al servizio di destinazione e funge da ponte che consente a {{site.data.keyword.Bluemix_notm}} di portare le informazioni `VCAP_SERVICES` dell'applicazione ponte all'istanza del contenitore in esecuzione. Per ulteriori informazioni sulla creazione di un'applicazione ponte, vedi [Esecuzione del bind di un servizio a un contenitore](../../../containers/container_integrations_binding.html){: new_window}. |
| CCS_BIND_SRV=*&lt;nome_istanza_servizio1&gt;*,*&lt;nome_istanza_servizio2&gt;* | Per eseguire direttamente il bind di un servizio Bluemix a un contenitore senza utilizzare un'applicazione ponte, utilizza CCS_BIND_SRV. Questo bind consente a Bluemix di inserire le informazioni VCAP_SERVICES nell'istanza del contenitore in esecuzione. Per elencare più servizi Bluemix, puoi includerli come parte della stessa variabile di ambiente. |
| LOG_LOCATIONS=*&lt;&gt;percorso_verso_file* | Aggiungere un file di log da monitorare nel contenitore. Includi la variabile di ambiente `LOG_LOCATIONS` in un percorso verso il file di log. |
{: caption="Table 2. Commonly used environment variables" caption-side="top"}

 <dl>
   <dt>--env-file <i>FILE_VARIABILE_AMBIENTE</i> (facoltativo)</dt>
   <dd> Importa variabili di ambiente da un file dove ENVFILE è il percorso del tuo file nella directory locale. Ogni riga nel file rappresenta una coppia key=value. </dd>
   <dt>--volume <i>VOLUME</i>:<i>PERCORSO_CONTENITORE</i>[:ro] (facoltativo)</dt>
   <dd>Collegare un volume a un contenitore, specificando i dettagli nel formato <i>IDVolume:PercorsoContenitore[:ro]</i>.
   <ul>
   <li><i>VOLUME</i>: l'ID o nome del volume.</li>
   <li><i>PERCORSO_CONTENITORE</i>: il percorso assoluto per il volume del contenitore.</li>
   <li>ro: facoltativo. La specifica di <i>ro</i> rende il volume di sola lettura invece della lettura/scrittura predefinita.</li></ul>
   </dd>
   <dt>-p <i>PORTA</i>|--publish <i>PORTA</i> (facoltativo)</dt>
   <dd>Esporre la porta per il traffico HTTP. I contenitori del tuo gruppo devono essere in ascolto sulla porta HTTP. Non possono essere effettuate richieste HTTPS. Per i gruppi di contenitori, non puoi includere più porte. <br><br>Quando specifichi una porta, stai rendendo l'applicazione disponibile al programma di bilanciamento del carico {{site.data.keyword.Bluemix_notm}} o ai contenitori che stanno provando a raggiungere l'host nello stesso spazio {{site.data.keyword.Bluemix_notm}}. Quindi i contenitori o il bilanciamento del carico {{site.data.keyword.Bluemix_notm}} possono utilizzare la porta per raggiungere l'host e l'applicazione nello stesso spazio {{site.data.keyword.Bluemix_notm}}. Se nel Dockerfile è specificata una porta per l'immagine che stai utilizzando, includila. <br>
   <strong>Suggerimenti</strong>: <ul>
   <li>Per l'immagine Liberty Server certificata da IBM o una versione modificata di questa immagine, immetti la porta 9080.</li>
   <li>Per l'immagine Node.js certificata da IBM o una versione modificata di questa immagine, immetti la porta 8000.</li>
   </ul>
   </dd>
   <dt>-P (facoltativo)</dt>
   <dd>Pubblica tutte le porte</dd>
   <dt>--min <i>MIN_INSTANCE_COUNT</i> (facoltativo)</dt>
   <dd>Il numero minimo di istanze. Il valore predefinito è 1. Se imposti un numero minimo di istanze, una volta creato il gruppo di contenitori non è più possibile modificare questo valore.</dd>
   <dt>--max <i>MAX_INSTANCE_COUNT</i> (facoltativo)</dt>
   <dd>Il numero massimo di istanze. Il valore predefinito è 2. Se imposti un numero massimo di istanze, una volta creato il gruppo di contenitori non è più possibile modificare questo valore.</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i> (facoltativo)</dt>
   <dd>Il numero di istanze da te richiesto. Il valore predefinito è 2.</dd>
   <dt>--auto (facoltativo)</dt>
   <dd>Quando si crea il gruppo di contenitori e il ripristino automatico è abilitato, IBM Containers verifica l'integrità di ciascuna istanza con una richiesta HTTP alla porta assegnata.<br>
   Se non viene ricevuta alcuna risposta da un'istanza del contenitore entro 2 intervalli consecutivi di 90 secondi, l'istanza viene rimossa e sostituita con una nuova istanza. Se il contenitore risponde non viene effettuata alcuna azione. Questo processo viene ripetuto continuamente. In una finestra di 30 minuti, se il numero totale di differenti contenitori membri del gruppo è uguale o 3 volte maggiore della dimensione massima osservata per il gruppo stesso, il ripristino automatico viene disabilitato in modo permanente per il gruppo di contenitori. Per abilitare di nuovo il ripristino automatico, devi ricreare il gruppo di contenitori.</dd>
  <dt>--anti (facoltativo)</dt>
  <dd> Utilizza l'opzione anti-affinity per rendere il tuo gruppo di contenitori molto più disponibile. L'opzione --anti forza l'inserimento di ogni istanza di contenitore del tuo gruppo in un nodo di elaborazione fisico separato, riducendo così la possibilità che si verifichi un arresto anomalo di tutti i contenitori nel gruppo a causa di un errore hardware. Potresti non essere in grado di utilizzare questa opzione con gruppi di dimensione maggiore in quanto ogni regione e organizzazione Bluemix ha a disposizione una serie di nodi di elaborazione limitata per la distribuzione. Se la distribuzione non riesce, riduci il numero di istanze del contenitore nel gruppo o rimuovi l'opzione --anti. </dd>
   <dt><i>CMD</i> (facoltativo)</dt>
   <dd>Il comando e gli argomenti trasmessi al gruppo di contenitori per l'esecuzione. Questo comando deve essere un comando a esecuzione prolungata. Non utilizzare un comando di breve durata che non viene eseguito per molto tempo, quale ad esempio <i>/bin/date</i>, poiché tale comando potrebbe provocare un arresto anomalo del contenitore.  <br> <strong>Note:</strong> <ul>
   <li>Il comando e i relativi argomenti devono trovarsi alla fine della riga di comando <i>bluemix ic run</i>.</li>
   <li>Se gli argomenti del comando includono il trattino -, come in <i>-c</i> nel comando di esempio precedente, il comando deve essere preceduto da due trattini (--).</li>
   </ul></dd>
   </dl>


<strong>Esempi</strong>:

Creare un gruppo di contenitori `my_container_group` utilizzando l'immagine `registry.ng.bluemix.net/ibmnode` fornita da IBM Containers, quindi eseguire il comando di lunga durata `ping localhost` su tale gruppo di contenitori:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

Creare un gruppo di contenitori `my_container_group` utilizzando l'immagine `registry.ng.bluemix.net/ibmnode` fornita da IBM Containers, quindi eseguire il comando di lunga durata `tail -f /dev/null` su tale gruppo di contenitori:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

Creare un gruppo scalabile `mygroup` con il ripristino automatico abilitato, utilizzando l'immagine `registry.ng.bluemix.net/ibmliberty`. La porta è `9080`, il nome host è `mycontainerhost`, il nome dominio è `mybluemix.net`.
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty
```


## bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

Visualizzare informazioni dettagliate, quali le variabili di ambiente, le porte o la memoria, specificate per un gruppo di contenitori al momento della creazione.

```
bluemix ic group-inspect GRUPPO_CONTENITORI
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>GRUPPO_CONTENITORI</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del gruppo di contenitori.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di controllo del gruppo di contenitori `my_group`:
```
bluemix ic group-inspect my_group
```


## bluemix ic group-instances
{: #bluemix_ic_group_instances}

Elencare istanze di un gruppo di contenitori specificato.

```
bluemix ic group-instances GRUPPO_CONTENITORI
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>GRUPPO_CONTENITORI</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del gruppo di contenitori.</dd>
   </dl>

<strong>Esempi</strong>:

Elencare tutte le istanze del gruppo di contenitori `my_group`:
```
bluemix ic group-instances my_group
```


## bluemix ic group-remove
{: #bluemix_ic_group_remove}

Rimuovere un gruppo di contenitori da uno spazio.

```
bluemix ic group-remove [-f|--force] GROUP_NAME [GROUP_NAME2 [...]]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-f|--force (facoltativo)</dt>
   <dd>Forza la rimozione di un contenitore in esecuzione o in errore.</dd>
   <dt><i>NOME GRUPPO</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del gruppo di contenitori.</dd>
   </dl>


<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di rimozione di un gruppo di contenitori, dove `my_group` è il nome del gruppo di contenitori.
```
bluemix ic group-remove my_group
```


## bluemix ic group-update
{: #bluemix_ic_group_update}

Aggiornare un gruppo di contenitori.


```
bluemix ic group-update [--anti] [--desired DESIRED_INSTANCE_COUNT] [-e ENV_KEY=ENV_VAL] GROUP_NAME
```

**Suggerimento:** per aggiornare il nome host o il dominio di un gruppo di contenitori, utilizza `bluemix ic route-map [-n HOST][-d DOMAIN] GRUPPO_CONTENITORI`.

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
 <dl>
   <dt>--anti (facoltativo)</dt>
   <dd>Utilizza l'opzione anti-affinity per rendere il tuo gruppo di contenitori molto più disponibile. L'opzione --anti forza l'inserimento di ogni istanza di contenitore del tuo gruppo in un nodo di elaborazione fisico separato, riducendo così la possibilità che si verifichi un arresto anomalo di tutti i contenitori nel gruppo a causa di un errore hardware. Potresti non essere in grado di utilizzare questa opzione con gruppi di dimensione maggiore in quanto ogni regione e organizzazione Bluemix ha a disposizione una serie di nodi di elaborazione limitata per la distribuzione. Se la distribuzione non riesce, riduci il numero di istanze del contenitore nel gruppo o rimuovi l'opzione --anti.</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i> (facoltativo)</dt>
   <dd>Il numero di istanze da te richiesto. Il valore predefinito è <i>2</i>.</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>(facoltativo)</dt>
   <dd>Imposta la variabile di ambiente. In caso di più chiavi, elencale separatamente. Se sono incluse virgolette, includile racchiudendo sia il valore che il nome della variabile di ambiente. Ad esempio: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`.</dd>
   <dt><i>NOME GRUPPO</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del gruppo di contenitori.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di aggiornamento del gruppo di contenitori `my_group`:
```
bluemix ic group-update --desired 5 my_group
```


## bluemix ic groups
{: #bluemix_ic_groups}

Elencare i gruppi di contenitori nel repository {{site.data.keyword.Bluemix_notm}} privato dell'organizzazione.

```
bluemix ic groups [-q]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
	<dl>
	<dt>-q (facoltativo)</dt>
   	<dd>Visualizza solo gli ID gruppo</dd>
	</dl>


## bluemix ic images
{: #bluemix_ic_images}

Visualizzare un elenco di tutte le immagini disponibili nel repository {{site.data.keyword.Bluemix_notm}} privato dell'organizzazione. Per ulteriori informazioni, vedi il comando [images ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/images){: new_window} nella guida di Docker. L'elenco include l'ID immagine, la data di creazione e il nome dell'immagine.

```
bluemix ic images [-a|--all] [-f CONDITION] [--no-trunc] [-q|--quiet]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-a|--all (facoltativo)</dt>
   <dd>Includere tutti i livelli di immagine per ciascuna immagine del repository dell'organizzazione e non solo il più recente.</dd>
   <dt>-f (facoltativo)</dt>
   <dd>Filtrare l'elenco di immagini in base alla condizione fornita.</dd>
   <dt>--no-trunc (facoltativo)</dt>
   <dd>Non troncare l'output.</dd>
   <dt>-q|--quiet (facoltativo)</dt>
   <dd>Visualizzare solo gli ID numerici.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di elenco delle immagini disponibili per l'organizzazione:
```
bluemix ic images
```


## bluemix ic info
{: #bluemix_ic_info}

Visualizzare un insieme di informazioni che descrivono lo stato dell'istanza del servizio cloud del contenitore. Le informazioni includono limite dei contenitori, utilizzo dei contenitori, contenitori in esecuzione, limite di memoria, utilizzo della memoria, limite dell'indirizzo IP mobile, utilizzo dell'indirizzo IP mobile, URL host CCS, URL host del registro e stato della modalità di debug.

```
bluemix ic info
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione


## bluemix ic init
{: #bluemix_ic_init}

Inizializzare l'ambiente dei contenitori sulla macchina locale in uso per sfruttare appieno le funzioni del servizio IBM Containers.

```
bluemix ic init
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

**Nota:** prima dell'inizializzazione, accertati che la CLI Docker (docker) sia installata e configurato nella tua variabile di ambiente PATH. Per passare a un'altra regione, utilizza il comando `bluemix region-set`.

<strong>Esempi</strong>:

Passare alla regione `us-south`:

```
bluemix region-set us-south
```


## bluemix ic inspect
{: #bluemix_ic_inspect}

Visualizzare le informazioni su un contenitore. Per ulteriori informazioni, vedi il comando [inspect ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/inspect){: new_window} nella guida di Docker.

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>IMAGE</i> (obbligatorio)</dt>
   <dd>Visualizzare informazioni dettagliate su un'immagine specifica indicando l'ID o il nome dell'immagine.</dd>
   <dt>images (obbligatorio)</dt>
   <dd>Visualizzare informazioni dettagliate su tutte le immagini del tuo repository.</dd>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Visualizzare informazioni dettagliate su un contenitore specifico, indicando l'ID o il nome del contenitore.</dd>
   </dl>

**Suggerimento:** non è possibile specificare *IMMAGINE*, *images* o il *CONTENITORE* contemporaneamente.

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di controllo di un contenitore denominato `proxy`:
```
bluemix ic inspect proxy
```


## bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

Eseguire il bind di un indirizzo IP a virgola mobile disponibile a un contenitore.

```
bluemix ic ip-bind CONTENITORE INDIRIZZO_IP
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (obbligatorio)</dt>
   <dd>L'indirizzo IP da associare mediante bind.</dd>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore da associare mediante bind.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di bind dell'indirizzo IP `192.123.12.12 al` contenitore `proxy`:
```
bluemix ic ip-bind 192.123.12.12 proxy
```


## bluemix ic ip-release
{: #bluemix_ic_ip_release}

Rilasciare un indirizzo IP a virgola mobile dall'istanza del servizio cloud del contenitore.

```
bluemix ic ip-release IP_ADDRESS [IP_ADDRESS2 [...]]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (obbligatorio)</dt>
   <dd>L'indirizzo IP da rilasciare.</dd>
   </dl>


## bluemix ic ip-request
{: #ip_request}
Richiedere un nuovo indirizzo IP mobile.

```
bluemix ic ip-request [-q]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-q (facoltativo)</dt>
   <dd>Elenca solo gli indirizzi IP, senza l'ID per i contenitori associati a tali indirizzi IP.</dd>
   </dl>


## bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

Annullare il bind di un indirizzo IP a virgola mobile dal relativo contenitore.

Gli indirizzi IP pubblici sono una risorsa limitata di IBM Containers. Pertanto, gli indirizzi IP pubblici assegnati a uno spazio e non associati mediante bind a un contenitore vengono recuperati periodicamente dagli utenti della versione di prova, approssimativamente su base settimanale. Gli indirizzi IP non associati non sono mai recuperati dai clienti con pagamento a consumo o con una sottoscrizione.

```
bluemix ic ip-unbind INDIRIZZO_IP CONTENITORE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (obbligatorio)</dt>
   <dd>L'indirizzo IP da scollegare.</dd>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore da scollegare.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di annullamento del bind dell'indirizzo IP `192.123.12.12` dal contenitore `proxy`:
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


## bluemix ic ips
{: #bluemix_ic_ips}

Elencare gli indirizzi IP a virgola mobile disponibili per l'utente che ha effettuato l'accesso. L'elenco include gli indirizzi IP e l'ID contenitore a cui sono collegati gli indirizzi IP. Se l'indirizzo IP non è in uso, non verrà visualizzato alcun ID contenitore.

```
bluemix ic ips [-q]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-q (facoltativo)</dt>
   <dd>Elenca solo gli indirizzi IP, senza l'ID per i contenitori associati a tali indirizzi IP.</dd>
   </dl>


<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta per ricevere un elenco di tutti gli indirizzi IP per l'organizzazione.
```
bluemix ic ips -q
```


## bluemix ic kill
{: #bluemix_ic_kill}

Arrestare un processo in esecuzione in un contenitore senza arrestare il contenitore. Per ulteriori informazioni, vedi il comando [kill ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/kill/){: new_window} nella guida di Docker.

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-s <i>CMD</i>|--signal <i>CMD</i> (facoltativo)</dt>
   <dd>Inviare un comando al processo in esecuzione nel contenitore.</dd>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   </dl>


<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di terminazione di un contenitore denominato `proxy`:
```
bluemix ic kill proxy
```


## bluemix ic logs
{: #bluemix_ic_logs}

Mostra i log di output o di errore per un contenitore in esecuzione. Per ulteriori informazioni, vedi il comando [logs ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/logs/){: new_window} nella guida di Docker.
```
bluemix ic logs [OPTIONS] CONTAINER
```


## bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

Visualizzare il nome del repository di immagini {{site.data.keyword.Bluemix_notm}} privato dell'organizzazione a cui sei collegato.

```
bluemix ic namespace-get
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione


## bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

Impostare il nome del repository di immagini {{site.data.keyword.Bluemix_notm}} privato dell'organizzazione a cui sei collegato.

*Limitazione*: non puoi utilizzare un trattino `-` nel nome del tuo spazio dei nomi del repository.

```
bluemix ic namespace-set NOME
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>NOME</i> (obbligatorio)</dt>
   <dd>Una funzione da eseguire una sola volta per impostare lo spazio dei nomi del repository per la tua organizzazione, se non già impostato. Una volta impostato lo spazio dei nomi, reinizializza IBM Containers attraverso il comando `bluemix ic init` prima di continuare.</dd>
   </dl>


## bluemix ic pause
{: #pause}

Mettere in pausa tutti i processi all'interno di un contenitore in esecuzione. Per ulteriori informazioni, vedi il comando [pause ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/pause/){: new_window} nella guida di Docker. Per arrestare un contenitore, vedi il comando [bluemix ic unpause](#unpause).

```
bluemix ic pause CONTENITORE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:
   <dl>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   </dl>

<strong>Risposte</strong>:

- Contenitore correttamente in pausa.

- Comando non riuscito con il servizio cloud del contenitore

 `{messaggio}`

 Dove `{messaggio}` è
l'errore correlato.

- Comando non riuscito - Impossibile connettersi al servizio cloud del contenitore

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di messa in pausa di un contenitore denominato `proxy`:
```
bluemix ic pause proxy
```


## bluemix ic port
{: #bluemix_ic_port}

Elenca le associazioni delle porte o un'associazione specifica del contenitore. Questo comando include il comando `docker port`. Per ulteriori informazioni, vedi il comando [port ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/port/){: new_window} nella guida di Docker.


## bluemix ic ps
{: #bluemix_ic_ps}
Visualizzare un elenco di contenitori in esecuzione nello spazio dei nomi dell'utente che ha effettuato l'accesso. Per impostazione predefinita, questo comando mostra solo i contenitori in esecuzione. Per ulteriori informazioni, vedi il comando [ps ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/ps/){: new_window} nella guida di Docker.

```
bluemix ic ps [-a|--all] [--filter env=SEARCH_CRITERIA] [-s|--size] [-l NUM|--limit NUM] [-q|--quiet]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-a|--all (facoltativo)</dt>
   <dd>Visualizzare tutti i contenitori, sia quelli in esecuzione sia quelli arrestati.</dd>
   <dt>--filter env=<i>SEARCH_CRITERIA</i> (facoltativo)</dt>
   <dd>Cerca i contenitori che hanno uno specifico valore di variabile di ambiente. Puoi filtrare i tuoi contenitori in base a qualsiasi chiave o valore di variabile di ambiente elencato nella sezione Env della tua risposta CLI quando ispezioni un contenitore. Sostituisci SEARCH_CRITERIA con la chiave o valore che stai cercando. I tuoi criteri di ricerca non devono necessariamente essere una corrispondenza esatta. </dd>
   <dt>-s|--size (facoltativo)</dt>
   <dd>Elencare le dimensioni dei contenitori.</dd>
   <dt>-l <i>NUM</i>|--limit <i>NUM</i> (facoltativo)</dt>
   <dd>Elencare i contenitori creati più di recente, dove <i>NUM</i> è il numero dei contenitori creati più di recente che desideri restituire. <br><br> Ad esempio, se hai creato i contenitori da <i>node1</i> a <i>node5</i> in modo sequenziale, il comando <i>bluemix ic ps --limit 2</i> restituisce node4 e node5 perché sono gli ultimi due contenitori creati. </dd>
   <dt>-q|--quiet (facoltativo)</dt>
   <dd>Visualizzare solo gli ID contenitore.</dd>
   </dl>


<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di visualizzazione di tutti i contenitori in esecuzione e arrestati:
```
bluemix ic ps -a
```


## bluemix ic rename
{: #bluemix_ic_rename}
Rinomina un contenitore. Per ulteriori informazioni, vedi il comando [rename ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rename/){: new_window} nella guida di Docker.

```
bluemix ic rename OLD_NAME NEW_NAME
```
<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

<dl>
   <dt><i>OLD_NAME</i> (obbligatorio)</dt>
   <dd>Il vecchio nome del contenitore.</dd>
   <dt><i>NEW_NAME</i> (obbligatorio)</dt>
   <dd>Il nuovo nome del contenitore.</dd>
   </dl>


## bluemix ic reprovision
{: #bluemix_ic_reprovision}

Ricrea il servizio IBM Containers nello spazio Bluemix a cui sei collegato. La quota originale per lo spazio viene mantenuta.

<strong>Importante</strong>: quando esegui questo comando, nessuno dei tuoi singoli contenitori e gruppi in questo spazio verrà migrato nello spazio di cui è stato eseguito di nuovo il provisioning e verranno rimossi durante il processo di migrazione.

```
bluemix ic reprovision [--force|-f] [ENVIRONMENT_NAME]
```
<strong>Opzioni del comando</strong>:

<dl>
   <dt>--force|-f (facoltativo)</dt>
   <dd>Forza la nuova creazione del servizio IBM Containers nello spazio Bluemix.</dd>
   <dt><i>AVAILABILITY_ZONE</i> (facoltativo)</dt>
   <dd>Il nome della zona di disponibilità IBM Containers in cui vengono distribuiti i tuoi contenitori. Se non si specifica alcuna zona di disponibilità, viene utilizzata la zona predefinita impostata per la regione.</dd>
   </dl>


## bluemix ic restart
{: #bluemix_ic_restart}

Riavviare un contenitore. Per ulteriori informazioni, vedi il comando [restart ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/restart/){: new_window} nella guida di Docker.

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   <dt>-t <i>SECONDI</i>|--time <i>SECONDI</i> (facoltativo)</dt>
   <dd>Il numero di secondi di attesa prima che il contenitore venga riavviato.</dd>
   </dl>


<strong>Risposte</strong>:

- Contenitore riavviato correttamente.

- Comando non riuscito con il servizio cloud del contenitore

 `{messaggio}`

 Dove `{messaggio}` è
l'errore correlato.

- Comando non riuscito - Impossibile connettersi al servizio cloud del contenitore

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di riavvio di un contenitore denominato `proxy`:
```
bluemix ic restart proxy
```


## bluemix ic rm
{: #bluemix_ic_rm}

Rimuovere un contenitore. Per ulteriori informazioni, vedi il comando [rm ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rm/){: new_window} nella guida di Docker.

```
bluemix ic rm [-f|--force] CONTAINER
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-f|--force (facoltativo)</dt>
   <dd>Forza la rimozione di un contenitore in esecuzione o in errore.</dd>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   </dl>

<strong>Risposte</strong>:

- Contenitore rimosso correttamente.

- Comando non riuscito con il servizio cloud del contenitore

 `{messaggio}`

 Dove `{messaggio}` è
l'errore correlato.

- Comando non riuscito - Impossibile connettersi al servizio cloud del contenitore.

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di rimozione di un contenitore denominato `proxy`:
```
bluemix ic rm proxy
```


## bluemix ic rmi
{: #bluemix_ic_rmi}

Rimuovere un'immagine dallo spazio dei nomi dell'utente che ha effettuato l'accesso. Per ulteriori informazioni, vedi il comando [rmi ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rmi/){: new_window} nella guida di Docker.

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-R <i>REGISTRO</i>|--registry <i>REGISTRO</i> (facoltativo)</dt>
   <dd>Modificare l'host del registro. Per impostazione predefinita verrà utilizzato il registro che hai specificato nel comando <i>bluemix ic init</i>.</dd>
   <dt><i>IMAGE</i> (obbligatorio)</dt>
   <dd>Il nome dell'immagine che desideri rimuovere. Se non viene specificata
una tag nel nome immagine, per impostazione predefinita viene eliminata
l'immagine contrassegnata come <i>latest</i>.</dd>
   </dl>

<strong>Risposte</strong>:

- Rimozione di: `{IMMAGINE}`

 Dove `{IMMAGINE}` è il
nome dell'immagine che è stata rimossa.

- Errore. Nessun host registro specificato.

- Rimozione dell'immagine non riuscita - Impossibile connettersi al registro cloud del contenitore

- Comando non riuscito con il servizio cloud del contenitore

 `{messaggio}`

 Dove `{messaggio}` è
l'errore correlato.

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di rimozione dell'immagine `mynamespace/myimage:latest`:
```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


## bluemix ic route-map
{: #bluemix_ic_route_map}

Stabilire la rotta per il traffico internet da utilizzare per accedere al gruppo di contenitori. Puoi utilizzare questo comando per stabilire una nuova rotta o aggiornarne una esistente.

```
bluemix ic route-map [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i> (facoltativo)</dt>
   <dd>Il nome host della rotta. Il nome host costituisce la prima parte dell'URL completo della rotta pubblica, quale ad esempio <i>mycontainerhost</i> nell'URL <i>mycontainerhost.mybluemix.net</i>.</dd>
   <dt>-d <i>DOMINIO</i>|--domain <i>DOMINIO</i> (facoltativo)</dt>
   <dd>Il nome dominio della rotta, che costituisce la seconda parte dell'URL completo della rotta pubblica. Nella maggior parte dei casi, il dominio è <i>mybluemix.net</i>. Puoi anche utilizzare questo parametro per specificare un dominio privato.</dd>
   <dt><i>GRUPPO_CONTENITORI</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del gruppo di contenitori.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di associazione della rotta del gruppo denominato `GROUP1`, dove `my_host` è il nome host e `mybluemix.net` è il dominio.
```
bluemix ic route-map -n my_host -d mybluemix.net GROUP1
```


## bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

Stabilire la rotta per il traffico internet da utilizzare per accedere al gruppo di contenitori. Puoi utilizzare questo comando per stabilire una nuova rotta o aggiornarne una esistente.

```
bluemix ic route-unmap [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i> (facoltativo)</dt>
   <dd>Il nome host della rotta.</dd>
   <dt>-d <i>DOMINIO</i>|--domain <i>DOMINIO</i> (facoltativo)</dt>
   <dd>Il nome dominio della rotta.</dd>
   <dt><i>GRUPPO_CONTENITORI</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del gruppo di contenitori.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di annullamento dell'associazione della rotta del gruppo denominato `GRUPPO1`, dove `mio_host` è il nome dell'host e `organization.com` è il dominio.
```
bluemix ic route-unmap -n mio_host -d organization.com GRUPPO1
```


## bluemix ic run
{: #bluemix_ic_run}

Avviare un nuovo contenitore nel servizio cloud del contenitore da
un nome immagine. Per ulteriori informazioni, vedi il comando [run ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/run/){: new_window} nella guida di Docker.


```
bluemix ic run [-p PORT|--publish PORTA] [-P] [-m MEMORIA|--memory MEMORIA] [-e ENV|--env ENV] [--volume VOLUME:PERCORSO_CONTENITORE] -n NOME|--name NOME [--link NOME:ALIAS] [-it] IMMAGINE [CMD [CMD ...]]
```
**Nota:** accertati che lo strumento di comando Cloud Foundry sia installato e di disporre di un token Cloud Foundry. Se si accede correttamente tramite `bluemix login` e `bluemix ic init` vengono creati i certificati e i token richiesti.


<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-p <i>PORTA</i>|--publish <i>PORTA</i> (facoltativo)</dt>
   <dd>Esporre la porta per il traffico HTTP. Includi le eventuali porte specificate nel Dockerfile per l'immagine che stai utilizzando. Puoi includere più porte con più opzioni <i>-p</i>. L'esposizione di una porta comporta automaticamente il bind di un indirizzo IP pubblico, se disponibile, al contenitore. <br><br>Se disponi già di un indirizzo IP nello spazio che desideri associare mediante bind al contenitore, puoi specificare l'indirizzo IP invece di eseguirne il bind successivamente. L'indirizzo IP deve essere specificato nel seguente formato: &lt;indirizzo_IP&gt;:&lt;porta_contenitore&gt;:&lt;porta_contenitore&gt; <br><br>Per ulteriori informazioni sulla richiesta di indirizzi IP per uno spazio, vedi il comando <a href="index.html#ip_request" target="_blank">bluemix ic ip-request</a>. <br><br>Quando specifichi una porta, stai rendendo l'applicazione disponibile al programma di bilanciamento del carico {{site.data.keyword.Bluemix_notm}} o ai contenitori dello stesso spazio {{site.data.keyword.Bluemix_notm}} che stanno provando a raggiungere l'host. Se nel Dockerfile è specificata una porta per l'immagine che stai utilizzando, includila. <br><br><strong>Suggerimenti:</strong><ul><li>Per l'immagine Liberty Server certificata da IBM o una versione modificata di questa immagine, immetti la porta 9080.</li><li>Per l'immagine Node.js certificata da IBM o una versione modificata di questa immagine, immetti la porta 8000.</li></ul></dd>
   <dt>-P (facoltativo)</dt>
   <dd>Esporre automaticamente le porte specificate nel Dockerfile dell'immagine per il traffico HTTP.</dd>
   <dt>-m <i>MEMORIA</i>|--memory <i>MEMORIA</i> (facoltativo)</dt>
   <dd>Assegnare un limite di memoria al gruppo in MB. Quando crei un gruppo di contenitori dalla CLI, il valore predefinito per ogni istanza del contenitore è 64 MB.  Quando crei un gruppo di contenitori dal Dashboard {{site.data.keyword.Bluemix_notm}}, il valore predefinito per ciascuna istanza è 256 MB. I valori accettati sono 64, 256, 512, 1024 e 2048. Una volta assegnato, il limite di memoria non può essere modificato.</dd>
   <dt>-e <i>AMB</i>|--env <i>AMB</i> (facoltativo)</dt>
   <dd>Impostare la variabile di ambiente, dove <i>AMB</i> è una coppia chiave=valore. In caso di più chiavi, elencale separatamente. Se includi virgolette, fallo racchiudendo sia il valore che il nome della variabile di ambiente. Ad esempio: -e "key1=value1" -e "key2=value2" -e "key3=value3". La seguente tabella mostra alcune variabili di ambiente comunemente utilizzate che puoi specificare:</dd>
   </dl>


|      Variabile di ambiente                          |   Descrizione                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;nome_applicazione&gt;*       | Eseguire il bind di un servizio a un contenitore. Utilizza la variabile di ambiente `CCS_BIND_APP` per eseguire il bind di un'applicazione al contenitore. L'applicazione viene associata mediante bind al servizio di destinazione e funge da ponte che consente a {{site.data.keyword.Bluemix_notm}} di portare le informazioni `VCAP_SERVICES` dell'applicazione ponte nell'istanza del contenitore in esecuzione. Per ulteriori informazioni sulla creazione di un'applicazione ponte, vedi [Esecuzione del bind di un servizio a un contenitore](../../../containers/container_integrations_binding.html){: new_window}. |
| CCS_BIND_SRV=*&lt;nome_istanza_servizio1&gt;*,*&lt;nome_istanza_servizio2&gt;* | Per eseguire direttamente il bind di un servizio Bluemix a un contenitore senza utilizzare un'applicazione ponte, utilizza CCS_BIND_SRV. Questo bind consente a Bluemix di inserire le informazioni VCAP_SERVICES nell'istanza del contenitore in esecuzione. Per elencare più servizi Bluemix, puoi includerli come parte della stessa variabile di ambiente. |
| LOG_LOCATIONS=*&lt;&gt;percorso_verso_file* | Aggiungere un file di log da monitorare nel contenitore. Includi la variabile di ambiente `LOG_LOCATIONS` in un percorso verso il file di log. |
{: caption="Table 3. Commonly used environment variables" caption-side="top"}


   <dl>
   <dt>--volume <i>VOLUME</i>:<i>PERCORSO_CONTENITORE</i>[:ro] (facoltativo)</dt>
   <dd>Collegare un volume a un contenitore, specificando i dettagli nel formato <i>IDVolume:PercorsoContenitore[:ro]</i>.
   <ul>
   <li><i>VOLUME</i>: l'ID o nome del volume.</li>
   <li><i>PERCORSO_CONTENITORE</i>: il percorso assoluto per il volume del contenitore.</li>
   <li>ro: facoltativo. La specifica di <i>ro</i> rende il volume di sola lettura invece della lettura/scrittura predefinita.</li></ul>
   </dd>
   <dt>-n <i>NOME</i>|--name <i>NOME</i> (facoltativo)</dt>
   <dd>Assegnare un nome al contenitore. <br> <strong>Suggerimento:</strong> il nome del contenitore deve iniziare con una lettera. Il nome può includere lettere maiuscole, lettere minuscole, numeri, punti., caratteri di sottolineatura _, o trattini -.</dd>
   <dt>--link <i>NOME</i>:<i>ALIAS</i> (facoltativo)</dt>
   <dd>Ogni volta che desideri che un contenitore comunichi con un altro contenitore in esecuzione, puoi farvi riferimento utilizzando un alias del nome host.</dd>
   <dt>-it (facoltativo)</dt>
   <dd>Eseguire il contenitore in modalità interattiva. Una volta creato il contenitore, mantieni l'input standard visualizzato. Immetti <i>exit</i> per uscire.</dd>
   <dt><i>IMAGE</i> (obbligatorio)</dt>
   <dd>L'immagine da includere nel contenitore. L'immagine può essere seguita da un elenco di comandi, ma non da opzioni. Includi tutte le opzioni prima di specificare un'immagine. Includi tutte le opzioni prima di specificare l'immagine. <br><br>Se utilizzi un'immagine nel repository {{site.data.keyword.Bluemix_notm}} privato della tua organizzazione, specificala con il seguente formato: <i>registry.ng.bluemix.net/SPAZIO_NOMI/IMMAGINE</i>. <br><br>Se utilizzi un'immagine fornita da IBM Containers, specificala nel seguente formato: <i>registry.ng.bluemix.net/IMMAGINE</i>. </dd>
   <dt><i>CMD</i> (facoltativo)</dt>
   <dd>Il comando e gli argomenti trasmessi al gruppo di contenitori per l'esecuzione. Questo comando deve essere un comando a esecuzione prolungata. Non utilizzare un comando di breve durata che non viene eseguito per molto tempo, quale ad esempio <i>/bin/date</i>, poiché tale comando potrebbe provocare un arresto anomalo del contenitore.</dd>
   </dl>


<strong>Esempi</strong>:

Esegui il comando a esecuzione prolungata `sh -c "while true; do date; sleep 20; done"` sul contenitore `mio_contenitore` creato sull'immagine `registry.ng.bluemix.net/ibmnode`.
```
bluemix ic run --name mio_contenitore registry.ng.bluemix.net/ibmnode -- sh -c "while true; do date; sleep 20; done"
```


Creare e successivamente riavviare un contenitore `proxy` con un limite di memoria di `1024` MB utilizzando l'immagine `mio_spazioNomi/nginx`, dove `mio_spazioNomi` è lo spazio dei nomi associato agli utenti che hanno effettuato l'accesso.
```
bluemix ic run -n proxy -m 1024 registry.ng.bluemix.net/my_namespace/nginx
```

Creare e successivamente riavviare un contenitore utilizzando l'immagine `mio_spazioNomi/blog`, trasmettere le credenziali come variabili di ambiente. `mio_spazioNomi` è lo spazio dei nomi associato agli utenti che hanno effettuato l'accesso.
```
bluemix ic run -n mio_contenitore -e USER=johnsmith -e PASS=password registry.ng.bluemix.net/mio_spazioNomi/blog
```

Aggiungere un volume a un contenitore utilizzando l'immagine `mio_spazioNomi/blog`, dove `mio_spazioNomi` è lo spazio dei nomi associato agli utenti che hanno effettuato l'accesso.
```
bluemix ic run -n mio_contenitore -v VolId1:/first/path -v VolId2:/second/path registry.ng.bluemix.net/mio_spazioNomi/blog
```


## bluemix ic service-bind
{: #bluemix_ic_service-bind}

Aggiungi un servizio a un gruppo di contenitori in esecuzione. Questo comando è disponibile solo per i gruppi di contenitori. I singoli contenitori devono essere associati tramite bind a un servizio come parte del comando bluemix ic run.

```
bluemix ic service-bind GROUP_NAME SERVICE_INSTANCE
```
<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>NOME GRUPPO</i> (obbligatorio)</dt>
   <dd>L'ID o il nome del gruppo.</dd>
   <dt><i>ISTANZA_SERVIZIO</i> (obbligatorio)</dt>
   <dd>Il nome dell'istanza del servizio da aggiungere al gruppo di contenitori.</dd>
   </dl>


## bluemix ic service-unbind
{: #bluemix_ic_service-unbind}

Rimuovi un servizio da un gruppo di contenitori in esecuzione. Questo comando è disponibile solo per i gruppi di contenitori. I singoli contenitori devono rimuovere il contenitore e crearne uno nuovo senza il servizio.

```
bluemix ic service-unbind GROUP_NAME SERVICE_INSTANCE
```
<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>NOME GRUPPO</i> (obbligatorio)</dt>
   <dd>L'ID o il nome del gruppo.</dd>
   <dt><i>ISTANZA_SERVIZIO</i> (obbligatorio)</dt>
   <dd>Il nome dell'istanza del servizio da aggiungere al gruppo di contenitori.</dd>
   </dl>


## bluemix ic start
{: #ic_start}
Avviare un contenitore arrestato. Per ulteriori informazioni, vedi il comando [start ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/start/){: new_window} nella guida di Docker. Per arrestare un contenitore, vedi il comando [bluemix ic stop](#ic_stop).

```
bluemix ic start CONTENITORE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   </dl>


<strong>Risposte</strong>:

- Contenitore avviato correttamente.

- Comando non riuscito con il servizio cloud del contenitore

 `{messaggio}`

 Dove `{messaggio}` è
l'errore correlato.

- Comando non riuscito - Impossibile connettersi al servizio cloud del contenitore

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di avvio di un contenitore denominato `proxy`.
```
bluemix ic start proxy
```


## bluemix ic stats
{: #bluemix_ic_stats}

Visualizzare le statistiche di utilizzo in tempo reale per uno o più contenitori. Utilizza `CTRL+C` per chiudere. Per ulteriori informazioni, vedi il comando [stats ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/stats/){: new_window} nella guida di Docker.

```
bluemix ic stats [--no-stream] CONTENITORE [CONTENITORE]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   <dt>--no-stream (facoltativo)</dt>
   <dd>Visualizzare solo il risultato più recente, senza includere informazioni precedenti.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di visualizzazione delle statistiche più recenti su un contenitore:
```
bluemix ic stats --no-stream mio_contenitore
```


## bluemix ic stop
{: #ic_stop}
Arrestare un contenitore in esecuzione. Per ulteriori informazioni, vedi il comando [stop ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/stop/){: new_window} nella guida di Docker. Per avviare un contenitore, vedi il comando [bluemix ic start](#ic_start).

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   <dt>-t <i>SECONDI</i>|--time <i>SECONDI</i> (facoltativo)</dt>
   <dd>Il numero di secondi di attesa prima che il contenitore venga arrestato.</dd>
   </dl>

<strong>Risposte</strong>:

- Contenitore arrestato correttamente.

- Comando non riuscito con il servizio cloud del contenitore

 `{messaggio}`

 Dove `{messaggio}` è
l'errore correlato.

- Comando non riuscito - Impossibile connettersi al servizio cloud del contenitore

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di arresto di un contenitore denominato `proxy`.
```
bluemix ic stop proxy
```


## bluemix ic top
{: #bluemix_ic_top}

Mostrare i processi in esecuzione nel contenitore. Per ulteriori informazioni, vedi il comando [top ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/top/){: new_window} nella guida di Docker.

```
bluemix ic top CONTENITORE [CONTENITORE]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di visualizzazione dei processi di un contenitore denominato `mio_contenitore`.
```
bluemix ic top mio_contenitore
```


## bluemix ic unpause
{: #unpause}

Riprendere tutti i processi all'interno di un contenitore in esecuzione. Per ulteriori informazioni, vedi il comando [unpause ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/unpause/){: new_window} nella guida di Docker. Per mettere in pausa un contenitore, vedi il comando [bluemix ic pause](#pause).

```
bluemix ic unpause CONTENITORE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   </dl>

<strong>Risposte</strong>:

- Esecuzione del contenitore ripresa correttamente.

- Comando non riuscito con il servizio cloud del contenitore

 `{messaggio}`

 Dove `{messaggio}` è
l'errore correlato.

- Comando non riuscito - Impossibile connettersi al servizio cloud del contenitore

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di ripresa dell'esecuzione di un contenitore denominato `proxy`:
```
bluemix ic unpause proxy
```


## bluemix ic unprovision
{: #bluemix_ic_unprovision}

Elimina il servizio IBM Containers dallo spazio Bluemix a cui sei collegato.

<strong>Attenzione</strong>: quando esegui questo comando, tutti i tuoi singoli contenitori e gruppi di contenitori vengono persi. Il tuo spazio sarà ancora disponibile in Bluemix. Per iniziare a utilizzare di nuovo IBM Containers, devi eseguire `bluemix ic reprovision` per effettuare nuovamente il provisioning del servizio IBM Containers.

```
bluemix ic reprovision [--force|-f]
```
<strong>Opzioni del comando</strong>:

<dl>
   <dt>--force|-f (facoltativo)</dt>
   <dd>Forza l'eliminazione di Bluemix dallo spazio Bluemix.</dd>
 </dl>


## bluemix ic version
{: #bluemix_ic_version}

Mostrare la versione di Docker e dell'API IBM Containers.

```
bluemix ic version
```

<strong>Prerequisiti</strong>:  Docker

Per visualizzare la versione di IBM Containers, eseguire `bluemix ic info`. Per ulteriori informazioni, vedi il comando [version ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/version/){: new_window} nella guida di Docker.


## bluemix ic volume-create
{: #bluemix_ic_volume_create}

Creare un volume.

```
bluemix ic volume-create NOME_VOLUME NOME_FS
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>NOME_FS</i> (facoltativo)</dt>
   <dd>Il nome della condivisione file. Se non viene denominata o non è disponibile alcuna condivisione file, il volume sarà creato nella condivisione file predefinita dello spazio.</dd>
   <dt><i>NOME_VOLUME</i> (obbligatorio)</dt>
   <dd>Il nome del volume. Il nome può contenere lettere minuscole, numeri, caratteri di sottolineatura (_) e trattini (-).</dd>
   </dl>


<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di creazione di un volume.
```
bluemix ic volume-create volume_name fileshare_name
```


## bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

Elencare le condivisioni file.

```
bluemix ic volume-fs
```


## bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

Creare una condivisione file.

```
bluemix ic volume-fs-create NOME_CONDIVISIONE_FILE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>NOME_CONDIVISIONE_FILE</i> (obbligatorio)</dt>
   <dd>Il nome della condivisione file. Il nome può contenere lettere minuscole, numeri, caratteri di sottolineatura (_) e trattini (-).</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di creazione di una condivisione file.
```
bluemix ic volume-fs-create my_file_share
```


## bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

Elencare tutte le caratteristiche della condivisione file.

```
bluemix ic volume-fs-flavors
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione


## bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

Ispezionare una condivisione file.

```
bluemix ic volume-fs-inspect NOME_CONDIVISIONE_FILE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

  <dl>
  <dt><i>NOME_CONDIVISIONE_FILE</i> (obbligatorio)</dt>
   <dd>Il nome della condivisione file.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio è una richiesta di ispezione di una condivisione file, dove `my_file_share` è il nome della condivisione file.
```
bluemix ic volume-fs-inspect my_file_share
```


## bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

Rimuovere una condivisione file.

```
bluemix ic volume-fs-remove NOME_CONDIVISIONE_FILE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>NOME_CONDIVISIONE_FILE</i> (obbligatorio)</dt>
   <dd>Il nome della condivisione file.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di rimozione di una condivisione file, dove `my_file_share` è il nome della condivisione file.
```
bluemix ic volume-fs-remove my_file_share
```


## bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

Ispezionare un volume.

```
bluemix ic volume-inspect NOME_VOLUME
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>NOME_VOLUME</i> (obbligatorio)</dt>
   <dd>Il nome del volume.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio è una richiesta di ispezione di un volume, dove `nome_volume` è il nome del volume.
```
bluemix ic volume-inspect volume_name
```


## bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

Rimuovere un volume.

```
bluemix ic volume-remove NOME_VOLUME
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>NOME_VOLUME</i> (obbligatorio)</dt>
   <dd>Il nome del volume.</dd>
    </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di rimozione di un volume, dove `nome_volume` è il nome del volume.
```
bluemix ic volume-remove nome_volume
```


## bluemix ic volumes
{: #bluemix_ic_volumes}

Elencare i volumi.

```
bluemix ic volumes
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione


## bluemix ic wait
{: #bluemix_ic_wait}

Chiudere un contenitore e visualizzare il codice di uscita come conferma. Per ulteriori informazioni, vedi il comando [wait ![icona link esterno](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/wait/){: new_window} nella guida di Docker.

```
bluemix ic wait CONTENITORE [CONTENITORE]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di chiusura di un contenitore denominato `mio_contenitore`:
```
bluemix ic wait mio_contenitore
```


## bluemix ic wait-status
{: #bluemix_ic_wait_status}

Attendere che un singolo contenitore o gruppo di contenitori raggiunga lo stato non temporaneo. Durante questo tempo di attesa, la riga di comando non viene restituita e non puoi immettere i comandi. Non appena il contenitore raggiunge lo stato non temporaneo, viene visualizzato il messaggio OK. Per i singoli contenitori, gli stati non temporanei includono In esecuzione, Arresto, Arresto anomalo, In pausa o Sospeso. Per i gruppi di contenitori, gli stati non temporanei includono CREATE_COMPLETE, UPDATE_COMPLETE o FAILED

```
bluemix ic wait-status CONTAINER
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di chiusura di un contenitore denominato `mio_contenitore`:
```
bluemix ic wait mio_contenitore
```
