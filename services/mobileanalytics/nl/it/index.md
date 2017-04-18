---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introduzione a {{site.data.keyword.mobileanalytics_short}}

{: #gettingstartedtemplate}

{{site.data.keyword.mobileanalytics_full}} fornisce agli sviluppatori, agli amministratori IT e alle parti interessate di business informazioni approfondite su come stanno venendo eseguite le loro applicazioni e su come stanno venendo utilizzate. {{site.data.keyword.mobileanalytics_short}} ti consente di:

* Monitora le prestazioni e l'utilizzo di tutte le tue applicazioni dal tuo desktop o tablet.  
* Identifica velocemente gli andamenti e le anomalie, esegue il drilldown per risolvere i problemi e attiva gli avvisi quando le metriche chiave superano le soglie critiche.
{: shortdesc}

**Importante:** la console {{site.data.keyword.mobileanalytics_short}} non è ancora pronta per l'utilizzo con il browser
Internet Explorer e alcune funzionalità potrebbero non funzionare correttamente. Utilizzare Firefox, Chrome o Safari.

Per essere operativi rapidamente con il servizio {{site.data.keyword.mobileanalytics_short}}, utilizza la seguente procedura:

1. Dopo che hai creato un'istanza <!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->del servizio {{site.data.keyword.mobileanalytics_short}}, puoi accedere alla console {{site.data.keyword.mobileanalytics_short}} facendo clic sul tuo tile nella sezione **Servizi** del dashboard {{site.data.keyword.Bluemix}}.

 Per aiutarti nell'entrare in confidenza rapidamente con le varie viste e grafici e il valore che visualizzano, ti forniamo un'opzione
**modalità demo** nella console {{site.data.keyword.mobileanalytics_short}}, in cui le viste e i grafici visualizzano
i *dati demo*. I dati demo sono la modalità predefinita della console all'avvio iniziale dopo aver istanziato il servizio. Quando disponi delle tue proprie applicazioni e i
dati di analisi hanno popolato il servizio, puoi *disattivare* la modalità demo per visualizzare i dati della tua applicazione
in grafici diversi. La console Mobile Analytics è in sola lettura nella modalità demo, quindi non sarai in grado di creare nuove definizioni dell'avviso.

2. Installa gli [SDK client](/docs/services/mobileanalytics/install-client-sdk.html) {{site.data.keyword.mobileanalytics_short}}. Puoi facoltativamente utilizzare
{{site.data.keyword.mobileanalytics_short}} l'API REST [
![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/ "icona link esterno"){:new_window}.

3. Importa gli SDK client e inizializzali con il seguente frammento di codice per registrare l'analisi dell'utilizzo:

	#### Android
	{: #android-import}

	Aggiungi le seguenti istruzioni `import` all'inizio del tuo file del progetto:
	
    ```
import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
  ```
    {: codeblock}
  
 #### iOS
 {: #ios-import}
	
 **Nota:** l'SDK Swift è disponibile per iOS e watchOS.
	
 Importa i framework `BMSCore` e `BMSAnalytics` aggiungendo le seguenti istruzioni `import` all'inizio del tuo file di progetto `AppDelegate.swift`: 

   ```Swift
  import BMSCore
  import BMSAnalytics
  ```
   {: codeblock}  
   
 #### Cordova
 {: #cordova-import}
		
 Aggiungi il plugin Cordova eseguendo il seguente comando dalla directory root della tua applicazione Cordova:

 ```Javascript
 cordova plugin add bms-core
 ```
 {: codeblock}  

4. Inizializza l'SDK client {{site.data.keyword.mobileanalytics_short}} nel tuo codice dell'applicazione per registrare l'analisi dell'utilizzo e le sessioni dell'applicazione, utilizzando il tuo valore [Chiave API](/docs/services/mobileanalytics/sdk.html#analytics-clientkey).	
	
 #### Android
 {: #android-initialize}	

  ```
  BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // Puoi modificare la regione
  Analytics.init(getApplication(), "your_app_name_here", "your_api_key_here", hasUserContext, Analytics.DeviceEvent.ALL);
  ```
  {: codeblock}
    
 Il parametro **bluemixRegion** specifica quale distribuzione {{site.data.keyword.Bluemix_notm}} stai utilizzando, ad esempio `BMSClient.REGION_US_SOUTH` e `BMSClient.REGION_UK`. 
    <!-- , or `BMSClient.Region.Sydney`.-->
    
 Imposta il valore per `hasUserContext` su **true** o **false**. Se false (valore predefinito), ogni dispositivo viene calcolato come un utente attivo. 

 #### iOS
 {: #ios-initialize}
  
  Inizializza l'SDK client all'interno del tuo codice dell'applicazione per registrare l'analisi dell'utilizzo e le sessioni dell'applicazione, utilizzando il tuo valore [Chiave API](/docs/services/mobileanalytics/sdk.html#analytics-clientkey).
	
  ```Swift
		BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Puoi modificare la regione
		Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: deviceEvents: .lifecycle, .network)
		```
  {: codeblock}
			
   Il parametro **bluemixRegion** specifica quale distribuzione Bluemix stai utilizzando, ad esempio, `BMSClient.Region.usSouth` o `BMSClient.Region.unitedKingdom`.
	<!-- , or `BMSClient.REGION_SYDNEY`. -->
 
 Imposta il valore per `hasUserContext` su **true** o **false**. Se false (valore predefinito), ogni dispositivo viene calcolato come un utente attivo. 
	
 #### Cordova
 {: #cordova-initialize}
	
 Inizializza l'SDK client all'interno del tuo codice dell'applicazione per registrare l'analisi dell'utilizzo e le sessioni dell'applicazione, utilizzando il tuo valore [Chiave API](/docs/services/mobileanalytics/sdk.html#analytics-clientkey).
	
  ```
  var appName = "your_app_name_here";
  var apiKey = "your_api_key_here";
	
  BMSClient.initialize(BMSClient.REGION_US_SOUTH); // Puoi modificare la regione
  BMSAnalytics.initialize(appName, apiKey, false, [BMSAnalytics.ALL])
  ```
  {: codeblock}
  
  Il parametro **bluemixRegion** specifica quale distribuzione {{site.data.keyword.Bluemix_notm}} stai utilizzando, ad esempio `BMSClient.REGION_US_SOUTH` e `BMSClient.REGION_UK`.
  
 **Nota:** il nome che hai selezionato per la tua applicazione (`your_app_name_here`) visualizza la console {{site.data.keyword.mobileanalytics_short}} come il nome dell'applicazione. Il nome applicazione viene utilizzato come un filtro per cercare i log applicazione nel dashboard Quando utilizzi lo stesso nome applicazione su diverse piattaforme (ad esempio Android e iOS), puoi visualizzare tutti i log da tale applicazione sotto lo stesso nome, indipendentemente da quale sia la piattaforma dalla quale i log erano stati inviati.

5. Invia l'analisi di utilizzo registrata al servizio Mobile Analytics. Un modo semplice per verificare la tua analisi consiste nell'eseguire il seguente codice quando viene avviata la tua applicazione:

	#### Android
	{: #android-send}

	Utilizza il metodo `Analytics.send()` per inviare i dati di analisi al server. Puoi inserire il metodo `Analytics.send()` ovunque nel metodo `onCreate` dell'attività principale nella tua applicazione Android o nell'ubicazione che ritieni più indicata per il tuo progetto. 
	
	Puoi inserire `Analytics.send()` ovunque.

	```
	Analytics.send();
	```
	{: codeblock}

	#### iOS
	{: #ios-send}

	Utilizza il metodo `Analytics.send` per inviare i dati di analisi al server. Puoi inserire il metodo `Analytics.send` ovunque nel metodo `application(_:didFinishLaunchingWithOptions:)` del delegato della tua applicazione oppure in un'ubicazione che ritieni più adatta per il tuo progetto. 

	```
	Analytics.send()
	```
	{: codeblock}
	
	#### Cordova
	{: #cordova-send}
	
	Utilizza il metodo `BMSAnalytics.send` per inviare i dati di analisi al server. Inserisci il metodo `BMSAnalytics.send` in un'ubicazione che ritieni più adatta per il tuo progetto.
	
	```
	BMSAnalytics.send()
	```
	{: codeblock}
	
	Leggi l'argomento [Strumentazione della tua applicazione](/docs/services/mobileanalytics/sdk.html) per ulteriori informazioni sulle funzionalità {{site.data.keyword.mobileanalytics_short}}, come ad esempio [registrazione](/docs/services/mobileanalytics/sdk.html#app-monitoring-logger), [richieste di rete](/docs/services/mobileanalytics/sdk.html#network-requests) e [analisi degli arresti anomali](/docs/services/mobileanalytics/sdk.html#report-crash-analytics).
	
6. Compila ed esegui l'applicazione sul tuo emulatore o sul tuo dispositivo.

7. Vai alla Console {{site.data.keyword.mobileanalytics_short}} per visualizzare l'utilizzo delle analisi per la tua applicazione. Puoi anche monitorare l'applicazione <!--[creating custom charts](app-monitoring.html#custom-charts),-->[impostando gli avvisi](/docs/services/mobileanalytics/app-monitoring.html#alerts) e [monitorando gli arresti anomali delle applicazioni](/docs/services/mobileanalytics/app-monitoring.html#monitor-app-crash).


# rellinks

## SDK
* [Android SDK ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics "icona link esterno"){: new_window}  
* [iOS SDK ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics "icona link esterno"){: new_window}
* [Cordova Plugin Core SDK ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://www.npmjs.com/package/bms-core "icona link esterno"){: new_window}

## Riferimento API
{: #api}
* [REST API ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/ "icona link esterno"){:new_window}
