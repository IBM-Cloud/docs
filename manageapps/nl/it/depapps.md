---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-11"
---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Distribuzione delle applicazioni
{: #deployingapps}

Puoi distribuire applicazioni in {{site.data.keyword.Bluemix}}
utilizzando vari metodi, quali ad esempio l'interfaccia riga di comando e gli ambienti di
sviluppo integrati (Integrated Development Environments, IDE). Puoi anche utilizzare i manifest
dell'applicazione per distribuire applicazioni. Utilizzando un manifest dell'applicazione, riduci
il numero di dettagli di distribuzione che devi specificare ogni volta che
distribuisci un'applicazione a {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Distribuzione delle applicazioni
{: #appdeploy}

La distribuzione di un'applicazione in {{site.data.keyword.Bluemix_notm}} include
due fasi, la preparazione dell'applicazione e il suo avvio.

Cloud Foundry supporta Diego, che è la nuova architettura di runtime predefinita che fornisce una serie di funzionalità che migliorano l'esperienza di sviluppo dell'applicazione per l'hosting e la messa a punto delle piattaforme cloud. Questo aggiornamento dell'architettura fornisce una miglioramento nelle prestazioni e operazioni generale della piattaforma Cloud Foundry. La nuova architettura fornisce supporto per diverse tecnologie del contenitore dell'applicazione, inclusi Garden e Windows, un pacchetto SSH che permette l'accesso diretto al contenitore dell'applicazione, e altre modifiche innovative. Per ulteriori informazioni sul recente aggiornamento dell'architettura, consulta [{{site.data.keyword.Bluemix_notm}} Cloud Foundry: Diego is live ![icona link esterno](../icons/launch-glyph.svg)](https://www.ibm.com/blogs/bluemix/2017/01/bluemix-cloud-foundry-diego-live/){: new_window}.


Tutte le nuove applicazioni che crei saranno eseguite su Diego e devi avviare la migrazione delle tue applicazioni esistenti in esecuzione sui DEA alla nuova architettura Diego.

**Nota**: l'architettura Diego Cloud Foundry influenza tutti gli ambiente della regione di {{site.data.keyword.Bluemix_notm}} pubblico. Gli ambienti {{site.data.keyword.Bluemix_notm}} dedicato e {{site.data.keyword.Bluemix_notm}} locale saranno aggiornati in una data successiva.

### Preparazione di un'applicazione
{: #diego}

Durante la fase di preparazione, Diego si occupa di tutti gli aspetti relativi alla organizzazione del contenitore dell'applicazione. Quando esegui il push di un'applicazione, il controller cloud invia una richiesta di preparazione a Diego, che esegue l'azione di assegnazione delle istanze dell'applicazione. Il backend di Diego organizza i contenitori dell'applicaizone in modo sicuro per garantire la congruenza a lungo termine e alla tolleranza dell'errore, che bilancia il carico tra una serie di macchine virtuali denominate celle. In aggiunta, Diego assicura che gli utenti possono accedere ai log delle loro applicazioni. Tutti i componenti Diego sono progettati per essere in cluster, che significa che puoi creare diverse zone di disponibilità.

Per convalidare l'integrità dell'applicazione, Diego supporta gli stessi controlli basati sulla PORTA che sono stati utilizzati da DEA. Tuttavia, Diego è anche progettato per avere più opzioni generiche come i controlli di integrità basati sull'URL, che dovrebbe venire abilitati in futuro.

#### Preparazione di una nuova applicazione
{: #stageapp}

Tutte le nuove applicazioni vengono distribuite all'architettura Diego. Per preparare una nuova applicazione, distribuiscila con il comando **cf push**.

  1. Distribuisci l'applicazione:
  ```
  $ cf push APPLICATION_NAME
  ```

Per ulteriori dettagli sul comando **cf push**, consulta [cf push](/docs/cli/reference/cfcommands/index.html#cf_push).

### Migrazione di un'applicazione esistente a Diego
{: #migrateapp}

Diego è l'architettura Cloud Foundry predefinita per {{site.data.keyword.Bluemix_notm}} e il supporto per i DEA sarà rimosso, per cui devi migrare tutte le tue applicazioni esistenti aggiornando ogni applicazione. Avvia la migrazione delle tue applicazioni a Diego aggiornando l'applicazione con l'indicatore Diego. L'applicazione tenta immediatamente di avviare l'esecuzione in Diego e arresta l'esecuzione nei DEA.

Come la tua applicazione viene aggiornata dall'architettura DEA a Diego, potresti riscontrare un tempo di inattività piccolo o prolungato, se l'applicazione non è compatibile con Diego. Per limitare il tempo di inattività, esegui [blue-green deploy](/docs/manageapps/updapps.html#blue_green) distribuendo una copia della tua applicazione a Diego e quindi scambiando le rotte e ridimensionando l'applicazione DEA.

Completa la seguente procedura per migrare la tua applicazione a Diego:

 1.  Installa [cf CLI ![icona link esterno](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window} e il [Diego-Enabler CLI Plugin ![icona link esterno](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-incubator/Diego-Enabler){:new_window}.
 2. Controlla l'[elenco di problemi noti](depapps.html#knownissues).
 3. Configura l'indicatore Diego per modificare la tua applicazione per l'esecuzione su Diego:
  ```
  $ cf enable-diego APPLICATION_NAME
  ```

Dopo aver aggiornato la tua applicazione, verifica che sia avviata. Se è impossibile avviare la tua applicazione migrata, rimarrà offline finché non identifichi e risolvi il problema e quindi riavvi l'applicazione.

IBM ti avviserà del prossimo periodo di migrazione obbligatoria quando il supporto all'architettura DEA sarà rimosso e se non hai migrato le tue applicazioni, il team operativo lo farà per te.

Per convalidare su quale backend l'applicazione è in esecuzione, utilizzare il seguente comando:

  ```
  $ cf has-diego-enabled APPLICATION_NAME
  ```

#### Problemi noti sulla migrazione a Diego
{: #knownissues}

I seguenti sono i problemi noti che potresti dover risolvere durante la migrazione delle tue applicazioni a Diego:

  * Le applicazioni di lavoro distribuite con l'opzione `--no-route` non sono riportate come integre. Per evitare questo, disabilita il controllo di integrità basato sulla porta con il comando `cf set-health-check APP_NAME none`.
  * Il comando **cf files** non è più supportato. Viene sostituito dal comando **cf ssh**. Per ulteriori dettagli sul comando **cf ssh**, consulta [cf ssh](/docs/cli/reference/cfcommands/index.html#cf_ssh).
  * Alcune applicazioni potrebbero utilizzare un gran numero di descrittori file (inode). Se riscontri questo problema, devi aumentare la quota disco della tua applicazione con il comando `cf scale APP_NAME [-k DISK]`.

Per l'elenco completo dei problemi noti, consulta la pagina della documentazione Cloud Foundry per [Migrating to Diego ![icona link esterno](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/diego-design-notes/blob/master/migrating-to-diego.md){: new_window}.

Finché il supporto per la vecchia architettura DEA non viene rimosso, puoi eseguire il seguente comando per tornare ai DEA: `cf disable-diego APPLICATION_NAME`. Puoi inoltre ancora distribuire nuove applicazioni all'architettura DEA finché non viene rimosso il supporto:

**Nota**: devi avere sia la [cf CLI ![icona link esterno](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window} che il [Diego-Enabler CLI Plugin ![icona link esterno](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-incubator/Diego-Enabler){:new_window} installati per utilizzare il comando `disable-diego`.

1. Distribuisci l'applicazione senza avviarla:
```
$ cf push APPLICATION_NAME --no-start
```
2. segui il comando disable-diego:
```
$ cf disable-diego APPLICATION_NAME
```
3. Avvia l'applicazione:
```
$ cf start APPLICATION_NAME
```

### Avvio di un'applicazione
{: #startapp}

Quando un'applicazione viene avviata, vengono create l'istanza o le istanze del contenitore dell'applicazione. Per le applicazioni in esecuzione su Diego, puoi utilizzare il comando **cf ssh** o **cf scp** per accedere al file system del contenitore dell'applicazione che include i log. Il comando **cf files** non funziona per le applicazioni in esecuzione sull'architettura Diego.

**Nota**: se hai ancora applicazioni in esecuzione sui DEA, puoi utilizzare il comando **cf files** per visualizzare i file nel contenitore dell'applicaizone finché il supporto per i DEA non viene rimosso.

Se l'avvio dell'applicazione non riesce, l'applicazione viene arrestata e l'intero contenuto del tuo contenitore dell'applicazione viene rimosso. Pertanto, se un'applicazione si arresta o se
il processo di preparazione di un'applicazione non riesce, i file di log non
saranno disponibili per l'uso.

Se i log della tua applicazione non sono più disponibili e i comandi **cf ssh**, **cf scp** o **cf files** non possono essere più utilizzati per visualizzare la causa degli errori di preparazione nel contenitore dell'applicaizone, puoi invece utilizzare il comando **cf logs**. Il comando **cf
logs** utilizza l'aggregatore di log di Cloud Foundry per
raccogliere i dettagli dei tuoi log di applicazione e di sistema e potrai vedere
ciò che è presente nel buffer all'interno dell'aggregatore di log. Per ulteriori informazioni sull'aggregatore di log, vedi [Logging in Cloud Foundry ![icona link esterno](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}.

**Nota:** la dimensione del buffer è limitata. Se un'applicazione viene eseguita per tanto tempo e non viene riavviata, è possibile quando immetti il comando `cf logs appname --recent` i log non vengano visualizzati perché il buffer dei log potrebbe essere stato cancellato. Pertanto, per eseguire il debug degli errori di preparazione di un'applicazione di grandi dimensioni, puoi immettere il comando `cf logs appname` in una riga di comando diversa dall'interfaccia riga di comando cf per tracciare i log quando distribuisci l'applicazione.

Se rilevi dei problemi durante la preparazione delle
tue applicazioni su {{site.data.keyword.Bluemix_notm}},
puoi seguire le istruzioni che si trovano in [Debug degli
errori di preparazione](/docs/debug/index.html#debugging-staging-errors) per risolvere il problema.


## Distribuzione delle applicazioni mediante il comando cf
{: #dep_apps}

Quando distribuisci le tue applicazioni in {{site.data.keyword.Bluemix_notm}} dall'interfaccia
riga di comando, devi fornire un pacchetto di build come ambiente di runtime a seconda del linguaggio
e del framework della tua applicazione. Inoltre, puoi utilizzare il servizio Delivery Pipeline per distribuire le applicazioni in {{site.data.keyword.Bluemix_notm}}.

{{site.data.keyword.Bluemix_notm}} fornisce pacchetti di build integrati che supportano Java e Node.js. Se utilizzi questi
linguaggi e questi framework, non dovrai specificare il pacchetto di build durante
la distribuzione della tua applicazione mediante l'interfaccia riga di comando. Poiché {{site.data.keyword.Bluemix_notm}} è
        creato su Cloud Foundry, il comando è impostato come valore predefinito su questi pacchetti di build.

Se utilizzi un pacchetto di build esterno, devi specificare
l'URL del pacchetto di build utilizzando l'opzione **-b**
quando esegui la distribuzione della tua applicazione in {{site.data.keyword.Bluemix_notm}} dal
prompt dei comandi.

  * Per distribuire pacchetti server Liberty in {{site.data.keyword.Bluemix_notm}}, utilizza il seguente comando dalla tua directory di origine:

  ```
  cf push
  ```

  Per ulteriori
informazioni sul pacchetto di build Liberty, vedi [Liberty
for Java](/docs/runtimes/liberty/index.html).

  * Per distribuire le applicazioni Java Tomcat a {{site.data.keyword.Bluemix_notm}}, utilizza il seguente comando:

  ```
  cf push appname -b https://github.com/cloudfoundry/java-buildpack.git -p app_path
  ```

  * Per distribuire pacchetti WAR in {{site.data.keyword.Bluemix_notm}},
utilizza il comando
seguente:

  ```
  cf push appname -p app.war
  ```
  In alternativa, puoi specificare
una directory contenente i tuoi file applicazione utilizzando il seguente
comando:

  ```
  cf push appname -p "./app"
  ```

  * Per distribuire le applicazioni Node.js in {{site.data.keyword.Bluemix_notm}}, utilizza il comando
                                                  seguente:

  ```
  cf push appname -p percorso_applicazione
  ```

Perché
                                                  l'applicazione venga riconosciuta dal pacchetto
                                                  di build Node.js, è necessario che un file
                                                  `package.json` sia presente nella tua applicazione Node.js. Il file `app.js`
è lo script di avvio per l'applicazione e può essere specificato nel file `package.json`. Il seguente
                                                  esempio mostra un semplice file
                                                  `package.json`:

  ```
  {
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": ">=3.4.7 <4",
                "jade": ">=1.1.4"
        },
        "scripts": {
                "start": "node app.js"
        },
        "engines": {
                "node": ">=0.10.0"
        },
        "repository": {}
  }
  ```

  Per ulteriori informazioni sul file `package.json`, consulta [package.json ![icona link esterno](../icons/launch-glyph.svg)](https://www.npmjs.org/doc/files/package.json.html){:new_window}.

  * Per distribuire applicazioni PHP, Ruby o Python a {{site.data.keyword.Bluemix_notm}},
utilizza il seguente comando dalla directory che contiene l'origine della tua applicazione:

  ```
  cf push nome_applicazione
  ```

### Distribuzione di un'applicazione in più spazi

Un'applicazione è specifica dello spazio in cui viene distribuita. In {{site.data.keyword.Bluemix_notm}} non puoi spostare o copiare un'applicazione da uno spazio all'altro. Per distribuire un'applicazione in più spazi, devi distribuirla in ciascuno spazio in
cui desideri utilizzarla attenendoti alla seguente procedura:

  1. Passa allo spazio in cui desideri distribuire la tua applicazione
utilizzando il comando **cf target** con l'opzione **-s**:

  ```
  cf target -s <space_name>
  ```

  2. Passa alla directory della tua applicazione e distribuiscila utilizzando il comando **cf push**, dove nome_applicazione deve essere univoco all'interno del tuo dominio.

  ```
  cf push nome_applicazione
  ```

## Manifest dell'applicazione
{: #appmanifest}

I manifest dell'applicazione contengono opzioni che si applicano
al comando **cf push**. Puoi utilizzare un
manifest dell'applicazione per ridurre il numero di dettagli di distribuzione che devi specificare
ogni volta che distribuisci un'applicazione in {{site.data.keyword.Bluemix_notm}}.

Nei manifest dell'applicazione puoi specificare opzioni,
quali ad esempio il numero di istanze dell'applicazione da creare,
la quantità di memoria e la quota di disco da assegnare alle applicazioni e
altre variabili di ambiente dell'applicazione. Inoltre, puoi
utilizzare i manifest dell'applicazione per automatizzare le distribuzioni dell'applicazione. Il nome predefinito di un file manifest è `manifest.yml`.

### Opzioni supportate nel file manifest

La seguente tabella mostra le opzioni supportate che puoi
utilizzare in un file manifest dell'applicazione. Se scegli di utilizzare
un nome file diverso da `manifest.yml`,
devi utilizzare l'opzione **-f** con il comando **cf
push**. Nel seguente esempio, `appManifest.yml` è
il nome file:

```
cf push -f appManifest.yml
```

<p>  </p>


|Opzioni	|Descrizione	|Utilizzo o esempio|
|:----------|:--------------|:---------------|
|**buildpack**	|L'URL o il nome del pacchetto di build personalizzato.	|`buildpack: ` *URL_pacchettodibuild*|
|**disk_quota**	|La quota di disco assegnata per un'applicazione. Il valore predefinito è 1 G.	|`disk_quota: 500M`|
|**dominio**	|Il nome dominio dell'applicazione in {{site.data.keyword.Bluemix_notm}}.	|`domain:` ng.bluemix.net|
|**host**	|Il nome host dell'applicazione in {{site.data.keyword.Bluemix_notm}}. Questo valore deve essere univoco nell'ambiente {{site.data.keyword.Bluemix_notm}}.	|`host: ` *home_host*|
|**nome**	|Il nome applicazione in {{site.data.keyword.Bluemix_notm}}. Questo valore deve essere univoco nell'ambiente {{site.data.keyword.Bluemix_notm}}.	|`name: ` *nomeapplicazione*|
|**path**	|L'ubicazione della tua applicazione. Questo valore può essere un percorso relativo o percorso assoluto.	|`path: ` *percorso_alla_applicazione*|
|**command**	|Il comando di avvio personalizzato per la tua applicazione o il comando per eseguire i file di script.	|`command:` *custom_command* `command:` *bash ./run.sh*|
|**memory**	|La quantità di memoria da assegnare per l'applicazione. Il valore predefinito è 1G.	|`memory: 512M`|
|**instances**	|Il numero di istanze da creare per la tua applicazione.	|`instances: 2`|
|**timeout**	|La quantità massima di tempo (in secondi) impiegata per l'avvio dell'applicazione. Il valore predefinito è 60 secondi.	|`timeout: 80
`|
|**no-route**	|Un valore booleano che impedisce l'assegnazione di una rotta all'applicazione se l'applicazione è solo in esecuzione in background. Il valore predefinito è **false**.	|`no-route: true`|
|**random-route**	|Un valore booleano per assegnare una rotta casuale all'applicazione. Il valore predefinito è **false**.	|`random-route: true`|
|**services**	|I servizi di cui eseguire il bind all'applicazione.	|`services:   - mysql_maptest`|
|**env**	|Le variabili di ambiente personalizzate per l'applicazione.|`env: DEV_ENV: production`|
{: caption="Table 1. Supported options in the manifest YAML file" caption-side="top"}

### Un file manifest.yml di esempio

Il seguente esempio mostra un file manifest per un'applicazione Node.js
che utilizza il pacchetto di build Node.js community integrato
in {{site.data.keyword.Bluemix_notm}}.

```
---
- name: myNodejsapp
  memory: 256M
  disk_quota: 512M
  path: /dev/myNodejsApp
  buildpack: nodejs_buildpack
  host: nodejs001
  domain: mybluemix.net
  command: node app.js
  timeout: 80
  services:
  - mongo_8917
  env:
    env_type: production
```
{:codeblock}

## Variabili di ambiente
{: #app_env}

Le variabili di ambiente contengono le informazioni di ambiente
di un'applicazione distribuita in {{site.data.keyword.Bluemix_notm}}. Oltre alle variabili di ambiente impostate da un * Droplet Execution Agent
(DEA)* e da pacchetti di build, su {{site.data.keyword.Bluemix_notm}}
puoi impostare anche variabili di ambiente specifiche dell'applicazione.

Puoi visualizzare le seguenti variabili di ambiente di
un'applicazione {{site.data.keyword.Bluemix_notm}} in esecuzione
utilizzando il comando **cf env** oppure dall'interfaccia utente
{{site.data.keyword.Bluemix_notm}}:

  * Variabili definite dall'utente specifiche di un'applicazione. Per informazioni su come aggiungere una variabile definita dall'utente a un'applicazione, vedi [Aggiunta di variabili di ambiente definite dall'utente ![icona link esterno](../icons/launch-glyph.svg)](#ud_env){:new_window}.

  * La variabile VCAP_SERVICES, che contiene informazioni di connessione per accedere a un'istanza di servizio. Se la tua applicazione è associata a più servizi, la variabile VCAP_SERVICES include le informazioni di connessione per ciascuna istanza di servizio. Ad
esempio:

  ```
  {
   "VCAP_SERVICES": {
    "AppScan Dynamic Analyzer": [
     {
      "credentials": {
       "bindingid": "0ab3162a-867e-4137-a2e7-39463a89472e",
       "password": "xE/jh/PlRj3ruuy8RCl8JNyEywaivRH1xXSZcbVExKg="
      },
      "label": "AppScan Dynamic Analyzer",
      "name": "AppScan Dynamic Analyzer-9q",
      "plan": "standard",
      "tags": [
       "Security",
       "security",
       "ibm_created"
      ]
     }
    ],
    "mysql-5.5": [
     {
      "credentials": {
       "host": "23.246.200.38",
       "hostname": "23.246.200.38",
       "name": "d296abcc06c9e418b94abcaafdf547620",
       "password": "peRiYCG4ZYqu3",
       "port": 3307,
       "uri": "mysql://uzpGf7eGJ7mtB:peRiYCG4ZYqu3@23.246.200.38:3307/d296abcc06c9e418b94abcaafdf547620",
       "user": "uzpGf7eGJ7mtB",
       "username": "uzpGf7eGJ7mtB"
      },
      "label": "mysql-5.5",
      "name": "mysql-ix",
      "plan": "300",
      "tags": [
       "mysql",
       "relational",
       "data_management",
       "ibm_experimental"
      ]
     }
    ]
   }
  }
  ```

Puoi accedere anche alle variabili di ambiente impostate dal DEA e dai pacchetti di build.

Le seguenti variabili sono definite dal DEA:

<dl>
  <dt><strong>HOME</strong></dt>
  <dd>La directory root dell'applicazione distribuita.</dd>
  <dt><strong>MEMORY_LIMIT</strong></dt>
  <dd>La quantità massima di memoria che ogni istanza della tua applicazione può
utilizzare. Puoi specificare il valore in un file <span class="ph filepath">manifest.yml</span> di applicazione
oppure nella riga di comando quando distribuisci l'applicazione.</dd>
  <dt><strong>PORT</strong></dt>
  <dd>La porta sul DEA per comunicare con l'applicazione. Il
DEA assegna una porta all'applicazione nel periodo di preparazione.</dd>
  <dt><strong>PWD</strong></dt>
  <dd>La directory di lavoro corrente in cui è in esecuzione il pacchetto di build.</dd>
  <dt><strong>TMPDIR</strong></dt>
  <dd>La directory in cui vengono archiviati i file temporanei e di preparazione.</dd>
  <dt><strong>USER</strong></dt>
  <dd>L'ID utente sotto cui il DEA è in esecuzione.</dd>
  <dt><strong>VCAP_APP_HOST</strong></dt>
  <dd>L'indirizzo IP dell'host DEA.</dd>
  <dt><strong>VCAP_APPLICATION</strong></dt>
  <dd>Una stringa JSON che contiene informazioni sull'applicazione distribuita. Le informazioni includono il nome dell'applicazione, gli URI, i limiti di memoria,
la data e l'ora in cui l'applicazione ha raggiunto lo stato attuale e
così via. Ad
                                    esempio:
  <pre class="pre codeblock"><code>
  {
    "limits": {
        "mem": 512,
        "disk": 1024,
        "fds": 16384
    },
    "application_version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "application_name": "testapp",
    "application_uris": [
        "testapp.AppDomainName.mybluemix.net"
    ],
    "version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "name": "testapp",
    "space_name": "dev",
    "space_id": "c6ed3a8e-436b-43ac-9f96-b676ee335000",
    "uris": [
        "testapp.AppDomainName.mybluemix.net"
    ],
    "users": null,
    "application_id": "e984bb73-4c4e-414b-84b7-c28c87f84003",
    "instance_id": "09f50e22848d4ec0b943e9e487c23569",
    "instance_index": 0,
    "host": "0.0.0.0",
    "port": 61399,
    "started_at": "2015-01-16 06:50:51 +0000",
    "started_at_timestamp": 1421391051,
    "start": "2015-01-16 06:50:51 +0000",
    "state_timestamp": 1421391051
}
</code></pre></dd>
  <dt><strong>VCAP_SERVICES</strong></dt>
  <dd>Una stringa JSON contenente informazioni sul servizio
associato all'applicazione distribuita. Ad
                                    esempio:
  <pre class="pre codeblock"><code>
  {
    "mysql-5.5": [
        {
            "name": "mysql-ix",
            "label": "mysql-5.5",
            "tags":[
                "mysql",
                "relational",
                "data_management",
                "ibm_experimental"
            ],
            "plan": "300",
            "credentials": {
                "name": "d296abcc06c9e418b94abcaafdf547620",
                "hostname": "23.246.200.38",
                "host": "23.246.200.38",
                "port": 3307,
                "user": "uzpGf7eGJ7mtB",
                "username": "uzpGf7eGJ7mtB",
                "password": "peRiYCG4ZYqu3",
                "uri": "mysql://uzpGf7eGJ7mtB:peRiYCG4ZYqu3@23.246.200.38:3307/d296abcc06c9e418b94abcaafdf547620"
            }
        }
    ]
}
</code></pre></dd>

</dl>

Le variabili definite dai pacchetti di build sono diverse
per ogni pacchetto di build. Consulta [Buildpacks ![icona link esterno](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-community/cf-docs-contrib/wiki/Buildpacks){:new_window} per eventuali altri pacchetti di build compatibili.

<ul>
    <li>Le seguenti variabili sono definite dal pacchetto di build Liberty:

	  <dl>
	  <dt><strong>JAVA_HOME</strong></dt>
	  <dd>L'ubicazione dell'SDK Java che esegue l'applicazione.</dd>
	  <dt><strong>IBM_JAVA_OPTIONS</strong></dt>
	  <dd>Le opzioni SDK Java da utilizzare durante l'esecuzione dell'applicazione.</dd>
	  <dt><strong>IBM_JAVA_COMMAND_LINE</strong></dt>
	  <dd>Il comando Java per avviare un'istanza del server di profili Liberty nel DEA.</dd>
	  <dt><strong>WLP_USR_DIR</strong></dt>
	  <dd>L'ubicazione delle risorse e delle definizioni server condivise durante l'avvio di
un'istanza del server di profili Liberty nel DEA.</dd>
	  <dt><strong>WLP_OUTPUT_DIR</strong></dt>
	  <dd>L'ubicazione dell'output generato, quali ad esempio file di log e
directory di lavoro di un'istanza del server di profili Liberty in esecuzione.</dd>
	  </dl>
</li>
<li>Le seguenti variabili sono definite dal pacchetto di build Node.js:
	<dl>
	<dt><strong>BUILD_DIR</strong></dt>
	<dd>La directory dell'ambiente di runtime Node.js.</dd>
	<dt><strong>CACHE_DIR</strong></dt>
	<dd>La directory che l'ambiente di runtime Node.js utilizza per la memorizzazione nella cache.</dd>
	<dt><strong>PATH</strong></dt>
	<dd>Il percorso di sistema utilizzato dall'ambiente di runtime Node.js.</dd>
	</dl>
</li>
</li>
</ul>

Puoi utilizzare il seguente codice di esempio Node.js per ottenere il valore della variabile di ambiente VCAP_SERVICES:

```
if (process.env.VCAP_SERVICES) {
    var env = JSON.parse (process.env.VCAP_SERVICES);
    myvar = env.foo[bar].foo;
}
```

Per ulteriori informazioni sulle singole variabili di ambiente, vedi [Cloud Foundry Environment Variables ![icona link esterno](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/environment-variable.html){:new_window}.

## Personalizzazione delle distribuzioni dell'applicazione
{: #customize_dep}

Puoi personalizzare le attività di distribuzione delle tue applicazioni. Ad esempio, puoi specificare i comandi di avvio delle tue applicazioni e
configurare il loro ambiente di avvio.
{:shortdesc}

### Specifica dei comandi di avvio

Per specificare i comandi di avvio della tua applicazione, puoi utilizzare uno dei seguenti modi. I comandi di avvio che specificherai sovrascriveranno i comandi di avvio predefiniti
forniti dal pacchetto di build.

**Nota:** se vuoi assegnare una precedenza ai comandi di avvio del pacchetto di build, specifica **null** come comando di avvio.

  * Utilizza il comando **cf push** e specifica il parametro -c. Ad esempio, quando distribuisci un'applicazione Node.js, puoi specificare il comando di avvio **node app.js** nel parametro -c:

  ```
  cf push appname -p app_path -c "node app.js"
  ```

  * Utilizza il parametro di comando nel file `manifest.yml`. Ad esempio, quando distribuisci un'applicazione Node.js,
puoi specificare il comando di avvio **node app.js**
nel file manifest:

  ```
  command: node app.js
  ```


### Aggiunta di variabili di ambiente definite dall'utente
{: #ud_env}

Le variabili di ambiente definite dall'utente sono specifiche per un'applicazione. Per aggiungere una variabile di ambiente definita dall'utente a un'applicazione in esecuzione puoi utilizzare le seguenti opzioni:

  * Utilizza l'interfaccia utente di {{site.data.keyword.Bluemix_notm}}. Completa la seguente
procedura:
    1. Sul Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sul tile della tua applicazione. Viene visualizzata la pagina dei dettagli dell'applicazione.
	2. Fai clic su **Variabili di ambiente**.
	3. Fai clic su **DEFINITO DALL'UTENTE** e quindi su **AGGIUNGI**.
	4. Compila i campi richiesti, quindi fai clic su **SALVA**.
  * Utilizza l'interfaccia riga di comando cf. Aggiungi una variabile definita dall'utente utilizzando il comando `cf set-env`. Ad
esempio:
    ```
    cf set-env appname env_var_name env_var_value
    ```

  * Utilizza il file `manifest.yml`. Aggiungi coppie di valori nel file. Ad
esempio:
    ```
	env:
      VAR1:value1
      VAR2:value2
    ```

Una volta aggiunta una variabile di ambiente definita dall'utente, puoi utilizzare il seguente codice di esempio Node.js per ottenere il valore della variabile che hai definito:

```
var myEnv = process.env.env_var_name;
console.log("My user defined = " + myEnv);
```

### Configurazione dell'ambiente di avvio

Per configurare l'ambiente di avvio della tua applicazione,
puoi aggiungere script di shell nella directory `/.profile.d`. La directory `/.profile.d` si trova nella directory
di build della tua applicazione. Gli script nella directory `/.profile.d`
vengono eseguiti da {{site.data.keyword.Bluemix_notm}} prima
dell'esecuzione dell'applicazione. Ad esempio, puoi impostare la variabile di ambiente NODE_ENV su **production** inserendo un file `node_env.sh` che contiene quanto segue nella directory `/.profile.d`:

```
export NODE_ENV=production;
```

###Blocco del caricamento di file e directory

Quando utilizzi l'interfaccia riga di comando cf per distribuire un'applicazione,
puoi risparmiare tempo per il caricamento ignorando alcuni file e
directory che {{site.data.keyword.Bluemix_notm}} può
ottenere altrove. Per impedire il caricamento di tali file e directory
in {{site.data.keyword.Bluemix_notm}},
puoi creare un file `.cfignore` nella
directory root della tua applicazione.

**Nota:** il file `.cfignore` deve essere in formato UTF-8.

Il file `.cfignore`
contiene i nomi dei file e delle directory che vuoi ignorare,
un nome per ciascuna riga. Puoi utilizzare un asterisco (*) come carattere jolly. Quando specifichi una directory, verranno ignorati anche tutti i file e le sottodirectory
sotto tale directory. Ad esempio, il seguente contenuto
nel file `.cfignore` indica che tutti i file `.swp`
e tutti i file e sottodirectory sotto la directory `tmp/`
non verranno caricati in {{site.data.keyword.Bluemix_notm}}.

```
*.swp
tmp/
```

# Link correlati
{: #rellinks notoc}

## Link correlati
{: #general}

* [Deploying with Application Manifests ![icona link esterno](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){:new_window}
* [CF Manifest Generator ![icona link esterno](../icons/launch-glyph.svg)](http://cfmanigen.mybluemix.net/){:new_window}
* [Getting Started with cf v6 ![icona link esterno](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html){:new_window}
* [Getting Started with IBM Continuous Delivery Pipeline for Bluemix](/docs/services/DeliveryPipeline/index.html#getstartwithCD)
