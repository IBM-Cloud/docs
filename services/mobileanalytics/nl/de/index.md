---

copyright:
  years: 2016
lastupdated: "2016-11-30"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Einführung in {{site.data.keyword.mobileanalytics_short}} (Beta)

{: #gettingstartedtemplate}

{{site.data.keyword.mobileanalytics_full}} liefert Entwicklern, IT-Administratoren und Verantwortlichen Aufschlüsse über Leistung und Nutzungsweise ihrer mobilen Apps. Überwachen Sie damit Leistung und Nutzung aller Ihrer Anwendungen vom Desktop oder Tablet aus. So erkennen Sie schnell Trends und Anomalien, gelangen durch Drilldown zur Problemlösung und lösen Alerts aus, wenn Schlüsselmesswerte kritische Schwellenwerte überschreiten. 
{: shortdesc}

Führen Sie die folgenden Schritte aus, damit der {{site.data.keyword.mobileanalytics_short}}-Service schnell betriebsbereit ist:

1. Nachdem Sie eine Instanz  <!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->des  {{site.data.keyword.mobileanalytics_short}}-Service erstellt haben, können Sie auf die  {{site.data.keyword.mobileanalytics_short}}-Konsole zugreifen, indem Sie auf die entsprechende Kachel im Abschnitt **Services** des {{site.data.keyword.Bluemix}}-Dashboards klicken.

 Der {{site.data.keyword.mobileanalytics_short}}-Service wird mit aktiviertem **Demo-Modus** gestartet. Der Demo-Modus füllt die Diagramme auf den Seiten **APP-DATEN** und **ALERTS**, sodass Sie sehen können, wie Ihre Daten angezeigt werden. Sie können den Demo-Modus abschalten, wenn Sie über eigene Daten verfügen. Die {{site.data.keyword.mobileanalytics_short}}-Konsole ist im Demo-Modus schreibgeschützt, weshalb Sie keine neuen Alertdefinitionen erstellen können.

2. Installieren Sie die {{site.data.keyword.mobileanalytics_short}} [Client-SDKs](/docs/services/mobileanalytics/install-client-sdk.html). Optional können Sie die {{site.data.keyword.mobileanalytics_short}}-[REST-API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window} verwenden.

3. Importieren Sie die Client-SDKs und initialisieren Sie sie mit dem folgenden Codeausschnitt, um die Nutzungsanalysedaten aufzuzeichnen:

	#### Android
	{: #android-import}

	Fügen Sie die folgenden `import`-Anweisungen am Anfang Ihrer Projektdatei ein:
	
    ```
    import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
    ```
    {: codeblock}
  
 #### iOS
 {: #ios-import}
	
 **Hinweis:** Das Swift-SDK ist für iOS und WatchOS verfügbar.
	
 Importieren Sie die Frameworks `BMSCore` und `BMSAnalytics` durch Hinzufügen der folgenden `import`-Anweisungen am Anfang der Projektdatei `AppDelegate.swift`:

   ```Swift
  import BMSCore
  import BMSAnalytics
   ```
   {: codeblock}  
   
 #### Cordova
 {: #cordova-import}
		
 Fügen Sie das Cordova-Plug-in hinzu, indem Sie den folgenden Befehl im Stammverzeichnis der Cordova-Anwendung ausführen:

 ```Javascript
 cordova plugin add bms-core
 ```
 {: codeblock}  

4. Initialisieren Sie das {{site.data.keyword.mobileanalytics_short}}-Client-SDK in Ihrem Anwendungscode, um Nutzungsanalysedaten und Anwendungssitzungen aufzuzeichnen. Verwenden Sie hierzu Ihren [API-Schlüsselwert](/docs/services/mobileanalytics/sdk.html#analytics-clientkey).	
	
 #### Android
 {: #android-initialize}	

  ```
  BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // Sie können die Region ändern
  Analytics.init(getApplication(), "your_app_name_here", "your_api_key_here", hasUserContext, Analytics.DeviceEvent.ALL);
  ```
  {: codeblock}
    
 Der Parameter **bluemixRegion** gibt an, welche {{site.data.keyword.Bluemix_notm}}-Bereitstellung Sie verwenden, z. B. `BMSClient.REGION_US_SOUTH` und `BMSClient.REGION_UK`. 
    <!-- , or `BMSClient.Region.Sydney`.-->

 #### iOS
 {: #ios-initialize}
  
  Initialisieren Sie das Client-SDK im Anwendungscode, um Nutzungsanalysedaten und Anwendungssitzungen aufzuzeichnen. Verwenden Sie hierzu Ihren [API-Schlüsselwert](/docs/services/mobileanalytics/sdk.html#analytics-clientkey).
	
  ```Swift
		BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Sie können die Region ändern
		Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: deviceEvents: .lifecycle, .network)
  ```
  {: codeblock}
			
   Der Parameter **bluemixRegion** gibt an, welche Bluemix-Bereitstellung Sie verwenden, zum Beispiel `BMSClient.Region.usSouth` oder `BMSClient.Region.unitedKingdom`.
	<!-- , or `BMSClient.REGION_SYDNEY`. -->
	
 #### Cordova
 {: #cordova-initialize}
	
 Initialisieren Sie das Client-SDK im Anwendungscode, um Nutzungsanalysedaten und Anwendungssitzungen aufzuzeichnen. Verwenden Sie hierzu Ihren [API-Schlüsselwert](/docs/services/mobileanalytics/sdk.html#analytics-clientkey).
	
  ```
  var appName = "your_app_name_here";
  var apiKey = "your_api_key_here";
	
  BMSClient.initialize(BMSClient.REGION_US_SOUTH); // Sie können die Region ändern
  BMSAnalytics.initialize(appName, apiKey, false, [BMSAnalytics.ALL])
  ```
  {: codeblock}
  
  Der Parameter **bluemixRegion** gibt an, welche {{site.data.keyword.Bluemix_notm}}-Bereitstellung Sie verwenden, z. B. `BMSClient.REGION_US_SOUTH` und `BMSClient.REGION_UK`.
  
 **Anmerkung:** Der Name, den Sie für Ihre Anwendung auswählen (`your_app_name_here`), wird in der {{site.data.keyword.mobileanalytics_short}}-Konsole als Anwendungsname angezeigt. Der Anwendungsname wird als Filter für die Suche nach Anwendungsprotokollen im Dashboard verwendet. Wenn Sie plattformübergreifend (zum Beispiel für Android und iOS) denselben Anwendungsnamen verwenden, können Sie unter einem Namen unabhängig von der Plattform, von der die Protokolle stammen, alle Protokolle zu dieser Anwendung anzeigen.

5. Senden Sie die aufgezeichneten Nutzungsanalysedaten an den Mobile Analytics-Service. Eine einfache Möglichkeit zum Testen der Analyse ist das Ausführen des folgenden Codes, wenn die Anwendung gestartet wird:

	#### Android
	{: #android-send}

	Verwenden Sie die Methode `Analytics.send()` zum Senden von Analysedaten an den Server. Sie können die Methode `Analytics.send()` an beliebiger Position in der Methode `onCreate` der Hauptaktivität in Ihrer Android-Anwendung oder an einer Position anordnen, die für Ihr Projekt am besten geeignet ist. 
	
	`Analytics.send()` kann an beliebiger Position eingefügt werden.

	```
	Analytics.send();
	```
	{: codeblock}

	#### iOS
	{: #ios-send}

	Verwenden Sie die Methode `Analytics.send` zum Senden der Analysedaten an den Server. Sie können die Methode `Analytics.send` an beliebiger Position in der Methode `application(_:didFinishLaunchingWithOptions:)` Ihres Anwendungsdelegierten oder an einer Position anordnen, die für Ihr Projekt am besten geeignet ist. 

	```
	Analytics.send()
	```
	{: codeblock}
	
	#### Cordova
	{: #cordova-send}
	
	Verwenden Sie die Methode `BMSAnalytics.send` zum Senden der Analysedaten an den Server. Legen Sie die Methode `BMSAnalytics.send` an einer Position ab, die sich am besten für Ihr Projekt eignet.
	
	```
	BMSAnalytics.send
	```
	{: codeblock}
	
	Lesen Sie den Abschnitt [Anwendung instrumentieren](/docs/services/mobileanalytics/sdk.html), um mehr über zusätzliche {{site.data.keyword.mobileanalytics_short}}-Funktionen, wie [Protokollierung](/docs/services/mobileanalytics/sdk.html#app-monitoring-logger), [Netzanforderungen](/docs/services/mobileanalytics/sdk.html#network-requests) und [Absturzanalysen](/docs/services/mobileanalytics/sdk.html#report-crash-analytics), zu erfahren.
	
6. Kompilieren Sie die Anwendung und führen Sie sie im Emulator oder einem Gerät aus.

7. Wechseln Sie zur {{site.data.keyword.mobileanalytics_short}}-Konsole, um die Nutzungsanalysedaten für Ihre Anwendung anzuzeigen. Sie können Ihre Anwendung auch überwachen, indem Sie <!--[creating custom charts](app-monitoring.html#custom-charts),-->[Alerts festlegen](/docs/services/mobileanalytics/app-monitoring.html#alerts) und [App-Abstürze überwachen](/docs/services/mobileanalytics/app-monitoring.html#monitor-app-crash).


# Zugehörige Links

## SDK
* [Android-SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS-SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
* [Kern-SDK des Cordova-Plug-ins](https://www.npmjs.com/package/bms-core){: new_window}

## API-Referenz
{: #api}
* [REST-API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
