---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-18"

---

# Strumentazione della tua applicazione per utilizzare gli SDK client {{site.data.keyword.mobileanalytics_short}}
{: #mobileanalytics_sdk}

Ultimo aggiornamento: 19 ottobre 2016
{: .last-updated}

Gli SDK {{site.data.keyword.mobileanalytics_full}} consentono di strumentare la tua applicazione mobile.
{: shortdesc}

{{site.data.keyword.mobileanalytics_short}} consente di raccogliere due categorie di dati <!--three--> e ciascuna richiede un diverso grado di strumentazione:

1. Dati predefiniti - questa categoria include informazioni generiche sull'utilizzo e sui dispositivi che si applicano a tutte le applicazioni. In questa categoria sono contenuti i metadati di dispositivo (sistema operativo e modello del dispositivo) e i dati di utilizzo (sessioni applicazione e utenti attivi) che indicano il volume, la frequenza o la durata dell'utilizzo delle applicazioni. I dati predefiniti vengono raccolti automaticamente dopo che hai inizializzato l'SDK {{site.data.keyword.mobileanalytics_short}} nella tua applicazione. 

2. Messaggi di log applicazione - questa categoria consente allo sviluppatore di aggiungere delle righe di codice in tutta l'applicazione che registrano dei messaggi personalizzati di supporto nelle attività di sviluppo e debug. Lo sviluppatore assegna un livello di severità/dettaglio a ciascun messaggio di log e può successivamente filtrare i messaggi in base al livello assegnato oppure risparmiare spazio di archiviazione configurando l'applicazione in modo che ignori i messaggi che sono al di sotto di un livello di log fornito. Per raccogliere i dati di log applicazione, devi inizializzare l'SDK {{site.data.keyword.mobileanalytics_short}} nella tua applicazione, nonché aggiungere una riga di codice per ciascun messaggio di log.

<!--2. Custom events - This category includes data that you define yourself and that is specific to your app. This data represents events that occur within your app, such as page views, button taps, or in-app purchases. In addition to initializing the {{site.data.keyword.mobileanalytics_short}} SDK in your app, you must add a line of code for each custom event that you want to track. -->

Attualmente, gli SDK sono disponibili per Android, iOS e WatchOS.

## Identificazione della tua chiave API alle credenziali del servizio
{: #analytics-clientkey}

Identifica il tuo valore **Chiave API** prima di impostare l'SDK client. La chiave API è necessaria per inizializzare l'SDK client.

1. Apri il tuo dashboard del servizio {{site.data.keyword.mobileanalytics_short}}.
2. Fai clic sulla scheda **Credenziali del servizio**.
3. Espandi **Visualizza credenziali** per visualizzare il tuo valore della chiave API. Avrai bisogno del valore della chiave API quando inizializzi l'SDK client {{site.data.keyword.mobileanalytics_short}}.


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
	BMSClient.getInstance().initialize(this.getApplicationContext(), BMSClient.REGION_US_SOUTH); // Assicurati che punti alla tua regione
	```
  {: codeblock}

  Per utilizzare l'SDK client {{site.data.keyword.mobileanalytics_short}}, devi inizializzare il `BMSClient` con
il parametro **bluemixRegion**. Nel programma di inizializzazione, il valore **bluemixRegion** specifica quale distribuzione {{site.data.keyword.Bluemix_notm}} stai utilizzando, ad esempio, `BMSClient.REGION_US_SOUTH` e `BMSClient.REGION_UK`.
    <!-- , or `BMSClient.REGION_SYDNEY`.-->  <!-- Set this value with a `BMSClient.REGION` static property. -->

  <!--You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. Avvia Analytics utilizzando il tuo oggetto applicazione Android e fornendo ad esso il nome della tua applicazione. Ti serve anche il valore [**Chiave API**](#analytics-clientkey).
	
	```Java
	// In questo esempio di codice, Analytics è configurato per registrare gli eventi del ciclo di vita.
	Analytics.init(getApplication(), "your_app_name_here", apiKey, hasUserContext, Analytics.DeviceEvent.LIFECYCLE);
	```
  {: codeblock}
	
	Il nome che hai selezionato per la tua applicazione (`your_app_name_here`) visualizza la console {{site.data.keyword.mobileanalytics_short}} come il nome dell'applicazione. Il nome applicazione viene utilizzato come un filtro per cercare i log applicazione nel dashboard Quando utilizzi lo stesso nome applicazione su diverse piattaforme (ad esempio Android e iOS), puoi visualizzare tutti i log da tale applicazione sotto lo stesso nome, indipendentemente da quale sia la piattaforma dalla quale i log erano stati inviati.
	
	**Nota:** imposta il valore per `hasUserContext` su **true** o **false**. Se false (valore predefinito), ogni dispositivo viene calcolato come un utente attivo. Il metodo [`Analytics.setUserIdentity("username")`](sdk.html#android-tracking-users), che ti abilita a tracciare il numero di utenti per dispositivo che sono attivi utilizzando la tua applicazione, non funzionerà quando `hasUserContext` è false. Se true, ogni utilizzo di [`Analytics.setUserIdentity("username")`](sdk.html#android-tracking-users) viene calcolato come un utente attivo. Non esiste un'identità utente predefinita quando `hasUserContext` è true e di conseguenza deve essere impostato per popolare i grafici dell'utente attivo.
	
4. [Invia dati di analisi](sdk.html#app-monitoring-gathering-analytics) al servizio (sdk.html#app-monitoring-gathering-analytics).

## Inizializzazione della tua applicazione iOS per raccogliere l'analisi 
{: #init-ma-sdk-ios}

Inizializza la tua applicazione per abilitare l'invio di log al servizio {{site.data.keyword.mobileanalytics_short}}. L'SDK Swift è disponibile per iOS e watchOS.

1. Importa i framework `BMSCore` e `BMSAnalytics` aggiungendo le seguenti istruzioni `import` all'inizio del tuo file di progetto `AppDelegate.swift`:

  ```Swift
  import BMSCore
  import BMSAnalytics
  ```
  {: codeblock}

2. Per utilizzare l'SDK client {{site.data.keyword.mobileanalytics_short}}, devi prima inizializzare la classe `BMSClient` utilizzando il seguente codice.

  Inserisci il codice di inizializzazione nel metodo `application(_:didFinishLaunchingWithOptions:)` del delegato della tua applicazione oppure in un'ubicazione che ritieni più adatta per il tuo progetto.
	
    ```Swift
    BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Assicurati che punti alla tua regione
    ```
    {: codeblock}

    Per utilizzare l'SDK client {{site.data.keyword.mobileanalytics_short}}, devi inizializzare il `BMSClient` con
il parametro **bluemixRegion**. Nel programma di inizializzazione, il valore **bluemixRegion** specifica quale distribuzione {{site.data.keyword.Bluemix_notm}} stai utilizzando, ad esempio `BMSClient.REGION_US_SOUTH` o `BMSClient.REGION_UK`.
    <!-- , or `BMSClient.REGION_SYDNEY`. -->
   
   <!-- Set this value with a `BMSClient.REGION` static property. -->

   <!-- You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. Inizializza Analytics fornendo ad esso il nome della tua applicazione mobile. Ti serve anche il valore [**Chiave API**](#analytics-clientkey).

 Il nome applicazione viene utilizzato come un filtro per cercare i log applicazione nel tuo dashboard {{site.data.keyword.mobileanalytics_short}}. Utilizzando lo stesso nome applicazione su diverse piattaforme (ad esempio Android e iOS), puoi visualizzare tutti i log da tale applicazione sotto lo stesso nome, indipendentemente da quale sia la piattaforma dalla quale i log erano stati inviati.

  Un parametro `deviceEvents` facoltativo raccoglie automaticamente l'analisi per gli eventi a livello di dispositivo.

 ### iOS
 {: #ios-initialize-analytics}
	
 ```Swift
 Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: DeviceEvent.lifecycle)
 ```
 {: codeblock}
  
 ### watchOS
 {: #watchos-initialize-analytics}
	
 ```Swift
 Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false)
  ```
 {: codeblock}
	
 Il nome che hai selezionato per la tua applicazione (`your_app_name_here`) visualizza la console {{site.data.keyword.mobileanalytics_short}} come il nome dell'applicazione. Il nome applicazione viene utilizzato come un filtro per cercare i log applicazione nel dashboard Quando utilizzi lo stesso nome applicazione su diverse piattaforme (ad esempio Android e iOS), puoi visualizzare tutti i log da tale applicazione sotto lo stesso nome, indipendentemente da quale sia la piattaforma dalla quale i log erano stati inviati.
	
 **Nota:** imposta il valore per `hasUserContext` su **true** o **false**. Se false (valore predefinito), ogni dispositivo viene calcolato come un utente attivo. Il metodo [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users), che ti abilita a tracciare il numero di utenti per dispositivo che sono attivi utilizzando la tua applicazione, non funzionerà quando `hasUserContext` è false. Se `hasUserContext` è true, ogni utilizzo di [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) viene calcolato come un utente attivo. Non esiste un'identità utente predefinita quando `hasUserContext` è true e di conseguenza deve essere impostato per popolare i grafici dell'utente attivo.

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
  
4. [Invia dati di analisi](sdk.html#app-monitoring-gathering-analytics) al servizio {{site.data.keyword.mobileanalytics_short}}.

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
		
// Invia l'analisi di utilizzo registrata al servizio Mobile Analytics
Analytics.send(new ResponseListener() {
            @Override
	    public void onSuccess(Response response) {
                // Gestione dell'invio Analytics con esito positivo.
            }

            @Override
            public void onFailure(Response response, Throwable throwable, JSONObject jsonObject) {
                // Gestione dell'invio Analytics con esito negativo.
            }
        });
```
{: codeblock}

<!-- removed: Analytics.log(eventJSONObject); -->

<!--	
Sample usage analytics for logging an event:
	
```
// Log a custom analytics event for custom charts, which is represented by a JSON object:
JSONObject eventJSONObject = new JSONObject();
	
eventJSONObject.put("customProperty" , "propertyValue");
```
{: codeblock}
-->

#### iOS - Swift
{: #ios-usage-api}

```
// Disabilita la registrazione dell'analisi di utilizzo (ad esempio per risparmiare spazio su disco)
// La registrazione è abilitata per impostazione predefinita
Analytics.isEnabled = false

// Abilita la registrazione dell'analisi di utilizzo
Analytics.isEnabled = true

// Invia l'analisi di utilizzo registrata al servizio Mobile Analytics
Analytics.send(completionHandler: { (response: Response?, error: Error?) in

    if let response = response {
        // Gestione dell'invio Analytics con esito positivo.
    }
    if let error = error {
        // Gestione dell'invio Analytics con esito negativo.
    }
})
```
{: codeblock}

<!--
Sample usage analytics for logging an event:

#### Swift
{: customchartsswift}

```Swift
// Log a custom analytics event for custom charts
let eventObject = ["customProperty": "propertyValue"]
Analytics.log(eventObject)
```
{: codeblock}

-->

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

**Nota:** accertati di avere strumentato la tua applicazione in modo che utilizzi l'SDK client {{site.data.keyword.mobileanalytics_short}} prima di utilizzare il framework di registrazione. 
 
  I seguenti frammenti di codice mostrano un utilizzo di esempio del Logger:

#### Android
{: #android-logger-sample}

```
// Configura il Logger per salvare i log sul dispositivo in modo che possano successivamente
// essere inviati al servizi Mobile Analytics
// Disabilitato per impostazione predefinita: imposta su true per abilitare
Logger.storeLogs(true);

// Modifica il livello di log minimo (facoltativo)
// L'impostazione predefinita è Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);

// Crea due istanze del logger
// Puoi creare più istanze di log per organizzare i tuoi log
Logger logger1 = Logger.getLogger("logger1");
Logger logger2 = Logger.getLogger("logger2");

// Registra i messaggi con livelli differenti
// Messaggio di debug per la funzione 1
// Messaggio informativo per la funzione 2
logger1.debug("debug message");
//il messaggio logger1.debug non viene registrato perché il logLevelFilter è impostato su Info
logger2.info("info message");

// Invia i log al servizio Mobile Analytics
        Logger.send(new ResponseListener() {
                    @Override
	    public void onSuccess(Response response) {
                        // Gestione del logger con esito positivo.
                    }

                    @Override
                    public void onFailure(Response response, Throwable throwable, JSONObject jsonObject) {
                        // Gestione del logger con esito negativo.
                    }
                });        
```
{: codeblock}

#### iOS - Swift
{: #ios-logger-sample-swift2}

```
// Configura il Logger per salvare i log sul dispositivo in modo che possano essere successivamente inviati al servizio Mobile Analytics
// Disabilitato per impostazione predefinita; imposta su true per abilitare
Logger.isLogStorageEnabled = true

// Modifica il livello di log minimo (facoltativo)
// L'impostazione predefinita è LogLevel.debug
Logger.logLevelFilter = LogLevel.info

// Crea due istanze del logger
// Puoi creare più istanze di log per organizzare i tuoi log
let logger1 = Logger.logger(name: "feature1Logger")
let logger2 = Logger.logger(name: "feature2Logger")
	
// Registra i messaggi con livelli differenti
logger1.debug(message: "debug message for feature 1") 
//il messaggio logger1.debug non viene registrato perché il logLevelFilter è impostato su info
logger2.info(message: "info message for feature 2")

// Invia i log al servizio Mobile Analytics
Logger.send(completionHandler: { (response: Response?, error: Error?) in
    
    if let response = response {
        logger.debug(message: "Status code: \(response.statusCode)")
        logger.debug(message: "Response: \(response.responseText)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
})
```
{: codeblock}

**Suggerimento:** per preoccupazioni relative alla privacy, puoi disabilitare l'output del Logger per le applicazioni create in modalità di rilascio. Per impostazione predefinita, la classe Logger stampa i log sulla console Xcode. Nelle impostazioni di build per la tua destinazione, aggiungi un indicatore `-D RELEASE_BUILD` alla sezione **Other Swift Flags** della configurazione della build di rilascio.
    

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
{: codeblock}
Logger.setSDKDebugLoggingEnabled(true);
```
{: codeblock}

#### iOS - Swift
{: #enable-logger-print-swift}

```
Logger.sdkDebugLoggingEnabled = true
```
{: codeblock}
-->

## Segnalazione analisi degli arresti anomali
{: #report-crash-analytics}

Puoi visualizzare i [dati sugli arresti anomali dell'applicazione](app-monitoring.html#monitor-app-crash) inviando le analisi e le informazioni di log a {{site.data.keyword.mobileanalytics_short}}.

Il metodo `Analytics.send()` popola le tabelle **Panoramica arresti anomali** e **Arresti anomali** nella pagina **Arresti anomali**. I grafici in questa sezione vengono abilitati utilizzando l'inizializzazione e l'invio del processo per le analisi; non è necessaria alcuna configurazione speciale.

Il metodo `Logger.send()` popola le tabelle **Riepilogo arresti anomali** e **Dettagli arresti anomali** nella pagina **Risoluzione dei problemi**. Devi abilitare la tua applicazione ad archiviare e inviare i log per popolare i grafici in questa sezione, aggiungendo un ulteriore istruzione nel tuo codice dell'applicazione:

#### Android
{: #android-crash-statement}

* `Logger.storeLogs(true);`
<!-- * `Logger.setLogLevel(Logger.LEVEL.FATAL); // or greater` -->

Consulta [Utilizzo del Logger di esempio](sdk.html#android-logger-sample).

#### iOS
{: #ios-crash-statement}

* `Logger.isLogStorageEnabled = true`
<!-- * `Logger.logLevelFilter = LogLevel.Fatal // or greater` -->

Consulta [Utilizzo del Logger di esempio](sdk.html##ios-logger-sample-swift2).

## Traccia degli utenti attivi
{: #trackingusers}

Se la tua applicazione può riconoscere utenti univoci su un dispositivo, puoi facoltativamente tenere traccia di quanti utenti stanno attivamente utilizzando la tua applicazione passando il nome dell'utente attivo a {{site.data.keyword.mobileanalytics_short}}. 

Abilita il tracciamento dell'utente inizializzando {{site.data.keyword.mobileanalytics_short}} con `hasUserContext=true`. Altrimenti, {{site.data.keyword.mobileanalytics_short}}  acquisisce solo un'utente per dispositivo. 

#### Android
{: #android-tracking-users}

Aggiungi il seguente codice per tracciare quando l'utente esegue l'accesso: 

```
Analytics.setUserIdentity("nomeutente");
```
{: codeblock}

<!--Add the following code for when the user logs out:

```
Analytics.clearUserIdentity();
```
{: codeblock}
-->

#### iOS - Swift
{: #ios-tracking-users}

Aggiungi il seguente codice per tracciare quando l'utente esegue l'accesso: 

```
Analytics.userIdentity = "nomeutente"
```
{: codeblock}

<!--
Add the following code for when the user logs out:

```
Analytics.userIdentity = nil
```
{: codeblock}
-->

<!--## Configuring MobileFirst Platform Foundation servers to use the {{site.data.keyword.mobileanalytics_short}} service (optional)
{: #configmfp}
  If you are using MobileFirst Platform Foundation Server V7 and higher, you can configure it to use the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} service to store analytics and logged data. 
  
  Configure MobileFirst Platform V7.0, V7.1, and V8.0 Beta servers to send analytics data to the {{site.data.keyword.mobileanalytics_short}} service on {{site.data.keyword.Bluemix_notm}}.

  1. Visit the dashboard for the {{site.data.keyword.mobileanalytics_short}} service where you want to send analytics data and note the browser URL for the dashboard.
  2. Determine the value for reporting analytics, as follows:
  	1. Get the {{site.data.keyword.mobileanalytics_short}} service route from the dashboard URL. The {{site.data.keyword.mobileanalytics_short}} service route is the part of the URL before ``/analytics/console/dashboard``.  

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

## Operazioni successive
{: #what-to-do-next}

Puoi ora andare alla **Console** {{site.data.keyword.mobileanalytics_short}} per visualizzare l'analisi di utilizzo, come ad esempio i nuovi dispositivi e il numero totale di dispositivi che utilizzano la tua applicazione. Puoi anche monitorare l'applicazione <!--[creating custom charts](app-monitoring.html#custom-charts),-->[impostando gli avvisi](app-monitoring.html#alerts) e [monitorando gli arresti anomali delle applicazioni](app-monitoring.html#monitor-app-crash).

# rellinks

## Riferimento API
{: #api}
* [API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
