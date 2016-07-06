---

copyright:
  years: 2015, 2016

---

# Anwendung zur Verwendung der Client-SDKs von {{site.data.keyword.mobileanalytics_short}} instrumentieren
{: #mobileanalytics_sdk}
*Letzte Aktualisierung: 27. April 2016*
{: .last-updated}

Mit den {{site.data.keyword.mobileanalytics_full}}-SDKs können Sie die mobile Anwendung instrumentieren.
{: shortdesc}

{{site.data.keyword.mobileanalytics_short}} ermöglicht das Erfassen von drei Datenkategorien, von denen für jede ein unterschiedlicher Umfang an Instrumentierung erforderlich ist:

1.  Vordefinierte Daten - Diese Kategorie umfasst Informationen zur allgemeinen Nutzung und zum Gerät, die auf alle Apps angewendet werden. Die Daten in dieser Kategorie werden in Gerätemetadaten (Betriebssystem und Gerätemodell) und Nutzungsdaten (aktive Benutzer und App-Sitzungen) unterteilt, aus denen Ausmaß, Häufigkeit und Dauer der App-Nutzung hervorgehen. Vordefinierte Daten werden nach der Initialisierung des {{site.data.keyword.mobileanalytics_short}}-SDKs in der App automatisch erfasst.
2. Benutzerdefinierte Ereignisse - Diese Kategorie umfasst Daten, die Sie selbst definieren und die für die App spezifisch sind. Diese Daten stellen Ereignisse dar, die in der App auftreten, zum Beispiel Seitenansichten, das Antippen von Schaltflächen oder In-App-Käufe. Zusätzlich zum Initialisieren des {{site.data.keyword.mobileanalytics_short}}-SDKs in der App müssen Sie eine Codezeile für jedes benutzerdefinierte Ereignis hinzufügen, das Sie verfolgen möchten.
3. Clientprotokollnachrichten - Diese Kategorie ermöglicht dem Entwickler das Hinzufügen von Codezeilen in der App, von denen benutzerdefinierte Nachrichten zur Erleichterung der Entwicklung und Fehlerbehebung protokolliert werden. Der Entwickler weist jeder Protokollnachricht eine Ebene für den Schweregrad bzw. die Ausführlichkeit zu und kann die Nachrichten danach anhand der zugewiesenen Ebene filtern; alternativ kann er konfigurieren, dass Nachrichten unter einer bestimmten Protokollebene ignoriert werden sollen, um Speicherplatz zu sparen. Wenn Sie Clientprotokolldaten erfassen möchten, müssen Sie das {{site.data.keyword.mobileanalytics_short}}-SDK mit der App initialisieren und eine Codezeile für jede Protokollnachricht hinzufügen.

Derzeit sind SDKs für Android, iOS und WatchOS verfügbar.

## Wert für Clientschlüssel angeben
{: #analytics-clientkey}

Geben Sie einen Wert für den **Clientschlüssel** an, bevor Sie das Client-SDK konfigurieren. Der Clientschlüssel ist für die Initialisierung des Client-SDKs erforderlich.
1. Öffnen Sie das Dashboard für den {{site.data.keyword.mobileanalytics_short}}-Service.
2. Klicken Sie in der Registerkarte für die API-Schlüssel auf das Schraubenschlüsselsymbol.
3. Notieren Sie in der Registerkarte für API-Schlüssel den Wert für den Clientschlüssel.


## Android-App zum Erfassen der Analysedaten initialisieren
{: #initalize-ma-sdk-android}

Initialisieren Sie die Anwendung, damit Protokolle an den {{site.data.keyword.mobileanalytics_short}}-Service gesendet werden können.

1. Importieren Sie das Client-SDK durch Hinzufügen der folgenden `import`-Anweisung ganz oben in der Projektdatei:

  ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
  ```
  {: codeblock}

2. Initialisieren Sie das {{site.data.keyword.mobileanalytics_short}}-Client-SDK in der Android-Anwendung durch Hinzufügen des Initialisierungscodes in der Methode `onCreate` der Hauptaktivität in der Android-Anwendung oder an einer Position, die sich für das Projekt am besten eignet.

	```Java
	try {
            BMSClient.getInstance().initialize(this.getApplicationContext(), "", "", BMSClient.REGION_US_SOUTH);
// Sicherstellen, dass auf eigene Region verwiesen wird
        } catch (MalformedURLException e) {
            Log.e(your_app_name,"URL should not be malformed:  " + e.getLocalizedMessage());
        } 
  ```
  {: codeblock}

  Zum Verwenden des {{site.data.keyword.mobileanalytics_short}}-Client-SDKs müssen Sie `BMSClient` mit dem Parameter **bluemixRegion** initialisieren. Im Initialisierungsoperator gibt der Wert für **bluemixRegion** an, welche {{site.data.keyword.Bluemix_notm}}-Bereitstellung verwendet wird, zum Beispiel `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` oder `BMSClient.REGION_SYDNEY`.
  <!-- Set this value with a `BMSClient.REGION` static property. -->

  <!--You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. Initialisieren Sie Analytics mithilfe des Android-Anwendungsobjekts und legen Sie dafür den Namen der Anwendung fest. Außerdem benötigen Sie den Wert für den [**Clientschlüssel**](#analytics-clientkey).
	
	```Java
	Analytics.init(getApplication(), "my_app", apiKey, Analytics.DeviceEvent.LIFECYCLE);
	// In diesem Codebeispiel ist Analytics zum Aufzeichnen von Lebenszyklusereignissen konfiguriert.
	```
  {: codeblock}

	**Tipp:** Der Anwendungsname wird als Filter für die Suche nach Clientprotokollen im Dashboard verwendet. Wenn Sie plattformübergreifend (zum Beispiel für Android und iOS) denselben Anwendungsnamen verwenden, können Sie unter einem Namen unabhängig von der Plattform, von der die Protokolle stammen, alle Protokolle zu dieser Anwendung anzeigen.

## iOS-App zum Erfassen der Analysedaten initialisieren
{: #init-ma-sdk-ios}

Initialisieren Sie die Anwendung, damit Protokolle an den {{site.data.keyword.mobileanalytics_short}}-Service gesendet werden können. Das Swift-SDK ist für iOS und WatchOS verfügbar.

1. Importieren Sie die Frameworks `BMSCore` und `BMSAnalytics` durch Hinzufügen der folgenden `import`-Anweisungen ganz oben in der Projektdatei `AppDelegate.swift`:

  ```Swift
  import BMSCore
  import BMSAnalytics
  ```
  {: screen}

2. Wenn Sie das {{site.data.keyword.mobileanalytics_short}}-Client-SDK verwenden möchten, müssen Sie zuerst die Klasse `BMSClient` mit dem folgenden Code initialisieren.

  Versetzen Sie den Initialisierungscode in die Methode `application(_:didFinishLaunchingWithOptions:)` des Anwendungsdelegierten oder an eine Position, die sich für das Projekt am besten eignet.

    ```Swift
    BMSClient.sharedInstance.initializeWithBluemixAppRoute(nil, bluemixAppGUID: nil, bluemixRegion: BMSClient.REGION_US_SOUTH)`
    ```
    {: codeblock}

    Zum Verwenden des {{site.data.keyword.mobileanalytics_short}}-Client-SDKs müssen Sie `BMSClient` mit dem Parameter **bluemixRegion** initialisieren. Im Initialisierungsoperator gibt der Wert für **bluemixRegion** an, welche {{site.data.keyword.Bluemix_notm}}-Bereitstellung verwendet wird, zum Beispiel `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` oder `BMSClient.REGION_SYDNEY`.
   
   <!-- Set this value with a `BMSClient.REGION` static property. -->

   <!-- You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. Initialisieren Sie Analytics durch Festlegen des Namens der mobilen Anwendung. Außerdem benötigen Sie den Wert für den [**Clientschlüssel**](#analytics-clientkey).

  Der Anwendungsname wird als Filter für die Suche nach Clientprotokollen im {{site.data.keyword.mobileanalytics_short}}-Dashboard verwendet. Wenn Sie plattformübergreifend (zum Beispiel für Android und iOS) denselben Anwendungsnamen verwenden, können Sie unter einem Namen unabhängig von der Plattform, von der die Protokolle stammen, alle Protokolle zu dieser Anwendung anzeigen.

  Mit dem optionalen Parameter `deviceEvents` können automatisch Analysedaten für gerätespezifische Ereignisse erfasst werden.

  ### iOS
    {: #ios-initialize-analytics}

      ```
      Analytics.initializeWithAppName("AppName", apiKey: your_client_key,
      deviceEvents: DeviceEvent.LIFECYCLE)
      ```

  ### WatchOS
  {: #watchos-initialize-analytics}

	```
	  Analytics.initializeWithAppName("AppName", apiKey: your_api_key)
	```

  Unter WatchOS können Sie Geräteereignisse mit den Methoden `Analytics.recordApplicationDidBecomeActive()` und `Analytics.recordApplicationWillResignActive()` aufzeichnen.
  
  Fügen Sie die folgende Zeile zur Methode `applicationDidBecomeActive()` der Klasse 'ExtensionDelegate' hinzu.

	```
	Analytics.recordApplicationDidBecomeActive()
	```
  {: codeblock}

  Fügen Sie die folgende Zeile zur Methode 'applicationWillResignActive()' der Klasse 'ExtensionDelegate' hinzu:
	```
	Analytics.recordApplicationWillResignActive()
	```
  {: codeblock}

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
	
Analytics.log(eventJSONObject);
	
// Aufgezeichnete Nutzungsanalysedaten an Mobile Analytics-Service senden
Analytics.send();
```
	
Beispielnutzungsanalysedaten für Protokollierung eines Ereignisses:
	
```
// Protokollierung eines benutzerdefinierten Ereignisses für benutzerdefinierte Diagramme, das von einem JSON-Objekt dargestellt wird:
JSONObject eventJSONObject = new JSONObject();
	
eventJSONObject.put("customProperty" , "propertyValue");
```

#### iOS - Swift
{: #ios-usage-api}

```
// Aufzeichnung der Nutzungsanalysedaten inaktivieren (z. B. zum Sparen von Speicherplatz)
// Aufzeichnung ist standardmäßig aktiviert
Analytics.enabled = false

// Aufzeichnung der Nutzungsanalysedaten aktivieren
Analytics.enabled = true

// Aufgezeichnete Nutzungsanalysedaten an {{site.data.keyword.mobileanalytics_short}}-Service senden
Analytics.send()
```

Beispielnutzungsanalysedaten für Protokollierung eines Ereignisses:

```
// Protokollierung eines benutzerdefinierten Ereignisses für benutzerdefinierte Diagramme
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

  <!--**Note:** Find full Logger API references for each platform at [SDKs, samples, API reference](sdks-samples-apis.html). The Logger API is part of the--> <!--{{site.data.keyword.mobileanalytics_short}} Client SDK Core.-->

  <!--### Cordova-->


  <!--```JavaScript-->

  <!--var logger = MFPLogger.getInstance("myLogger");-->

  <!--logger.debug("debug info");-->
  <!--logger.info("info message");-->
  <!--logger.warn("warning message");-->
  <!--logger.fatal("fatal message");-->

  <!--```-->


### Beispiel für Verwendung der Protokollfunktion
{: #sample-logger-usage}

**Hinweis:** Stellen Sie sicher, dass Sie die App zu Verwendung des [{{site.data.keyword.mobileanalytics_short}}-Client-SDKs](sdk.html) instrumentiert haben, bevor Sie das Protokollierungsframework verwenden.
 
  An den folgenden Codeausschnitten wird die Verwendung der Beispielprotokollfunktion veranschaulicht:

#### Android
{: #android-logger-sample}

```
// Protokollfunktion zum Speichern der Protokolle auf dem Gerät konfigurieren, sodass sie später
// an den {{site.data.keyword.mobileanalytics_short}}-Service gesendet werden können
// Standardmäßig inaktiviert; zum Aktivieren auf true setzen
Logger.storeLogs(true);

// Mindestprotokollierungsebene ändern (optional)
// Die Standardeinstellung ist Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);

// Protokolle an den {{site.data.keyword.mobileanalytics_short}}-Service senden
Logger.send();
```

Szenarios für die Protokollfunktion:

```
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
```

#### iOS - Swift
{: ios-logger-sample}

```
// Protokollfunktion zum Speichern der Protokolle auf dem Gerät konfigurieren, sodass sie später
// an den {{site.data.keyword.mobileanalytics_short}}-Service gesendet werden können
// Standardmäßig inaktiviert; zum Aktivieren auf true setzen
Logger.logStoreEnabled = true

// Mindestprotokollierungsebene ändern (optional)
// Die Standardeinstellung ist LogLevel.Debug
Logger.logLevelFilter = LogLevel.Info

// Protokolle an den {{site.data.keyword.mobileanalytics_short}}-Service senden
Logger.send()
```

Szenarios für die Protokollfunktion:
    
```
// Zwei Instanzen für Protokollfunktion erstellen
// Sie können mehrere Protokollinstanzen zum Organisieren der Protokolle erstellen
let logger1 = Logger.logger(forName: "feature1Logger")
let logger2 = Logger.logger(forName: "feature2Logger")
	
// Protokollnachrichten mit unterschiedlichen Ebenen
logger1.debug("debug message for feature 1") 
// Die Nachricht logger1.debug wird nicht protokolliert, weil für logLevelFilter der Wert Info eingestellt ist
logger2.info("info message for feature 2")
```

**Tipp:** Aus Datenschutzgründen können Sie die Ausgabe der Protokollfunktion für Anwendungen inaktivieren, die im Releasemodus erstellt werden. Von der Protokollfunktionsklasse werden Protokolle standardmäßig in der Xcode-Konsole gedruckt. Fügen Sie in den Erstellungseinstellungen für das Ziel das Flag `-D RELEASE_BUILD` zum Abschnitt mit den weiteren Swift-Flags der Buildkonfiguration des Release hinzu.
    

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

## Aktive Benutzer verfolgen
{: #trackingusers}
Sie können optional verfolgen, wie viele Benutzer die Anwendung aktiv verwenden, indem Sie den Benutzernamen des aktiven Benutzers an {{site.data.keyword.mobileanalytics_short}} übergeben.

#### Android
{: #android-tracking-users}

Fügen Sie den folgenden Code für den Zeitpunkt hinzu, an dem sich der Benutzer anmeldet:

```
Analytics.setUserIdentity("username");
```

Fügen Sie den folgenden Code für den Zeitpunkt hinzu, an dem sich der Benutzer abmeldet:

```
Analytics.clearUserIdentity();
```

#### iOS - Swift
{: #ios-tracking-users}

Fügen Sie den folgenden Code für den Zeitpunkt hinzu, an dem sich der Benutzer anmeldet:

```
Analytics.userIdentity = "username"
```

Fügen Sie den folgenden Code für den Zeitpunkt hinzu, an dem sich der Benutzer abmeldet:

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

# Zugehörige Links

## API-Referenz
{: #api}
* [REST-API](https://mobile-analytics-dashboard.eu-gb.bluemix.net/analytics-service/){:new_window}
