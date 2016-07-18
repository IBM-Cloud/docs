---

copyright:
  year: 2016

---

# Abilitazione dell'autenticazione Facebook per le applicazioni Web

Utilizza  Facebook per autenticare gli utenti alla tua applicazione web.

## Prima di cominciare
{: #facebook-auth-android-before}
È necessario disporre di:
* Un'applicazione web.  
* Un'istanza di un'applicazione  {{site.data.keyword.Bluemix_notm}} che è protetta da un servizio {{site.data.keyword.amashort}}. Per ulteriori informazioni su come creare un back-end {{site.data.keyword.Bluemix_notm}}, consulta [Introduzione](index.html).
* Un segreto applicazione e un ID dell'applicazione Facebook. Per ulteriori informazioni, vedi [Ottenimento di un ID applicazione Facebook dal portale sviluppatori Facebook](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).


## Configurazione di un'applicazione Facebook per il tuo sito web
Per utilizzare Facebook come provider di identità per il tuo sito web, devi aggiungere e impostare la piattaforma del sito web sull'applicazione Facebook.

1. Apri la tua applicazione Facebook nel portale sviluppatori Facebook.
1. Prendi nota dell'ID applicazione della tua applicazione e del segreto applicazione. Questo valore ti servirà quando configuri il tuo progetto web per l'autenticazione Facebook.
1. Dalla pagina **Settings** fai clic su **Add Platform** e scegli **Website**.
1. Salva le modifiche.
1. Fai clic su **Facebook Login** nella barra laterale sinistra.
1. Immetti l'endpoint di callback del server di autorizzazione nella casella **Valid OAuth redirect URIs**: https://imf-newauthserver.bluemix.net/oauth/{bluemix_app_guid}/callback. Salva le modifiche.




# Configurazione di {{site.data.keyword.amashort}} per l'autenticazione Facebook
Una volta che disponi del tuo ID applicazione Facebook e del segreto applicazione e la tua applicazione Facebook è stata configurata perché serva i client web, puoi abilitare l'autenticazione Facebook nel dashboard  {{site.data.keyword.Bluemix_notm}}.

1. Apri la tua applicazione nel dashboard {{site.data.keyword.Bluemix_notm}}.
1. Fai clic sul tile {{site.data.keyword.amashort}}. Il dashboard {{site.data.keyword.amashort}} viene caricato.
1. Fai clic sul tile Facebook.
1. Immetti il segreto applicazione e l'ID dell'applicazione Facebook e salva.




## Utilizzo di Mobile Client Access per l'autenticazione web Facebook

Per avviare il processo di autorizzazione:

1. Vai dalla tua applicazione web al seguente endpoint del server di autenticazione:  https://imf-newauthserver.bluemix.net/oauth/v2/authorization.

1. Aggiungi i seguenti parametri della query:
   ```
    response_type='authorization_code'
    client_id= <bluemix_app_guid>
    redirect_uri= <uri per il reindirizzamento dopo la ricezione del codice di autorizzazione>
    scope= 'openid'
    state= <state>
    ```


  Il parametro `state` non è utilizzato per ora e può essere lasciato vuoto.
  Il parametro `redirect_uri` è l'uri per il reindirizzamento dopo l'esito positivo o negativo dell'autenticazione con Facebook.

1. Dopo il reindirizzamento dell'endpoint di autorizzazione visualizzerai un modulo
di accesso da Facebook. Immetti il nome utente e la password per il reindirizzamento a `redirect_uri`.
   La risposta restituita dopo il reindirizzamento contiene il codice di autorizzazione nei parametri di query della richiesta.

1. Effettua una richiesta `POST` all'endpoint del token del server di autorizzazione:

  https://imf-newauthserver.bluemix.net/oauth/v2/token

  utilizzando i seguenti parametri di query:
  ```
  grant_type='authorization_code'
  client_id= <bluemix_app_guid>
  code= <authorization code>
  ```
Il parametro `redirect_uri` deve corrispondere al `redirect_uri` del passo 2.
Il valore `code` è il codice di autorizzazione ricevuto in risposta alla chiamata end-to-end del passo 3.
Assicurati di inviare questa richiesta `POST` in 10 minuti perché il codice di autorizzazione è valido per un massimo di 10 minuti.

  Il corpo della risposta `POST` contiene `access_token` e il `id_token` codificati in base64.

## Verifica dell'autenticazione
Ora puoi iniziare ad effettuare richieste alle tue risorse protette.
Tutte le richieste a risorse protette devono contenere il `access_token` nel campo di intestazione della richiesta di autorizzazione.


