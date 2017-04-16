---

copyright:
  years: 2015, 2016
  
---

# Monitoraggio delle applicazioni
{: #app-monitoring}
Ultimo aggiornamento: 22 settembre 2016
{: .last-updated}

Oltre alle funzioni di sicurezza, {{site.data.keyword.amafull}} fornisce anche il monitoraggio e l'analisi per le tue applicazioni mobili. Puoi registrare i log client e i dati di monitoraggio con l'SDK client {{site.data.keyword.amashort}}. Gli sviluppatori possono controllare quando inviare questi dati al servizio {{site.data.keyword.amashort}}. Tutti gli eventi di sicurezza, quali la riuscita o meno dell'autenticazione, che si verificano nel servizio {{site.data.keyword.amashort}} vengono registrati automaticamente.
<!--
**Note**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available. -->

Quando i dati vengono distribuiti a {{site.data.keyword.amashort}}, puoi utilizzare il dashboard di monitoraggio {{site.data.keyword.amashort}} per ottenere informazioni approfondite di analisi relative alle tue applicazioni mobili e ai tuoi dispositivi e log client. Le informazioni sulle richieste effettuate dalla tua applicazione alle risorse protette {{site.data.keyword.amashort}} sono registrate per impostazione predefinita.

I dati registrati automaticamente includono informazioni quali il numero di autenticazioni, nuovi dispositivi e nuovi utenti. Puoi inoltre configurare
l'SDK client {{site.data.keyword.amashort}} per notificare le seguenti informazioni:

### Statistiche di utilizzo delle tue applicazioni mobili
{: #usage-stats}

Puoi configurare le tue applicazioni mobili per registrare gli eventi del ciclo di vita dell'applicazione e inviare i dati registrati al servizio {{site.data.keyword.amashort}} con poche e semplici chiamate API. Puoi registrare il
                                numero di aperture di applicazioni, notifiche di push ricevute e così via.

### Acquisizione di log lato client
{: #client-side-logcapture}

Le applicazioni in uso di produzione di tanto in tanto riscontrano dei problemi la cui
                                correzione richiede l'attenzione di uno sviluppatore. È spesso difficile riprodurre
                                tali problemi. Gli sviluppatori che hanno lavorato sul codice potrebbero non disporre
                                dell'ambiente o dell'esatto dispositivo con cui eseguire la verifica. In tali situazioni,
                                è utile poter richiamare i log di debug dai dispositivi client poiché i problemi si verificano
                                nell'ambiente in cui succedono.

### Conservazione dei dati acquisiti
{: #preserve-captureddata}

Non c'è modo di garantire che tutti i dati catturati vengano conservati sul lato client. I tuoi utenti
                                potrebbero eseguire l'applicazione mobile non in linea e accumulare simultaneamente
                                dati di analisi e di log acquisiti. Poiché il client è non in linea con uno spazio
                                su file system limitato, gli eventi registrati meno recenti devono essere
                                eliminati al fine di conservare gli eventi registrati più di recente. Spetta allo sviluppatore decidere quando inviare i dati catturati
al servizio {{site.data.keyword.amashort}} utilizzando le API fornite.

## Utilizzo del dashboard di monitoraggio {{site.data.keyword.amashort}}
{: #monitoring-dashboard}

1. Apri il dashboard {{site.data.keyword.Bluemix}} e fai clic sulla tua applicazione {{site.data.keyword.Bluemix_notm}}.

2. Quando il tuo dashboard dell'applicazione {{site.data.keyword.Bluemix_notm}} si è aperto, fai clic su un tile {{site.data.keyword.amashort}}.

3. Fai clic sul pulsante **Monitoraggio** nella navigazione del dashboard {{site.data.keyword.amashort}}.


## Abilitazione, configurazione e utilizzo del Logger
{: #enable-logger}

L'SDK client {{site.data.keyword.amashort}} fornisce un framework di registrazione in log simile ad altri framework di log con cui potresti avere dimestichezza, come `java.util.logging` o `log4j`. Il framework di registrazione in log supporta, tra l'altro, più istanze logger per pacchetto, diversi livelli di log e l'acquisizione di tracce di stack per un arresto anomalo di applicazioni.

Puoi anche configurare che i dati registrati in log vengano memorizzati in modo persistente in un archivio locale e che è quindi possibile inviare al servizio {{site.data.keyword.amashort}} su richiesta.

Il framework di registrazione in log dell'SDK client {{site.data.keyword.amashort}} supporta i seguenti livelli di log, elencati da quello meno dettagliato a quello più dettagliato, con le linee guida di utilizzo consigliato:

* `FATAL` - utilizzalo per i blocchi o gli arresti anomali irreversibili. Il livello
FATAL è riservato per la registrazione degli errori irreversibili, che si
presentano agli utenti come un arresto anomalo dell'applicazione.
* `ERROR` - utilizzalo per le eccezioni impreviste o gli errori di protocollo di rete imprevisti.
* `WARN` - per registrare le avvertenze di utilizzo che non sono considerate degli errori critici, come ad esempio l'utilizzo di API dichiarate obsolete o una risposta di rete lenta.
* `INFO` - utilizzalo per la notifica di eventi di inizializzazione e altri dati che potrebbero essere utili.
* `DEBUG` - utilizzalo per la notifica delle istruzioni di debug per aiutare gli sviluppatori a risolvere i difetti delle applicazioni.

#### Scenari di livello di log
{: #log-level-scenario}

Quando il livello del logger è configurato in `FATAL`, il logger cattura le eccezioni non rilevate, ma non acquisisce alcun log che porti all'evento dell'arresto anomalo. Puoi impostare un livello del logger più dettagliato per assicurarti che vengano catturati anche i log che portano a una voce del logger `FATAL`, come `WARN` e `ERROR`.

Assicurati di avere inizializzato l'SDK client {{site.data.keyword.amashort}} prima di utilizzare il framework di registrazione in log. I seguenti esempi illustrano l'utilizzo di base di un framework di registrazione in log dell'SDK client {{site.data.keyword.amashort}}.

<!-- **Important**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available.-->

#### Android
{: #enable-logger-android}

```Java
BMSClient.getInstance().initialize(this.getApplicationContext(), BMSClient.REGION_US_SOUTH); // Make sure that you point to your region

Logger logger = Logger.getLogger("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```
{: codeblock}

Il parametro **bluemixRegion** specifica quale distribuzione Bluemix stai utilizzando, ad esempio, `BMSClient.REGION_US_SOUTH` e `BMSClient.REGION_UK`. 

#### iOS - Swift
{: #enable-logger-swift}

```Swift
BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.REGION_US_SOUTH) // Puoi modificare la regione
Analytics.initializeWithAppName(your_app_name_here, apiKey: your_api_key_here, hasUserContext: false, deviceEvents: DeviceEvent.LIFECYCLE)

let logger = Logger.logger(forName: "myLogger")

logger.debug(“debug info")
logger.info(“info message")
logger.warn(“warning message")
logger.error(“error message")
logger.fatal(“fatal message")
```
{: codeblock}
<!--
**Note:** The {{site.data.keyword.amashort}} client SDK is implemented with Objective-C, therefore you might need to add the `IMFLoggerExtension.swift` file to your Swift project to use the previous logger API. You can find this file in the [{{site.data.keyword.amashort}} client SDK archive](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).
-->

#### Cordova
{: #enable-logger-android-cordova}

```JavaScript
BMSClient.initialize(BMSClient.REGION_US_SOUTH); // Puoi modificare la regione

var logger = BMSLogger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```
{: codeblock}

Puoi trovare i seguenti metodi aggiuntivi nelle classi Logger:

* `setCapture` - abilita o disabilita la memorizzazione in modo persistente delle informazioni di log da inviare successivamente al servizio {{site.data.keyword.amashort}}.
* `setLevel` - imposta il livello di log minimo per salvare i messaggi di log.
* `send` - invia i log memorizzati in modo persistente al servizio {{site.data.keyword.amashort}}.

Ad esempio, quando l'acquisizione è attiva (ON) e il livello del logger è configurato
su FATAL, il logger acquisisce le eccezioni non rilevate. Le eccezioni non rilevate spesso
si presentano agli utenti come arresti anomali dell'applicazione, ma non acquisiscono
alcun log che porti all'evento dell'arresto anomalo. In alternativa, un livello del logger più dettagliato assicura che vengano catturati anche i log che portano a una voce del logger FATAL, come WARN ed ERROR.

**Nota:** dei riferimenti alle API logger completi per ciascuna piattaforma sono a tua disposizione in [SDK, esempi e guida di riferimento API](sdks-samples-apis.html). L'API Logger fa parte dell'SDK client {{site.data.keyword.amashort}} Core.


### Utilizzo del logger di esempio
{: #sample-logger-usage}

I seguenti frammenti di codice mostrano un utilizzo di Logger di esempio:

#### Android
{: #enable-logger-sample-android}

```Java
// Configura il logger per  salvare i log nel dispositivo in modo che
// possano essere inviati successivamente al servizio {{site.data.keyword.amashort}}
// Disabilitato per impostazione predefinita; imposta su true per abilitarlo
Logger.storeLogs(true);

// Modifica il livello di log minimo (facoltativo)
// L'impostazione predefinita è Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);

// Crea due istanze logger
// Puoi creare più istanze logger per organizzare i tuoi log
Logger logger1 = Logger.getLogger("logger1");
Logger logger2 = Logger.getLogger("logger2");

// Registra nel log messaggi con livelli differenti
// Messaggio di debug per la funzione 1 1
// Messaggio informativo per la funzione 2 2
logger1.debug("debug message");
// il messaggio logger1.debug non viene registrato perché il logLevelFilter è impostato su Info
logger2.info("info message");

// Invia i log al servizio {{site.data.keyword.amashort}}
Logger.send();
```
{: codeblock}

#### iOS - Swift
{: #enable-logger-sample-swift}

```Swift
// Configura il logger per  salvare i log nel dispositivo in modo che possano essere inviati successivamente al servizio {{site.data.keyword.amashort}}
// Disabilitato per impostazione predefinita; imposta su true per abilitarlo
Logger.logStoreEnabled = true

// Modifica il livello di log minimo (facoltativo)
// L'impostazione predefinita è LogLevel.Debug
Logger.logLevelFilter = LogLevel.Info

// Crea due istanze logger
// Puoi creare più istanze logger per organizzare i tuoi log
let logger1 = Logger.logger(forName: "feature1Logger")
let logger2 = Logger.logger(forName: "feature2Logger")

// Registra nel log messaggi con livelli differenti
logger1.debug("debug message for feature 1")
//il messaggio logger1.debug non viene registrato perché il logLevelFilter è impostato su Info
logger2.info("info message for feature 2")

// Invia i log al servizio {{site.data.keyword.amashort}}
Logger.send()
```
{: codeblock}

#### Cordova
{: #enable-logger-sample-cordova}

```JavaScript
// Abilita la memorizzazione in modo persistente dei log
BMSLogger.setCapture(true);

// Imposta il livello di log minimo da scrivere e memorizzare in modo persistente
BMSLogger.setLevel(BMSLogger.INFO);

// Crea due istanze logger
var logger1 = BMSLogger.getInstance("logger1");
var logger2 = BMSLogger.getInstance("logger2");

// Registra nel log messaggi con livelli differenti
logger1.debug("debug message");
logger2.info("info message");

// Invia i log memorizzati in modo persistente al servizio {{site.data.keyword.amashort}}
BMSLogger.send(success, failure);
```
{: codeblock}

### Abilitazione dei log interni dell'SDK client {{site.data.keyword.amashort}}
{: #enable-logger-sdklogs}
Questa funzione è attualmente disponibile solo nella versione Android dell'SDK client {{site.data.keyword.amashort}}.

L'SDK client {{site.data.keyword.amashort}} fornisce una migliore esperienza di sviluppo senza necessariamente aumentare l'output Logcat con i suoi messaggi di debug interni. Pertanto, per impostazione predefinita, i messaggi di log interni prodotti dall'SDK {{site.data.keyword.amashort}} con il livello DEBUG non vengono scritti. Puoi abilitare la scrittura di tutti i messaggi di log interni dell'SDK client {{site.data.keyword.amashort}} con la seguente API:


```
Logger.setSDKInternalLoggingEnabled(true);
```
{: codeblock}

## Raccolta dell'analisi dell'utilizzo
{: #usage-analytics}

Puoi configurare l'SDK client {{site.data.keyword.amashort}} per registrare l'analisi dell'utilizzo e inviare i dati registrati al servizio {{site.data.keyword.amashort}}.
<!--
**Important**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available. -->

**Nota:** assicurati di avere abilitato la cattura della registrazione prima di avviare la registrazione dell'analisi dell'utilizzo.

Utilizza le seguenti API per avviare la registrazione e inviare l'analisi dell'utilizzo:

#### Android
{: #usage-analytics-android}

```Java
// Disabilita la registrazione dell'analisi di utilizzo (ad esempio per risparmiare spazio su disco)
// La registrazione è abilitata per impostazione predefinita
Analytics.disable();
	
// Abilita la registrazione dell'analisi dell'utilizzo
Analytics.enable();
	
Analytics.log(eventJSONObject);
	
// Invia l'analisi dell'utilizzo registrata al servizio Mobile Analytics
Analytics.send();
```
{: codeblock}

#### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Disabilita la registrazione dell'analisi di utilizzo (ad esempio per risparmiare spazio su disco)
// La registrazione è abilitata per impostazione predefinita
Analytics.enabled = false

// Abilita la registrazione dell'analisi dell'utilizzo
Analytics.enabled = true

// Invia l'analisi dell'utilizzo registrata al servizio {{site.data.keyword.mobileanalytics_short}}
Analytics.send()
```
{: codeblock}

#### Cordova
{: #usage-analytics-cordova}

```JavaScript
// Abilita la registrazione dell'analisi dell'utilizzo
BMSAnalytics.enable();

// Invia l'analisi dell'utilizzo registrata al servizio {{site.data.keyword.amashort}}
BMSAnalytics.send();
```
{: codeblock}

**Nota:** quando sviluppi applicazioni Cordova, usa l'API nativa per abilitare la registrazione degli eventi del ciclo di vita dell'applicazione.
