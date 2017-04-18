---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

**Importante: il servizio {{site.data.keyword.amafull}} è stato sostituito con il servizio {{site.data.keyword.appid_full}}.**

# Configurazione del plugin Cordova
{: #getting-started-cordova}

Instrumenta la tua applicazione client Cordova con l'SDK client {{site.data.keyword.amafull}}. Inizializza il gestore autorizzazione nel tuo codice Android (Java) o iOS (Objective C che utilizza l'SDK Swift e il file di intestazione relativo). Inizializza il client ed effettua le richieste per proteggere e annullare la protezione alle risorse da WebView.

{:shortdesc}

## Prima di cominciare
{: #before-you-begin}
È necessario disporre di:

* Un'istanza di un'applicazione  {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni su come creare un'applicazione di back-end {{site.data.keyword.Bluemix_notm}}, vedi [Introduzione](index.html).
* Un'istanza di un servizio {{site.data.keyword.amafull}}.
* L'URL della tua applicazione di back-end (**Rotta applicazione**). Avrai bisogno di questo valore per inviare le richieste agli endpoint protetti della tua applicazione di back-end.
* Il tuo valore **TenantID**. Apri il tuo servizio nel dashboard {{site.data.keyword.amashort}}. Fai clic sul pulsante **Opzioni per dispositivi mobili**. Il valore `tenantId` (noto anche come `appGUID`)  viene visualizzato nel campo **GUID applicazione / TenantId**. Avrai bisogno di questo valore per inizializzare il gestore autorizzazione.
* La tua **Regione** {{site.data.keyword.Bluemix_notm}}. Puoi trovare la tua regione {{site.data.keyword.Bluemix_notm}} corrente nell'intestazione, accanto all'icona **Avatar** ![Icona Avatar](images/face.jpg "Icona Avatar"). Il valore della regione visualizzato deve essere uno dei seguenti: `Stati Uniti Sud`, `Regno Unito` o `Sydney` e corrisponde ai valori delle SDK richiesti nel codice WebView Javascript: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` o `BMSClient.REGION_UK`. Avrai bisogno di questo valore per inizializzare il client {{site.data.keyword.amashort}}.
* Crea un'applicazione Cordova o un progetto esistente. Per ulteriori informazioni su come configurare la tua applicazione Cordova, visita il [sito Web Cordova ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cordova.apache.org/){: new_window}.

## Installazione del plugin Cordova {{site.data.keyword.amashort}}
{: #getting-started-cordova-plugin}

L'SDK client {{site.data.keyword.amashort}} per Cordova è un plugin Cordova che racchiude gli SDK client {{site.data.keyword.amashort}} nativi. Viene distribuito utilizzando
l'interfaccia riga di comando (CLI) Cordova e `npmjs`, un repository di plug-in per i progetti Cordova. La CLI Cordova scarica automaticamente i plugin dai repository e li rende disponibili alla tua applicazione Cordova.

1. Aggiungi le piattaforme Android e/o iOS alla tua applicazione Cordova. Dalla riga di comando, esegui uno dei seguenti comandi, o entrambi:

	###Android
	{: #install-cordova-android}

	```
	cordova platform add android
	```
	{: codeblock}

	###iOS
	{: #install-cordova-ios}

	```Bash
	cordova platform add ios
	```
	{: codeblock}

2. Se hai aggiunto la piattaforma Android, devi aggiungere il livello API minimo supportato al file `config.xml` della
tua applicazione Cordova. Apri il file `config.xml` e aggiungi la seguente riga all'elemento `<platform name="android">`:

	```XML
	<platform name="android">  
		<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
		<!-- add minimum and target Android API level declaration -->
	</platform>
	```
	{: codeblock}

	Il valore *minSdkVersion* deve essere maggiore di `15`. Fai riferimento alla [Guida della piattaforma Android ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cordova.apache.org/docs/en/latest/guide/platforms/android/){: new_window} per restare aggiornato sulla *targetSdkVersion* supportata per l'SDK Android.

3. Se hai aggiunto il sistema operativo iOS, aggiorna l'elemento `<platform name="ios">` con una dichiarazione di destinazione:

	```XML
	<platform name="ios">
		<preference name="deployment-target" value="8.0"/>
		<!-- add deployment target declaration -->
	 </platform>
	```
	{: codeblock}

4. Installa il plugin Cordova {{site.data.keyword.amashort}}:

 	```Bash
	cordova plugin add bms-core
	```
	{: codeblock}

5. Configura la tua piattaforma per Android, iOS o per entrambi.

	####Android
	{: #cordova-android}

	Prima di aprire il tuo progetto in Android Studio, genera la tua applicazione Cordova tramite l'interfaccia riga di comando (CLI) per evitare errori di generazione.

	```Bash
	cordova build android
	```
	{: codeblock}

	####iOS
	{: #cordova-ios}

	Configura il tuo progetto Xcode nel seguente modo.

	1. Utilizza la versione più recente di Xcode per aprire il tuo file `xcode.proj` nella directory `<app_name>/platforms/ios`.

		**Importante:** se ricevi un messaggio che indica di eseguire la conversione alla sintassi Swift più recente, fai clic su **Cancel**.

	2. Genera ed esegui la tua applicazione con Xcode.

	**Nota**: potresti ricevere il seguente errore durante l'esecuzione di `cordova build ios`. Questo problema è causato da un bug in un plugin della dipendenza che sta venendo tracciato in  [Issue 12 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/blakgeek/cordova-plugin-cocoapods-support/issues/12){: new_window}. Puoi ancora eseguire il progetto iOS in XCode tramite un simulatore o un dispositivo.

	```
	xcodebuild: error: Unable to find a destination matching the provided destination specifier:
			{ platform:iOS Simulator }

		Missing required device specifier option.
		The device type “iOS Simulator” requires that either “name” or “id” be specified.
		Please supply either “name” or “id”.
	```

6. Verifica che il plug-in sia stato installato correttamente eseguendo questo comando:

	```Bash
	cordova plugin list
	```
	{: codeblock}

7. Abilita Keychain Sharing per iOS impostando **Keychain Sharing** su `On` nella scheda **Capabilities**.

8. Abilita **Defines Module** per iOS impostando **Defines Module** su`YES` nella scheda **Build Settings** > **Packaging**.


## Inizializzazione del client {{site.data.keyword.amashort}} in WebView Cordova (Javascript)
{: #getting-started-cordova-initialize}

Per utilizzare l'SDK client {{site.data.keyword.amashort}}, devi inizializzare l'SDK passando `applicationBluemixRegion`.

Aggiungi la seguente chiamata al tuo file `index.js` per inizializzare l'SDK client {{site.data.keyword.amashort}}.

```JavaScript
BMSClient.initialize(<applicationBluemixRegion>);
```
{: codeblock}

**NB:** Sostituisci `<applicationBluemixRegion>` con la regione in cui è ospitato il tuo servizio {{site.data.keyword.Bluemix_notm}}, consulta [Prima di cominciare](#before-you-begin).

##Inizializzazione di AuthorizationManager {{site.data.keyword.amashort}} dal tuo codice nativo
{: #initializing-auth-manager}

Per utilizzare `BMSAuthorizationManager` dovrai aggiungere il seguente frammento di codice. Il seguente codice nativo inizializza `BMSAuthorizationManager` con il servizio {{site.data.keyword.amashort}} `tenantId` (consulta [Prima di cominciare](#before-you-begin)).

### Android (Java)

Nel metodo `OnCreate` nel file `MainActivity.java` aggiungi il codice prima di `loadUrl`.
```Java
MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),"<tenantId>");
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
```
{: codeblock}
### iOS (Objective C)
Aggiungi l'inizializzazione del gestore autorizzazione in `AppDelegate.m` in base alla tua versione di Xcode.

```Objective-C
  #import "<your_module_name>-Swift.h"
  [CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];
```
{: codeblock}

**Nota:** il nome del file di intestazione importato è formato dal nome modulo concatenato alla stringa `-Swift.h`,
ad esempio, se il tuo nome modulo è `Cordova` la riga importata dovrebbe essere `#import "Cordova-Swift.h"` Per trovare il nome modulo vai a
`Build Settings` > `Packaging` > `Product Module Name`.
Sostituisci `<tenantId>` il tuo ID tenant (consulta [Prima di cominciare](#before-you-begin)).


## Effettuare una richiesta al servizio di back-end mobile
{: #getting-started-request}

Dopo che l'SDK client {{site.data.keyword.amashort}} è stato inizializzato, puoi iniziare a effettuare richieste al tuo servizio di back-end mobile.

1. Prova a inviare una richiesta a un endpoint protetto della tua applicazione di back-end mobile. Nel tuo browser, apri il seguente URL: `{applicationRoute}/protected` (ad esempio: `http://my-mobile-backend.mybluemix.net/protected`).

	L'endpoint `/protected` di un'applicazione di backend mobile creato con il contenitore tipo MobileFirst Services Starter è protetto con {{site.data.keyword.amashort}}. Nel tuo browser viene restituito un messaggio `Unauthorized`. Questo messaggio viene restituito perché a questo endpoint accedono solo le applicazioni mobili strumentate con l'SDK client {{site.data.keyword.amashort}}.

2. Utilizza la tua applicazione Cordova per effettuare una richiesta allo stesso endpoint. Aggiungi il seguente codice dopo che hai inizializzato `BMSClient`:

	```Javascript
	var success = function(data){
	 console.log("success", data);
	 }

	 var failure = function(error){
	 console.log("failure", error);
	 }

	 var request = new BMSRequest("<your route>/protected", BMSRequest.GET);

	 request.send(success, failure);
	```
	{: codeblock}

3. Quando la tua richiesta ha esito positivo, vedrai il seguente output nella console LogCat o Xcode (a seconda della piattaforma che stai usando):

	![messaggio di esito positivo](images/getting-started-android-success.png)

	## Fasi successive
	{: #next-steps}

	Quando ti sei connesso all'endpoint protetto, non è stata richiesta alcuna credenziale. Per richiedere ai tuoi utenti di accedere alla tua applicazione, devi configurare l'autenticazione Facebook, Google o personalizzata.
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [Personalizzata](custom-auth-cordova.html)
