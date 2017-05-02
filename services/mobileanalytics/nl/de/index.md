---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-20"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Einführung in {{site.data.keyword.mobileanalytics_short}}

{: #gettingstartedtemplate}

{{site.data.keyword.mobileanalytics_full}} liefert Entwicklern, IT-Administratoren und Verantwortlichen Aufschlüsse über Leistung und Nutzungsweise ihrer mobilen Apps. Mit {{site.data.keyword.mobileanalytics_short}} haben Sie die folgenden Möglichkeiten:

* Überwachen Sie damit Leistung und Nutzung aller Ihrer Anwendungen vom Desktop oder Tablet aus. 
* So erkennen Sie schnell Trends und Anomalien, gelangen durch Drilldown zur Problemlösung und lösen Alerts aus, wenn Schlüsselmesswerte kritische Schwellenwerte überschreiten. 
{: shortdesc}

Führen Sie die folgenden Schritte aus, um den {{site.data.keyword.mobileanalytics_short}}-Service ohne zeitliche Verzögerung betriebsbereit zu machen:

1. Nachdem Sie eine Instanz <!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->des {{site.data.keyword.mobileanalytics_short}}-Service erstellt haben, können Sie auf die {{site.data.keyword.mobileanalytics_short}}-Konsole zugreifen, indem Sie auf die entsprechende Kachel im Abschnitt **Services** des {{site.data.keyword.Bluemix}}-Dashboards klicken.

 Damit Sie ein Gefühl für die unterschiedlichen Ansichten und Diagramme und deren Nutzen bekommen, stellen wir in der {{site.data.keyword.mobileanalytics_short}}-Konsole eine Demomodusoption bereit, mit der in den Ansichten und Diagrammen *Demodaten* zu sehen sind. Der Demo-Modus ist der Standardmodus der Konsole bei deren erstem Start nachdem der Service instanziiert wurde. Wenn Sie den Service mit Ihren eigenen Anwendungen und Analysedaten gefüllt haben, können Sie den Demomodus *inaktivieren* und die Daten Ihrer Anwendungen in den anderen Diagrammen anzeigen. Die {{site.data.keyword.mobileanalytics_short}}-Konsole ist im Demo-Modus schreibgeschützt, weshalb Sie keine neuen Alertdefinitionen erstellen können.

2. Installieren Sie die {{site.data.keyword.mobileanalytics_short}} [Client-SDKs](/docs/services/mobileanalytics/install-client-sdk.html). Sie können optional die [REST-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window} von {{site.data.keyword.mobileanalytics_short}} verwenden.

3. Importieren Sie die Client-SDKs und initialisieren Sie sie mit dem folgenden Codeausschnitt, um die Nutzungsanalysedaten aufzuzeichnen:

	## Android
	{: #android-import notoc}

	Fügen Sie die folgenden `import`-Anweisungen am Anfang Ihrer Projektdatei ein:
	
    ```
    import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
    ```
	{: codeblock}

	## iOS
	{: #ios-import notoc}
	
	**Hinweis:** Das Swift-SDK ist für iOS und WatchOS verfügbar.
	
	Importieren Sie die Frameworks `BMSCore` und `BMSAnalytics` durch Hinzufügen der folgenden `import`-Anweisungen am Anfang der Projektdatei `AppDelegate.swift`:

	```Swift
	import BMSCore
	import BMSAnalytics
	```
	{: codeblock}
   
	## Cordova
	{: #cordova-import notoc}
		
	Fügen Sie das Cordova-Plug-in hinzu, indem Sie den folgenden Befehl im Stammverzeichnis der Cordova-Anwendung ausführen:

	```Javascript
	cordova plugin add bms-core
	```
	{: codeblock}  

4. Initialisieren Sie das {{site.data.keyword.mobileanalytics_short}}-Client-SDK in Ihrem Anwendungscode, um Nutzungsanalysedaten und Anwendungssitzungen aufzuzeichnen. Verwenden Sie hierzu Ihren [API-Schlüsselwert](/docs/services/mobileanalytics/sdk.html#analytics-clientkey).	
	
	## Android
	{: #android-initialize notoc}	

	```
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // Sie können die Region ändern
  Analytics.init(getApplication(), "your_app_name_here", "your_api_key_here", hasUserContext, Analytics.DeviceEvent.ALL);
	```
	{: codeblock}
    
	Der Parameter **bluemixRegion** gibt an, welche {{site.data.keyword.Bluemix_notm}}-Bereitstellung Sie verwenden, z. B. `BMSClient.REGION_US_SOUTH` und `BMSClient.REGION_UK`. 
    <!-- , or `BMSClient.Region.Sydney`.-->
    
	Setzen Sie den Wert für `hasUserContext` auf **true** oder **false**. Bei 'false' (Standardwert) wird jedes Gerät als aktiver Benutzer gezählt.

	## iOS
	{: #ios-initialize notoc}
  
	Initialisieren Sie das Client-SDK im Anwendungscode, um Nutzungsanalysedaten und Anwendungssitzungen aufzuzeichnen. Verwenden Sie hierzu Ihren [API-Schlüsselwert](/docs/services/mobileanalytics/sdk.html#analytics-clientkey).
	
	```Swift
		BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Sie können die Region ändern
		Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: deviceEvents: .lifecycle, .network)
	```
	{: codeblock}
			
	Der Parameter **bluemixRegion** gibt an, welche Bluemix-Bereitstellung Sie verwenden, zum Beispiel `BMSClient.Region.usSouth` oder `BMSClient.Region.unitedKingdom`.
	<!-- , or `BMSClient.REGION_SYDNEY`. -->
 
	Setzen Sie den Wert für `hasUserContext` auf **true** oder **false**. Bei 'false' (Standardwert) wird jedes Gerät als aktiver Benutzer gezählt.
	
	## Cordova
	{: #cordova-initialize notoc}
	
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

5. Senden Sie die aufgezeichneten Nutzungsanalysedaten an den {{site.data.keyword.mobileanalytics_short}}-Service. Eine einfache Möglichkeit zum Testen der Analyse ist das Ausführen des folgenden Codes, wenn die Anwendung gestartet wird:

	## Android
	{: #android-send notoc}

	Verwenden Sie die Methode `Analytics.send()` zum Senden von Analysedaten an den Server. Sie können die Methode `Analytics.send()` an beliebiger Position in der Methode `onCreate` der Hauptaktivität in Ihrer Android-Anwendung oder an einer Position anordnen, die für Ihr Projekt am besten geeignet ist. 
	
	`Analytics.send()` kann an beliebiger Position eingefügt werden.

	```
	Analytics.send();
	```
	{: codeblock}

	## iOS
	{: #ios-send notoc}

	Verwenden Sie die Methode `Analytics.send` zum Senden der Analysedaten an den Server. Sie können die Methode `Analytics.send` an beliebiger Position in der Methode `application(_:didFinishLaunchingWithOptions:)` Ihres Anwendungsdelegierten oder an einer Position anordnen, die für Ihr Projekt am besten geeignet ist. 

	```
	Analytics.send()
	```
	{: codeblock}
	
	## Cordova
	{: #cordova-send notoc}
	
	Verwenden Sie die Methode `BMSAnalytics.send` zum Senden der Analysedaten an den Server. Legen Sie die Methode `BMSAnalytics.send` an einer Position ab, die sich am besten für Ihr Projekt eignet.
	
	```
	BMSAnalytics.send()
	```
	{: codeblock}
	
	Lesen Sie den Abschnitt [Anwendung instrumentieren](/docs/services/mobileanalytics/sdk.html), um mehr über zusätzliche {{site.data.keyword.mobileanalytics_short}}-Funktionen, wie [Protokollierung](/docs/services/mobileanalytics/sdk.html#app-monitoring-logger), [Netzanforderungen](/docs/services/mobileanalytics/sdk.html#network-requests) und [Absturzanalysen](/docs/services/mobileanalytics/sdk.html#report-crash-analytics), zu erfahren.
	
6. Kompilieren Sie die Anwendung und führen Sie sie im Emulator oder einem Gerät aus.

7. Wechseln Sie zur {{site.data.keyword.mobileanalytics_short}}-Konsole, um die Nutzungsanalysedaten für Ihre Anwendung anzuzeigen. Sie können Ihre Anwendung auch überwachen, indem Sie <!--[creating custom charts](app-monitoring.html#custom-charts),-->[Alerts festlegen](/docs/services/mobileanalytics/app-monitoring.html#alerts) und [App-Abstürze überwachen](/docs/services/mobileanalytics/app-monitoring.html#monitor-app-crash).


# Zugehörige Links
{: #rellinks notoc}

## SDK
{: #sdk notoc}
* [Android-SDK ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS-SDK ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
* [Cordova-Plug-in-Core-SDK ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.npmjs.com/package/bms-core){: new_window}

## API-Referenz
{: #api notoc}
* [REST-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
