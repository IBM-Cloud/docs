---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Distribuzione delle applicazioni
{: #deployingapps}

*Ultimo aggiornamento: 9 maggio 2016*

Puoi distribuire applicazioni in {{site.data.keyword.Bluemix}}
utilizzando vari metodi, quali ad esempio l'interfaccia riga di comando e gli ambienti di
sviluppo integrati (Integrated Development Environments, IDE). Puoi anche utilizzare i manifest
dell'applicazione per distribuire applicazioni. Utilizzando un manifest dell'applicazione, riduci
il numero di dettagli di distribuzione che devi specificare ogni volta che
distribuisci un'applicazione a {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

##Distribuzione delle applicazioni
{: #appdeploy}

La distribuzione di un'applicazione in {{site.data.keyword.Bluemix_notm}} include
due fasi, la preparazione dell'applicazione e il suo avvio.

###Preparazione di un'applicazione

Durante la fase
di preparazione, un Droplet Execution Agent    (DEA) utilizza le informazioni
che tu fornisci nell'interfaccia riga di comando cf o nel file `manifest.yml`
per stabilire che cosa creare per la preparazione dell'applicazione. Il DEA seleziona
un pacchetto di build appropriato per preparare la tua applicazione; il risultato del
processo di preparazione è un droplet. Per ulteriori informazioni sulla distribuzione di un'applicazione in {{site.data.keyword.Bluemix_notm}}, vedi [Architettura {{site.data.keyword.Bluemix_notm}}, come funziona {{site.data.keyword.Bluemix_notm}}](../public/index.html#publicarch).

Durante
il processo di preparazione, il DEA verifica se il pacchetto di build
corrisponde all'applicazione. Ad esempio, un runtime Liberty per un file .war o
un runtime Node.js per i file .js. Il DEA quindi crea un contenitore
isolato contenente il pacchetto di build e il codice applicativo. Il
contenitore è gestito dal componente Warden. Per ulteriori informazioni,
vedi [How Applications Are Staged](http://docs.cloudfoundry.org/concepts/how-applications-are-staged.html){:new_window}.

###Avvio di un'applicazione

Quando un'applicazione
viene avviata, vengono create l'istanza o le istanze del
contenitore Warden. Puoi utilizzare il comando **cf files** per
visualizzare i file archiviati nel file system del contenitore Warden,
quali ad esempio i log. Se l'avvio dell'applicazione non riesce, il
DEA arresta l'applicazione e tutti i contenuti del tuo contenitore Warden
vengono rimossi. Pertanto, se un'applicazione si arresta o se
il processo di preparazione di un'applicazione non riesce, i file di log non
saranno disponibili per l'uso.

Se i log della tua applicazione
non sono più disponibili e il comando **cf     files**
non potrà più essere utilizzato per vedere la causa degli errori di preparazione,
al suo posto potrai utilizzare il comando **cf logs**. Il comando **cf
logs** utilizza l'aggregatore di log di Cloud Foundry per
raccogliere i dettagli dei tuoi log di applicazione e di sistema e potrai vedere
ciò che è presente nel buffer all'interno dell'aggregatore di log. Per
ulteriori informazioni sull'aggregatore di log, vedi [Logging in Cloud Foundry](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}.

**Nota:** la dimensione del buffer è limitata. Se un'applicazione viene eseguita per tanto tempo e non viene riavviata, è possibile quando immetti `cf logs nomeapplicazione --recent` i log non vengano visualizzati perché il buffer dei log potrebbe essere stato cancellato. Pertanto, per eseguire il debug degli errori di preparazione di un'applicazione di grandi dimensioni, puoi immettere `cf logs nomeapplicazione` in una riga di comando diversa dall'interfaccia riga di comando cf per tracciare i log quando distribuisci l'applicazione.

Se rilevi dei problemi durante la preparazione delle
tue applicazioni su {{site.data.keyword.Bluemix_notm}},
puoi seguire le istruzioni che si trovano in [Debug degli
errori di preparazione](../debug/index.html#debugging-staging-errors) per risolvere il problema.

##Distribuzione delle applicazioni mediante il comando cf
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
for Java](../runtimes/liberty/index.html).
  
  * Per distribuire le applicazioni Java Tomcat a {{site.data.keyword.Bluemix_notm}}, utilizza il seguente comando:
  
```
  cf push nomeapplicazione -b https://github.com/cloudfoundry/java-buildpack.git -p app_path
```
  
  * Per distribuire pacchetti WAR in {{site.data.keyword.Bluemix_notm}},
utilizza il comando
seguente:
  
```
  cf push nomeapplicazione -p app.war
```
  In alternativa, puoi specificare
una directory contenente i tuoi file applicazione utilizzando il seguente
comando:
  
```
  cf push nomeapplicazione -p "./app"
```
  
  * Per distribuire le applicazioni Node.js in {{site.data.keyword.Bluemix_notm}}, utilizza il comando
                                                  seguente:
  
```
  cf push nomeapplicazione -p percorso_applicazione
```
  
Perché l'applicazione venga riconosciuta dal pacchetto di build Node.js, è necessario che un file
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
    
  Per
                                                  ulteriori informazioni sul file
                                                  `package.json`, vedi [package.json](https://www.npmjs.org/doc/files/package.json.html){:new_window}.
  
  * Per distribuire applicazioni PHP, Ruby o Python a {{site.data.keyword.Bluemix_notm}},
utilizza il seguente comando dalla directory che contiene l'origine della tua applicazione:
  
```
  cf push nomeapplicazione
```

###Distribuzione di un'applicazione in più spazi

Un'applicazione è specifica dello spazio in cui viene distribuita. In {{site.data.keyword.Bluemix_notm}} non puoi spostare o copiare un'applicazione da uno spazio all'altro. Per distribuire un'applicazione in più spazi, devi distribuirla in ciascuno spazio in
cui desideri utilizzarla attenendoti alla seguente procedura:

  1. Passa allo spazio in cui desideri distribuire la tua applicazione
utilizzando il comando **cf target** con l'opzione **-s**:
  
```
  cf target -s <space_name>
```
  
  2. Passa alla directory della tua applicazione e distribuiscila utilizzando il comando **cf push**, dove nomeapplicazione deve essere univoco all'interno del tuo dominio.
  
```
  cf push nomeapplicazione
```
  
##Manifest dell'applicazione
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

###Opzioni supportate nel file manifest

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
*Tabella 1. Opzioni supportate nel file manifest.yml*

###Un file `manifest.yml` di esempio

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

##Variabili di ambiente
{: #app_env}

Le variabili di ambiente contengono le informazioni di ambiente
di un'applicazione distribuita in {{site.data.keyword.Bluemix_notm}}. Oltre alle variabili di ambiente impostate da un * Droplet Execution Agent
(DEA)* e da pacchetti di build, su {{site.data.keyword.Bluemix_notm}}
puoi impostare anche variabili di ambiente specifiche dell'applicazione.

Puoi visualizzare le seguenti variabili di ambiente di
un'applicazione {{site.data.keyword.Bluemix_notm}} in esecuzione
utilizzando il comando **cf env** oppure dall'interfaccia utente
{{site.data.keyword.Bluemix_notm}}:
	
  * Variabili definite dall'utente specifiche di un'applicazione. Per informazioni su come aggiungere una variabile definita dall'utente a un'applicazione, vedi [Aggiunta di variabili di ambiente definite dall'utente](#ud_env){:new_window}.
	 
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
        "testapp.AppDomainNameng.mybluemix.net"
    ],
    "version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "name": "testapp",
    "space_name": "dev",
    "space_id": "c6ed3a8e-436b-43ac-9f96-b676ee335000",
    "uris": [
        "testapp.AppDomainNameng.mybluemix.net"
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
            "tags": [
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
per ogni pacchetto di build. Vedi [Buildpacks](https://github.com/cloudfoundry-community/cf-docs-contrib/wiki/Buildpacks){:new_window} per eventuali altri pacchetti di build compatibili.

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

Per ulteriori informazioni sulle singole variabili di ambiente, vedi [Cloud Foundry Environment Variables](http://docs.cloudfoundry.org/devguide/deploy-apps/environment-variable.html){:new_window}.

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
  cf push nomeapplicazione -p app_path -c "node app.js"
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

  * Utilizza l'interfaccia utente {{site.data.keyword.Bluemix_notm}}. Completa la seguente
procedura:
    1. Sul Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sul tile della tua applicazione. Viene visualizzata la pagina dei dettagli dell'applicazione.
	2. Nel riquadro di navigazione a sinistra,  fai clic su **Variabili di ambiente**.
	3. Fai clic su **DEFINITO DALL'UTENTE** e quindi su **AGGIUNGI**.
	4. Compila i campi richiesti, quindi fai clic su **SALVA**.
  * Utilizza l'interfaccia riga di comando cf. Aggiungi una variabile definita dall'utente utilizzando il comando `cf set-env`. Ad
                                    esempio: 
    ```
    cf set-env nomeapplicazione env_var_name env_var_value
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
{: #rellinks}

## Link correlati
{: #general}

* [Deploying with Application Manifests](http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){:new_window}
* [CF Manifest Generator](http://cfmanigen.mybluemix.net/){:new_window}
* [Getting Started with cf v6](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html){:new_window}
* [Getting Started with IBM Continuous Delivery Pipeline for Bluemix](../services/DeliveryPipeline/index.html#getstartwithCD)
