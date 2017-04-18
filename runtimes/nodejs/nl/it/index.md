---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# SDK for Nodejs
{: #nodejs_runtime}

Il runtime Node.js su {{site.data.keyword.Bluemix}} si avvale della tecnologia del pacchetto di build sdk-for-nodejs.
Il pacchetto di build sdk-for-nodejs fornisce un ambiente di runtime completo per le applicazioni Node.js.
{: shortdesc}

Il pacchetto di build sdk-for-nodejs è utilizzato quando l'applicazione contiene un file **package.json** nella directory root.

## Applicazione starter
{: #starter_application}

{{site.data.keyword.Bluemix}} Fornisce un'applicazione starter Node.js.  L'applicazione starter Node.js è un'applicazione Node.js semplice che fornisce un template che puoi utilizzare per la tua applicazione. Puoi sperimentare l'applicazione starter ed effettuare e inviare modifiche all'ambiente Bluemix  Consulta [Utilizzo di applicazioni starter](/docs/cfapps/starter_app_usage.html) per informazioni sull'utilizzo dell'applicazione starter. 

## Comando di avvio
{: #starup_commmand}

Per specificare un comando di avvio per la tua applicazione Node.js Bluemix si consiglia di utilizzare un file **Procfile** o **package.json**.

Specifica un comando di avvio nel tuo **Procfile** nel seguente formato. Qui, app.js è lo script js di avvio per la tua applicazione.
```
web: node app.js
```
{: codeblock}

Salva il **Procfile** nella directory root della tua applicazione.

Se non è presente un **Procfile**, il pacchetto di build Node.js IBM Bluemix verifica se è presente una voce scripts.start nel file **package.json**. Anche nell'esempio sottostante, app.js è lo script js di avvio per la tua applicazione.
```
{
    ...   
    "scripts": {
      "start": "node app.js"
    }
}
```
{: codeblock}

Se nel file **package.json** è presente una voce di script di avvio, un **Procfile** viene generato automaticamente. Il contenuto del **Procfile** generato automaticamente è il seguente:
```
    web: npm start
```
{: codeblock}

Per ulteriori informazioni sui file **Procfile** e **package.json** consulta [Tips for Node.js Applications](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html).

## Suggerimenti per eseguire in locale la tua applicazione Node.js
{: #hints}

Utilizza queste informazioni per agevolare l'esecuzione della tua applicazione Node.js sia in locale che su Bluemix.

Il seguente esempio mostra parte del sorgente per un file **js**:
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

Con questo codice, quando l'applicazione è in esecuzione su Bluemix, la variabile di ambiente PORT contiene il valore della porta su cui l'applicazione è in ascolto per le connessioni in entrata. Quando l'applicazione è in esecuzione in locale, PORT non è definita per cui **3000** viene utilizzato come il numero della porta. Scritto in questo modo, puoi eseguire l'applicazione in locale per attività di test e su Bluemix senza apportare ulteriori modifiche.

## Modalità offline
{: #offline_mode}

Consulta [Modalità offline](offlineMode.html) per informazioni sul controllo dell'accesso al pacchetto di build da siti esterni. 

## Gestione applicazioni
{{site.data.keyword.Bluemix}} fornisce diversi programmi di utilità per la gestione e il debug della tua applicazione Node.js.  Consulta [Gestione applicazione](/docs/manageapps/app_mng.html) per i dettagli completi.

## Versioni disponibili
{: #available_versions}

{{site.data.keyword.Bluemix}} fornisce tutti i [runtime Node.js attualmente disponibili](http://nodejs.org/dist/). Di questi, IBM fornisce delle versioni contenenti miglioramenti e correzioni di bug. Per ulteriori informazioni, consulta [Aggiornamenti più recenti al pacchetto di build Node.js](/docs/runtimes/nodejs/updates.html).

Il pacchetto di build IBM Node.js memorizza in cache le versioni di runtime di IBM. Quindi, se utilizzi il runtime IBM SDK for Node.js nella tua applicazione, ottieni delle prestazioni della tua applicazione più rapide quando ne viene eseguito il push a Bluemix.

Utilizza il parametro **node** nella sezione **engines** nel file **package.json** per specificare la versione di runtime Node.js che vuoi eseguire.

Utilizza il parametro **npm** nella sezione **engines** nel file **package.json** se devi specificare una versione di npm diversa da quella integrata in Node.js.  

Guarda il seguente esempio:

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "2.11.3"
  }
}
```
{: codeblock}

Nel file **package.json** deve essere sempre specificata una versione di nodo. In caso contrario, viene utilizzata la versione di nodo più recente.

## Opzioni di configurazione
{: #configuration_options}

### script NPM
{: #npm_scripts}
NPM fornisce una funzione per gli script che ti consente di eseguire gli script, compresi quelli **preinstall** e **postinstall** che vengono applicati prima e dopo l'installazione dei tuoi node_modules.  Per i dettagli completi, consulta [npm-scripts](https://docs.npmjs.com/misc/scripts).

### Funzionamento della cache
{: #cache_behavior}
{{site.data.keyword.Bluemix}} gestisce una directory di cache per ogni applicazione nodo che viene conservata tra i build. La cache memorizza le dipendenze risolte in modo che non vengano scaricate e installate ogni volta che l'applicazione viene distribuita.  Supponi, ad esempio, che myapp dipenda da **express**.  La prima volta che myapp viene distribuita, il modulo **express** viene scaricato.  Nelle successive distribuzioni di myapp, viene utilizzata l'istanza memorizzata in cache di **express**. Il comportamento predefinito è di inserire nella cache tutti i node_modules installati da NPM e i bower_components installati da bower.

Utilizza la variabile NODE_MODULES_CACHE per determinare se il pacchetto di build Node utilizza o ignora la cache dai build precedenti. Il valore predefinito è true.  Per disabilitare la memorizzazione in cache, imposta NODE_MODULES_CACHE su false, ad esempio mediante la riga di comando cf:
```
    $ cf set-env myapp NODE_MODULES_CACHE false
```
{: codeblock}

Nota che i node_modules inclusi nella tua applicazione non vengono memorizzati in cache.

Puoi utilizzare un array **cacheDirectories** nel **package.json** di livello superiore per ottenere il controllo dettagliato su quali moduli vengono memorizzati in cache.  Quando l'elemento **cacheDirectories** è presente nel **package.json**, verranno memorizzati in cache solo i moduli presenti nell'array **cacheDirectories**.  Nel seguente esempio, sono memorizzati in cache solo node_modules e bower_components.
```
{
  "cacheDirectories": ["node_modules","bower_components"],
  ...
}
```
{: codeblock}

### FIPS MODE
{: #fips_mode}

Le versioni del pacchetto di build Nodejs v3.2-20160315-1257 e successive supportano [FIPS](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards).  Per utilizzare un nodo abilitato FIPS imposta la variabile di ambiente FIPS_MODE su true.
Ad esempio:

```
    $ cf set-env myapp FIPS_MODE true
```
{: codeblock}

È importante comprendere che quando FIPS_MODE è true alcuni moduli del nodo hanno esito negativo.  Ad esempio, **i moduli del nodo che utilizzano [MD5](https://en.wikipedia.org/wiki/MD5) hanno esito negativo**, come ad esempio [Express](http://expressjs.com/).  Per Express, l'impostazione di [etag](http://expressjs.com/en/api.html) su
false nella tua applicazione Express può aiutare ad aggirare questo problema. Ad esempio puoi eseguire quanto segue nel tuo codice:
```
    app.set('etag', false);
```
{: codeblock}
Consulta post stackoverflow [](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js)
per ulteriori informazioni.

**NOTA** [Gestione applicazioni](/docs/manageapps/app_mng.html) e FIPS_MODE *NON* sono supportati contemporaneamente.  Se la variabile di ambiente BLUEMIX_APP_MGMT_ENABLE è configurata e le variabili di ambiente FIPS_MODE sono impostate su true, la preparazione dell'applicazione avrà esito negativo.

Esistono vari metodi per controllare lo stato di FIPS_MODE:
<ul>
<li> Puoi controllare il staging_task.log per la tua applicazione per
un messaggio simile al seguente:    

  <pre>
  Installing FIPS-enabled IBM SDK for Node.js (4.4.3) from cache
  </pre>
  {: codeblock}

Questo messaggio indica che un motore node.js abilitato FIPS è in esecuzione ma non necessariamente che FIPS sia in esecuzione.
</li>

<li> Puoi controllare il valore di **process.versions.openssl**. Ad esempio:

  <pre>
  console.log('ssl version is [' +process.versions.openssl +']');
  </pre>
  {: codeblock}

Se la versione SSL contiene "fips", la versione di SSL utilizzata supporta FIPS.  
</li>

<li> Per node.js versione 6 o successiva, puoi controllare il valore restituito da crypto.fips in codice come nel seguente esempio:

  <pre>
  console.log('crypto.fips== [' +crypto.fips +']');
  </pre>
  {: codeblock}

Se il valore restituito è 1, FIPS è in utilizzo. Nota che crypto.fips restituirà *undefined* per le versioni di node.js precedenti alla 6.
</li>
</ul>

#### Nodejs v4
{: #nodejs_v4_fips}

La seguente tabella illustra il funzionamento di node.js v4 con FIPS:

|                 | Risultato        |
| :-------------- | :------------ |
|FIPS_MODE=true   |positivo (1)    |
|FIPS_MODE !=true |positivo (2)    |

* positivo (1)
  * FIPS è in utilizzo.
  * staging_task.log includerà il messaggio *Installing FIPS-enabled IBM SDK for Node.js*.
  * Il valore restituito da process.versions.openssl conterrà "fips".
* positivo (2)
  * FIPS *NON* è in utilizzo.
  * staging_task.log *NON* includerà il messaggio *Installing FIPS-enabled IBM SDK for Node.js*.
  * Il valore restituito da process.versions.openssl *NON* conterrà "fips".

#### Nodejs v6
{: #nodejs_v6_fips}

Per eseguire la modalità FIPS con Node.js versione 6  in aggiunta all'impostazione **FIPS_MODE=true**, devi inoltre includere
**--enable-fips** nel tuo comando di avvio come nel seguente esempio:
```
{
    ...   
    "scripts": {
      "start": "node --enable-fips app.js"
    }
}
```
{: codeblock}

La seguente tabella illustra il funzionamento di node.js v6 con FIPS.

|                 |--enable-fips  |NO --enable-fips |
| :-------------- | :------------ | :-------------- |
|FIPS_MODE=true   |positivo (1)    |positivo (2)      |
|FIPS_MODE !=true |non riuscito (3)    |positivo (4)      |

* positivo (1)
  * FIPS è in utilizzo.
  * staging_task.log includerà il messaggio *Installing FIPS-enabled IBM SDK for Node.js*.
  * Il valore restituito da process.versions.openssl conterrà "fips"
  * crypto.fips restituirà 1, che indica che FIPS è in utilizzo
* positivo (2)
  * FIPS *NON* è in utilizzo.
  * staging_task.log includerà il messaggio *Installing FIPS-enabled IBM SDK for Node.js*.
  * Il valore restituito da process.versions.openssl conterrà "fips"
  * crypto.fips restituirà 0, che indica che FIPS *NON* è in utilizzo
* non riuscito (3)
  * FIPS *NON* è in utilizzo.
  * staging_task.log *NON* includerà il messaggio *Installing FIPS-enabled IBM SDK for Node.js*.
  * staging avrà esito negativo con il messaggio "ERR node: bad option: --enable-fips"
* positivo (4)
  * FIPS *NON* è in utilizzo.
  * staging_task.log *NON* includerà il messaggio *Installing FIPS-enabled IBM SDK for Node.js*.
  * Il valore restituito da process.versions.openssl *NON* conterrà "fips"
  * crypto.fips restituirà 0, che indica che FIPS *NON* è in utilizzo


## Pacchetti di build Node.js

Bluemix fornisce più versioni del pacchetto di build Node.js.
* Il pacchetto di build **sdk-for-nodejs** creato da IBM è il pacchetto di build predefinito utilizzato per le applicazioni Node.js in Bluemix.
* Il **nodejs_buildpack** è il pacchetto di build esterno fornito dalla community Cloud Foundry.

Il pacchetto di build **sdk-for-nodejs** ha la precedenza su **nodejs_buildpack** in Bluemix. Se vuoi utilizzare **nodejs_buildpack** con la tua applicazione invece del pacchetto di build **sdk-for-nodejs**, devi specificare il tuo pacchetto di build, ad esempio utilizzando l'opzione -b con il comando **cf push**.

Di norma, sono disponibili il pacchetto di build **sdk-for-nodejs** e una versione back-level.  Per visualizzare tutti i pacchetti di build disponibili, utilizza il comando **cf buildpacks**.  Ad esempio:
<pre>
      cf buildpacks
      Getting buildpacks...

      buildpack                                 position   enabled   locked   filename   

      sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
      nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
      sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
</pre>
{: codeblock}

# rellinks
{: #rellinks}
## general
{: #general}
* [Aggiornamenti più recenti al pacchetto di build Node.js](/docs/runtimes/nodejs/updates.html)
* [Gestione applicazioni](/docs/manageapps/app_mng.html)
* [Node.js](https://nodejs.org)
* [IBM API Connect](https://strongloop.com/)
