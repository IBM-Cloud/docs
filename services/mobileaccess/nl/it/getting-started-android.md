---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-10"
---
{:shortdesc: .shortdesc}
{:screen:.screen}


# Configurazione dell'SDK Android
{: #getting-started-android}

Strumenta la tua applicazione Android con l'SDK client {{site.data.keyword.amafull}}, inizializza l'SDK e effettua richieste a risorse protette e non protette.

{:shortdesc}

## Prima di cominciare
{: #before-you-begin}
È necessario disporre di:
* Un'istanza di un'applicazione  {{site.data.keyword.Bluemix_notm}} che è protetta da un servizio {{site.data.keyword.amashort}}. Per ulteriori informazioni su come creare un'applicazione di back-end {{site.data.keyword.Bluemix_notm}}, vedi [Introduzione](index.html).
* I valori del parametro del servizio. Apri il tuo servizio nel dashboard {{site.data.keyword.Bluemix_notm}}. Fai clic su **Opzioni mobili**. I valori `applicationRoute` e `tenantId` (conosciuti anche come `appGUID`)  sono visualizzati nei campi **Rotta** and **GUID applicazione / TenantId**. Avrai bisogno di questi valori per inizializzare l'SDK e per inviare le richieste all'applicazione di backend.
* Un progetto Android Studio, configurato per lavorare con Gradle. Per ulteriori informazioni su come configurare il tuo ambiente di sviluppo Android, vedi gli [strumenti per sviluppatori Google](http://developer.android.com/sdk/index.html).

## Installazione dell'SDK client {{site.data.keyword.amashort}}
{: #install-mca-sdk}

L'SDK client {{site.data.keyword.amashort}} viene distribuito con Gradle, un gestore dipendenze per i progetti Android. Gradle scarica automaticamente le risorse utente dai repository e le rende disponibili alla tua applicazione Android.

1. Crea un progetto Android Studio oppure apri un progetto esistente.

1. Apri il file `build.gradle` per la tua applicazione (**non** il file `build.gradle` del progetto).

1. Trova la sezione **dependencies** del file `build.gradle`.  Aggiungi una dipendenza di compilazione per l'SDK client {{site.data.keyword.amashort}}:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'core',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
```

1. Sincronizza il tuo progetto con Gradle. Fai clic su **Tools &gt; Android &gt; Sync Project with Gradle Files**.

1. Apri il file `AndroidManifest.xml` per il tuo progetto Android. Aggiungi l'autorizzazione di accesso a internet sotto l'elemento `<manifest>`:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
```

## Inizializzazione dell'SDK client {{site.data.keyword.amashort}}
{: #initalize-mca-sdk}

Inizializza l'SDK client passando i parametri **context** e **region** al metodo `initialize`. Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `onCreate` dell'attività principale nella tua applicazione Android.

```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);
					
  BMSClient.getInstance().setAuthorizationManager(
                 MCAAuthorizationManager.createInstance(this, "MCAServiceTenantId"));

```

   * Sostituisci `BMSClient.REGION_UK` con la regione appropriata.  Per visualizzare la tua regione {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona **Avatar** ![icona Avatar](images/face.jpg "icona Avatar")  nella barra del menu per aprire il widget **Account e supporto**. Il valore della regione deve essere uno dei seguenti: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` o `BMSClient.REGION_UK`.
   * Sostituisci "MCAServiceTenantId" con il valore **tenantId** (consulta [Prima di cominciare](#before-you-begin)). 

## Effettuare una richiesta alla tua applicazione di back-end mobile
{: #request}

Dopo che l'SDK client {{site.data.keyword.amashort}} è stato inizializzato, puoi iniziare a effettuare richieste alla tua applicazione di back-end mobile.

1. Prova a inviare una richiesta a un endpoint protetto della tua nuova applicazione di back-end mobile. Nel tuo browser, apri il seguente URL: `{applicationRoute}/protected` (ad esempio `http://my-mobile-backend.mybluemix.net/protected`).   Per informazioni su come ottenere il valore `{applicationRoute}`, consulta   [Prima di cominciare](#before-you-begin). 
	
	L'endpoint `/protected` di un'applicazione di backend mobile creato con il contenitore tipo MobileFirst Services Starter è protetto con {{site.data.keyword.amashort}}. Nel tuo browser viene restituito un messaggio `Unauthorized` perché a questo endpoint possono accedere solo le applicazioni mobili strumentate con l'SDK client {{site.data.keyword.amashort}}.

1. Utilizza la tua applicazione Android per effettuare una richiesta allo stesso endpoint. Aggiungi il seguente codice dopo che hai inizializzato `BMSClient`:

	```Java
	Request request = new Request("/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
		}
		@Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
			if (null != t) {
				Log.d("Myapp", "onFailure :: " + t.getMessage());
			} else if (null != extendedInfo) {
				Log.d("Myapp", "onFailure :: " + extendedInfo.toString());
			} else {
				Log.d("Myapp", "onFailure :: " + response.getResponseText());
			}
		}
	});
	```

1. Quando la tua richiesta ha esito positivo, vedrai il seguente output nello strumento di utilità LogCat:

	![immagine](images/getting-started-android-success.png)

## Fasi successive
{: #next-steps}

Quando ti sei connesso all'endpoint protetto, non è stata richiesta alcuna credenziale. Per richiedere ai tuoi utenti di accedere alla tua applicazione, devi configurare l'autenticazione Facebook, Google o personalizzata.
* [Facebook](facebook-auth-android.html)
* [Google](google-auth-android.html)
* [Personalizzata](custom-auth-android.html)
