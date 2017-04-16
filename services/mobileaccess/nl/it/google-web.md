---

copyright:
  year: 2016, 2017
lastupdated: "2017-01-08"

---

# Abilitazione dell'autenticazione Google per le applicazioni web
{: #google-auth-web}

Utilizza Google Sign-In per autenticare gli utenti alla tua applicazione web.


## Prima di cominciare
{: #before-you-begin}

È necessario disporre di:
* Un'applicazione web.
* Un'istanza di un'applicazione  {{site.data.keyword.Bluemix_notm}} che è protetta da un servizio {{site.data.keyword.amashort}}. Per ulteriori informazioni su come creare un back-end {{site.data.keyword.Bluemix_notm}}, consulta [Introduzione](index.html).

## Configurazione di un'applicazione Google per il tuo sito web
Per iniziare a usare Google come un provider di identità, creare un progetto nella [Google Developer Console](https://console.developers.google.com). Parte della creazione di un progetto consiste nell'ottenere un segreto e un ID client Google. Il segreto e l'ID client Google sono identificativi univoci per la tua applicazione utilizzati dall'autenticazione Google e sono necessari per la configurazione dell'applicazione {{site.data.keyword.Bluemix_notm}}.

1. Crea un progetto utilizzando l'API Google+.
1. Crea le credenziali utilizzando **OAuth**. Per creare le credenziali devi:
    * Selezionare il tip odi applicazione **Web application**.
    * Fornire il valore **Authorized redirect URIs**:

     https://imf-newauthserver.bluemix.net/oauth/{bluemix_app_guid}/callback
1. Completa la creazione delle credenziali e prendi nota del segreto e dell'ID client Google.


## Configurazione di {{site.data.keyword.amashort}} per l'autenticazione Google
Dopo aver ottenuto il segreto e l'ID client Google, puoi abilitare l'autenticazione Google nel dashboard {{site.data.keyword.amashort}}.

1. Apri la tua applicazione nel dashboard {{site.data.keyword.Bluemix_notm}}.
1. Fai clic sul tile {{site.data.keyword.amashort}}. Il dashboard {{site.data.keyword.amashort}} viene caricato.
1. Fai clic sul tile Google.
1. Immetti il segreto e l'ID client Google e salva.


## Utilizzo di {{site.data.keyword.amashort}} per l'autenticazione web Google
Per avviare il processo di autorizzazione:

1. Vai dalla tua applicazione web al seguente endpoint del server di autenticazione:  
  https://imf-newauthserver.bluemix.net/oauth/v2/authorization

  utilizzando i seguenti parametri di query:
	```
   response_type='authorization_code'
   client_id= <bluemix_app_guid>
   redirect_uri= <uri a cui desideri tornare dopo l'ottenimento di un codice di accesso>
   scope= ‘openid’
   state= <state>
	```

  Il parametro `state` non è utilizzato per ora e può essere rimanere vuoto.

  L'uri del parametro `redirect_uri` è il reindirizzamento dopo un'autenticazione positiva o negativa con Google.
  La risposta restituita dopo il reindirizzamento contiene il codice di autorizzazione nei parametri di query della richiesta.
1. Effettua una richiesta `POST` all'endpoint del token del server di autorizzazione:

 https://imf-newauthserver.bluemix.net/oauth/v2/token


  utilizzando i seguenti parametri di query:

	```
  	grant_type=’authorization_code’
    client_id= < bluemix_app_guid >
    redirect_uri= <redirect_uri >
    code= <authorization code>
	```
  Il parametro `redirect_uri` deve corrispondere al `redirect_uri` del passo 1 e il valore `<authorization code>` è ricevuto dalla risposta.
  Assicurati di inviare questa richiesta `POST` in 10 minuti perché il codice concesso è valido per un massimo di 10 minuti.

Il corpo della risposta `POST` contiene `access_token` e il `id_token` codificati in base64.

## Verifica dell'autenticazione

Ora puoi iniziare ad effettuare richieste alle tue risorse protette.
Tutte le richieste a risorse protette devono contenere il token di accesso nel campo di intestazione della richiesta di autorizzazione.
