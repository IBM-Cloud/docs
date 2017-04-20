---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Configurazione dei provider di identità
{: #setting-up-idp}

Puoi configurare Facebook, Google o entrambi per configurare un'esperienza SSO (Single Sign On) per i tuoi utenti. Utilizzando un provider di identità, gli utenti sono in grado di accedere con le credenziali con cui hanno già familiarità.
{:shortdesc}


## Configurazione dell'autenticazione Facebook
{: #facebook}

Configura il servizio {{site.data.keyword.appid_short}} per utilizzare Facebook come provider di identità.

<!--- ### Sequence diagram
{: #facebook-sequence-diagram}--->

### Ottenere un ID applicazione e un segreto da Facebook
{: #getting-facebook-appid}

Per utilizzare Facebook come provider di identità per le tue applicazioni web o mobili, devi aggiungere e impostare la piattaforma del sito web sull'applicazione Facebook.

1. Accedi al tuo account sul <a href="https://developers.facebook.com/docs/apps/register" target="_blank">sito Facebook for Developers <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
2. Prendi nota del segreto e dell'ID applicazione di Facebook. Hai bisogno di questi valori per configurare il tuo progetto web per l'autenticazione nel tuo dashboard del servizio. 
3. Aggiungi la piattaforma web e immetti l'URL del sito.
4. Dall'elenco dei prodotti, seleziona **Facebook Login**.
5. Nel campo Valid OAuth redirect URLs, immetti l'URL dell'endpoint di callback del server di autenticazione. Puoi aggiungere questo valore dopo aver configurato il tuo servizio {{site.data.keyword.appid_short_notm}} nelle seguenti istruzioni.
6. Fai clic su **Save Changes**.

### Configurazione di {{site.data.keyword.appid_short_notm}} per l'autenticazione Facebook
{: #configuring-facebook-appid}

Quando disponi del tuo ID applicazione e del segreto Facebook e la tua applicazione Facebook for Developers è configurata per utilizzare i client web, puoi modificare l'autenticazione Facebook nel tuo dashboard del servizio.

1. Dalla scheda **Manage** del tuo dashboard del servizio, seleziona **Facebook** e fai clic su **Edit**.
2. Immetti l'ID applicazione e il segreto di Facebook che hai ottenuto dal sito web Facebook for Developers.
3. Copia l'URI nel campo **Redirect URI for Facebook for Developers**. Incolla l'URI nel campo **Valid OAuth redirect URIs** nella sezione **Facebook Login** del portale Facebook Developers.
4. Fai clic su **Save**.
5. Facoltativo: per configurare l'autenticazione per le tue applicazioni web, immetti l'URL di reindirizzamento nei tuoi URL di reindirizzamento dell'applicazione web. Questo valore viene determinato dallo sviluppatore e utilizzato per accedere all'URL di reindirizzamento dopo il completamento del processo di autorizzazione. 


## Configurazione dell'autenticazione Google
{: #google}

Configura il servizio {{site.data.keyword.appid_short_notm}} per utilizzare Google come provider di identità.

<!--- ### Sequence diagram
{: #google-sequence-diagram}--->

### Ottenere l'ID client e il segreto da Google
{: #google-client-id}

Per utilizzare Google come un provider di identità, ottieni un ID client e un segreto di Google e crea un progetto nella Google Developers Console.

1. Apri la tua applicazione Google nella <a href="https://console.developers.google.com/apis/library" target="_blank">Google Developer Console <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
2. Aggiungi l'API Google+.
3. Crea le credenziali utilizzando OAuth. Nel campo **Application Type**, seleziona **Web application**. Nel campo **Authorized redirect URIs**, immetti l'URI di reindirizzamento dell'ID dell'applicazione. Puoi ottenere l'URI di autorizzazione di reindirizzamento dell'ID dell'applicazione dalla schermata di configurazione di Google del dashboard del servizio.
4. Salva le tue modifiche. Prendi nota del segreto e dell'ID client di Google.



### Configurazione di {{site.data.keyword.appid_short_notm}} per l'autenticazione Google
{: #google-client-appid}

Quando disponi del segreto e del client di Google e la tua console Google Developers è configurata per utilizzare i client web, puoi modificare l'autenticazione Google nel tuo dashboard del servizio.

1. Dalla scheda **Manage** del tuo dashboard del servizio, seleziona **Google** e fai clic su **Edit**.
3. Immetti l'ID client e il segreto di Google che hai ottenuto dalla console Google Developers.
4. Copia l'URI nel campo **Redirect URI for Google for Developers**. Incolla l'URI nel campo **Authorized redirect URIs** in **Restrictions** nella sezione **Client ID for Web application** del portale Google Developers.
5. Fai clic su **Save**.
6. Facoltativo: per configurare l'autenticazione per le tue applicazioni web, immetti l'URI di reindirizzamento nei campi degli URI di reindirizzamento dell'applicazione web. Questo valore viene determinato dallo sviluppatore e utilizzato per accedere all'URI di reindirizzamento dopo il completamento del processo di autorizzazione.



<!---[## Bring your own OAuth2/OIDC identity provider
{: #oauth2}

### About
{: #oauth2-about}
### Sequence diagram
{: #oauth2-sequence-diagram}
### Configuring AppID for BYOIDP OAuth2 authentication
{: #oauth2-appid} SHAWNA: Is this Interconnect?]--->
