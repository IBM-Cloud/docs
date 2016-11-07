---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"
---
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Abilitazione dell'autenticazione Facebook per le applicazioni Cordova
{: #facebook-auth-cordova}


Per configurare le applicazioni Cordova {{site.data.keyword.amafull}}  per l'integrazione dell'autenticazione Facebook, apporta le modifiche in codice nativo dell'applicazione Cordova in Java, Objective-C o Swift. Configura ciascuna piattaforma separatamente. Questa applicazione Cordova deve già essere instrumentata con l'SDK {{site.data.keyword.amashort}}. 


Utilizza l'ambiente di sviluppo nativo per apportare modifiche nel codice nativo, ad esempio in Android Studio o Xcode.
{:shortdesc}

## Prima di cominciare
{: #facebook-auth-before}
È necessario disporre di:
* Un progetto Cordova instrumentato con l'SDK client {{site.data.keyword.amashort}}, consulta [Configurazione del plugin Cordova](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html).
* Un'istanza di un'applicazione  {{site.data.keyword.Bluemix_notm}} che è protetta da un servizio {{site.data.keyword.amashort}}. Per ulteriori informazioni su come creare un'applicazione di back-end {{site.data.keyword.Bluemix_notm}}, vedi [Introduzione](index.html).
* Un ID dell'applicazione Facebook. er ulteriori informazioni, vedi [Ottenimento di un ID applicazione Facebook dal portale sviluppatori Facebook](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).



## Configurazione della piattaforma Android
{: #facebook-auth-cordova-android}

I passi richiesti per configurare la piattaforma Android di un'applicazione Cordova per l'integrazione dell'autenticazione Facebook sono molto simili a quelli richiesti per le applicazioni Android native. Per ulteriori informazioni, vedi [Abilitazione dell'autenticazione Facebook nelle applicazioni Android](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html). Completa la seguente procedura:

* Configurazione dell'applicazione Facebook per la piattaforma Android
* Configurazione di {{site.data.keyword.amashort}} per l'autenticazione Facebook

### Configurazione dell'SDK client {{site.data.keyword.amashort}} per Android

Configura l'SDK client {{site.data.keyword.amashort}} per Android nella tua applicazione Cordova.

1. Nella cartella del tuo progetto Android, apri il file `build.gradle` per il modulo dell'applicazione (**non** il file `build.gradle` del progetto). Trova la sezione delle dipendenze e aggiungi una nuova dipendenza di compilazione per l'SDK client:

	```Gradle
	dependencies {
     		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
     		name:'facebookauthentication',
     		version: '1.+',
     		ext: 'aar',
     		transitive: true
     		// other dependencies  
		 }
	```
	
2. Sincronizza il tuo progetto con Gradle facendo clic su **Tools > Android > Sync Project with Gradle Files**.

3. Apri il file `android/res/values/strings.xml` e aggiungi una stringa `facebook_app_id` che contiene il tuo ID applicazione Facebook. 

	```XML
	<resources>
		<string name="app_name">HelloCordova</string>
		<string name="launcher_name">@string/app_name</string>
		<string name="activity_name">@string/launcher_name</string>
		<string name="facebook_app_id">522733366802111</string>
	</resources>
	```
	
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

2. Per le applicazioni Cordova inizializza l'SDK client {{site.data.keyword.amashort}} nel tuo codice JavaScript invece che nel codice Java. L'API `FacebookAuthenticationManager` continua a dover essere registrata nel tuo codice nativo. Aggiungi questo codice al metodo `onCreate` del'attività principale:  

	```Java
	FacebookAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
	```

6. Aggiungi il seguente codice alla tua attività:

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
	      super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
	          .onActivityResultCalled(requestCode, resultCode, data);
	}
	```

## Configurazione della piattaforma iOS
{: #facebook-auth-cordova-ios}

I passi richiesti per configurare la piattaforma iOS di un'applicazione Cordova per l'integrazione dell'autenticazione Facebook sono simili a quelli richiesti per le applicazioni iOS native. La differenza principale consiste nel fatto che attualmente la CLI Cordova non supporta il gestore dipendenze CocoaPods. Devi aggiungere manualmente i file richiesti per l'integrazione con l'autenticazione Facebook. Per ulteriori informazioni, vedi [Abilitazione dell'autenticazione Facebook nelle applicazioni iOS](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html). Completa la seguente procedura:

* Configurazione dell'applicazione Facebook per la piattaforma iOS
* Configurazione di {{site.data.keyword.amashort}} per l'autenticazione Facebook

### Installazione manuale dell'SDK {{site.data.keyword.amashort}} per l'autenticazione Facebook e dell'SDK Facebook
{: #facebook-auth-cordova-ios-sdk}
1. Scarica l'archivio che contiene l'[SDK {{site.data.keyword.Bluemix_notm}} Mobile Services per iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).

1. Vai alla directory `Sources/Authenticators/IMFFacebookAuthentication` e copia (trascina e rilascia) tutti i file nel tuo progetto iOS in Xcode. Copia i seguenti file:

	* IMFDefaultFacebookAuthenticationDelegate.h
	* IMFDefaultFacebookAuthenticationDelegate.m
	* IMFFacebookAuthenticationDelegate.h
	* IMFFacebookAuthenticationHandler.h
	* IMFFacebookAuthenticationHandler.m

	Quando richiesto da Xcode, seleziona **Copy files...**.

1. Scarica e installa [Facebook SDK v3.19](https://developers.facebook.com/resources/facebook-ios-sdk-3.19.pkg).

1. L'SDK Facebook sarà installato nella directory `~/Documents/FacebookSDK`. Passa a tale directory e copia (trascina e rilascia) il file `FacebookSDK.framework` nel tuo progetto iOS in Xcode.

1. Fai clic sulla root del tuo progetto in Xcode e seleziona la scheda **Build Phases**.

1. Aggiungi il file `FacebookSDK.framework` all'elenco di librerie collegate in **Link Binary With Libraries**.

 Vedi [Configurazione della piattaforma iOS per l'autenticazione Facebook](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html). Registra l'API `IMFFacebookAuthenticationHandler` in codice nativo come descritto nella sezione **Inizializzazione dell'SDK client {{site.data.keyword.amashort}}**. Non inizializzare `IMFClient` nel tuo codice nativo.

Aggiungi la seguente riga al metodo `application:openURL:sourceApplication:annotation` del tuo delegato dell'applicazione. Questo codice assicura che tutti i plugin Cordova vengano informati dei rispettivi eventi.

```
[[NSNotificationCenter defaultCenter] postNotification:[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```
{: codeblock}

## Inizializzazione dell'SDK client {{site.data.keyword.amashort}}
{: #facebook-auth-cordova-init}

Utilizza il seguente codice JavaScript nella tua applicazione Cordova per inizializzare l'SDK client {{site.data.keyword.amashort}}.

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```
{: codeblock}

Sostituisci `applicationRoute` e `applicationGUID` con i valori ottenuti per **Rotta** e **GUID applicazione** da **Opzioni mobili**.
	



##Inizializzazione di AuthorizationManager {{site.data.keyword.amashort}}
Utilizza il seguente codice JavaScript nella tua applicazione Cordova per inizializzare AuthorizationManager {{site.data.keyword.amashort}}.
```JavaScript
  MFPAuthorizationManager.initialize("tenantId");
```
{: codeblock}

Sostituisci il valore `tenantId` con il servizio {{site.data.keyword.amashort}} `tenantId`. Puoi trovare questo valore facendo clic sul pulsante **Visualizza credenziali** nel tile del servizio {{site.data.keyword.amashort}}.



## Verifica dell'autenticazione
{: #facebook-auth-cordova-test}
Dopo che l'SDK client è stato inizializzato e il gestore autenticazione Facebook è stato registrato, puoi iniziare a effettuare richieste alla tua applicazione di back-end mobile.

### Prima di cominciare
Devi utilizzare il contenitore tipo {{site.data.keyword.mobilefirstbp}} e disporre già di una risorsa protetta da {{site.data.keyword.amashort}} all'endpoint `/protected`. Per ulteriori informazioni, vedi [Protezione delle risorse](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Prova a inviare una richiesta all'endpoint protected del backend mobile appena creato dal tuo browser. Apri il seguente URL: `{applicationRoute}/protected`. Ad esempio: `http://my-mobile-backend.mybluemix.net/protected`
<br/>L'endpoint `/protected` di un'applicazione di back-end mobile creato con il contenitore tipo MobileFirst Services Starter è protetto con {{site.data.keyword.amashort}}. Nel tuo browser viene restituito un messaggio `Unauthorized`. Questo messaggio viene restituito perché a questo endpoint possono accedere solo le applicazioni mobili strumentate con l'SDK client{{site.data.keyword.amashort}}.

1. Utilizza la tua applicazione Cordova per effettuare una richiesta allo stesso endpoint. Aggiungi il seguente codice dopo che hai inizializzato `BMSClient`:

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new MFPRequest("/protected", MFPRequest.GET);
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
