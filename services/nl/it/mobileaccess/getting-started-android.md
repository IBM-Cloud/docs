---

copyright:
  years: 2015, 2016
  
---

# Configurazione dell'SDK Android
{: #getting-started-android}

Strumenta la tua applicazione Android con l'SDK client {{site.data.keyword.amashort}}, inizializza l'SDK e effettua richieste a risorse protette e non protette.

## Prima di cominciare
{: #before-you-begin}
* Devi disporre di un'istanza di un backend mobile protetto dal servizio {{site.data.keyword.amashort}}. Per ulteriori informazioni su come creare un backend mobile, consulta [Introduzione](getting-started.html).
* Configura Android Studio e l'SDK Android Studio. Per ulteriori informazioni su come configurare il tuo ambiente di sviluppo Android, vedi gli [strumenti per sviluppatori Google](http://developer.android.com/sdk/index.html).


## Installazione dell'SDK client {{site.data.keyword.amashort}}
{: #install-mca-sdk}

L'SDK client {{site.data.keyword.amashort}} viene distribuito con Gradle, un gestore dipendenze per i progetti Android. Gradle scarica automaticamente le risorse utente dai repository e le rende disponibili alla tua applicazione Android.

1. Crea un progetto Android Studio oppure apri un progetto esistente.

1. Apri il file `build.gradle`.
**Suggerimento**: il tuo progetto Android potrebbe avere due file `build.gradle`: per il progetto e per il modulo applicazione. Utilizza il file di modulo applicazione.

1. Trova la sezione **Dependencies** del file `build.gradle`.  Aggiungi una dipendenza di compilazione per l'SDK client {{site.data.keyword.amashort}}:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'core',
        version: '1.+',
        ext: 'aar',
        transitive: true
    	// altre dipendenze  
}
```

1. Sincronizza il tuo progetto con Gradle. Fai clic su **Tools &gt; Android &gt; Sync Project with Gradle Files**.

1. Apri il file `AndroidManifest.xml` per il tuo progetto Android. Aggiungi l'autorizzazione di accesso a internet sotto l'elemento `<manifest>`:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
```

## Inizializzazione dell'SDK client {{site.data.keyword.amashort}}
{: #initalize-mca-sdk}

Inizializza l'SDK passando i parametri context, applicationGUID e applicationRoute al metodo `initialize`.


1. Dalla pagina principale del dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sulla tua applicazione. Fai clic su **Opzioni mobili**. Per inizializzare l'SDK ti servono i valori rotta applicazione (**Application Route**) e GUID applicazione (**Application GUID**).

2. Inizializza l'SDK client {{site.data.keyword.amashort}} nella tua applicazione Android.  Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `onCreate` dell'attività principale nella tua applicazione Android.
<br/>Sostituisci *applicationRoute* e *applicationGUID* con i valori da **Opzioni mobili** nel dashboard {{site.data.keyword.Bluemix_notm}}.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");
```


## Effettuazione di una richiesta al tuo backend mobile
{: #request}

Dopo che l'SDK client {{site.data.keyword.amashort}} è stato inizializzato, puoi iniziare a effettuare richieste al tuo backend mobile.

1. Prova a inviare una richiesta a un endpoint protetto del tuo nuovo backend mobile. Nel tuo browser, apri il seguente URL: `{applicationRoute}/protected`. Ad esempio: `http://my-mobile-backend.mybluemix.net/protected`
<br/>L'endpoint `/protected` di un backend mobile creato con il contenitore tipo MobileFirst Services Starter è protetto con {{site.data.keyword.amashort}}. Nel tuo browser viene restituito un messaggio `Unauthorized` perché a questo endpoint possono accedere solo le applicazioni mobili strumentate con l'SDK client {{site.data.keyword.amashort}}.

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
