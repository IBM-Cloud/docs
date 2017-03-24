---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:pre: .pre}

# Configurazione dell'SDK Android
{: #android-sdk}

Crea le tue applicazioni Android con l'SDK client {{site.data.keyword.appid_short}}, inizializza l'SDK, autentica gli utenti ed effettua le richieste alle risorse protette e non protette.
{:shortdesc}


## Prima di cominciare
{: #before-you-begin}

Hai bisogno delle seguenti informazioni:
  * Un'istanza del servizio {{site.data.keyword.appid_short_notm}}.
  * Il tuo ID tenant.
    * Nella scheda **Credenziali del servizio** del tuo dashboard del servizio, fai clic su **Visualizza credenziali**. Il tuo ID tenant viene visualizzato nel campo **ID tenant**. Questo valore viene utilizzato per inizializzare la tua applicazione.
  * La tua regione {{site.data.keyword.Bluemix}}. Puoi trovare la tua regione cercando nella IU. Il valore viene utilizzato per inizializzare la tua applicazione.
    <table> <caption> Tabella 1. Regioni {{site.data.keyword.Bluemix_notm}} e valori SDK corrispondenti </caption>
    <tr>
      <th> Regione Bluemix </th>
      <th> Valore SDK </th>
    </tr>
    <tr>
      <td> Stati Uniti Sud</td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> Sydney </td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> Regno Unito</td>
      <td> AppID.REGION_UK </td>
    </tr>
  </table>

  * Un progetto Android Studio, configurato per lavorare con Gradle.
    * Per ulteriori informazioni su come configurare il tuo ambiente di sviluppo Android, consulta <a href="https://developers.google.com/web/tools/setup/" target="_blank">the Google Developer Tools docs <img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a>.

## Installazione dell'SDK client 
{: #install-appid-sdk}

1. Crea un progetto Android Studio oppure apri un progetto esistente.
2.  Aggiungi JitPack al tuo file `build.gradle` della root.

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {:pre}

3. Apri il file `build.gradle` per la tua applicazione.

    **Nota**: assicurati di aprire il file per la tua applicazione, non il file `build.gradle` del progetto.
4. Trova la sezione delle dipendenze del file e aggiungi una dipendenza di compilazione per l'SDK client {{site.data.keyword.appid_short_notm}}:

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {:pre}

5. Trova la sezione defaultConfig e aggiungi le seguenti righe di codice:

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {:pre}

6. Sincronizza il tuo progetto con Gradle. Fai clic su **Tools** > **Android** > **Sync Project with Gradle Files**.

## Inizializzazione dell'SDK client
{: #initialize-client-sdk}

Inizializza l'SDK client passando i parametri contesto, ID tenant e regione al metodo di inizializzazione. Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo onCreate dell'attività principale nella tua applicazione Android.

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {:pre}

1. Sostituisci "tenantId" con l'ID tenant del servizio {{site.data.keyword.appid_short_notm}}.
2. Sostituisci AppID.REGION_UK con la tua regione {{site.data.keyword.Bluemix_notm}}.


## Autentica gli utenti utilizzando il widget di accesso 
{: #authenticate-login-widget}

La configurazione predefinita del widget di accesso richiede l'utilizzo sia di Facebook che di Google per l'autenticazione. Se configuri solo uno dei due, il widget di accesso non si avvia e l'utente viene reindirizzato alla schermata di autenticazione IDP configurata.

Dopo che l'SDK client {{site.data.keyword.appid_short_notm}} è stato inizializzato, puoi autenticare i tuoi utenti eseguendo il widget di accesso.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launch(this, new AuthorizationListener() {
        @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Si è verificata un'eccezione
        }

        @Override
        public void onAuthorizationCanceled () {
          //Autenticazione annullata dall'utente
        }

        @Override
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          //Utente autenticato
        }
      });
  ```
  {:pre}


## Accesso agli attributi dell'utente
{: #accessing}

Quando ottieni un token di accesso, è possibile ottenere l'accesso all'endpoint degli attributi protetti dell'utente. Puoi ottenere l'accesso utilizzando i seguenti metodi API:

  ```   
  void setAttribute(@NonNull String name, @NonNull String value, UserAttributeResponseListener listener);
  void setAttribute(@NonNull String name, @NonNull String value, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void getAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void deleteAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void deleteAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAllAttributes(@NonNull UserAttributeResponseListener listener);
  void getAllAttributes(@NonNull AccessToken accessToken, @NonNull UserAttributeResponseListener listener);
  ```
  {:pre}

Quando il token di accesso non viene esplicitamente trasmesso, {{site.data.keyword.appid_short_notm}} utilizza l'ultimo token ricevuto.

Ad esempio, puoi richiamare questo codice per impostare un nuovo attributo o sovrascriverne uno esistente:

  ```
  appId.getUserAttributeManager().setAttribute(name, value, useThisToken,new UserAttributeResponseListener() {
		@Override
		public void onSuccess(JSONObject attributes) {
			//attributi ricevuti nel formato JSON per una risposta positiva
		}

		@Override
		public void onFailure(UserAttributesException e) {
			//Si è verificata un'eccezione
		}
	});
  ```
  {:pre}

### Accesso anonimo
{: #anonymous notoc}

Con {{site.data.keyword.appid_short_notm}} puoi accedere in modo anonimo, consulta [identità anonima](/docs/services/appid/user-profile.html#anonymous).

  ```
  appId.loginAnonymously(getApplicationContext(), new AuthorizationListener() {
		@Override
		public void onAuthorizationFailure(AuthorizationException exception) {
			//Si è verificata un'eccezione
		}

		@Override
		public void onAuthorizationCanceled() {
			//Autenticazione annullata dall'utente
		}

		@Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
			//Utente autenticato
		}
	});
  ```
  {:pre}

### Autenticazione progressiva
{: #progressive notoc}

Quando l'utente contiene un token di accesso anonimo, può essere identificato trasmettendolo al metodo `loginWidget.launch`.

  ```
  void launch (@NonNull final Activity activity, @NonNull final AuthorizationListener authorizationListener, String accessTokenString);
  ```
  {:pre}

Dopo un accesso anonimo, si verifica l'autenticazione progressiva anche se il widget di accesso viene richiamato trasmettendo un token di accesso, perché il servizio ha utilizzato l'ultimo token ricevuto. Se desideri cancellare i tuoi token memorizzati, esegui il seguente comando:

  ```
  	appIDAuthorizationManager = new AppIDAuthorizationManager(this.appId);
  appIDAuthorizationManager.clearAuthorizationData();
  ```
  {:pre}


## Fasi successive
{: #next-steps}

{{site.data.keyword.appid_short_notm}} fornisce una configurazione predefinita quando configuri per la prima volta i tuoi provider di identità. Puoi utilizzare la configurazione predefinita solo nella modalità di sviluppo. Prima di pubblicare la tua applicazione, aggiorna la configurazione [Facebook](/docs/services/appid/identity-providers.html#facebook) e [Google](/docs/services/appid/identity-providers.html#google) predefinita con le tue proprie credenziali.
