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

# Abilitazione dell'autenticazione Facebook per le applicazioni Android
{: #facebook-auth-android}

Per utilizzare Facebook come provider di identità nelle tue applicazioni client Android {{site.data.keyword.amafull}} aggiungi e configura il client Android per accedere alla tua applicazione Facebook sul sito Facebook for Developers.
{:shortdesc}

## Prima di cominciare
{: #before-you-begin}

È necessario disporre di:

* Un'istanza di un servizio {{site.data.keyword.amafull}} e di un'applicazione {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni su come creare un'applicazione di back-end {{site.data.keyword.Bluemix_notm}}, vedi [Introduzione](index.html).
* L'URL della tua applicazione di back-end (**Rotta applicazione**). Avrai bisogno di questo valore per inviare le richieste agli endpoint protetti della tua applicazione di back-end.
* Il tuo valore **TenantID**. Apri il tuo servizio nel dashboard {{site.data.keyword.amashort}}. Fai clic sul pulsante **Opzioni per dispositivi mobili**. Il valore `tenantId` (noto anche come `appGUID`)  viene visualizzato nel campo **GUID applicazione / TenantId**. Avrai bisogno di questo valore per inizializzare il gestore autorizzazione.
* La tua **Regione** {{site.data.keyword.Bluemix_notm}}. Puoi trovare la tua regione {{site.data.keyword.Bluemix_notm}} corrente nell'intestazione, accanto all'icona **Avatar** ![Icona Avatar](images/face.jpg "Icona Avatar"). Il valore della regione visualizzato deve essere uno dei seguenti: `Stati Uniti Sud`, `Regno Unito` o `Sydney` e corrisponde al valore delle SDK richiesto nel codice WebView Javascript: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` o `BMSClient.REGION_UK`. Avrai bisogno di questo valore per inizializzare il client {{site.data.keyword.amashort}}.
* Un progetto Android configurato per lavorare con Gradle. Il progetto non deve essere instrumentato con l'SDK client {{site.data.keyword.amashort}}.  
* Un'applicazione Facebook con una piattaforma Android sul [sito Facebook for Developers ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developers.facebook.com/){: new_window} .

**Importante:** non devi necessariamente installare separatamente l'SDK Facebook (`com.facebook.FacebookSdk`). L'SDK Facebook viene installato automaticamente da Gradle quando aggiungi l'SDK client Facebook {{site.data.keyword.amashort}}. Puoi saltare questo passo quando aggiungi la piattaforma Android nel sito Facebook for Developers.

## Configurazione dell'applicazione sul sito Facebook  for Developers
{: #facebook-auth-android-config}

Dal sito web Facebook for Developers:

1. Accedi al tuo account nel [sito Web Facebook for Developers ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developers.facebook.com){: new_window}.

1. Da **Products List**, scegli **Facebook Login**.

1. Aggiungi o configura la piattaforma Android.

1. Specifica il nome pacchetto della tua applicazione Android nel prompt Google Play Package Name. Per trovare il nome pacchetto della tua applicazione Android ricerca `<manifest ..... package="{your-package-name}">` nel file `AndroidManifest.xml` nel progetto Android Studio.

1. Specifica il nome classe della tua attività principale nel prompt **Class Name**. Il nome della classe è il valore della proprietà `android:name` nel simbolo dell'attività. Se è presente più di una attività nel file `AndroidManifest.xml`, cerca l'attività che contiene `<intent-filter>`:

	```XML
	<activity
		android:name=".MainActivity"
		android:label="@string/app_name">
		<intent-filter>
			<action android:name="android.intent.action.MAIN"/>
			<category android:name="android.intent.category.LAUNCHER"/>
		</intent-filter>
	</activity>
	```
	{: codeblock}

1. Per fare in modo che Facebook garantisca l'autenticità della tua applicazione, devi specificare un hash del tuo certificato sviluppatore SHA1.

	**Ulteriori informazioni sulla sicurezza Android:** il sistema operativo Android richiede che tutte le applicazioni installate su un dispositivo Android siano firmate con un certificato sviluppatore. L'applicazione Android può essere messa a punto in due modalità: debug e rilascio.

	Utilizza certificati differenti per le modalità di debug e rilascio.  I certificati utilizzati per firmare le applicazioni Android in modalità di debug sono forniti con l'SDK Android, che viene di norma installato automaticamente da Android Studio. Quando vuoi rilasciare la tua applicazione al negozio Google Play, devi firmare la tua applicazione con un altro certificato che di norma generi tu stesso.

	Puoi immettere due serie di hash chiave con Facebook: un hash chiave per le applicazioni messe a punto in modalità di debug con un certificato di debug e un altro hash chiave per le applicazioni messe a punto in modalità di rilascio con un certificato di rilascio. Per ulteriori informazioni, vedi il documento relativo alla [firma delle tue applicazioni Android ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://developer.android.com/tools/publishing/app-signing.html){: new_window}.

1. Il keystore che contiene il certificato che stai usando per l'ambiente di sviluppo è memorizzato nel file `~/.android/debug.keystore`. La password keystore predefinita è: `android`. Utilizza questo certificato per mettere a punto applicazioni in modalità di debug.

1. Recupera l'hash chiave del tuo certificato di modalità di debug:

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore | openssl sha1 -binary | openssl base64
	```
	{: codeblock}

	**Suggerimento**: puoi utilizzare la stessa sintassi per recuperare l'hash chiave del tuo certificato di modalità di rilascio. Sostituisci percorso keystore e alias nel comando.

1. Copia e incolla l'hash chiave che hai ottenuto con il comando **keytool** a un prompt Development/Release Key Hashes nel sito Facebook for Developers.

	**Suggerimento**: se intendi utilizzare questa funzione, considera l'abilitazione di SSO (single sign on).

1. Fai clic su **Save Settings**.

## Configurazione del servizio {{site.data.keyword.amashort}} per l'autenticazione Facebook
{: #facebook-auth-android-mca}

Dopo che hai configurato l'ID applicazione Facebook e la tua applicazione Facebook perché serva client Android, puoi abilitare l'autenticazione Facebook con il dashboard {{site.data.keyword.amashort}}.

1. Apri il tuo servizio {{site.data.keyword.amashort}} nel dashboard.
1. Dalla scheda **Manage**, attiva **Authorization**.
1. Espandi la sezione **Facebook**.
1. Aggiungi l'**ID dell'applicazione Facebook**.
1. Fai clic su **Save**.

## Configurazione dell'SDK Android client {{site.data.keyword.amashort}} per l'autenticazione Facebook
{: #facebook-auth-android-sdk}

Per configurare l'SDK client per Android, utilizza il gestore dipendenze Gradle in Android Studio.

1.  Apri il file `build.gradle` del tuo modulo applicazione.
Il tuo progetto Android può avere due file `build.gradle`:  per il progetto e per il modulo applicazione. Utilizza il file di modulo applicazione.

1. Trova la sezione delle dipendenze del file `build.gradle` e aggiungi una nuova dipendenza di compilazione per l'SDK client:

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

	**Nota:** Puoi rimuovere la dipendenza sul modulo `core` del gruppo `com.ibm.mobilefirstplatform.clientsdk.android`, se è presente nel tuo file. Il modulo `facebookauthentication` scarica il modulo `core`, così come automaticamente l'SDK proprio di Facebook.

	Dopo che hai salvato i tuoi aggiornamenti, il modulo `facebookauthentication` scarica e installa tutte le SDK necessarie nel tuo progetto Android.

1. Sincronizza il tuo progetto con Gradle facendo clic su **Tools > Android > Sync project with Gradle Files**.

1. Apri il file `res/values/strings.xml` e aggiungi una stringa `facebook_app_id` che contiene il tuo ID applicazione Facebook:

	```XML
	<resources>
		<string name="app_name">HelloWorld</string>
		<string name="action_settings">Settings</string>
		<string name="facebook_app_id">522733366802111</string>
	</resources>
	```
	{: codeblock}

1. Nel file `AndroidManifest.xml` del tuo progetto Android:
	* Aggiungi l'autorizzazione di accesso a internet sotto l'elemento `<manifest>`:

		```XML
	<uses-permission android:name="android.permission.INTERNET" />
		```
		{: codeblock}

	* Aggiungi i metadati richiesti per l'SDK Facebook all'elemento `<application>`:

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

			<activity android:name="com.facebook.FacebookActivity"
				android:configChanges="keyboard|keyboardHidden|screenLayout|screenSize|orientation"
				android:theme="@android:style/Theme.Translucent.NoTitleBar"
				android:label="@string/app_name" />
		</application>
		```
		{: codeblock}

1. Inizializza l'SDK client e registra il gestore autenticazione. Inizializza l'SDK client {{site.data.keyword.amashort}} passando i parametri **context** e **region**.

	Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `onCreate` dell'attività principale nella tua applicazione Android.<br/>

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

	BMSClient.getInstance().setAuthorizationManager(
					MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));

	FacebookAuthenticationManager.getInstance().register(this);
	```
	{: codeblock}

   * Sostituisci `BMSClient.REGION_UK` con la regione appropriata.
   * Sostituisci `<MCAServiceTenantId>` con il valore `tenantId`

	Per ulteriori informazioni su come ottenere questi valori consulta [Prima di cominciare](#before-you-begin)).

	**Nota:** se la tua applicazione Android è alla versione 6.0 (Livello API 23) o successiva, ti devi assicurare che l'applicazione disponga di una chiamata `android.permission.GET_ACCOUNTS` prima di richiamare il `register`. Per ulteriori informazioni, vedi [questo argomento ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.android.com/training/permissions/requesting.html){: new_window} sul sito Android Developers.

1. Aggiungi il seguente codice alla tua attività:

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}


## Verifica dell'autenticazione
{: #testing_auth}

Dopo che l'SDK client è stato inizializzato e il gestore autenticazione Facebook è stato registrato, puoi iniziare a effettuare richieste al tuo backend mobile.

### Prima di cominciare il test
{: #facebook-auth-android-testing-before}

Devi utilizzare il contenitore tipo {{site.data.keyword.mobilefirstbp}} e disporre già di una risorsa protetta da {{site.data.keyword.amashort}} all'endpoint `/protected`. Se devi configurare un endpoint `/protected`, consulta [Protezione delle risorse](protecting-resources.html).

1. Prova a inviare una richiesta all'endpoint protetto del backend mobile appena creato nel tuo browser. Apri il seguente URL:  

	`{applicationRoute}/protected`. Ad esempio: `http://my-mobile-backend.mybluemix.net/protected`.  

	L'endpoint `/protected` di un'applicazione di backend mobile creato con il contenitore tipo MobileFirst Services Starter è protetto con {{site.data.keyword.amashort}}. Nel tuo browser viene restituito un messaggio `Unauthorized`. Questo messaggio viene restituito perché a questo endpoint possono accedere solo le applicazioni mobili strumentate con l'SDK client{{site.data.keyword.amashort}}.

1. Utilizza la tua applicazione Android per effettuare una richiesta allo stesso endpoint. Aggiungi il seguente codice dopo che hai inizializzato `BMSClient` e registrato `FacebookAuthenticationManager`.

	```Java
	Request request = new Request("{applicationRoute}/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp", MCAAuthorizationManager.getInstance().getUserIdentity().toString());
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

1. Esegui la tua applicazione. Viene visualizzata una schermata di accesso Facebook.

	![immagine](images/android-facebook-login.png)

	Questa schermata può avere un aspetto lievemente differente se sul tuo dispositivo non è installata l'applicazione Facebook o se non sei attualmente collegato a Facebook.

1. Fai clic su **OK** per autorizzare {{site.data.keyword.amashort}} a usare la tua identità utente Facebook per scopi di autenticazione.

1. Quando la tua richiesta ha esito positivo, nel programma di utilità LogCat è presente il seguente output:

	![immagine](images/android-facebook-login-success.png)

	Puoi anche aggiungere la funzionalità di disconnessione aggiungendo il seguente codice:

	```
	FacebookAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
	```
	{: codeblock}

	Se richiami questo codice dopo che un utente ha eseguito l'accesso con Facebook, l'utente viene disconnesso da Facebook. Quando un utente prova ad eseguire nuovamente l'accesso, gli vengono richieste le sue credenziali Facebook.

	Il valore per `listener` passato alla funzione di disconnessione può essere `null`.
