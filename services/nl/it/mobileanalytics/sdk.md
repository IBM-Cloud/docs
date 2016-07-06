---

copyright:
  years: 2015, 2016

---

# Strumentazione della tua applicazione per utilizzare gli SDK client {{site.data.keyword.mobileanalytics_short}}
{: #mobileanalytics_sdk}
*Ultimo aggiornamento: 27 aprile 2016*
{: .last-updated}

Gli SDK {{site.data.keyword.mobileanalytics_full}} consentono di strumentare la tua applicazione mobile.
{: shortdesc}

{{site.data.keyword.mobileanalytics_short}} consente di raccogliere tre categorie di dati e ciascuna richiede un diverso grado di strumentazione:

1.  Dati predefiniti - questa categoria include informazioni generiche sull'utilizzo e sui dispositivi che si applicano a tutte le applicazioni. In questa categoria sono contenuti i metadati di dispositivo (sistema operativo e modello del dispositivo) e i dati di utilizzo (sessioni applicazione e utenti attivi) che indicano il volume, la frequenza o la
durata dell'utilizzo delle applicazioni. I dati predefiniti vengono raccolti automaticamente dopo che hai inizializzato
l'SDK {{site.data.keyword.mobileanalytics_short}} nella tua applicazione.
2. Eventi personalizzati - questa categoria include i dati che definisci tu stesso e che sono specifici per la tua applicazione. Questi dati rappresentano gli eventi che si verificano nella tua applicazione, come le visualizzazioni di pagine, le selezioni di pulsanti o gli acquisti all'interno dell'applicazione. Oltre a inizializzare l'SDK {{site.data.keyword.mobileanalytics_short}} nella tua applicazione, devi aggiungere una riga di codice per ciascun evento personalizzato che vuoi tracciare.
3. Messaggi di log client - questa categoria consente allo sviluppatore di aggiungere delle righe di codice in tutta l'applicazione che registrano dei messaggi personalizzati di supporto nelle attività di sviluppo e debug. Lo sviluppatore assegna un livello di severità/dettaglio a ciascun messaggio di log e può successivamente filtrare i messaggi in base al livello assegnato oppure risparmiare spazio di archiviazione configurando l'applicazione in modo che ignori i messaggi che sono al di sotto di un certo livello
di log. Per raccogliere i dati di log client, devi inizializzare l'SDK {{site.data.keyword.mobileanalytics_short}} nella tua applicazione, nonché aggiungere una riga di codice per ciascun messaggio di log.

Attualmente, gli SDK sono disponibili per Android, iOS e WatchOS.

## Identificazione del tuo valore Chiave client
{: #analytics-clientkey}

Identifica il tuo valore **Chiave client** prima di impostare l'SDK client. La chiave client è necessaria per inizializzare l'SDK client.
1. Apri il tuo dashboard del servizio {{site.data.keyword.mobileanalytics_short}}.
2. Fai clic sull'icona che rappresenta una chiave inglese per aprire la scheda Chiavi API.
3. Nella scheda Chiavi API, annota il valore di Chiave client.


## Inizializzazione della tua applicazione Android per raccogliere l'analisi
{: #initalize-ma-sdk-android}

Inizializza la tua applicazione per abilitare l'invio di log al servizio {{site.data.keyword.mobileanalytics_short}}.

1. Importa l'SDK client aggiungendo la seguente istruzione `import` all'inizio del tuo file di progetto:

  ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
  ```
  {: codeblock}

2. Inizializza l'SDK client {{site.data.keyword.mobileanalytics_short}} nella tua applicazione Android aggiungendo il codice di inizializzazione nel metodo `onCreate` dell'attività principale nella tua applicazione Android oppure in un'ubicazione che ritieni più indicata per il tuo progetto.

	```Java
	try {
            BMSClient.getInstance().initialize(this.getApplicationContext(), "", "", BMSClient.REGION_US_SOUTH); // Accertati di puntare alla tua regione
        } catch (MalformedURLException e) {
            Log.e(il_nome_della_tua_applicazione,"L'URL non deve avere un formato non corretto:  " + e.getLocalizedMessage());
        }
  ```
  {: codeblock}

  Per utilizzare l'SDK client {{site.data.keyword.mobileanalytics_short}}, devi inizializzare il `BMSClient` con
il parametro **bluemixRegion**. Nel programma di inizializzazione, il valore **bluemixRegion** specifica quale
distribuzione {{site.data.keyword.Bluemix_notm}} stai utilizzando, ad esempio `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` o `BMSClient.REGION_SYDNEY`.
  <!-- Set this value with a `BMSClient.REGION` static property. -->

  <!--You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. Avvia Analytics utilizzando il tuo oggetto applicazione Android e fornendo ad esso il nome della tua applicazione. Ti serve anche
il valore [**Chiave client**](#analytics-clientkey).
	
	```Java
	Analytics.init(getApplication(), "my_app", apiKey, Analytics.DeviceEvent.LIFECYCLE);
	// In questo esempio di codice, Analytics è configurato per registrare gli eventi del ciclo di vita.
	```
  {: codeblock}

	**Suggerimento:** il nome applicazione viene utilizzato come un filtro per cercare i log client nel dashboard. Quando utilizzi lo stesso nome applicazione su diverse piattaforme (ad esempio Android e iOS), puoi visualizzare tutti i log da tale applicazione sotto lo stesso nome, indipendentemente da quale sia la piattaforma dalla quale i log erano stati inviati.

## Inizializzazione della tua applicazione iOS per raccogliere l'analisi
{: #init-ma-sdk-ios}

Inizializza la tua applicazione per abilitare l'invio di log al servizio {{site.data.keyword.mobileanalytics_short}}. L'SDK Swift è disponibile per iOS e watchOS.

1. Importa i framework `BMSCore` e `BMSAnalytics` aggiungendo le seguenti istruzioni `import` all'inizio
del tuo file di progetto `AppDelegate.swift`:

  ```Swift
  import BMSCore
  import BMSAnalytics
  ```
  {: screen}

2. Per utilizzare l'SDK client {{site.data.keyword.mobileanalytics_short}}, devi prima inizializzare la classe `BMSClient` utilizzando il seguente codice.

  Inserisci il codice di inizializzazione nel metodo `application(_:didFinishLaunchingWithOptions:)` del delegato della tua applicazione oppure in un'ubicazione che ritieni più adatta per il tuo progetto.

    ```Swift
    BMSClient.sharedInstance.initializeWithBluemixAppRoute(nil, bluemixAppGUID: nil, bluemixRegion: BMSClient.REGION_US_SOUTH)`
    ```
    {: codeblock}

    Per utilizzare l'SDK client {{site.data.keyword.mobileanalytics_short}}, devi inizializzare il `BMSClient` con
il parametro **bluemixRegion**. Nel programma di inizializzazione, il valore **bluemixRegion** specifica quale
distribuzione {{site.data.keyword.Bluemix_notm}} stai utilizzando, ad esempio `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` o `BMSClient.REGION_SYDNEY`.
   
   <!-- Set this value with a `BMSClient.REGION` static property. -->

   <!-- You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. Inizializza Analytics fornendo ad esso il nome della tua applicazione mobile. Ti serve anche il valore [**Chiave client**](#analytics-clientkey).

  Il nome applicazione viene utilizzato come un filtro per cercare i log client nel tuo dashboard {{site.data.keyword.mobileanalytics_short}}. Utilizzando lo stesso nome applicazione su diverse piattaforme (ad esempio Android e iOS), puoi visualizzare tutti i log da tale applicazione sotto lo stesso nome, indipendentemente da quale sia la piattaforma dalla quale i log erano stati inviati.

  Un parametro `deviceEvents` facoltativo raccoglie automaticamente l'analisi per gli eventi a livello di dispositivo.

  ### iOS
    {: #ios-initialize-analytics}

      ```
      Analytics.initializeWithAppName("AppName", apiKey: la_tua_chiave_client,
      deviceEvents: DeviceEvent.LIFECYCLE)
      ```

  ### watchOS
  {: #watchos-initialize-analytics}

	```
	  Analytics.initializeWithAppName("AppName", apiKey: la_tua_chiave_api)
	```

  Puoi registrare gli eventi dispositivo su WatchOS utilizzando i metodi `Analytics.recordApplicationDidBecomeActive()` e `Analytics.recordApplicationWillResignActive()`.
  
  Aggiungi la seguente riga al metodo `applicationDidBecomeActive()` della classe ExtensionDelegate.

	```
	Analytics.recordApplicationDidBecomeActive()
	```
  {: codeblock}

  Aggiungi la seguente riga al metodo applicationWillResignActive() della classe ExtensionDelegate:
	```
	Analytics.recordApplicationWillResignActive()
	```
  {: codeblock}

## Raccolta dell'analisi di utilizzo
{: #app-monitoring-gathering-analytics}

  Puoi configurare l'SDK client {{site.data.keyword.mobileanalytics_short}} per registrare l'analisi di utilizzo e inviare i dati registrati al
servizio {{site.data.keyword.mobileanalytics_short}}.

  Utilizza le seguenti API per avviare la registrazione e inviare l'analisi di utilizzo:

#### Android
{: #android-usage-api}
	
```
// Disabilita la registrazione dell'analisi di utilizzo (ad esempio per risparmiare spazio su disco)
// La registrazione è abilitata per impostazione predefinita
Analytics.disable();
	
// Abilita la registrazione dell'analisi di utilizzo
Analytics.enable();
	
Analytics.log(eventJSONObject);
	
// Invia l'analisi di utilizzo registrata al servizio Mobile Analytics
Analytics.send();
```
	
Analisi di utilizzo di esempio per la registrazione di un evento:
	
```
//Registra un evento di analisi personalizzato per i grafici personalizzati, che è rappresentato da un oggetto JSON:
JSONObject eventJSONObject = new JSONObject();
	
eventJSONObject.put("customProperty" , "propertyValue");
```

#### iOS - Swift
{: #ios-usage-api}

```
// Disabilita la registrazione dell'analisi di utilizzo (ad esempio per risparmiare spazio su disco)
// La registrazione è abilitata per impostazione predefinita
Analytics.enabled = false

// Abilita la registrazione dell'analisi di utilizzo
Analytics.enabled = true

// Invia l'analisi di utilizzo registrata al servizio {{site.data.keyword.mobileanalytics_short}}
Analytics.send()
```

Analisi di utilizzo di esempio per la registrazione di un evento:

```
// Registra un evento di analisi personalizzato per i grafici personalizzati
let eventObject = ["customProperty": "propertyValue"]
Analytics.log(eventObject)
```

  <!--Removing Cordova for experimental-->
  <!--### Cordova-->
  <!--{: #usage-analytics-cordova}-->

  <!--```JavaScript-->
  <!--// Enable usage analytics recording-->
  <!--Analytics.enable();-->

  <!--// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service-->
  <!--Analytics.send();-->
  <!--```-->
  <!--**Note:** When you are developing Cordova applications, use the native API to enable application lifecycle event recording.-->

## Abilitazione, configurazione e utilizzo di Logger
{: #app-monitoring-logger}

  L'SDK client {{site.data.keyword.mobileanalytics_full}} fornisce un framework di registrazione simile ad altri framework di log con cui potresti avere dimestichezza, come `java.util.logging` o `log4j`. Il framework di registrazione supporta più istanze logger per pacchetto, diversi livelli di log, l'acquisizione di tracce di stack per l'arresto anomalo di un'applicazione e altro.

  Puoi anche configurare i dati registrati in modo che vengano archiviati sul dispositivo dove è in esecuzione l'applicazione e inviare questi log dispositivo
al servizio {{site.data.keyword.mobileanalytics_short}} in un secondo momento.

  <!-- Initialization has to happen first to be able to collect logs and send them to the {{site.data.keyword.mobileanalytics_short}} service. -->

  Il framework di registrazione dell'SDK client {{site.data.keyword.mobileanalytics_short}} supporta i seguenti livelli di log, che sono elencati dal meno dettagliato al più dettagliato, con le linee guida d'uso consigliate:

  * `FATAL` - da utilizzare per i blocchi o gli arresti anomali irreversibili. Il livello `FATAL` è riservato per la registrazione degli errori irreversibili, che si presentano agli utenti come un arresto anomalo dell'applicazione
  * `ERROR` - da utilizzare per le eccezioni impreviste o gli errori di protocollo di rete imprevisti
  * `WARN` - da utilizzare per registrare le avvertenze di utilizzo che non sono considerate degli errori critici, come l'utilizzo di API ritenute obsolete o una risposta di rete lenta
  * `INFO` - da utilizzare per la notifica di eventi di inizializzazione e altri dati che potrebbero essere importanti senza però essere urgenti
  * `DEBUG` - da utilizzare per la notifica delle istruzioni di debug per aiutare gli sviluppatori a risolvere i difetti delle applicazioni

    #### Scenario di livello di log
    {: #log-level-scenario}

    Quando il livello del logger è configurato su `FATAL`, il logger acquisisce le eccezioni non rilevate ma non acquisisce i log che portano all'evento di arresto anomalo. Puoi impostare un livello del logger più dettagliato per accertarti che vengano acquisiti anche log che possano portare a una voce di logger `FATAL`, come `WARN`
e `ERROR`.

  <!--**Note:** Find full Logger API references for each platform at [SDKs, samples, API reference](sdks-samples-apis.html). The Logger API is part of the--> <!--{{site.data.keyword.mobileanalytics_short}} Client SDK Core.-->

  <!--### Cordova-->


  <!--```JavaScript-->

  <!--var logger = MFPLogger.getInstance("myLogger");-->

  <!--logger.debug("debug info");-->
  <!--logger.info("info message");-->
  <!--logger.warn("warning message");-->
  <!--logger.fatal("fatal message");-->

  <!--```-->


### Utilizzo del Logger di esempio
{: #sample-logger-usage}

**Nota:** accertati di avere strumentato la tua applicazione in modo che utilizzi l'[SDK client {{site.data.keyword.mobileanalytics_short}}](sdk.html) prima di utilizzare il framework di registrazione.
 
  I seguenti frammenti di codice mostrano un utilizzo di esempio del Logger:

#### Android
{: #android-logger-sample}

```
// Configura il Logger per salvare i log sul dispositivo in modo che possano successivamente
// essere inviati al servizio {{site.data.keyword.mobileanalytics_short}}
// Disabilitato per impostazione predefinita: imposta su true per abilitare
Logger.storeLogs(true);

// Modifica il livello di log minimo (facoltativo)
// L'impostazione predefinita è Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);

// Invia i log al servizio {{site.data.keyword.mobileanalytics_short}}
Logger.send();
```

Scenari di Logger:

```
// Crea due istanze del logger
// Puoi creare più istanze di log per organizzare i tuoi log
Logger logger1 = Logger.getLogger("logger1");
Logger logger2 = Logger.getLogger("logger2");

// Registra i messaggi con livelli differenti
// Messaggio di debug per la funzione 1
// Messaggio informativo per la funzione 2
logger1.debug("debug message");
//il messaggiologger1.debug non viene registrato perché il logLevelFilter è impostato su Info
logger2.info("info message");
```

#### iOS - Swift
{: ios-logger-sample}

```
// Configura il Logger per salvare i log sul dispositivo in modo che possano essere successivamente inviati al servizio {{site.data.keyword.mobileanalytics_short}}
// Disabilitato per impostazione predefinita; imposta su true per abilitare
Logger.logStoreEnabled = true

// Modifica il livello di log minimo (facoltativo)
// L'impostazione predefinita è LogLevel.Debug
Logger.logLevelFilter = LogLevel.Info

// Invia i log al servizio {{site.data.keyword.mobileanalytics_short}}
Logger.send()
```

Scenari di Logger:
    
```
// Crea due istanze del logger
// Puoi creare più istanze di log per organizzare i tuoi log
let logger1 = Logger.logger(forName: "feature1Logger")
let logger2 = Logger.logger(forName: "feature2Logger")
	
// Registra i messaggi con livelli differenti
logger1.debug("debug message for feature 1") 
//il messaggio logger1.debug non viene registrato perché il logLevelFilter è impostato su Info
logger2.info("info message for feature 2")
```

**Suggerimento**: per preoccupazioni relative alla privacy, puoi disabilitare l'output del Logger per le applicazioni create in modalità di rilascio. Per impostazione predefinita, la classe Logger stampa i log sulla console Xcode. Nelle impostazioni di build per la tua destinazione, aggiungi un indicatore `-D RELEASE_BUILD` alla sezione **Other Swift Flags** della configurazione della build di rilascio.
    

  <!-- ### Cordova-->
  <!--{: #enable-logger-sample-cordova}-->

  <!--// Enable persisting logs-->
  <!--MFPLogger.setCapture(true);-->

  <!--// Set the minimum log level to be printed and persisted-->
  <!--MFPLogger.setLevel(MFPLogger.INFO);-->

  <!--var logger1 = MFPLogger.getInstance("logger1");-->
  <!--var logger2 = MFPLogger.getInstance("logger2");   -->

  <!--// Log messages with different levels-->
  <!--logger1.debug ("debug message");-->
  <!--logger2.info ("info message");-->

  <!--// Send persisted logs to the {{site.data.keyword.mobileanalytics_short}} Service-->
  <!--```-->

<!--## Enabling the {{site.data.keyword.mobileanalytics_short}} Client SDK internal logs
{: #enable-logger-sdklogs}

  The {{site.data.keyword.mobileanalytics_short}} Client SDK provides a better development experience by not unnecessarily increasing the console output with its internal debug messages. Therefore, by default, internal log messages that are produced by the {{site.data.keyword.mobileanalytics_short}} SDK with the DEBUG level are not printed. You can enable printing of all internal log messages of the {{site.data.keyword.mobileanalytics_short}} Client SDK with the following API:

#### Android
{: #enable-logger-print-android}

```
Logger.setSDKDebugLoggingEnabled(true);
```

#### iOS - Swift
{: #enable-logger-print-swift}

```
Logger.sdkDebugLoggingEnabled = true
```
-->

## Traccia degli utenti attivi
{: #trackingusers}
Puoi, facoltativamente, tenere traccia di quanti utenti stanno attivamente utilizzando la tua applicazione passando il nome dell'utente attivo a {{site.data.keyword.mobileanalytics_short}}.

#### Android
{: #android-tracking-users}

Aggiungi il seguente codice per quando l'utente esegue l'accesso:

```
Analytics.setUserIdentity("nomeutente");
```

Aggiungi il seguente codice per quando l'utente si disconnette:

```
Analytics.clearUserIdentity();
```

#### iOS - Swift
{: #ios-tracking-users}

Aggiungi il seguente codice per quando l'utente esegue l'accesso:

```
Analytics.userIdentity = "nomeutente"
```

Aggiungi il seguente codice per quando l'utente si disconnette:

```
Analytics.userIdentity = nil
```

<!--## Configuring MobileFirst Platform Foundation servers to use the {{site.data.keyword.mobileanalytics_short}} service (optional)
{: #configmfp}
  If you are using MobileFirst Platform Foundation Server V7 and higher, you can configure it to use the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} service to store analytics and logged data. 
  
  Configure MobileFirst Platform V7.0, V7.1, and V8.0 Beta servers to send analytics data to the {{site.data.keyword.mobileanalytics_short}} service on {{site.data.keyword.Bluemix_notm}}.

  1. Visit the dashboard for the {{site.data.keyword.mobileanalytics_short}} service where you want to send analytics data and note the browser URL for the dashboard.
  2. Determine the value for reporting analytics, as follows:
  	1. Get the {{site.data.keyword.mobileanalytics_short}} service route from the dashboard URL. The {{site.data.keyword.mobileanalytics_short}} service route is the part of the URL before `/analytics/console/dashboard`.  

  		For example, if the dashboard URL is: `http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde`
      {: screen}

  		then the Analytics Service Route is
      `http://mobile-analytics-dashboard.ng.bluemix.net`
      {: screen}

  	2. Get the [Client API Key](#analytics-clientkey) value from the Analytics dashboard.

  	You will use the {{site.data.keyword.mobileanalytics_short}} service route and API Key to construct a URL to report analytics data, depending on the version of your MobileFirst Platform server. -->

<!--  3. Copy the URL for your {{site.data.keyword.mobileanalytics_short}} service dashboard. Include the `instanceId` query parameter, for example:
      `http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=1212345abcde`
      {: screen}

  4. Configure the values for the MobileFirst Platform server JNDI properties, as follows:-->

<!--    ### MobileFirst Platform V7.0
    {: #mfp70}

        The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/data?tenant=<Client API Key>`
        {: screen}

        The `wl.analytics.console.url` JNDI property is the Analytics service dashboard URL.

        #### Example of MobileFirst Platform V7.0 JNDI property values
        {: #example-mfp70-jndi-values}

        For a MobileFirst Platform project named `Myproj7000`, based on the examples in steps 2 and 3, replace the current JNDI property values in the `server.xml` file with:
        ```
        <jndiEntry jndiName="MyProj7000/wl.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data?tenant=12345abcde"'/>
        ```
        {: screen}
        ```
        <jndiEntry jndiName="MyProj7000/wl.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
        ```
        {: screen}

    ### MobileFirst Platform V7.1
    {: #mfp71}

      The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/v2/<Client API Key>`
      {: screen}

      #### Example of MobileFirst Platform JNDI V7.1 property values
      {: #example-mfp71-jndi-values}

      For a MobileFirst Platform project named `MyProj7101`, replace the current JNDI property values in the `server.xml` file with:
      ```
      <jndiEntry jndiName="MyProj7101/wl.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/v2/data?tenant=12345abcde"'/>
      ```
      {: screen}
      ```
      <jndiEntry jndiName="MyProj7101/wl.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
      ```
      {: screen}

      ### MobileFirst Platform V8.0
      {: #mfp80}

      The format of the `mfp.analytics.url` JNDI property is:
      `<Analytics Service Route>/analytics-service/rest/v2/<Client API Key>`  

    #### Example MobileFirst Platform V8.0 Beta JNDI property values
      {: example-mfp80b-jndi-values}

      For a MobileFirst Platform project named `mfp`, which is the default, replace the current JNDI property values in the `server.xml` file with:
      ```
      <jndiEntry jndiName="mfp/mfp.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data?tenant=12345abcde"'/>
      ```
      {: screen}
      ```
      <jndiEntry jndiName="mfp/mfp.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
      ```
      {: screen}
-->
<!-- #### Ignored events and event retention
{: #ignored-events}
The {{site.data.keyword.mobileanalytics_short}} service saves the following data for ignored events and event retention:
  
<dl>	
<dt>Ignored events</dt>
	<dd>`ANALYTICS_SDK_CFG_IGNORE_AppPushAction: true`
		  `ANALYTICS_SDK_CFG_IGNORE_ServerLog: true`
		  `ANALYTICS_SDK_CFG_IGNORE_NetworkTransaction: true`
		  `ANALYTICS_SDK_CFG_IGNORE_NetworkTransactionSummarizedHourly: true`
		  `ANALYTICS_SDK_CFG_IGNORE_PushNotification: true`
		  `ANALYTICS_SDK_CFG_IGNORE_PushSubscription: true`</dd>
</dt>
<dt>Event retention</dd>
<dd>
`ANALYTICS_TTL_AlertNotification: 14d`<br>
`ANALYTICS_TTL_CustomData: 7d`<br>
`ANALYTICS_TTL_Device: 90d`<br>
`ANALYTICS_TTL_AppLog: 3d`<br>
`ANALYTICS_TTL_AppSession: 7d`
</dd>
</dt>
</dl>
  
-->

# rellinks

## Riferimento API
{: #api}
* [API REST](https://mobile-analytics-dashboard.eu-gb.bluemix.net/analytics-service/){:new_window}
