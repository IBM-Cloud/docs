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

# Abilitazione dell'autenticazione Facebook per le applicazioni Cordova
{: #facebook-auth-cordova}

Per configurare le applicazioni Cordova {{site.data.keyword.amafull}}  per l'integrazione dell'autenticazione Facebook, configura ogni piattaforma separatamente. L'applicazione Cordova deve già essere instrumentata con l'SDK {{site.data.keyword.amashort}}.

Sia la piattaforma nativa che il codice WebView Javascript Cordova richiedono le modifiche per abilitare l'autenticazione Facebook.

Utilizza l'ambiente di sviluppo nativo per apportare modifiche nel codice nativo, ad esempio in Android Studio o Xcode.
{:shortdesc}

## Prima di cominciare
{: #facebook-auth-before}

È necessario disporre di:
* Un progetto Cordova (Android o iOS) instrumentato con l'SDK client {{site.data.keyword.amashort}}, consulta [Configurazione del plugin Cordova](getting-started-cordova.html#getting-started-cordova-plugin).
* Un'istanza di un'applicazione  {{site.data.keyword.Bluemix_notm}} che è protetta da un servizio {{site.data.keyword.amashort}}. Per ulteriori informazioni su come creare un servizio di back-end {{site.data.keyword.Bluemix_notm}}, consulta [Introduzione](index.html).
* La tua rotta dell'applicazione. Questa è l'URL della tua applicazione di back-end.
* Il tuo valore `tenantId`. Apri il tuo dashboard del servizio {{site.data.keyword.amashort}}. Fai clic su **Opzioni mobili**. Il valore `tenantId` (noto anche come `appGUID`)  viene visualizzato nel campo **GUID applicazione / TenantId**. Avrai bisogno di questi valori per inizializzare l'SDK e per inviare le richieste al servizio di backend.
*  Trova la regione in cui è ospitato il tuo servizio {{site.data.keyword.Bluemix_notm}}. Puoi trovare la tua regione {{site.data.keyword.Bluemix_notm}} corrente nell'intestazione, accanto all'icona **Avatar** ![Icona Avatar](images/face.jpg "Icona Avatar")  nella barra del menu. Il valore della regione deve essere uno dei seguenti: **Stati Uniti Sud**, **Sydney** o **UK**. I valori costanti della SDK esatti che corrispondono a tali nomi sono indicati negli esempi di codice.
* Un'applicazione Facebook e l'ID applicazione. Per ulteriori informazioni, [Creazione di un'applicazione nel sito web Facebook for Developers](facebook-auth-overview.html#facebook-appID).



## Configurazione della piattaforma Android
{: #facebook-auth-cordova-android}

I passi richiesti per configurare la piattaforma Android di un'applicazione Cordova per l'integrazione dell'autenticazione Facebook sono molto simili a quelli richiesti per le applicazioni Android native. Per ulteriori informazioni, vedi [Abilitazione dell'autenticazione Facebook nelle applicazioni Android](facebook-auth-android.html). Completa la seguente procedura:

* [Configurazione della tua applicazione Facebook per la piattaforma Android](facebook-auth-android.html#facebook-auth-android-config). Viene configurata l'autenticazione Facebook sul sito Facebook Developers per le applicazioni Android.
* [Configurazione MCA per l'autenticazione Facebook](facebook-auth-android.html#facebook-auth-android-mca). Viene configurato il tuo servizio {{site.data.keyword.amashort}} nel server {{site.data.keyword.Bluemix}} per l'autenticazione Facebook Android.


### Configurazione dell'SDK client Facebook {{site.data.keyword.amashort}} per la piattaforma Android
{: #configure_android}

L'SDK client Facebook {{site.data.keyword.amashort}} deve essere aggiunta da Gradle nel tuo progetto dell'applicazione Android nativa.

1. Nella cartella del tuo progetto Android, apri il file `build.gradle` per il modulo dell'applicazione (**non** il file `build.gradle` del progetto). Trova la sezione delle dipendenze e aggiungi una nuova dipendenza di compilazione per l'SDK client:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',
        name:'facebookauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// altre dipendenze
	}
	```
	{: codeblock}

2. Fai clic su **Tools > Android > Sync Project with Gradle Files** per sincronizzare il tuo progetto con Gradle.

3. Apri il file `android/res/values/strings.xml` e aggiungi una stringa `<facebook_app_id>` che contiene il tuo ID applicazione Facebook.

	```XML
	<resources>
		<string name="app_name">HelloCordova</string>
		<string name="launcher_name">@string/app_name</string>
		<string name="activity_name">@string/launcher_name</string>
		<string name="facebook_app_id">"<facebook_app_id>"</string>
	</resources>
	```
	{: codeblock}

4. Nel file `AndroidManifest.xml` del tuo progetto Android (`android/manifests/AndroidManifest.xml`):

	* Aggiungi i metadati richiesti per l'SDK Facebook all'elemento <application>:

    ```XML
    <application .......>
    <meta-data
			android:name="com.facebook.sdk.ApplicationId"
			android:value="@string/facebook_app_id"/>

    <activity ...../>
    <activity ...../>
    </application>
    ```
    {: codeblock}

   * Aggiungi un elemento di attività Facebook (FacebookActivity) sotto le tue attività esistenti:

    ```XML
    <application .....>
        <activity ...../>
		<activity ...../>

        <activity   android:name="com.facebook.FacebookActivity"
	              android:configChanges="keyboard|keyboardHidden|screenLayout|screenSize|orientation"
	              android:theme="@android:style/Theme.Translucent.NoTitleBar"
	              android:label="@string/app_name"
        />
    </application>
    ```
    {: codeblock}

5. Aggiungi quanto segue al tuo codice Java dell'attività

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
	   super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
	      .onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}

### Inizializza il gestore autorizzazione nel tuo codice Android nativo
{: #initialize_android}

L'API `FacebookAuthenticationManager` continua a dover essere registrata nel tuo codice nativo. Aggiungi questo codice al metodo `onCreate` dell'attività principale utilizzando `<tenantId>` (consulta [Prima di cominciare](#before-you-begin)).

```
String tenantId = "<tenantId>";
MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
FacebookAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
```
{: codeblock}


## Configurazione della piattaforma iOS
{: #facebook-auth-cordova-ios}

I passi richiesti per configurare la piattaforma iOS di un'applicazione Cordova per l'integrazione dell'autenticazione Facebook sono simili a quelli richiesti per le applicazioni Swift iOS native (sono richiesti dei file di intestazione per utilizzare il codice Objective-C con l'SDK Swift). La differenza principale consiste nel fatto che attualmente la CLI Cordova non supporta il gestore dipendenze CocoaPods. Devi aggiungere manualmente i file richiesti per l'integrazione del client {{site.data.keyword.amashort}} con l'autenticazione Facebook. Per ulteriori informazioni, vedi [Abilitazione dell'autenticazione Facebook per le applicazioni iOS (SDK Swift)](facebook-auth-ios-swift-sdk.html). Completa la seguente procedura:

* [Configurazione della tua applicazione Facebook per la piattaforma iOS](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-config). Viene configurato il servizio di autenticazione Facebook sul sito Facebook Developers.
* [Configurazione MCA per l'autenticazione Facebook](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-configmca). Viene configurato il tuo servizio {{site.data.keyword.amashort}} nel server {{site.data.keyword.Bluemix}}.
* [Configurazione dell'SDK client Facebook MCA per iOS](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-sdk). Viene installata l'SDK Swift iOS {{site.data.keyword.amashort}} per l'autorizzazione Facebook utilizzando CocoaPods.


### Abilitare Keychain Sharing per iOS
{: #enable_keychain}

Abilita `Keychain Sharing`. Vai alla scheda `Funzionalità` e passa `Keychain Sharing` su `Attivo` nel tuo progetto Xcode.

### Inizializza il gestore autorizzazione {{site.data.keyword.amashort}} in Objective-C
{: #initialize_objc}

Il gestore autorizzazione deve essere inizializzato nel codice Objective-C nativo nel file  `app-delegate.m `, in base alla tua versione di Xcode.

```
	#import "<your_module_name>-Swift.h"

	- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

	    [CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];

	    [[FacebookAuthenticationManager sharedInstance] register];

	    self.viewController = [[MainViewController alloc] init];

	    [[FacebookAuthenticationManager sharedInstance] onFinishLaunchingWithApplication:application withOptions:launchOptions];


	    return [super application:application didFinishLaunchingWithOptions:launchOptions];
	}


	- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {

	   return [[FacebookAuthenticationManager sharedInstance] onOpenURLWithApplication:application 
	   		url:url sourceApplication:sourceApplication annotation:annotation];
	}

```
{: codeblock}

**Nota:** il nome del file di intestazione importato è formato dal nome modulo concatenato alla stringa `-Swift.h`,
ad esempio, se il tuo nome modulo è `Cordova` la riga importata dovrebbe essere `#import "Cordova-Swift.h"` Per trovare il nome modulo vai a
`Build Settings` > `Packaging` > `Product Module Name`.

Sostituisci `<tenantId>` il tuo ID tenant (consulta [Prima di cominciare](#facebook-auth-before)).


##Inizializzazione dell'SDK client {{site.data.keyword.amashort}} in Cordova WebView
{: #initialize_webview}

Per tutte le piattaforme, utilizza il seguente codice JavaScript, nella tua Javascript WebView Cordova per inizializzare l'SDK client {{site.data.keyword.amashort}}.

```javascript
BMSClient.initialize(<applicationBluemixRegion>);
```
{: codeblock}

Sostituisci `<applicationBluemixRegion>` con la tua regione (consulta [Prima di cominciare](#facebook-auth-before)).

## Verifica dell'autenticazione
{: #facebook-auth-cordova-test}

Dopo che l'SDK client è stato inizializzato e il gestore autenticazione Facebook è stato registrato, puoi iniziare a effettuare richieste al tuo servizio di back-end mobile.

### Prima di cominciare
{: #testing_auth_before}

Devi utilizzare il contenitore tipo {{site.data.keyword.mobilefirstbp}} e disporre già di una risorsa protetta da {{site.data.keyword.amashort}} all'endpoint `/protected`. Per ulteriori informazioni, vedi [Protezione delle risorse](protecting-resources.html).

1. Prova a inviare una richiesta all'endpoint protetto del backend mobile dal tuo browser. Apri il seguente URL: `{applicationRoute}/protected`. Ad esempio: `http://my-mobile-backend.mybluemix.net/protected`.

	Il valore dell'endpoint `/protected` dovrebbe essere qualsiasi endpoint protetto di un servizio di back-end creato con il contenitore tipo MobileFirst Services Starter e protetto con {{site.data.keyword.amashort}}. Nel tuo browser viene restituito un messaggio `Unauthorized`. Questo messaggio viene restituito perché a questo endpoint possono accedere solo le applicazioni mobili strumentate con l'SDK client{{site.data.keyword.amashort}}.

1. Utilizza la tua applicazione Cordova per effettuare una richiesta allo stesso endpoint. Aggiungi il seguente codice dopo che hai inizializzato `BMSClient`:

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error){
    	console.log("failure", error);
    }
	var request = new BMSRequest("<applicationRoute}/protected>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}

1. Esegui la tua applicazione. Viene visualizzata una schermata di accesso a Facebook:

	![immagine](images/android-facebook-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![immagine](images/ios-facebook-login.png)

	Questa schermata può avere un aspetto lievemente differente se sul tuo dispositivo non è installata l'applicazione Facebook o se non sei attualmente collegato a Facebook.

1. Fai clic su **OK** per autorizzare {{site.data.keyword.amashort}} a usare la tua identità utente Facebook per scopi di autenticazione.

1. 	Quando la tua richiesta ha esito positivo, nel programma di utilità LogCat o nella console Xcode è presente il seguente output:

	![Messaggio di esito positivo dell'autenticazione Facebook per Android](images/android-facebook-login-success.png)

	![Messaggio di esito positivo dell'autenticazione Facebook per iOS ](images/ios-facebook-login-success.png)
