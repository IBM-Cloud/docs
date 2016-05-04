---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# SDK for Nodejs
{: #nodejs_runtime}
*Ultimo aggiornamento: 16 marzo 2016*

Il runtime Node.js su {{site.data.keyword.Bluemix}} si avvale della tecnologia del pacchetto di build sdk-for-nodejs.
Il pacchetto di build sdk-for-nodejs fornisce un ambiente di runtime completo per le applicazioni Node.js.
{: shortdesc}

Il pacchetto di build sdk-for-nodejs è utilizzato quando l'applicazione contiene un file **package.json** nella directory root.

## Applicazione starter
{: #starter_application}

{{site.data.keyword.Bluemix}} Fornisce un'applicazione starter Node.js.  L'applicazione starter Node.js è un'applicazione Node.js semplice che fornisce un template che puoi utilizzare per la tua applicazione. Puoi sperimentare l'applicazione starter ed effettuare e inviare modifiche all'ambiente Bluemix  Consulta [Utilizzo di applicazioni starter](../../cfapps/starter_app_usage.html) per informazioni sull'utilizzo dell'applicazione starter.

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
var port = (process.env.VCAP_APP_PORT || 3000);
var host = (process.env.VCAP_APP_HOST || 'localhost');
```
{: codeblock}

Con questo codice, quando l'applicazione è in esecuzione su Bluemix, le variabili di ambiente VCAP_APP_HOST e VCAP_APP_PORT contengono i valori di host e porta interni per Bluemix e su cui l'applicazione è in ascolto per le connessioni in entrata. Quando l'applicazione è in esecuzione in locale, VCAP_APP_HOST e VCAP_APP_PORT non sono definite e si utilizza pertanto **localhost** come host e **3000** come numero porta. Scritto in questo modo, puoi eseguire l'applicazione in locale per attività di test e su Bluemix senza apportare ulteriori modifiche.

## Gestione applicazioni
{{site.data.keyword.Bluemix}} fornisce diversi programmi di utilità per la gestione e il debug della tua applicazione Node.js.  Consulta [Gestione applicazioni](../../manageapps/app_mng.html) per i dettagli completi.

## Versioni disponibili
{: #available_versions}

{{site.data.keyword.Bluemix}} fornisce tutti i [runtime Node.js attualmente disponibili](http://nodejs.org/dist/). Di questi, IBM fornisce delle versioni contenenti miglioramenti e correzioni di bug. Per ulteriori informazioni, consulta [Aggiornamenti più recenti al pacchetto di build Node.js](../../runtimes/nodejs/updates.html).

Il pacchetto di build IBM Node.js memorizza in cache tutte le versioni di runtime di IBM. Quindi, se utilizzi il runtime IBM SDK for Node.js nella tua applicazione, ottieni delle prestazioni della tua applicazione più rapide quando ne viene eseguito il push a Bluemix.

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

Le versioni del pacchetto di build Nodejs v3.2-20160315-1257 e successive supportano [FIPS](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards).  Per abilitare FIPS per imposta la variabile di ambiente FIPS_MODE su true.
Ad esempio:

```
    $ cf set-env myapp FIPS_MODE true
```
{: codeblock}

È importante comprendere che quando FIPS_MODE è true **i moduli del nodo che utilizzano [MD5](https://en.wikipedia.org/wiki/MD5) hanno esito negativo**. Ad esempio i moduli
[Express](http://expressjs.com/) hanno esito negativo.  L'impostazione di [etag](http://expressjs.com/en/api.html) su
false nella tua applicazione Expess può aiutare ad aggirare questo problema. Ad esempio puoi eseguire quanto segue nel tuo codice:
```
    app.set('etag', false);
```
{: codeblock}
Per ulteriori informazioni, consulta post stackoverflow [](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js).

Per verificare se FIPS_MODE è true nella tua applicazione, controlla il valore di **process.versions.openssl**. Ad esempio:
```
    console.log('ssl version is [' +process.versions.openssl +']');
```
{: codeblockd}

Se la versione SSl contiene "fips", vuol dire che l'applicazione è in esecuzione in modalità FIPS.    


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
## general
* [Aggiornamenti più recenti al pacchetto di build Node.js](../../runtimes/nodejs/updates.html)
* [Gestione applicazioni](../../manageapps/app_mng.html)
* [Node.js](https://nodejs.org)
* [StrongLoop](https://strongloop.com)
