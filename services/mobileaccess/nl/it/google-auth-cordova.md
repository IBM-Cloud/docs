---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"
---
{:screen: .screen}
{:shortdesc: .shortdesc}

# Abilitazione dell'autenticazione Google per le applicazioni Cordova
{: #google-auth-cordova}


Per configurare le applicazioni Cordova {{site.data.keyword.amafull}} per l'integrazione dell'autenticazione Google, devi apportare le modifiche in codice nativo dell'applicazione Cordova (Java, Objective-C o Swift). Ciascuna piattaforma deve essere configurata separatamente. Utilizza l'ambiente di sviluppo nativo per apportare modifiche nel codice nativo, ad esempio in Android Studio o Xcode.

## Prima di cominciare
{: #before-you-begin}
È necessario disporre di:
* Un progetto Cordova instrumentato con l'SDK client {{site.data.keyword.amashort}}.  Per ulteriori informazioni, vedi  [Configurazione del plugin Cordova](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html).  
* Un'istanza di un'applicazione  {{site.data.keyword.Bluemix_notm}} che è protetta da un servizio {{site.data.keyword.amashort}}. Per ulteriori informazioni su come creare un'applicazione di back-end {{site.data.keyword.Bluemix_notm}}, vedi [Introduzione](index.html).
* (facoltativo) Acquisisci dimestichezza con le seguenti sezioni:
   * [Abilitazione dell'autenticazione Google per le applicazioni Android](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)
   * [Abilitazione dell'autenticazione Google per le applicazioni iOS](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html)


## Configurazione della piattaforma Android
{: #google-auth-cordova-android}

I passi richiesti per configurare la piattaforma Android di un'applicazione Cordova per l'integrazione dell'autenticazione Google sono molti simili a quelli richiesti per le applicazioni native. Consulta [Abilitazione dell'autenticazione Google nelle applicazioni Android](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html) e configura quanto segue:

* Configurazione del progetto Google per la piattaforma Android
* Configurazione di {{site.data.keyword.amashort}} per l'autenticazione Google

### Configura l'SDK client {{site.data.keyword.amashort}} per Android Cordova


2. Nella cartella del tuo progetto Android, apri il file `build.gradle` per il modulo dell'applicazione (**non** il file `build.gradle` del progetto).
Trova la sezione delle dipendenze e aggiungi una nuova dipendenza di compilazione per l'SDK client:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'googleauthentication',
        version: '1.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```

2. Sincronizza il tuo progetto con Gradle facendo clic su **Tools > Android > Sync Project with Gradle Files**.

3. Per le applicazioni Cordova inizializza l'SDK client {{site.data.keyword.amashort}} nel tuo codice JavaScript invece che nel codice Java. L'API `GoogleAuthenticationManager` continua a dover essere registrata nel tuo codice nativo. Aggiungi questo codice al metodo `onCreate` del'attività principale: 

	```Java
	GoogleAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
	```

1. Aggiungi il seguente codice alla tua attività:
 
 	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
	     super.onActivityResult(requestCode, resultCode, data);
		GoogleAuthenticationManager.getInstance()
	         .onActivityResultCalled(requestCode, resultCode, data);
	}
	```

## Configurazione della piattaforma iOS
{: #google-auth-cordova-ios}

I passi richiesti per configurare la piattaforma iOS di un'applicazione Cordova per l'integrazione dell'autenticazione Google sono simili a quelli per le applicazioni native. La differenza principale consiste nel fatto che attualmente la CLI Cordova non supporta il gestore dipendenze CocoaPods.  Devi aggiungere manualmente i file richiesti per l'integrazione con l'autenticazione Google. Per ulteriori informazioni, vedi [Abilitazione dell'autenticazione Google nelle applicazioni iOS](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html). Completa la seguente procedura:

* Configurazione del progetto Google per la piattaforma iOS
* Configurazione di {{site.data.keyword.amashort}} per l'autenticazione Google

### Installazione manuale dell'SDK {{site.data.keyword.amashort}} per l'autenticazione Google e dell'SDK Google
{: #google-auth-cordova-ios-sdk}
1. Scarica l'archivio che contiene l'SDK [{{site.data.keyword.Bluemix}} Mobile Services SDK per iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).

1. Vai alla directory `Sources/Authenticators/IMFGoogleAuthentication` e copia (trascina e rilascia) tutti i file nel tuo progetto iOS in Xcode. I file che devi copiare sono:

	* IMFDefaultGoogleAuthenticationDelegate.h
	* IMFDefaultGoogleAuthenticationDelegate.m
	* IMFGoogleAuthenticationDelegate.h
	* IMFGoogleAuthenticationHandler.h
	* IMFGoogleAuthenticationHandler.m

	Seleziona la casella di spunta **Copia file....**.

1. Scarica e installa l'[SDK iOS Google+](http://goo.gl/9cTqyZ).

1. Attieniti al passo 2 dell'esercitazione [Start integrating Google+ into your iOS app](https://developers.google.com/+/mobile/ios/getting-started) per integrare l'SDK iOS Google+ nel tuo progetto Xcode.

Continua alla sezione **Configurazione del progetto iOS per l'autenticazione Google** di [Configurazione della piattaforma iOS per l'autenticazione Google](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html). Registra l'`IMFGoogleAuthenticationHandler` in codice nativo come descritto nella sezione `Inizializzazione dell'SDK client {{site.data.keyword.amashort}}`. Non inizializzare `IMFClient` nel tuo codice nativo (il client viene inizializzato in JavaScript nella seguente sezione).

Aggiungi questa riga al metodo `application:openURL:sourceApplication:annotation` del tuo delegato dell'applicazione. Questa riga assicura che tutti i plugin Cordova vengano informati dei rispettivi eventi.

```
[[NSNotificationCenter defaultCenter] postNotification:[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```
{: codeblock}

## Inizializzazione dell'SDK client {{site.data.keyword.amashort}}
{: #google-auth-cordova-initialize}

Utilizza il seguente codice JavaScript nella tua applicazione Cordova per inizializzare l'SDK client {{site.data.keyword.amashort}}.

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```
{: codeblock}

Sostituisci i valori `applicationRoute` e `applicationGUID` con i valori **Route** e **AppGuid** dell'applicazione. Puoi trovare questi valori facendo clic sul pulsante **Opzioni mobili** dalla pagina dell'applicaizone nel dashboard.
	



##Inizializzazione di AuthorizationManager {{site.data.keyword.amashort}}
Utilizza il seguente codice JavaScript nella tua applicazione Cordova per inizializzare AuthorizationManager {{site.data.keyword.amashort}}.

```JavaScript
  MFPAuthorizationManager.initialize("tenantId");
```
{: codeblock}

Sostituisci il valore `tenantId` con il servizio {{site.data.keyword.amashort}} `tenantId`. Puoi trovare questo valore facendo clic sul pulsante **Visualizza credenziali** nel tile del servizio {{site.data.keyword.amashort}}.





## Verifica dell'autenticazione
{: #google-auth-cordova-test}
Dopo che l'SDK client è stato inizializzato, puoi iniziare a effettuare richieste alla tua applicazione di back-end mobile.

### Prima di cominciare
{: #google-auth-cordova-testing-before}
Devi disporre di una applicazione di backend protetta da {{site.data.keyword.amashort}} all'endpoint `/protected`. Se devi configurare un endpoint `/protected`, consulta [Protezione delle risorse](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Prova a inviare una richiesta a un endpoint protetto della tua applicazione di back-end mobile nel tuo browser desktop aprendo `{applicationRoute}/protected`, ad esempio `http://my-mobile-backend.mybluemix.net/protected`.

1. L'endpoint `/protected` di un'applicazione di back-end mobile creato con il contenitore tipo MobileFirst Services è protetto con {{site.data.keyword.amashort}}; pertanto, possono accedere ad esso solo le applicazioni mobili strumentate con l'SDK client {{site.data.keyword.amashort}}. Di conseguenza, vedrai `Unauthorized` nel tuo browser del desktop.

1. Utilizza la tua applicazione Cordova per effettuare una richiesta allo stesso endpoint. Aggiungi il seguente codice dopo che hai inizializzato `BMSClient`.

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

1. Esegui la tua applicazione. Viene visualizzata la schermata di accesso a Google.

	![Schermata di accesso Google](images/android-google-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![Schermata di accesso Google](images/ios-google-login.png)
	
	Questa schermata può avere un aspetto lievemente differente se sul tuo dispositivo non è installata l'applicazione Facebook o se non sei attualmente collegato a Facebook.
1. Facendo clic su **OK**, stai autorizzando {{site.data.keyword.amashort}} a utilizzare la tua identità utente Google per scopi di autenticazione.

1. La tua richiesta dovrebbe avere esito positivo. A seconda della piattaforma che stai utilizzando, visualizzerai il seguente output nella console LogCat/Xcode:

	![Frammento di codice su android](images/android-google-login-success.png)

	![Frammento di codice su iOS](images/ios-google-login-success.png)
