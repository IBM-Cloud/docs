---

copyright:
  years: 2015, 2016
  
---

# Monitoraggio delle applicazioni
{: #app-monitoring}
*Ultimo aggiornamento: 28 giugno 2016*
{: .last-updated}

Oltre alle funzioni di sicurezza, {{site.data.keyword.amafull}} fornisce anche il monitoraggio e l'analisi per le tue applicazioni mobili. Puoi registrare i log client e i dati di monitoraggio con l'SDK client {{site.data.keyword.amashort}}. Gli sviluppatori possono controllare quando inviare questi dati al servizio {{site.data.keyword.amashort}}. Tutti gli eventi di sicurezza, quali la riuscita o meno dell'autenticazione, che si verificano nel servizio {{site.data.keyword.amashort}} vengono registrati automaticamente.

**Nota**: le funzioni di monitoraggio del servizio {{site.data.keyword.amashort}} è pianificato che vengano migrate al nuovo servizio [{{site.data.keyword.mobileanalytics_short}}](https://console.ng.bluemix.net/catalog/services/mobile-analytics). La nuova SDK Swift utilizza il nuovo servizio {{site.data.keyword.mobileanalytics_short}}, che fornisce una migliore esperienza di analisi. Il servizio {{site.data.keyword.mobileanalytics_short}} è al momento in fase sperimentale, si pianifica di farlo diventare disponibile più avanti in questo anno. Ci raccomandiamo di studiare la migrazione delle tue applicazioni per utilizzare il nuovo servizio {{site.data.keyword.mobileanalytics_short}} e la SDK Swift perché le funzioni di monitoraggio del servizio {{site.data.keyword.amashort}} saranno abbandonate quando {{site.data.keyword.mobileanalytics_short}} diventa disponibile.

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
                                tali problemi. <!--in R&D.--> Gli sviluppatori che hanno lavorato sul codice potrebbero non disporre
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

3. Nel dashboard {{site.data.keyword.amashort}}, fai clic sul link **Monitoraggio** nel menu di sinistra.

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

Assicurati di avere inizializzato l'SDK client {{site.data.keyword.amashort}} prima di utilizzare il framework di registrazione in log. I seguenti esempi illustrano l'utilizzo di base di un framework di registrazione in log dell'SDK client {{site.data.keyword.amashort}}.

**Importante**: le funzioni di monitoraggio del servizio {{site.data.keyword.amashort}} è pianificato che vengano migrate al nuovo servizio [{{site.data.keyword.mobileanalytics_short}}](https://console.ng.bluemix.net/catalog/services/mobile-analytics). La nuova SDK Swift utilizza il nuovo servizio {{site.data.keyword.mobileanalytics_short}}, che fornisce una migliore esperienza di analisi. Il servizio {{site.data.keyword.mobileanalytics_short}} è al momento in fase sperimentale, si pianifica di farlo diventare disponibile più avanti in questo anno. Ci raccomandiamo di studiare la migrazione delle tue applicazioni per utilizzare il nuovo servizio {{site.data.keyword.mobileanalytics_short}} e la SDK Swift perché le funzioni di monitoraggio del servizio {{site.data.keyword.amashort}} saranno abbandonate quando {{site.data.keyword.mobileanalytics_short}} diventa disponibile.

#### Android
{: #enable-logger-android}

```Java
BMSClient.getInstance().initialize(context, appRoute, appGUID);

Logger logger = Logger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```

#### iOS - Objective-C
{: #enable-logger-objectc}

**Importante**: mentre la SDK Objective-C SDK rimane completamente supportata ed è ancora considerata la SDK primaria per i servizi mobili {{site.data.keyword.Bluemix}}, è pianificato di abbandonarla più avanti questo anno in favore della nuova SDK Swift.

La SDK Objective-C riporta i dati di monitoraggio alla console di monitoraggio del servizio {{site.data.keyword.amashort}}. Se fai affidamento sulle funzioni di monitoraggio del servizio {{site.data.keyword.amashort}}, continua ad utilizzare la SDK Objective-C.

```Objective-C
[[IMFClient sharedInstance] initializeWithBackendRoute:appRoute backendGUID:appGUID];

IMFLogger *logger = [IMFLogger loggerForName:@"myLogger"];

[logger logDebugWithMessages:@"debug"];
[logger logInfoWithMessages:@"info"];
[logger logWarnWithMessages:@"warn"];
[logger logErrorWithMessages:@"error"];
[logger logFatalWithMessages:@"fatal"];

```

#### iOS - Swift
{: #enable-logger-swift}

```Swift
IMFClient.sharedInstance().initializeWithBackendRoute(appRoute, backendGUID: appGuid)

let logger = IMFLogger(forName: "myLogger");

logger.logDebugWithMessages("debug");
logger.logInfoWithMessages("info");
logger.logWarnWithMessages("warn");
logger.logErrorWithMessages("error");
logger.logFatalWithMessages("fatal");
```

**Nota:** l'SDK client {{site.data.keyword.amashort}} è implementato con Objective-C, pertanto potresti dover
aggiungere il file `IMFLoggerExtension.swift` al tuo progetto Swift per utilizzare l'API logger precedente. Puoi trovare questo file
nell'[archivio dell'SDK client {{site.data.keyword.amashort}}](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).


#### Cordova
{: #enable-logger-android-cordova}

```JavaScript
BMSClient.initialize(appRoute , appGUID);

var logger = MFPLogger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");

```

Puoi trovare i seguenti metodi aggiuntivi nelle classi Logger:

* `setCapture` - abilita o disabilita la memorizzazione in modo persistente delle informazioni di log da inviare successivamente al servizio {{site.data.keyword.amashort}}.
* `setLevel` - imposta il livello di log minimo per salvare i messaggi di log.
* `send` - invia i log memorizzati in modo persistente al servizio {{site.data.keyword.amashort}}.

Ad esempio, quando l'acquisizione è attiva (ON) e il livello del logger è configurato
su FATAL, il logger acquisisce le eccezioni non rilevate. Le eccezioni non rilevate spesso
si presentano agli utenti come arresti anomali dell'applicazione, ma non acquisiscono
alcun log che porti all'evento dell'arresto anomalo. In alternativa, un livello del logger più dettagliato assicura che vengano catturati anche i log che portano a una voce del logger FATAL, come WARN ed ERROR.

**Nota:** dei riferimenti alle API logger completi per ciascuna piattaforma sono a tua disposizione in [SDK, esempi e guida di riferimento API](sdks-samples-apis.html). L'API Logger fa parte dell'SDK client {{site.data.keyword.amashort}} Core.


### Utilizzo di esempio
{: #sample-logger-usage}

I seguenti frammenti di codice mostrano un utilizzo di Logger di esempio:

#### Android
{: #enable-logger-sample-android}

```Java
// Abilita la memorizzazione in modo persistente dei log
Logger.setCapture(true);

// Imposta il livello di log minimo da scrivere e memorizzare in modo persistente
Logger.setLevel(Logger.LEVEL.INFO);

// Crea due istanze logger
Logger logger1 = Logger.getInstance("logger1");
Logger logger2 = Logger.getInstance("logger2");

// Registra nel log messaggi con livelli differenti
logger1.debug("debug message");
logger2.info("info message");

// Invia i log memorizzati in modo persistente al servizio {{site.data.keyword.amashort}}
Logger.send();
```

#### iOS - Objective-C
{: #enable-logger-sample-objectc}

```Objective-C
// Abilita la memorizzazione in modo persistente dei log
[IMFLogger setCapture:YES];

// Avvia l'acquisizione delle eccezioni non rilevate
[IMFLogger captureUncaughtExceptions];

// Imposta il livello di log minimo da scrivere e memorizzare in modo persistente
[IMFLogger setLogLevel:IMFLogLevelInfo];

// Crea due istanze logger
IMFLogger *logger1 = [IMFLogger loggerForName:@"logger1"];
IMFLogger *logger2 = [IMFLogger loggerForName:@"logger2"];

// Registra nel log messaggi con livelli differenti
[logger1 logDebugWithMessages:@"debug message"];
[logger2 logInfoWithMessages:@"info message"];

// Invia i log memorizzati in modo persistente al servizio {{site.data.keyword.amashort}}
[IMFLogger send];
```

#### iOS - Swift
{: #enable-logger-sample-swift}

```Swift
// Abilita la memorizzazione in modo persistente dei log
IMFLogger.setCapture(true)

// Avvia l'acquisizione delle eccezioni non rilevate
IMFLogger.captureUncaughtExceptions()

// Imposta il livello di log minimo da scrivere e memorizzare in modo persistente
IMFLogger.setLogLevel(IMFLogLevel.Info)

// Crea due istanze logger
let logger1 = IMFLogger(forName: "logger1");
let logger2 = IMFLogger(forName: "logger2");

// Registra nel log messaggi con livelli differenti
logger1.logDebugWithMessages("debug message")
logger2.logInfoWithMessages("info message")

// Invia i log memorizzati in modo persistente al servizio {{site.data.keyword.amashort}}
IMFLogger.send()

```

#### Cordova
{: #enable-logger-sample-cordova}

```JavaScript
// Abilita la memorizzazione in modo persistente dei log
MFPLogger.setCapture(true);

// Imposta il livello di log minimo da scrivere e memorizzare in modo persistente
MFPLogger.setLevel(MFPLogger.INFO);

// Crea due istanze logger
var logger1 = MFPLogger.getInstance("logger1");
var logger2 = MFPLogger.getInstance("logger2");    

// Registra nel log messaggi con livelli differenti
logger1.debug("debug message");
logger2.info("info message");

// Invia i log memorizzati in modo persistente al servizio {{site.data.keyword.amashort}}
MFPLogger.send(success, failure);
```

### Abilitazione dei log interni dell'SDK client {{site.data.keyword.amashort}}
{: #enable-logger-sdklogs}
Questa funzione è attualmente disponibile solo nella versione Android dell'SDK client {{site.data.keyword.amashort}}.

L'SDK client {{site.data.keyword.amashort}} fornisce una migliore esperienza di sviluppo senza necessariamente aumentare l'output Logcat con i suoi messaggi di debug interni. Pertanto, per impostazione predefinita, i messaggi di log interni prodotti dall'SDK {{site.data.keyword.amashort}} con il livello DEBUG non vengono scritti. Puoi abilitare la scrittura di tutti i messaggi di log interni dell'SDK client {{site.data.keyword.amashort}} con la seguente API:


```
Logger.setSDKInternalLoggingEnabled(true);
```

## Raccolta dell'analisi dell'utilizzo
{: #usage-analytics}

Puoi configurare l'SDK client {{site.data.keyword.amashort}} per registrare l'analisi dell'utilizzo e inviare i dati registrati al servizio {{site.data.keyword.amashort}}.

**Importante**: le funzioni di monitoraggio del servizio {{site.data.keyword.amashort}} è pianificato che vengano migrate al nuovo servizio [{{site.data.keyword.mobileanalytics_short}}](https://console.ng.bluemix.net/catalog/services/mobile-analytics). La nuova SDK Swift utilizza il nuovo servizio {{site.data.keyword.mobileanalytics_short}}, che fornisce una migliore esperienza di analisi. Il servizio {{site.data.keyword.mobileanalytics_short}} è al momento in fase sperimentale, si pianifica di farlo diventare disponibile più avanti in questo anno. Ci raccomandiamo di studiare la migrazione delle tue applicazioni per utilizzare il nuovo servizio {{site.data.keyword.mobileanalytics_short}} e la SDK Swift perché le funzioni di monitoraggio del servizio {{site.data.keyword.amashort}} saranno abbandonate quando {{site.data.keyword.mobileanalytics_short}} diventa disponibile.

**Nota:** assicurati di avere abilitato la cattura della registrazione prima di avviare la registrazione dell'analisi dell'utilizzo.

Utilizza le seguenti API per avviare la registrazione e inviare l'analisi dell'utilizzo:

#### Android
{: #usage-analytics-android}

```Java
// Abilita la registrazione dell'analisi dell'utilizzo
MFPAnalytics.enable();

// Avvia la registrazione dell'ora di avvio dell'applicazione
// Aggiungi questo codice nel metodo onCreate della tua attività principale
MFPAnalytics.startLoggingApplicationStartup();

// Registra la durata dell'avvio dell'applicazione
// Aggiungi questo codice nel metodo onStart della tua attività principale
MFPAnalytics.logApplicationStartup();

// Registra gli eventi in primo piano e in background dell'applicazione
// Aggiungi questo codice nei metodi onPause e onResume della tua attività principale
MFPAnalytics.logSessionStart();
MFPAnalytics.logSessionEnd();

// Invia l'analisi dell'utilizzo registrata al servizio {{site.data.keyword.amashort}}
MFPAnalytics.send();
```

#### iOS - Objective-C
{: #usage-analytics-objectc}

**Importante**: mentre la SDK Objective-C SDK rimane completamente supportata ed è ancora considerata la SDK primaria per i servizi mobili {{site.data.keyword.Bluemix}}, è pianificato di abbandonarla più avanti questo anno in favore della nuova SDK Swift.

La SDK Objective-C riporta i dati di monitoraggio alla console di monitoraggio del servizio {{site.data.keyword.amashort}}. Se fai affidamento sulle funzioni di monitoraggio del servizio {{site.data.keyword.amashort}}, continua ad utilizzare la SDK Objective-C.

```Objective-C
// Abilita la registrazione dell'analisi di utilizzo
[[IMFAnalytics sharedInstance] setEnabled:YES];

// Avvia la registrazione degli eventi del ciclo di vita dell'applicazione
[[IMFAnalytics sharedInstance] startRecordingApplicationLifecycleEvents];


// Invia l'analisi dell'utilizzo registrata al servizio {{site.data.keyword.amashort}}
[[IMFAnalytics sharedInstance] sendPersistedLogs];
```

#### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Abilita la registrazione dell'analisi dell'utilizzo
IMFAnalytics.sharedInstance().setEnabled(true)

// Avvia la registrazione degli eventi del ciclo di vita dell'applicazione
IMFAnalytics.sharedInstance().startRecordingApplicationLifecycleEvents()


// Invia l'analisi dell'utilizzo registrata al servizio {{site.data.keyword.amashort}}
IMFAnalytics.sharedInstance().sendPersistedLogs()
```

#### Cordova
{: #usage-analytics-cordova}

```JavaScript
// Abilita la registrazione dell'analisi dell'utilizzo
MFPAnalytics.enable();

// Invia l'analisi dell'utilizzo registrata al servizio {{site.data.keyword.amashort}}
MFPAnalytics.send();
```
**Nota:** quando sviluppi applicazioni Cordova, usa l'API nativa per abilitare la registrazione degli eventi del ciclo di vita dell'applicazione.
