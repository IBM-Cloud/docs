---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Anwendung zur Verwendung der Client-SDKs von {{site.data.keyword.mobileanalytics_short}} instrumentieren
{: #mobileanalytics_sdk}

Mit den {{site.data.keyword.mobileanalytics_full}}-SDKs können Sie die mobile Anwendung instrumentieren.
{: shortdesc}

{{site.data.keyword.mobileanalytics_short}} ermöglicht das Erfassen von zwei Datenkategorien, von denen für jede ein unterschiedlicher Umfang an Instrumentierung erforderlich ist:

1. Vordefinierte Daten - Diese Kategorie umfasst Informationen zur allgemeinen Nutzung und zum Gerät, die auf alle Anwendungen zutreffen. Diese Kategorie setzt sich aus Gerätemetadaten (Betriebssystem und Gerätemodell) und Nutzungsdaten (aktive Benutzer und Anwendungssitzungen) zusammen, aus denen das Volumen, die Häufigkeit oder die Dauer der Anwendungsnutzung hervorgehen. Vordefinierte Daten werden nach der Initialisierung des {{site.data.keyword.mobileanalytics_short}}-SDKs in Ihrer Anwendung automatisch erfasst.

2. Anwendungsprotokollnachrichten - Diese Kategorie ermöglicht dem Entwickler das Hinzufügen von Codezeilen in der ganzen Anwendung, die zur Erleichterung der Entwicklung und Fehlerbehebung benutzerdefinierte Nachrichten protokollieren. Der Entwickler weist jeder Protokollnachricht eine Ebene für den Schweregrad bzw. die Ausführlichkeit zu und kann die Nachrichten danach anhand der zugewiesenen Ebene filtern; alternativ kann er die Anwendung so konfigurieren, dass Nachrichten auf einer niedrigeren Ebene einer bestimmten Protokollebene ignoriert werden, um Speicherplatz zu sparen. Wenn Sie Anwendungsprotokolldaten erfassen möchten, müssen Sie das {{site.data.keyword.mobileanalytics_short}}-SDK innerhalb Ihrer Anwendung initialisieren und für jede Protokollnachricht eine Codezeile hinzufügen.

3. Angepasste Ereignisse - Diese Kategorie umfasst Daten, die Sie selbst definieren und die für Ihre App spezifisch sind. Diese Daten stellen Ereignisse in Ihrer App dar, z. B. Seitenansichten, Schaltflächenantipper oder app-interne Käufe. Zusätzlich zur Initialisierung des {{site.data.keyword.mobileanalytics_short}}-SDK in Ihrer App müssen Sie für jedes angepasste Ereignis, das Sie verfolgen möchten, eine Codezeile hinzufügen. 

Derzeit sind SDKs für Android, iOS, WatchOS und Cordova verfügbar.

## API-Schlüsselwert für Serviceberechtigungsnachweise angeben
{: #analytics-clientkey}

Geben Sie Ihren **API-Schlüsselwert** an, bevor Sie das Client-SDK konfigurieren. Der API-Schlüssel ist für die Initialisierung des Client-SDKs erforderlich.

1. Öffnen Sie das Dashboard für den {{site.data.keyword.mobileanalytics_short}}-Service.
2. Erweitern Sie **Berechtigungsnachweise anzeigen**, um Ihren API-Schlüsselwert sichtbar zu machen. Den API-Schlüsselwert benötigen Sie für die Initialisierung des {{site.data.keyword.mobileanalytics_short}}-Client-SDK.


## Anwendung zum Erfassen von Analysedaten initialisieren
{: #initalize-ma-sdk}

Initialisieren Sie die Anwendung, damit Protokolle an den {{site.data.keyword.mobileanalytics_short}}-Service gesendet werden können.

1. Importieren Sie das Client-SDK.

	### Android
	{: #android-import}

	Fügen Sie die folgenden `import`-Anweisungen am Anfang Ihrer Projektdatei ein:
	
  	```
  	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
  	```
  	{: codeblock}
  
	### iOS
	{: #ios-import}
	
	**Hinweis:** Das Swift-SDK ist für iOS und WatchOS verfügbar.
	
	Importieren Sie die Frameworks `BMSCore` und `BMSAnalytics` durch Hinzufügen der folgenden `import`-Anweisungen am Anfang der Projektdatei `AppDelegate.swift`:

   ```Swift
  import BMSCore
  import BMSAnalytics
   ```
   {: codeblock}  
   
   ### Cordova
	{: #cordova-import}
		
	Fügen Sie das Cordova-Plug-in hinzu, indem Sie den folgenden Befehl im Stammverzeichnis der Cordova-Anwendung ausführen:

   ```Javascript
   cordova plugin add bms-core
   ```
   {: codeblock}  

2. Initialisieren Sie das {{site.data.keyword.mobileanalytics_short}}-Client-SDK in Ihrer Anwendung.

	### Android
	{: #android-init}
	
	Initialisieren Sie das {{site.data.keyword.mobileanalytics_short}}-Client-SDK in der Android-Anwendung durch Hinzufügen des Initialisierungscodes in der Methode `onCreate` der Hauptaktivität in der Android-Anwendung oder an einer Position, die sich für das Projekt am besten eignet.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // Sicherstellen, dass auf eigene Region verwiesen wird
	```
	{: codeblock}

  Sie müssen `BMSClient` mit dem Parameter **bluemixRegion** initialisieren. Im Initialisierungsoperator gibt der Wert für **bluemixRegion** an, welche {{site.data.keyword.Bluemix_notm}}-Bereitstellung verwendet wird, zum Beispiel `BMSClient.REGION_US_SOUTH` und `BMSClient.REGION_UK`. 
    <!-- , or `BMSClient.REGION_SYDNEY`.--> 
    
 ### iOS
 {: #ios-init}
    
 Initialisieren Sie zuerst mithilfe des nachfolgenden Codes die Klasse `BMSClient`. Versetzen Sie den Initialisierungscode in die Methode `application(_:didFinishLaunchingWithOptions:)` des Anwendungsdelegierten oder an eine Position, die sich für das Projekt am besten eignet.
	
    ```Swift
    BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Sicherstellen, dass auf eigene Region verwiesen wird
    ```
   {: codeblock}

   Sie müssen `BMSClient` mit dem Parameter **bluemixRegion** initialisieren. Im Initialisierungsoperator gibt der Wert für **bluemixRegion** an, welche {{site.data.keyword.Bluemix_notm}}-Bereitstellung verwendet wird, zum Beispiel `BMSClient.Region.usSouth` oder `BMSClient.Region.unitedKingdom`.
    <!-- , or `BMSClient.Region.Sydney`. -->
    
 ### Cordova
 {: #cordova-init}
    
 Initialisieren Sie **BMSClient** und **BMSAnalytics**. Sie benötigen den Wert für den [**API-Schlüssel**](#analytics-clientkey).

  ```Javascript
  var applicationName = "HelloWorld";
  var apiKey =  "your_api_key_here";
  var hasUserContext = true;
  var deviceEvents = [BMSAnalytics.ALL];

  BMSClient.initialize(BMSClient.REGION_US_SOUTH); //Sicherstellen, dass auf eigene Region verwiesen wird	
  BMSAnalytics.initialize(applicationName, apiKey, hasUserContext, deviceEvents)
  ```
  {:codeblock}

 Zum Verwenden des {{site.data.keyword.mobileanalytics_short}}-Client-SDKs müssen Sie `BMSClient` mit dem Parameter **bluemixRegion** initialisieren. Im Initialisierungsoperator gibt der Wert für **bluemixRegion** an, welche {{site.data.keyword.Bluemix_notm}}-Bereitstellung verwendet wird, zum Beispiel `BMSClient.REGION_US_SOUTH` oder `BMSClient.REGION_UK`.
    <!-- , or `BMSClient.REGION_SYDNEY`. -->
    
3. Initialisieren Sie Analytics mithilfe des Anwendungsobjekts und legen Sie dafür den Namen der Anwendung fest. 

	Der Name, den Sie für Ihre Anwendung auswählen (`your_app_name_here`), wird in der {{site.data.keyword.mobileanalytics_short}}-Konsole als Anwendungsname angezeigt. Der Anwendungsname wird als Filter für die Suche nach Anwendungsprotokollen im Dashboard verwendet. Wenn Sie plattformübergreifend (zum Beispiel für Android und iOS) denselben Anwendungsnamen verwenden, können Sie unter einem Namen unabhängig von der Plattform, von der die Protokolle stammen, alle Protokolle zu dieser Anwendung anzeigen.

	Außerdem benötigen Sie den Wert für den [**API-Schlüssel**](#analytics-clientkey).

	### Android
	{: #android-init-analytics}
	
	```Java
	// In diesem Codebeispiel ist Analytics für die Aufzeichnung von Lebenszyklusereignissen konfiguriert.
	Analytics.init(getApplication(), "your_app_name_here", apiKey, hasUserContext, Analytics.DeviceEvent.ALL);
	```
	{: codeblock}
	
	**Hinweis:** Setzen Sie den Wert für `hasUserContext` auf **true** oder **false**. Bei 'false' (Standardwert) wird jedes Gerät als aktiver Benutzer gezählt. Die Methode [`Analytics.setUserIdentity("username")`](sdk.html#android-tracking-users), mit der Sie die Anzahl der Benutzer pro Gerät verfolgen können, die Ihre Anwendung aktiv nutzen, funktioniert nicht, wenn der Wert für `hasUserContext` 'false' ist. Bei 'true' wird jede Verwendung von  [`Analytics.setUserIdentity("username")`](sdk.html#android-tracking-users) als ein aktiver Benutzer gezählt. Wenn `hasUserContext` auf 'true' gesetzt ist, gibt es keine Standardbenutzer-ID. Daher muss diese festgelegt werden, damit die Diagramme für aktive Benutzer gefüllt werden.
	
	### iOS
	{: #ios-initialize-analytics}
	
 	```Swift 
	Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: .lifecycle, .network)
 	```
 	{: codeblock}
 	
   ### WatchOS
   {: #watchos-initialize-analytics}
	 	
 	```Swift
 	Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", deviceEvents: .network)
 	```
 	{: codeblock}
 	
 	Mit dem optionalen Parameter `deviceEvents` können automatisch Analysedaten für gerätespezifische Ereignisse erfasst werden.
	
 **Hinweis:** Setzen Sie den Wert für `hasUserContext` auf **true** oder **false**. Bei 'false' (Standardwert) wird jedes Gerät als aktiver Benutzer gezählt. Die Methode [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users), mit der Sie die Anzahl der Benutzer pro Gerät verfolgen können, die Ihre Anwendung aktiv nutzen, funktioniert nicht, wenn `hasUserContext` auf 'false' gesetzt ist. Wenn `hasUserContext` auf 'true' gesetzt ist, zählt jede Verwendung von [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) als ein aktiver Benutzer. Wenn `hasUserContext` auf 'true' gesetzt ist, gibt es keine Standardbenutzer-ID. Daher muss diese festgelegt werden, damit die Diagramme für aktive Benutzer gefüllt werden.

 #### WatchOS
 {: #watchos-record-device}

 Unter WatchOS können Sie Geräteereignisse mit den Methoden `Analytics.recordApplicationDidBecomeActive()` und `Analytics.recordApplicationWillResignActive()` aufzeichnen.
  
 Fügen Sie die folgende Zeile zur Methode `applicationDidBecomeActive()` der Klasse 'ExtensionDelegate' hinzu:
 
	```
	Analytics.recordApplicationDidBecomeActive()
	```
   {: codeblock}

 Fügen Sie die folgende Zeile zur Methode `applicationWillResignActive()` der Klasse 'ExtensionDelegate' hinzu:
 
	```
	Analytics.recordApplicationWillResignActive()
	```
	{: codeblock}	
		
4. Sie haben die Anwendung nun für die Erfassung von Analysedaten initialisiert. Als Nächstes können Sie die Schritte zum [Senden von Analysedaten](sdk.html#app-monitoring-gathering-analytics) an den {{site.data.keyword.mobileanalytics_short}}-Service durchführen.


## Nutzungsanalysedaten zusammenstellen
{: #app-monitoring-gathering-analytics}

  Sie können das {{site.data.keyword.mobileanalytics_short}}-Client-SDK zum Aufzeichnen der Nutzungsanalysedaten und Senden der aufgezeichneten Daten an den {{site.data.keyword.mobileanalytics_short}}-Service konfigurieren.

  Verwenden Sie die folgende API zum Starten einer Aufzeichnung und zum Senden der Nutzungsanalysedaten:

#### Android
{: #android-usage-api}
	
```
// Aufzeichnung der Nutzungsanalysedaten inaktivieren (z. B. zum Sparen von Speicherplatz)
// Aufzeichnung ist standardmäßig aktiviert
Analytics.disable();
	
// Aufzeichnung der Nutzungsanalysedaten aktivieren
Analytics.enable();
		
// Aufgezeichnete Nutzungsanalysedaten an Mobile Analytics-Service senden
Analytics.send(new ResponseListener() {
            @Override
            public void onSuccess(Response response) {
                // Sendeerfolg für Analytics hier bearbeiten.
            }

            @Override
            public void onFailure(Response response, Throwable throwable, JSONObject jsonObject) {
                // Sendefehler für Analytics hier bearbeiten.
            }
        });
```
{: codeblock}
	
Beispiel für Nutzungsanalyse zur Protokollierung eines Ereignisses:
	
```
// Angepasstes Analyseereignis protokollieren
JSONObject eventJSONObject = new JSONObject();
	
eventJSONObject.put("customProperty" , "propertyValue");

Analytics.log(eventJSONObject);
```
{: codeblock}


#### iOS - Swift
{: #ios-usage-api}

```
// Aufzeichnung der Nutzungsanalysedaten inaktivieren (z. B. zum Sparen von Speicherplatz)
// Aufzeichnung ist standardmäßig aktiviert
Analytics.isEnabled = false

// Aufzeichnung der Nutzungsanalysedaten aktivieren
Analytics.isEnabled = true

// Aufgezeichnete Nutzungsanalysedaten an Mobile Analytics-Service senden
Analytics.send(completionHandler: { (response: Response?, error: Error?) in

    if let response = response {
        // Sendeerfolg für Analytics hier bearbeiten.
    }
    if let error = error {
        // Sendefehler für Analytics hier bearbeiten.
    }
})
```
{: codeblock}

Beispiel für Nutzungsanalyse zur Protokollierung eines Ereignisses:

```Swift
// Angepasstes Analyseereignis protokollieren
let eventObject = ["customProperty": "propertyValue"]
Analytics.log(metadata: eventObject)
```
{: codeblock}

#### Cordova
{: #usage-analytics-cordova}

  ```JavaScript
  // Aufzeichnung von Nutzungsanalysedaten aktivieren
  BMSAnalytics.enable();
  
  // Aufzeichnung von Nutzungsanalysedaten deaktivieren
  BMSAnalytics.disable();

  // Aufgezeichnete Nutzungsanalysedaten an den {{site.data.keyword.mobileanalytics_short}}-Service senden
  BMSAnalytics.send(
	function(response) {
		console.log('success: ' + response);
		},
	function (err) {
		console.log('fail: ' + err);
		});
  ```
  {: codeblock}

Beispiel für Nutzungsanalyse zur Protokollierung eines Ereignisses:

```JavaScript
// Angepasstes Analyseereignis protokollieren
var eventObject = {"customProperty": "propertyValue"}
BMSAnalytics.log(eventObject)
```
{: codeblock}

  
  **Hinweis:** Verwenden Sie bei der Entwicklung von Cordova-Anwendungen die native API zum Aktivieren der Aufzeichnung von Anwendungslebenszyklusereignissen.
  
## Protokollfunktion aktivieren, konfigurieren und verwenden
{: #app-monitoring-logger}

  Vom {{site.data.keyword.mobileanalytics_full}}-Client-SDK wird ein Protokollierungsframework bereitgestellt, das anderen Protokollierungsframeworks ähnelt, mit denen Sie unter Umständen vertraut sind, zum Beispiel `java.util.logging` oder `log4j`. Vom Protokollierungsframework werden mehrere paketweise arbeitende Protokollfunktionen, unterschiedliche Protokollebenen, die Erfassung von Stack-Traces für einen Anwendungsabsturz, etc bereitgestellt.

  Sie können auch konfigurieren, dass die protokollierten Daten auf dem Gerät gespeichert werden sollen, auf dem die Anwendung ausgeführt wird und dass diese Geräteprotokolle zu einem späteren Zeitpunkt an den {{site.data.keyword.mobileanalytics_short}}-Service gesendet werden sollen.

  <!-- Initialization has to happen first to be able to collect logs and send them to the {{site.data.keyword.mobileanalytics_short}} service. -->

  Vom Protokollierungsframework des {{site.data.keyword.mobileanalytics_short}}-Client-SDKs werden die folgenden Protokollebenen (aufgelistet von der am wenigsten ausführlichen bis zur ausführlichsten Ebene) unterstützt, für die die nachfolgenden Verwendungsrichtlinien empfohlen werden:

  * `FATAL` - Für nicht behebbare Abstürze oder Blockierungen. Die Ebene `FATAL` ist für die Protokollierung nicht behebbarer Fehler reserviert, die vom Benutzer als Absturz der Anwendung wahrgenommen werden.
  * `ERROR` - Für unerwartete Ausnahmebedingungen oder nicht erwartete Netzprotokollfehler.
  * `WARN` - Für Protokollbelegungswarnungen, die nicht als kritische Fehler betrachtet werden, zum Beispiel die Verwendung nicht weiter unterstützter APIs oder eine langsame Netzantwort.
  * `INFO` - Für die Berichterstellung bei Initialisierungsfehlern und anderen Daten, die wichtig sein können, aber nicht dringend sind.
  * `DEBUG` - Für die Berichterstellung bei Debuganweisungen zur Unterstützung der Entwickler bei der Behebung von Mängeln.

    #### Szenario für eine Protokollebene
    {: #log-level-scenario}

    Wenn für die Protokollfunktion die Ebene `FATAL` konfiguriert ist, werden von der Protokollfunktion nicht abgefangene Ausnahmebedingungen erfasst, aber nicht Protokolle, die Aufschluss über den Vorlauf vor dem Absturzereignis liefern. Sie können eine ausführlichere Protokollebene festlegen, um sicherzustellen, dass auch Protokolle erfasst werden, die zum Eintrag `FATAL` der Protokollfunktion führen, zum Beispiel `WARN` oder `ERROR`.

    Wenn die Protokollierungsstufe auf `DEBUG` gesetzt ist, erhalten Sie zudem Protokolle des Mobile Analytics-Client-SDK, die im Sendeumfang der Protokolle enthalten sind.

  <!--**Note:** Find full Logger API references for each platform at [SDKs, samples, API reference](sdks-samples-apis.html). The Logger API is part of the--> <!--{{site.data.keyword.mobileanalytics_short}} Client SDK Core.-->

### Beispiel für Verwendung der Protokollfunktion
{: #sample-logger-usage}

**Hinweis:** Stellen Sie sicher, dass Sie die Anwendung zur Verwendung des {{site.data.keyword.mobileanalytics_short}}-Client-SDKs instrumentiert haben, bevor Sie das Protokollierungsframework verwenden.
 
  An den folgenden Codeausschnitten wird die Verwendung der Beispielprotokollfunktion veranschaulicht:
#### Android
{: #android-logger-sample}

```
// Protokollfunktion zum Speichern der Protokolle auf dem Gerät konfigurieren, sodass sie später
// an den Mobile Analytics-Service gesendet werden können
// Standardmäßig inaktiviert; zum Aktivieren auf true setzen
Logger.storeLogs(true);

// Mindestprotokollierungsebene ändern (optional)
// Die Standardeinstellung ist Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);

// Zwei Instanzen für Protokollfunktion erstellen
// Sie können mehrere Protokollinstanzen zum Organisieren der Protokolle erstellen
Logger logger1 = Logger.getLogger("logger1");
Logger logger2 = Logger.getLogger("logger2");

// Protokollnachrichten mit unterschiedlichen Ebenen
// Debugnachricht für Funktion 1
// Informationsnachricht für Funktion 2
logger1.debug("debug message");
// Die Nachricht logger1.debug wird nicht protokolliert, weil für logLevelFilter der Wert Info eingestellt ist
logger2.info("info message");

// Protokolle an den Mobile Analytics-Service senden
        Logger.send(new ResponseListener() {
                    @Override
                    public void onSuccess(Response response) {
                        // Sendeerfolg für Logger hier bearbeiten.
                    }

                    @Override
                    public void onFailure(Response response, Throwable throwable, JSONObject jsonObject) {
                        // Sendefehler für Logger hier bearbeiten.
                    }
                });        
```
{: codeblock}

#### iOS - Swift
{: #ios-logger-sample-swift2}

```
// Protokollfunktion zum Speichern der Protokolle auf dem Gerät konfigurieren, sodass sie
// später an den Mobile Analytics-Service gesendet werden können.
// Standardmäßig inaktiviert; zum Aktivieren auf true setzen
Logger.isLogStorageEnabled = true

// Mindestprotokollierungsebene ändern (optional)
// Die Standardeinstellung ist LogLevel.debug
Logger.logLevelFilter = LogLevel.info

// Zwei Instanzen für Protokollfunktion erstellen
// Sie können mehrere Protokollinstanzen zum Organisieren der Protokolle erstellen
let logger1 = Logger.logger(name: "feature1Logger")
let logger2 = Logger.logger(name: "feature2Logger")

// Protokollnachrichten mit unterschiedlichen Ebenen
logger1.debug(message: "debug message for feature 1") 
// Die Nachricht logger1.debug wird nicht protokolliert, weil für
// logLevelFilter der Wert info eingestellt ist
logger2.info(message: "info message for feature 2")

// Protokolle an den Mobile Analytics-Service senden
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

**Tipp:** Aus Datenschutzgründen können Sie die Ausgabe der Protokollfunktion für Anwendungen inaktivieren, die im Releasemodus erstellt werden. Von der Protokollfunktionsklasse werden Protokolle standardmäßig in der Xcode-Konsole gedruckt. Fügen Sie in den Erstellungseinstellungen für das Ziel das Flag `-D RELEASE_BUILD` zum Abschnitt mit den weiteren Swift-Flags der Buildkonfiguration des Release hinzu.
    

#### Cordova
{: #enable-logger-sample-cordova}

  ```
  // Speicherung von Protokollen aktivieren
  BMSLogger.storeLogs(true);

  // Auszugebende und zu speichernde Mindestprotokollstufe festlegen
  BMSLogger.setLogLevel(BMSLogger.INFO);

  var logger1 = BMSLogger.getLogger("logger1");
  var logger2 = BMSLogger.getLogger("logger2");   

  // Protokollnachrichten mit unterschiedlichen Ebenen
  logger1.debug ("debug message");
  logger2.info ("info message");

  // Gespeicherte Protokolle an den {{site.data.keyword.mobileanalytics_short}}-Service senden
  BMSLogger.send();
  BMSAnalytics.send();
  ```
  {: codeblock}


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

## Eine Netzanforderung ausführen
{: #network-requests}

Sie können das {{site.data.keyword.mobileanalytics_short}}-Client-SDK zum [Ausführen einer Netzanforderung](/docs/mobile/sdk_network_request.html) konfigurieren. Stellen Sie sicher, dass Sie `BMSClient` und `BMSAnalytics` bereits initialisiert und die Client-SDKs importiert haben.

<!--
#### Android
{: #android-network-requests}

**Note:** This code snippet assumes that you have [imported the Client SDKs](#android-import).

```
public void makeGetCall(){
    Thread thread = new Thread(new Runnable() {
        @Override
        public void run() {
            try  {
                Request request = new Request("http://httpbin.org/get", "GET");
                    request.send(null, null);
            } catch (Exception e) {
                // Handle failure here.
            }
        }
    });
    thread.start();
}
```
{: codeblock}

-->

<!-- 
#### Swift 3.0
{: #ios-network-requests}

 ```Swift
 	// Make a network request
	let customResourceURL = "<your resource URL>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
   	if error == nil {
       	    print ("response:\(response?.responseText), no error")
    	  } else {
       	    print ("error: \(error)")
    	}
	}
	request.send(completionHandler: callBack)
 ```
 {: codeblock}
 
 -->

<!-- Commenting out bmsurlsession
```
// Make a network request
let urlSession = BMSURLSession(configuration: .default, delegate: nil, delegateQueue: nil)
var request = URLRequest(url: URL(string: "http://httpbin.org/get")!)
request.httpMethod = "GET"
request.allHTTPHeaderFields = ["foo":"bar"]

urlSession.dataTask(with: request) { (data: Data?, response: URLResponse?, error: Error?) in
    if let httpResponse = response as? HTTPURLResponse {
        logger.info(message: "Status code: \(httpResponse.statusCode)")
    }
    if data != nil, let responseString = String(data: data!, encoding: .utf8) {
        logger.info(message: "Response data: \(responseString)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
}.resume()
```
{: codeblock}
-->

<!--
#### Swift 2.2
{: ios-swift22-network-requests}

```Swift
 	// Make a network request
	let customResourceURL = "<your resource URL>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: NSError?) in
   	if error == nil {
       	    print ("response:\(response?.responseText), no error")
    	  } else {
       	    print ("error: \(error)")
    	}
	}
	request.send(completionHandler: callBack)
 ```
 {: codeblock}
-->
<!--
```
// Make a network request
let urlSession = BMSURLSession(configuration: .defaultSessionConfiguration(), delegate: nil, delegateQueue: nil)
let request = NSMutableURLRequest(URL: NSURL(string: "http://httpbin.org/get")!)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = ["foo":"bar"]

urlSession.dataTaskWithRequest(request) { (data: NSData?, response: NSURLResponse?, error: NSError?) in
    if let httpResponse = response as? NSHTTPURLResponse {
        logger.info(message: "Status code: \(httpResponse.statusCode)")
    }
    if data != nil, let responseString = NSString(data: data!, encoding: NSUTF8StringEncoding) {
        logger.info(message: "Response data: \(responseString)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
}.resume()
```
{: codeblock}
-->
<!--
#### Cordova
{: #cordova-network-requests}

```
var success = function(data){
     console.log("success", data);
 }
 var failure = function(error)
     {console.log("failure", error);
 }
 var request = new BMSRequest("<your application route>", BMSRequest.GET);
 request.send(success, failure);
```
{: codeblock}

-->

## Berichterstellung über Ausfallanalysen
{: #report-crash-analytics}

Sie können [Daten zu Anwendungsausfällen](app-monitoring.html#monitor-app-crash) anzeigen, indem Sie Analyse- und Protokolldaten an {{site.data.keyword.mobileanalytics_short}} senden.

Die Methode `Analytics.send()` füllt die Tabellen für Absturzübersicht und Abstürze auf der Seite für Abstürze. Die Diagramme in diesem Abschnitt werden unter Verwendung der Initialisierung und des Sendevorgangs für Analysedaten aktiviert; eine spezielle Konfiguration ist nicht notwendig.

Die Methode `Logger.send()` füllt die Tabellen für Absturzzusammenfassung und Absturzdetails auf der Seite **Fehlerbehebung**. Zum Füllen der Diagramme in diesem Abschnitt müssen Sie Ihre Anwendung für das Speichern und Senden von Protokollen aktivieren. Dies geschieht durch Hinzufügen einer zusätzlichen Anweisung in Ihrem Anwendungscode:

#### Android
{: #android-crash-statement}

* `Logger.storeLogs(true);`
<!-- * `Logger.setLogLevel(Logger.LEVEL.FATAL); // or greater` -->

Siehe [Beispiel für die Verwendung einer Protokollfunktion](sdk.html#android-logger-sample).

#### iOS
{: #ios-crash-statement}

* `Logger.isLogStorageEnabled = true`
<!-- * `Logger.logLevelFilter = LogLevel.Fatal // or greater` -->

Siehe [Beispiel für die Verwendung einer Protokollfunktion](sdk.html##ios-logger-sample-swift2).

#### Cordova
{: #cordova-crash-statement}

* `BMSLogger.storeLogs(true);`
<!-- * `Logger.logLevelFilter = LogLevel.Fatal // or greater` -->

Siehe [Beispiel für die Verwendung einer Protokollfunktion](sdk.html##ios-logger-sample-swift2).


## Aktive Benutzer verfolgen
{: #trackingusers}

Wenn Ihre Anwendung eindeutige Benutzer für ein Gerät erkennen kann, können Sie optional verfolgen, wie viele Benutzer die Anwendung aktiv nutzen, indem Sie den Benutzernamen des aktiven Benutzers an {{site.data.keyword.mobileanalytics_short}} übergeben. 

Aktivieren Sie die Benutzerverfolgung, indem Sie {{site.data.keyword.mobileanalytics_short}} mit `hasUserContext=true` initialisieren. Andernfalls erfasst {{site.data.keyword.mobileanalytics_short}} nur einen Benutzer pro Gerät. 
#### Android
{: #android-tracking-users}

Fügen Sie den folgenden Code hinzu, um zu verfolgen, wann sich der Benutzer anmeldet:

```
Analytics.setUserIdentity("username");
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

Fügen Sie den folgenden Code hinzu, um zu verfolgen, wann sich der Benutzer anmeldet:

```
Analytics.userIdentity = "username"
```
{: codeblock}

<!--
Add the following code for when the user logs out:

```
Analytics.userIdentity = nil
```
{: codeblock}
-->

#### Cordova
{: #cordova-tracking-users}

Fügen Sie den folgenden Code hinzu, um zu verfolgen, wann sich der Benutzer anmeldet:

```
BMSAnalytics.setUserIdentity("username");
```
{: codeblock}


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

## Nächste Schritte
{: #what-to-do-next}

Wechseln Sie jetzt zur {{site.data.keyword.mobileanalytics_short}}-Konsole, um die Nutzungsanalysedaten, z. B. neue Geräte und die Gesamtzahl der Geräte, die Ihre Anwendung nutzen, anzuzeigen. Sie können Ihre Anwendung auch überwachen, indem Sie <!--[creating custom charts](app-monitoring.html#custom-charts),-->[Alerts festlegen](app-monitoring.html#alerts) und [App-Abstürze überwachen](app-monitoring.html#monitor-app-crash).

# Zugehörige Links

## API-Referenz
{: #api}
* [REST-API ![Symbol für externen Link](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}(../../icons/launch-glyph.svg "Symbol für externen Link")]
