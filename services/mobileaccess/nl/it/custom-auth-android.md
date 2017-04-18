---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---

Il servizio {{site.data.keyword.amafull}} è stato sostituito con il servizio {{site.data.keyword.appid_full}}.

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Configurazione dell'autenticazione personalizzata per l'applicazione Android {{site.data.keyword.amashort}}
{: #custom-android}


Configura la tua applicazione Android con l'autenticazione personalizzata per utilizzare l'SDK client {{site.data.keyword.amashort}} e connettere la tua applicazione a {{site.data.keyword.Bluemix}}.

## Prima di cominciare
{: #before-you-begin}
Prima di iniziare devi disporre di:

* Una risorsa che sia protetta da un'istanza del servizio {{site.data.keyword.amashort}} configurata per utilizzare un provider di identità personalizzato (consulta [Configurazione dell'autenticazione personalizzata](custom-auth-config-mca.html)).  
* Il tuo valore **TenantID**. Apri il tuo servizio nel dashboard {{site.data.keyword.amashort}}. Fai clic sul pulsante **Opzioni per dispositivi mobili**. Il valore `tenantId` (noto anche come `appGUID`)  viene visualizzato nel campo **GUID applicazione / TenantId**. Avrai bisogno di questo valore per inizializzare il gestore autorizzazione.
* Il tuo nome **Realm**. Questo è il valore che hai specificato nel campo **Nome realm** della sezione **Personalizzato** nella scheda **Gestione** del dashboard {{site.data.keyword.amashort}}.
* L'URL della tua applicazione di back-end (**Rotta applicazione**). Avrai bisogno di questo valore per inviare le richieste agli endpoint protetti della tua applicazione di back-end.
* La tua **Regione** {{site.data.keyword.Bluemix_notm}}. Puoi trovare la tua regione {{site.data.keyword.Bluemix_notm}} corrente nell'intestazione, accanto all'icona **Avatar** ![Icona Avatar](images/face.jpg "Icona Avatar"). Il valore della regione visualizzato deve essere uno dei seguenti: `Stati Uniti Sud`, `Regno Unito` o `Sydney` e corrisponde ai valori delle SDK richiesti nel codice WebView Javascript: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` o `BMSClient.REGION_UK`. Avrai bisogno di questo valore per inizializzare il client {{site.data.keyword.amashort}}.

Per ulteriori informazioni, consulta:
 * [Introduzione a {{site.data.keyword.amashort}}](getting-started.html)
 * [Configurazione dell'SDK Android](getting-started-android.html)
 * [Utilizzo di un provider di identità personalizzato](custom-auth.html)
 * [Creazione di un provider di identità personalizzato](custom-auth-identity-provider.html)
 * [Configurazione di {{site.data.keyword.amashort}} per l'autenticazione personalizzata](custom-auth-config-mca.html)



## Inizializzazione dell'SDK client {{site.data.keyword.amashort}}
{: #custom-android-initialize}
Se disponi di un'applicazione Android strumentata con l'SDK Android {{site.data.keyword.amashort}} puoi saltare questa sezione.
1. Nel tuo progetto Android in Android Studio, apri il file `build.gradle` del tuo modulo applicazione (non il progetto `build.gradle`).

1. Nel file `build.gradle`, trova la sezione `dependencies` e controlla che esista la seguente dipendenza:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',
        name:'core',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// altre dipendenze
	}
	```
	{: codeblock}

1. Sincronizza il tuo progetto con Gradle. Fai clic su **Tools > Android > Sync Project with Gradle Files**.

1. Apri il file `AndroidManifest.xml` del tuo progetto Android.
Aggiungi l'autorizzazione di accesso a internet sotto l'elemento `<manifest>`:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```
	{: codeblock}

1. Inizializza l'SDK.  
	Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `onCreate` dell'attività principale nella tua applicazione Android.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);
	```
	{: codeblock}

Sostituisci `BMSClient.REGION_UK` con la regione {{site.data.keyword.amashort}}. Per ulteriori informazioni su come ottenere questi valori consulta [Prima di cominciare](#before-you-begin).


## Interfaccia AuthenticationListener
{: #custom-android-authlistener}

L'SDK client {{site.data.keyword.amashort}} fornisce l'interfaccia `AuthenticationListener` per consentirti di implementare un flusso di autenticazione personalizzato. L'interfaccia `AuthenticationListener` espone tre metodi richiamati in fasi differenti durante il processo di autenticazione.

### Metodo onAuthenticationChallengeReceived
{: #custom-onAuth}
Richiama questo metodo quando una richiesta di verifica dell'autenticazione personalizzata viene ricevuta dal servizio {{site.data.keyword.amashort}}.

```Java
void onAuthenticationChallengeReceived(AuthenticationContext authContext, JSONObject challenge, Context context);
```
{: codeblock}


#### Argomenti
{: #custom-android-onAuth-arg}

* `AuthenticationContext`: fornito dall'SDK client {{site.data.keyword.amashort}} per consentirti di notificare a tua volta le risposte alla richiesta di verifica dell'autenticazione oppure gli errori durante la raccolta di credenziali.  Un esempio è un utente che annulla l'autenticazione.
* `JSONObject`: contiene una richiesta di verifica dell'autenticazione personalizzata, come restituito da un provider di identità personalizzato.
* `Context`: un riferimento al contesto Android che è stato utilizzato quando è stata inviata la richiesta. Di norma, questo argomento rappresenta un'attività Android.

Richiamando il metodo `onAuthenticationChallengeReceived`, l'SDK client {{site.data.keyword.amashort}} sta delegando il controllo allo sviluppatore.  Il servizio attende le credenziali. Lo sviluppatore deve raccogliere le credenziali e notificarle a sua volta all'SDK client {{site.data.keyword.amashort}} utilizzando
uno dei metodi di interfaccia `AuthenticationContext`.

### Metodo onAuthenticationSuccess
{: #custom-android-authlistener-onsuccess}
Richiama questo metodo dopo un'autenticazione con esito positivo. Gli argomenti includono il contesto Android e un JSONObject facoltativo che contiene informazioni estese sull'esito positivo dell'autenticazione.
```Java
void onAuthenticationSuccess(Context context, JSONObject info);
```
{: codeblock}

### Metodo onAuthenticationFailure
{: #custom-android-authlistener-onfail}
Richiama questo metodo dopo che l'autenticazione ha esito negativo. Gli argomenti includono il contesto Android e un `JSONObject` facoltativo che contiene informazioni estese sull'esito negativo dell'autenticazione.
```Java
void onAuthenticationFailure(Context context, JSONObject info);
```
{: codeblock}

## Interfaccia AuthenticationContext
{: #custom-android-authcontext}

L'`AuthenticationContext` viene fornito come un argomento al metodo `onAuthenticationChallengeReceived` di
un `AuthenticationListener` personalizzato. Devi raccogliere le credenziali e utilizzare i metodi `AuthenticationContext` per restituire le credenziali all'SDK client {{site.data.keyword.amashort}} o notificare un errore. Utilizza uno dei seguenti metodi.

```Java
void submitAuthenticationChallengeAnswer(JSONObject answer);
```
{: codeblock}

```Java
void submitAuthenticationFailure (JSONObject info);
```
{: codeblock}

## Implementazione di esempio di un AuthenticationListener personalizzato
{: #custom-android-samplecustom}

Questo esempio AuthenticationListener è progettato per funzionare con un provider di identità personalizzato. Puoi scaricare questo esempio dal [Repository Github ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}.

```Java
package com.ibm.helloworld;
import android.content.Context;
import android.util.Log;
import com.ibm.mobilefirstplatform.clientsdk.android.security.mca.api.AuthenticationContext;
import com.ibm.mobilefirstplatform.clientsdk.android.security.mca.api.AuthenticationListener;
import org.json.JSONException;
import org.json.JSONObject;

public class CustomAuthenticationListener implements AuthenticationListener {
	@Override
	public void onAuthenticationChallengeReceived (AuthenticationContext authContext,
											JSONObject challenge, Context context) {

		log("onAuthenticationChallengeResceived :: " + challenge.toString());

		// In questo esempio, l'AuthenticationListener restituisce immediatamente una
		// serie di credenziali codificata (hardcoded). In uno scenario realistico, questo è il punto
		// in cui lo sviluppatore mostra uno schermo di accesso, raccoglie le credenziali e richiama
		// l'API authContext.submitAuthenticationChallengeAnswer()

		JSONObject challengeResponse = new JSONObject();
		try {
			challengeResponse.put("username", "john.lennon");
			challengeResponse.put("password", "12345");
			authContext.submitAuthenticationChallengeAnswer(challengeResponse);
		} catch (JSONException e){

			// Se si è verificato un errore di raccolta delle credenziali, devi
		// segnalarlo all'AuthenticationContext. In caso contrario, l'SDK client Mobile Client
		// Access resterà in uno stato di attesa delle credenziali
		// per sempre

			log("Questo non dovrebbe mai accadere...");
			authContext.submitAuthenticationFailure(null);
		}
	}

	@Override
	public void onAuthenticationSuccess (Context context, JSONObject info) {
		log("onAuthenticationSuccess :: " + info.toString());
	}

	@Override
	public void onAuthenticationFailure (Context context, JSONObject info) {
		log("onAuthenticationFailure :: " + info.toString());
	}

	private void log(String text){
		Log.d("CustomAuthListener", text);
	}
}
```
{: codeblock}

## Registrazione di un AuthenticationListener personalizzato
{: #custom-android-register}

Dopo che hai creato un AuthenticationListener personalizzato, registralo presso `BMSClient` prima di iniziare a utilizzare il listener. Aggiungi il seguente codice alla tua applicazione. Questo codice deve essere richiamato prima di inviare qualsiasi richiesta alle tue risorse protette.

```Java
MCAAuthorizationManager mcaAuthorizationManager = 
      MCAAuthorizationManager.createInstance(this.getApplicationContext(),"<MCAServiceTenantId>");
mcaAuthorizationManager.registerAuthenticationListener(realmName, new CustomAuthenticationListener());
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);

```
{: codeblock}


Nel codice:
* Sostituisci `MCAServiceTenantId` con il valore **TenantId** (consulta [Prima di cominciare](##before-you-begin)).
* Utilizza il `realmName` che hai specifico nel dashboard {{site.data.keyword.amashort}} (consulta [Configurazione dell'autenticazione personalizzata](custom-auth-config-mca.html)).


## Verifica dell'autenticazione
{: #custom-android-testing}
Dopo che l'SDK client è stato inizializzato e che un AuthenticationListener personalizzato è stato registrato, puoi iniziare a effettuare richieste alla tua applicazione di back-end mobile.

### Prima del tuo test
{: #custom-android-testing-before}
Devi disporre di un'applicazione con una risorsa protetta da {{site.data.keyword.amashort}} all'endpoint `/protected`.


1. Invia una richiesta all'endpoint protetto (`{applicationRoute}/protected`) dell'applicazione di backend mobile dal tuo browser, ad esempio `http://my-mobile-backend.mybluemix.net/protected`. Per informazioni su come ottenere il valore `{applicationRoute}`, consulta   [Prima di cominciare](#before-you-begin).

1. L'endpoint `/protected` di un'applicazione di back-end mobile creato con il contenitore tipo {{site.data.keyword.mobilefirstbp}} è protetto con {{site.data.keyword.amashort}}. All'endpoint possono accedere solo le applicazioni mobili strumentate con l'SDK client {{site.data.keyword.amashort}}. Di conseguenza, nel tuo browser viene visualizzato un messaggio `Unauthorized`.

1. Utilizza la tua applicazione Android per effettuare una richiesta allo stesso endpoint protetto che include `{applicationRoute}`. Aggiungi il seguente codice dopo che hai inizializzato `BMSClient` e registrato il tuo AuthenticationListener personalizzato.

	```Java
	Request request = new Request("{applicationRoute}/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp",  MCAAuthorizationManager.getInstance().getUserIdentity().toString());
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
	{: codeblock}

1. 	Quando la tua richiesta ha esito positivo, nello strumento LogCat è presente il seguente output:

	![immagine](images/android-custom-login-success.png)

 Puoi anche aggiungere la funzionalità di disconnessione aggiungendo il seguente codice:

 ```Java
 MCAAuthorizationManager.getInstance().logout(getApplicationContext(), listener);
 ```
 {: codeblock}


 Se richiami questo codice dopo che un utente ha eseguito l'accesso, l'utente viene disconnesso. Quando l'utente prova ad eseguire nuovamente l'accesso, deve rispondere nuovamente alla richiesta di verifica proveniente dal server.

 Il valore per `listener` passato alla funzione di disconnessione può essere `null`.
