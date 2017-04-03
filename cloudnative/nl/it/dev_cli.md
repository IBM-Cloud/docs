---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}  
{:screen: .screen}  
{:codeblock: .codeblock}  
{:pre: .pre}  

# {{site.data.keyword.dev_cli_short}}
{: #developercli}	

{{site.data.keyword.dev_cli_long}} fornisce un approccio guidato al comando estensibile per la creazione, lo sviluppo e la distribuzione di un progetto web con il plugin `dev`. Ideale per gli sviluppatori che desiderano utilizzare il controllo della riga di comando mentre sviluppano le applicazioni del microservizio end-to-end.

{: shortdesc}

{{site.data.keyword.dev_cli_notm}} utilizza due contenitori per facilitare la creazione e la verifica della tua applicazione. Il primo è il contenitore degli strumenti che contiene i programmi di utilità necessari per creare e verificare la tua applicazione. Il Dockerfile per questo contenitore è definito dal parametro [dockerfile-tools](#command-parameters). Puoi pensare ad esso come a un contenitore di sviluppo poiché contiene gli strumenti normalmente utili per lo sviluppo di uno specifico runtime.

Il secondo contenitore è il contenitore di esecuzione. Questo contenitore è di un formato adeguato per essere distribuito per l'utilizzo, ad esempio, in {{site.data.keyword.Bluemix}}. Di conseguenza, questo contenitore generalmente disporrà di un punto di ingresso definito che avvia la tua applicazione. Quando selezioni di eseguire la tua applicazione tramite {{site.data.keyword.dev_cli_short}}, utilizza questo contenitore. Il Dockerfile per questo contenitore è definito dal parametro [dockerfile-run](#run-parameters). 


## Aggiunta di {{site.data.keyword.dev_cli_notm}}
{: #add-cli}


### Prerequisiti
{: #prereq}

Sono necessari pochi prerequisiti per esplorare completamente e correttamente l'utilizzo di {{site.data.keyword.dev_cli_short}}, poiché è altamente estendibile e ti consente di utilizzare ulteriori tecnologie complementari.

1. Installa la CLI [Cloud Foundry ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://github.com/cloudfoundry/cli#getting-started).

2. Installa la CLI [{{site.data.keyword.Bluemix}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](http://clis.ng.bluemix.net/ui/home.html).

3. Ottieni un ID [{{site.data.keyword.Bluemix_notm}}](https://www.bluemix.net).

4. Facoltativo: se stai pianificando l'esecuzione e il debug delle applicazioni localmente, devi installare anche [Docker ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.docker.com/get-docker). Questo è obbligatorio solo per i progetti non mobili.


### installazione
{: #installation}

1. Installa la [{{site.data.keyword.dev_cli_short}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/cli/reference/bluemix_cli/index.html#install_plug-in){: new_window} eseguendo il seguente comando:
 
	```
	bx plugin install dev -r Bluemix
	```
	{: codeblock}

2. 	Convalida la validità dell'installazione eseguendo il seguente comando:  
 
	```
	bx dev
	```
	{: codeblock}
	

### Prima di iniziare
{: #before-install}
	
1. Accedi a {{site.data.keyword.Bluemix_notm}}.

	```
	bx login
	```
	{: codeblock}
	
	**Nota:** se le tue credenziali vengono rifiutate potresti stare utilizzando un ID federato. Utilizza queste istruzioni per l'autenticazione con un ID federato.
	
	<!-- 
	POINT TO BLUEMIX CLI LOG IN DOCUMENTATION !!!
	
	This link does not work in production yet --> 
	
	1. Accedi a [{{site.data.keyword.iamshort}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.bluemix.net/iam/#/apikeys){: new_window}.
	2. Seleziona **Crea chiave API**.
		* Immetti un nome e una descrizione per apiKey
	3. Scarica la tua apiKey.
	4. Apri il file e copia il valore dal campo `apiKey`.
	5. Accedi utilizzando il seguente comando:
	 
		```
		bx login --apikey <value>
		```
		{: codeblock}


## Comandi
{: #commands}

Utilizzare i seguenti comandi per creare un progetto, distribuirlo, eseguirne il debug, e verificarlo. 

### Creazione
{: #build}

Puoi creare la tua applicazione utilizzando il comando `build`. L'elemento di configurazione `build-cmd-run` viene utilizzato per creare l'applicazione. I comandi `test`, `debug` e `run` eseguono tutti una build perché questo comando è parte delle loro operazioni normali per cui eseguire questo comando prima non è necessario.

Esegui il seguente comando nella tua directory del progetto corrente per creare la tua applicazione:  

```
bx dev build
```
{: codeblock}


[Crea parametri del comando](#command-parameters)


### Codice
{: #code}

Il comando `code` ti consente di scaricare il codice dell'applicazione dopo la distribuzione, in modo che puoi eseguire la verifica localmente o effettuare ulteriori modifiche.

Esegui il seguente comando per scaricare il codice da un progetto specificato.

```
bx dev code <projectName>
```
{: codeblock}


### Creazione
{: #create}

Crea un nuovo progetto, fornendo tutte le informazioni necessarie, inclusi lingua, nome progetto e tipo di modello dell'applicazione. Il progetto sarà creato nella directory corrente. 

Per creare un nuovo progetto nella directory corrente e associare dei servizi ad esso, esegui il seguente comando:

```
bx dev create
```
{: codeblock}


### Debug
{: #debug}

Puoi eseguire il debug della tua applicazione tramite il comando `debug`. Viene prima completata una build per il progetto utilizzando l'elemento di configurazione `build-cmd-debug` come istruzioni di build. Un contenitore inizia quindi ad esporre una porta o più porte di debug come definito in `container-port-map-debug`. Collegando il tuo strumento di debug preferito alla porta o alle porte puoi eseguire il debug della tua applicazione come normale.

**Limitazione**: al momento i progetti Swift non sono disponibili per il debug.

Esegui il seguente comando nella tua directory del progetto corrente per eseguire il debug della tua applicazione:

```
bx dev debug
```
{: codeblock}	

Per uscire dalla sessione di debug utilizza `CTRL-C`.


#### Debug dei parametri del comando
{: #debug-parameters}

I seguenti parametri sono esclusivi del comando `debug` e forniscono supporto
con il debug di un'applicazione.

##### `container-port-map-debug`
{: #port-map-debug}

* Le associazioni di porta per la porta di debug. Il primo valore è la porta da utilizzare nel SO host, il secondo è la porta nel contenitore (host:container).
* Utilizzo: `bx dev debug container-port-map-debug [7777:7777]`
 
##### `build-cmd-debug`
{: #build-cmd-debug}

* Utilizzato per creare il codice per DEBUG. 
* Utilizzo: `bx dev debug build-cmd-debug build.command.sh`

##### `debug-cmd`
{: #debug-cmd}

* Utilizzato per eseguire il debug del codice nel contenitore degli strumenti. Questo è facoltativo se `build-cmd-debug` avvierà la tua applicazione in debug.
* Utilizzo: `bx dev debug debug-cmd /the/debug/command`

#### Debug dell'applicazione locale:
{: #local-app-dev}

Per ulteriori informazioni sul debug dell'applicazione locale, vedi [Debug dell'applicazione locale](docs/cloudnative/dev_cli_local_debug.html#local-debug).


### Eliminazione
{: #delete}

Questo comando ti consente di rimuovere i progetti dal tuo spazio {{site.data.keyword.Bluemix}}.

Esegui il seguente comando per eliminare il tuo progetto da {{site.data.keyword.Bluemix}}:

```
bx dev delete <projectName>
```
{: codeblock}
 

**Nota** i servizi {{site.data.keyword.Bluemix}} **non** vengono rimossi.


### Guida 
{: #help}

Per impostazione predefinita, se non viene trasmesso alcun argomento o azione o se viene fornita l'azione 'help', questo comando mostrerà un testo generale "Help". La guida generale visualizzata include una descrizione degli argomenti di base così come un elenco di azioni disponibili.  

Esegui il seguente comando per visualizzare le informazioni sulla guida generali: 

```
bx dev help
```
{: codeblock}


### Elenco
{: #list}

Puoi elencare tutti i progetti {{site.data.keyword.Bluemix_notm}} in uno spazio.

Esegui il seguente comando per elencare i tuoi progetti: 

```
bx dev list
```
{: codeblock}


<!--
### Editing a project
{: #edit}

You can edit a project, such as changing the name, pattern or starter type, or adding services to your project. Run the following command:

```
bx dev edit
```
{: codeblock}
-->


### Esecuzione
{: #run}

Puoi eseguire la tua applicazione tramite il comando `run`. Viene prima completata una build per il progetto utilizzando l'elemento di configurazione `build-cmd-run` come istruzioni di build. Il contenitore di esecuzione viene quindi avviato ed espone le porte come definite in `container-port-map`. `run-cmd` può essere utilizzato per richiamare l'applicazione se il contenitore di esecuzione non contiene un punto di ingresso per completare questa fase. 

Esegui il seguente comando nella tua directory del progetto corrente per avviare la tua applicazione: 

```
bx dev run
```
{: codeblock}

Per uscire dalla sessione utilizza `CTRL-C`.


#### Eseguire i parametri
{: #run-parameters}

I seguenti parametri sono esclusivi del comando `run` e forniscono supporto
nella gestione della tua applicazione nel contenitore di esecuzione.

##### `container-name-run`
{: #container-name-run}
	
* Il nome del contenitore per il tuo contenitore di esecuzione.
* Utilizzo: `bx dev run container-name-run <projectName>`

##### `container-path-run`
{: #container-path-run}

* L'ubicazione nel contenitore da condividere nell'esecuzione.
* Utilizzo: `bx dev run container-path-run [/path/to/app]`

##### `host-path-run`
{: #host-path-run}

* L'ubicazione del sistema host da condividere nel contenitore nell'esecuzione.
* Utilizzo: `bx dev run host-path-run [/path/to/app/bin]`

##### `dockerfile-run`
{: #dockerfile-run}

* Il Dockerfile per il contenitore di esecuzione.
* Utilizzo: `bx dev run dockerfile-run [/path/to/Dockerfile.yml]`

##### `image-name-run`
{: #image-name-run}

* L'immagine da creare da dockerfile-run.
* Utilizzo: `bx dev run image-name-run [/path/to/image-name]`

##### `run-cmd`
{: #run-cmd}

* Parametro facoltativo utilizzato per eseguire il codice nel contenitore di esecuzione. Questo è facoltativo se la tua immagine avvierà la tua applicazione. 
* Utilizzo: `bx dev run run-cmd [/the/run/command]`
	
### Stato
{: #status}

Puoi eseguire la query dello stato dei contenitori utilizzati dalla {{site.data.keyword.dev_cli_short}} come definito da `container-name-run` e `container-name-tools`. 

Esegui il seguente comando nella tua directory del progetto corrente per controllare lo stato del contenitore: 

```
bx dev status
```
{: codeblock}


[Stato dei parametri del comando](#command-parameters)


### Arresto
{: #stop}

Puoi arrestare un contenitore tramite il comando `stop`. Il parametro `container-name` ti consente di specificare il contenitore da arrestare. Se non viene specificato, il comando stop arresta il contenitore di esecuzione come definito da `container-name-run`. 

Esegui il seguente comando nella tua directory del progetto corrente per arrestare un contenitore: 

```
bx dev stop
```
{: codeblock}


#### Ulteriori parametri di arresto: 
{: #stop-parameter}

##### `container-name`
{: #container-name}

* Il nome del contenitore per il tuo contenitore degli strumenti. 
* Utilizzo: `bx dev stop container-name <demo-tools>` 

### Verifica
{: #test}

Puoi verificare la tua applicazione tramite il comando `test`. Viene prima completata una build per il progetto utilizzando l'elemento di configurazione `build-cmd-run` come istruzioni di build. Il contenitore degli strumenti viene quindi utilizzato per richiamare `test-cmd` per l'applicazione.

Esegui il seguente comando per verificare la tua applicazione:  

```
bx dev test
```
{: codeblock}


[Verifica dei parametri del comando](#command-parameters)


## I parametri per la creazione, il debug, l'esecuzione e la verifica
{: #command-parameters}

I seguenti parametri possono essere utilizzati insieme ai comandi `build|debug|run|test` e possono essere specificati tramite la riga di comando e/o aggiornando la directory del file `cli-config.yml` del progetto. Sono disponibili ulteriori parametri per i comandi [`debug`](#debug-parameters) e [`run`](#run-parameters) e sono illustrati nelle rispettive sezioni.

**Nota**: i parametri del comando immessi nella riga di comando hanno la precedenza sulla configurazione `cli-config.yml`.

##### `container-name-tools`  
{: #container-name-tools}

* Il nome del contenitore per il tuo contenitore degli strumenti. 
* Utilizzo: `bx dev <build|debug|run|test> container-name-tools [<demo-tools>]`
 
##### `host-path-tools`
{: #host-path-tools}

* L'ubicazione sull'host da condividere per la creazione, il debug e la verifica.
* Utilizzo: `bx dev <build|debug|run|test> host-path-tools [/path/to/build/tools]`

##### `container-path-tools`
{: #container-path-tools}

* L'ubicazione nel contenitore da condividere per la creazione, il debug e la verifica. 
* Utilizzo: `bx dev <build|debug|run|test> container-path-tools [/path/for/build]`

##### `container-port-map`
{: #container-port-map}

* Le associazioni di porta per il contenitore. Il primo valore è la porta da utilizzare nel SO host, il secondo è la porta nel contenitore (host:container).
* Utilizzo: `bx dev <build|debug|run|test> container-port-map [8090:8090,9090,9090]`

##### `dockerfile-tools`
{: #dockerfile-tools}

* Il Dockerfile per il contenitore degli strumenti. 
* Utilizzo: `bx dev <build|debug|run|test> dockerfile-tools [path/to/dockerfile]`

##### `image-name-tools`
{: #image-name-tools}

* L'immagine da creare da dockerfile-tools.
* Utilizzo: `bx dev <build|debug|run|test> image-name-tools [path/to/image-name]`

##### `build-cmd-run`
{: #build-cmd-run}

* Il comando per creare il codice per tutti gli utilizzi di DEBUG.
* Utilizzo: `bx dev <build|debug|run|test> build-cmd-run [some.build.command]`

##### `test-cmd`
{: #test-cmd}

* Il comando per verificare il codice nel contenitore degli strumenti. 
* Utilizzo: `bx dev <build|debug|run|test> test-cmd [/the/test/command]`

