---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

Il servizio {{site.data.keyword.amafull}} è stato sostituito con il servizio {{site.data.keyword.appid_full}}.

# Abilitazione dell'autenticazione Google per le applicazioni Cordova
{: #google-auth-cordova}

Per integrare le tue applicazioni Cordova {{site.data.keyword.amafull}} con l'autenticazione Google, devi effettuare delle modifiche nel codice della piattaforma nativa dell'applicazione Cordova (Java o Objective-C), così come in WebView Cordova (Javascript). Ciascuna piattaforma deve essere configurata separatamente. Utilizza l'ambiente di sviluppo nativo per apportare modifiche nel codice nativo, ad esempio in Android Studio o Xcode.

## Prima di cominciare
{: #before-you-begin}

È necessario disporre di:

* Un progetto Cordova instrumentato con l'SDK client {{site.data.keyword.amashort}}.  Per ulteriori informazioni, vedi  [Configurazione del plugin Cordova](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html).  
* Un'istanza di un'applicazione  {{site.data.keyword.Bluemix_notm}} che è protetta da un servizio {{site.data.keyword.amashort}}. Per ulteriori informazioni su come creare un servizio di back-end {{site.data.keyword.Bluemix_notm}}, consulta [Introduzione](index.html).
* La tua rotta dell'applicazione. Questa è l'URL della tua applicazione di back-end.
* Il tuo **TenantID**. Apri il tuo servizio nel dashboard {{site.data.keyword.Bluemix_notm}}. Fai clic su **Opzioni mobili**. Il valore `tenantId` (noto anche come `appGUID`)  viene visualizzato nel campo **GUID applicazione / TenantId**. Avrai bisogno di questo valore per inizializzare il gestore autorizzazione.
*  Trova la regione in cui è ospitata la tua applicazione {{site.data.keyword.Bluemix_notm}}. Puoi trovare la tua regione Bluemix corrente nell'intestazione, accanto all'icona **Avatar** ![Icona Avatar](images/face.jpg "Icona Avatar"). Il valore della regione deve essere uno dei seguenti: **Stati Uniti Sud**, **Sydney** o **UK**. I valori costanti della SDK esatti che corrispondono a tali nomi sono indicati negli esempi di codice.
* (facoltativo) Acquisisci dimestichezza con le seguenti sezioni:
   * [Abilitazione dell'autenticazione Google per le applicazioni Android](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)
   * [Abilitazione dell'autenticazione Google per le applicazioni iOS](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html)


## Configurazione della piattaforma Android
{: #google-auth-cordova-android}

I passi richiesti per configurare la piattaforma Android di un'applicazione Cordova per l'autenticazione Google sono molti simili a quelli richiesti per le applicazioni native. Consulta [Abilitazione dell'autenticazione Google nelle applicazioni Android](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html) e configura quanto segue:

   * [Creazione di un progetto con Google Developer Console](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html#create-google-project). Viene illustrato come configurare il servizio di autenticazione sul sito web Google Developers.
   * [Configurazione MCA per l'autenticazione Google](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html#google-auth-android-config). Viene illustrato come configurare {{site.data.keyword.amashort}} per utilizzare l'autorizzazione Google.

### Configura l'SDK client {{site.data.keyword.amashort}} per Android Cordova

1. Nella cartella del tuo progetto Android, apri il file `build.gradle` per il modulo dell'applicazione (**non** il file `build.gradle` del progetto).
	Trova la sezione delle dipendenze e aggiungi una nuova dipendenza di compilazione per l'SDK client:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',
        name:'googleauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// altre dipendenze
	}
	```
	{: codeblock}

1. Sincronizza il tuo progetto con Gradle facendo clic su **Tools > Android > Sync Project with Gradle Files**.

1. L'API `GoogleAuthenticationManager` continua a dover essere registrata nel tuo codice nativo. Aggiungi questo codice al metodo `onCreate` del'attività principale:

	```Java
	String tenantId = "<tenantId>";
	MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
	BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
	GoogleAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
	```
	{: codeblock}

1. Aggiungi il seguente codice alla tua attività:

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		GoogleAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}

## Configurazione della piattaforma iOS
{: #google-auth-cordova-ios}

I passi richiesti per configurare la piattaforma iOS di un'applicazione Cordova per l'integrazione dell'autenticazione Google sono simili a quelli per le applicazioni native. La differenza principale consiste nel fatto che attualmente la CLI Cordova non supporta il gestore dipendenze CocoaPods. Devi aggiungere manualmente i file richiesti per l'integrazione con l'autenticazione Google. Per ulteriori informazioni, vedi [Abilitazione dell'autenticazione Google per le applicazioni iOS (SDK Swift)](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html). Completa la seguente procedura:

   * [Preparazione della tua applicazione per l'accesso Google](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-sign-in-ios): prepara l'accesso Google per l'autenticazione delle applicazioni iOS {{site.data.keyword.amashort}}.

   * [Configurazione di MCA per l'autenticazione Google](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-auth-ios-config): configura il tuo servizio {{site.data.keyword.amashort}} ad utilizzare l'accesso Google.

   * [Configurazione dell'SDK client MCA per iOS](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-auth-ios-sdk): configura il tuo client {{site.data.keyword.amashort}} ad utilizzare l'accesso Google.


### Abilitare Keychain Sharing per iOS
{: #enable_keychain}

Abilita `Keychain Sharing`. Vai alla scheda `Funzionalità` e passa `Keychain Sharing` su `Attivo` nel tuo progetto Xcode.


### Inizializzazione del gestore autorizzazione nel tuo codice iOS.

Inizializza il gestore autorizzazione {{site.data.keyword.amashort}} in Objective-C nel file `AppDelgate.m`.

```
#import "<your_module_name>-Swift.h"

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions

{
	[CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];

	[[GoogleAuthenticationManager sharedInstance] register];

	self.viewController = [[MainViewController alloc] init];

	[[GoogleAuthenticationManager sharedInstance] onFinishLaunchingWithApplication:application withOptions:launchOptions];

	return [super application:application didFinishLaunchingWithOptions:launchOptions];
	}

- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {
	return [[GoogleAuthenticationManager sharedInstance] onOpenURLWithApplication:application url:url 
	sourceApplication:sourceApplication annotation:annotation];
}
```
{: codeblock}


####Nota:
{: #note notoc}

* Sostituisci `<your_module_name>` con il nome modulo del tuo progetto. Ad esempio, se il tuo nome modulo è `Cordova`,
la riga importata deve essere `#import "Cordova-Swift.h"` Trova il nome modulo e vai alla scheda
`Build Settings`,  `Packaging` > `Product Module Name`.
* Sostituisci il tuo `<tenantId>` con il tuo ID tenant (consulta [Prima di cominciare](#before-you-begin)).


## Inizializzazione dell'SDK client {{site.data.keyword.amashort}} nel tuo Cordova WebView
{: #google-auth-cordova-initialize}

Per tutte le piattaforme, utilizza il seguente codice Javascript nella tua applicazione Cordova per inizializzare l'SDK client {{site.data.keyword.amashort}}.

```JavaScript
BMSClient.initialize("<applicationBluemixRegion>");
```
{: codeblock}

Sostituisci `<applicationBluemixRegion>` con la tua regione (consulta [Prima di cominciare](#before-you-begin)).

## Verifica dell'autenticazione
{: #google-auth-cordova-test}

Dopo che l'SDK client è stato inizializzato, puoi iniziare a effettuare richieste alla tua applicazione di back-end mobile.

### Prima di cominciare
{: #google-auth-cordova-testing-before}

Devi disporre di una applicazione di backend protetta da {{site.data.keyword.amashort}} all'endpoint `/protected`. Se devi configurare un endpoint `/protected`, consulta [Protezione delle risorse](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Prova a inviare una richiesta a un endpoint protetto della tua applicazione di back-end mobile nel tuo browser desktop aprendo `{applicationRoute}/protected`, ad esempio `http://my-mobile-backend.mybluemix.net/protected`.

1. L'endpoint `/protected` di un'applicazione di back-end mobile creato con il contenitore tipo MobileFirst Services è protetto con {{site.data.keyword.amashort}}; pertanto, possono accedere ad esso solo le applicazioni mobili strumentate con l'SDK client {{site.data.keyword.amashort}}. Di conseguenza, vedrai `Unauthorized` nel tuo browser del desktop.

1. Utilizza la tua applicazione Cordova per effettuare una richiesta allo stesso endpoint, utilizzando l'URL completo (ad esempio `http://my-mobile-backend.mybluemix.net/protected`). Aggiungi il seguente codice dopo che hai inizializzato `BMSClient`.

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new BMSRequest("<your-application-route>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}

1. Esegui la tua applicazione. Viene visualizzata la schermata di accesso a Google.

	![Schermata di accesso Google](images/android-google-login.png)

	![Schermata di accesso Google](images/ios-google-login.png)

	Questa schermata può avere un aspetto lievemente differente se sul tuo dispositivo non è installata l'applicazione Facebook o se non sei attualmente collegato a Facebook.

1. Facendo clic su **OK**, stai autorizzando {{site.data.keyword.amashort}} a utilizzare la tua identità utente Google per scopi di autenticazione.

1. La tua richiesta dovrebbe avere esito positivo. A seconda della piattaforma che stai utilizzando, visualizzerai il seguente output nella console LogCat/Xcode:

	![Frammento di codice su android](images/android-google-login-success.png)

	![Frammento di codice su iOS](images/ios-google-login-success.png)
