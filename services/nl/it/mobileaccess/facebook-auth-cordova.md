---

copyright:
  years: 2015, 2016

---

# Abilitazione dell'autenticazione Facebook nelle applicazioni Cordova
{: #facebook-auth-cordova}
Per configurare le applicazioni Cordova per l'integrazione dell'autenticazione Facebook, devi apportare le modifiche in codice nativo dell'applicazione Cordova in Java, Objective-C o Swift. Configura ciascuna piattaforma separatamente. Utilizza l'ambiente di sviluppo nativo per apportare modifiche nel codice nativo, ad esempio in Android Studio o Xcode.

## Prima di cominciare
{: #facebook-auth-before}
* Devi disporre di una risorsa protetta da {{site.data.keyword.amashort}} e di un progetto Cordova strumentato con l'SDK client {{site.data.keyword.amashort}}.  Per ulteriori informazioni, vedi [Introduzione a {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) e [Configurazione del plugin Cordova](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html).
* Proteggi manualmente la tua applicazione di backend con l'SDK server {{site.data.keyword.amashort}}. Per ulteriori informazioni, vedi [Protezione delle risorse](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).
* Crea un ID applicazione Facebook. Per ulteriori informazioni, vedi [Ottenimento di un ID applicazione Facebook dal portale sviluppatori Facebook](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).
* (facoltativo) Acquisisci dimestichezza con le seguenti sezioni:
   * [Abilitazione dell'autenticazione Facebook nelle applicazioni Android](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html)
   * [Abilitazione dell'autenticazione Facebook nelle applicazioni iOS](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html)


## Configurazione della piattaforma Android
{: #facebook-auth-cordova-android}

I passi richiesti per configurare la piattaforma Android di un'applicazione Cordova per l'integrazione dell'autenticazione Facebook sono molto simili a quelli richiesti per le applicazioni Android native. Per ulteriori informazioni, vedi [Abilitazione dell'autenticazione Facebook nelle applicazioni Android](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html). Completa la seguente procedura:

* Configurazione dell'applicazione Facebook per la piattaforma Android
* Configurazione di {{site.data.keyword.amashort}} per l'autenticazione Facebook
* Configurazione dell'SDK client {{site.data.keyword.amashort}} per Android

La sola differenza quando configuri le applicazioni Cordova è che devi inizializzare l'SDK client {{site.data.keyword.amashort}} nel tuo codice JavaScript invece che nel codice Java. L'API `FacebookAuthenticationManager` continua a dover essere registrata nel tuo codice nativo.

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

1. 	Fai clic sulla tua root del progetto nel riquadro sinistro di Xcode e seleziona **Build Phases**.

1. Aggiungi il file `FacebookSDK.framework` all'elenco di librerie collegate in **Link Binary With Libraries**.

 Vedi [Configurazione della piattaforma iOS per l'autenticazione Facebook](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html). Registra l'API `IMFFacebookAuthenticationHandler` in codice nativo come descritto nella sezione **Inizializzazione dell'SDK client {{site.data.keyword.amashort}}**. Non inizializzare `IMFClient` nel tuo codice nativo.

Aggiungi la seguente riga al metodo `application:openURL:sourceApplication:annotation` del tuo delegato dell'applicazione. Questo codice assicura che tutti i plugin Cordova vengano informati dei rispettivi eventi.

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```

## Inizializzazione dell'SDK client {{site.data.keyword.amashort}}
{: #facebook-auth-cordova-init}

Utilizza il seguente codice JavaScript nella tua applicazione Cordova per inizializzare l'SDK client {{site.data.keyword.amashort}}.

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```

Sostituisci *applicationRoute* e *applicationGUID* con i valori ottenuti per **Rotta** e **GUID applicazione** da **Opzioni mobili**.

## Verifica dell'autenticazione
{: #facebook-auth-cordova-test}
Dopo che l'SDK client è stato inizializzato e il gestore autenticazione Facebook è stato registrato, puoi iniziare a effettuare richieste al tuo backend mobile.

### Prima di cominciare
Devi utilizzare il contenitore tipo {{site.data.keyword.mobilefirstbp}} e disporre già di una risorsa protetta da {{site.data.keyword.amashort}} all'endpoint `/protected`. Per ulteriori informazioni, vedi [Protezione delle risorse](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Prova a inviare una richiesta all'endpoint protected del backend mobile appena creato nel tuo browser. Apri il seguente URL: `{applicationRoute}/protected`. Ad esempio: `http://my-mobile-backend.mybluemix.net/protected`
<br/>L'endpoint `/protected` di un backend mobile creato con il contenitore tipo MobileFirst Services Starter è protetto con {{site.data.keyword.amashort}}. Nel tuo browser viene restituito un messaggio `Unauthorized`. Questo messaggio viene restituito perché a questo endpoint possono accedere solo le applicazioni mobili strumentate con l'SDK client{{site.data.keyword.amashort}}.

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

1. Esegui la tua applicazione. Viene visualizzata una schermata di accesso a Facebook:

	![immagine](images/android-facebook-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![immagine](images/ios-facebook-login.png)

	> Questa schermata può avere un aspetto lievemente differente se sul tuo dispositivo non è installata l'applicazione Facebook o se non sei attualmente collegato a Facebook.

1. Fai clic su **OK** per autorizzare {{site.data.keyword.amashort}} a usare la tua identità utente Facebook per scopi di autenticazione.

1. 	Quando la tua richiesta ha esito positivo, nel programma di utilità LogCat o nella console Xcode è presente il seguente output:

	![Messaggio di esito positivo dell'autenticazione Facebook per Android](images/android-facebook-login-success.png)

	![Messaggio di esito positivo dell'autenticazione Facebook per iOS ](images/ios-facebook-login-success.png)
