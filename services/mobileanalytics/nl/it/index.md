---

copyright:
  years: 2016
lastupdated: "2016-10-19"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introduzione a {{site.data.keyword.mobileanalytics_short}}
{: #gettingstartedtemplate}


Ultimo aggiornamento: 19 ottobre 2016
{: .last-updated}

{{site.data.keyword.mobileanalytics_full}} fornisce agli sviluppatori, agli amministratori IT e alle parti interessate di business informazioni approfondite su come stanno venendo eseguite le loro applicazioni e su come stanno venendo utilizzate. Monitora le prestazioni e l'utilizzo di tutte le tue applicazioni dal tuo desktop o tablet. Identifica velocemente gli andamenti e le anomalie, esegue il drilldown per risolvere i problemi e attiva gli avvisi quando le metriche chiave superano le soglie critiche. 
{: shortdesc}

Per iniziare a lavorare rapidamente con il servizio {{site.data.keyword.mobileanalytics_short}}, attieniti alla seguente procedura:

1. Dopo che hai creato un'istanza <!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->del servizio {{site.data.keyword.mobileanalytics_short}}, puoi accedere alla console {{site.data.keyword.mobileanalytics_short}} facendo clic sul tuo tile nella sezione **Servizi** del dashboard {{site.data.keyword.Bluemix}}.

 Il servizio {{site.data.keyword.mobileanalytics_short}} viene avviato con la **modalità demo** abilitata. La modalità demo popola i grafici nelle pagine **DATI APPLICAZIONE** e **AVVISI**, in modo che puoi vedere come i tuoi dati saranno visualizzati. Puoi disattivare la modalità demo quando disponi dei tuoi propri dati. La console {{site.data.keyword.mobileanalytics_short}} è in sola lettura nella modalità demo, quindi non sarai in grado di creare nuove definizioni dell'avviso.

2. Installa gli [SDK client](install-client-sdk.html) {{site.data.keyword.mobileanalytics_short}}.Puoi facoltativamente utilizzare l'API REST {{site.data.keyword.mobileanalytics_short}} [](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}.

3. Importa gli SDK client e inizializzali con il seguente frammento di codice per registrare l'analisi dell'utilizzo.

	#### Android
	{: #android-initialize}
	1. Importa l'SDK client:

		```
		import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
		import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
		```
		{: codeblock}
		
	2. Inizializza l'SDK client all'interno del tuo codice dell'applicazione per registrare l'analisi dell'utilizzo e le sessioni dell'applicazione, utilizzando il tuo valore [Chiave API](sdk.html#analytics-clientkey).

		```Java
			BMSClient.getInstance().initialize(this.getApplicationContext(), BMSClient.REGION_US_SOUTH); // Puoi modificare la regione
			
			Analytics.init(getApplication(), "your_app_name_here", "your_api_key_here", hasUserContext, Analytics.DeviceEvent.LIFECYCLE);
		```
		{: codeblock}
		
    Il nome che hai selezionato per la tua applicazione (`your_app_name_here`) visualizza la console {{site.data.keyword.mobileanalytics_short}} come il nome dell'applicazione. Il nome applicazione viene utilizzato come un filtro per cercare i log applicazione nel dashboard Quando utilizzi lo stesso nome applicazione su diverse piattaforme (ad esempio Android e iOS), puoi visualizzare tutti i log da tale applicazione sotto lo stesso nome, indipendentemente da quale sia la piattaforma dalla quale i log erano stati inviati.
    
    Il parametro **bluemixRegion** specifica quale distribuzione {{site.data.keyword.Bluemix_notm}} stai utilizzando, ad esempio `BMSClient.REGION_US_SOUTH` e `BMSClient.REGION_UK`. 
    <!-- , or `BMSClient.REGION_SYDNEY`.-->
    
    **Nota:** imposta il valore per `hasUserContext` su **true** o **false**. Se false (valore predefinito), ogni dispositivo viene calcolato come un utente attivo. Il metodo [`Analytics.setUserIdentity("username");`](sdk.html#android-tracking-users) non funzionerà quando `hasUserContext` è false. Se true, ogni utilizzo di [`Analytics.setUserIdentity("username");`](sdk.html#android-tracking-users) viene calcolato come un utente attivo. Non esiste un'identità utente predefinita quando `hasUserContext` è true e di conseguenza deve essere impostato per popolare i grafici dell'utente attivo.

  #### iOS
  {: #ios-initialize}
  
  1. Importa i framework `BMSCore` e `BMSAnalytics`:
	```
	import BMSCore
    import BMSAnalytics
	```
	{: codeblock}
    
  2. Inizializza l'SDK client all'interno del tuo codice dell'applicazione per registrare l'analisi dell'utilizzo e le sessioni dell'applicazione, utilizzando il tuo valore [Chiave API](sdk.html#analytics-clientkey).
 
	Swift:
	
	```Swift
	BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Puoi modificare la regione
	Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: DeviceEvent.lifecycle)	
	```
	{: codeblock}
		
	Il nome che hai selezionato per la tua applicazione (`your_app_name_here`) visualizza la console {{site.data.keyword.mobileanalytics_short}} come il nome dell'applicazione. Il nome applicazione viene utilizzato come un filtro per cercare i log applicazione nel dashboard Quando utilizzi lo stesso nome applicazione su diverse piattaforme (ad esempio Android e iOS), puoi visualizzare tutti i log da tale applicazione sotto lo stesso nome, indipendentemente da quale sia la piattaforma dalla quale i log erano stati inviati.
	
	Il parametro **bluemixRegion** specifica quale distribuzione Bluemix stai utilizzando, ad esempio `BMSClient.REGION_US_SOUTH` e `BMSClient.REGION_UK`.
	<!-- , or `BMSClient.REGION_SYDNEY`. -->
	
	**Nota:** imposta il valore per `hasUserContext` su **true** o **false**. Se false (valore predefinito), ogni dispositivo viene calcolato come un utente attivo. Il metodo [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) non funzionerà quando `hasUserContext` è false. Se true, ogni utilizzo di [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) viene calcolato come un utente attivo. Non esiste un'identità utente predefinita quando `hasUserContext` è true e di conseguenza deve essere impostato per popolare i grafici dell'utente attivo.

4. Invia l'analisi di utilizzo registrata al servizio Mobile Analytics. Un modo semplice per verificare la tua analisi consiste nell'eseguire il seguente codice quando viene avviata la tua applicazione:

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

	Leggi l'argomento [Strumentazione della tua applicazione](sdk.html) per ulteriori informazioni sulle funzionalità {{site.data.keyword.mobileanalytics_short}}.
5. Compila ed esegui l'applicazione sul tuo emulatore o sul tuo dispositivo.

6. Vai alla **Console** {{site.data.keyword.mobileanalytics_short}} per visualizzare l'utilizzo delle analisi per la tua applicazione. Puoi anche monitorare l'applicazione <!--[creating custom charts](app-monitoring.html#custom-charts),-->[impostando gli avvisi](app-monitoring.html#alerts) e [monitorando gli arresti anomali delle applicazioni](app-monitoring.html#monitor-app-crash).


# rellinks

## SDK
* [SDK Android](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [SDK iOS](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## Riferimento API
{: #api}
* [API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
