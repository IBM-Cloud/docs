---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-06"

---

**Importante: il servizio {{site.data.keyword.amafull}} è stato sostituito con il servizio {{site.data.keyword.appid_full}}.**

# Autenticazione personalizzata dell'applicazione web
{: #custom-web}

Aggiungi l'autenticazione personalizzata alla tua applicazione web

## Prima di cominciare
{: #before-you-begin}

È necessario disporre di:
* Un'applicazione web con un endpoint  `/apps/:Guid/<RealmName>/handleChallengeAnswer`,
che restituisce una identità utente dopo l'esito positivo dell'autenticazione. La struttura JSON dell'identità utente dovrebbe essere simile alla seguente:

   ```json
  userIdentity: {
  userName: <username>,
  displayName: <displayName>;
 };
```
* Un'istanza di un'applicazione  {{site.data.keyword.Bluemix_notm}} che è protetta da un servizio {{site.data.keyword.amashort}}. Per ulteriori informazioni su come creare un back-end {{site.data.keyword.Bluemix_notm}}, consulta [Introduzione](index.html).



## Configurazione di un'applicazione {{site.data.keyword.amashort}} per l'autenticazione personalizzata


1. Apri la tua applicazione nel dashboard {{site.data.keyword.Bluemix_notm}}.
1. Fai clic sul tile {{site.data.keyword.amashort}}. Il dashboard {{site.data.keyword.amashort}} viene caricato.
1. Fai clic sul tile Personalizza.
1. Immetti **custom realm**, **custom identity provider url** e **redirect_uri**. Fai clic su salva.

## Utilizzo di {{site.data.keyword.amashort}} per l'autenticazione web personalizzata

Per avviare il processo di autorizzazione:

1. Vai dalla tua applicazione web al seguente endpoint del server di autenticazione:

    https://imf-newauthserver.bluemix.net/oauth/v2/authorization

  utilizzando i seguenti parametri di query:
   ```
   response_type=’authorization_code’
   client_id= <bluemix\_app\_guid>
   redirect_uri= <uri per il reindirizzamento dopo aver ottenuto un codice di autorizzazione>
   scope= ‘openid’
   state= <state>
   ```

    Il parametro `state` non è utilizzato per ora e può essere lasciato vuoto.

    Il parametro `redirect_uri` determina il reindirizzamento dopo l'esito positivo o negativo dell'autenticazione del tuo provider di identità personalizzato.

1. Dopo il reindirizzamento dell'endpoint di autorizzazione visualizzerai un modulo
di accesso. Immetti il nome utente e la password per iniziare l'autenticazione
al tuo provider di identità e un reindirizzamento a `redirect_uri`.
La risposta restituita dopo un'autenticazione corretta contiene il codice di autorizzazione nei parametri di query della richiesta.

4. Effettua una richiesta `POST` all'endpoint del token del server di autorizzazione:

 https://imf-newauthserver.bluemix.net/*oauth/v2/token

 utilizzando i seguenti parametri di query:
 ```
 grant_type = 'authorization_code'
 client_id = <bluemix_app_guid>
 redirect_uri = <redirect_uri>
 code = <authorization code>
 ```
  Il parametro `redirect_uri` deve corrispondere al `redirect_uri` del passo 1. Il codice di autorizzazione è stato restituito dalla richiesta nel passo 2.

  Assicurati di inviare questa richiesta `POST` in 10 minuti perché il codice concesso è valido per un massimo di 10 minuti.

Il corpo della risposta `POST` contiene *access_token* e il
*id_token* codificati in base64.

## Verifica dell'autenticazione


Ora puoi iniziare ad effettuare richieste alle tue risorse protette.
Tutte le richieste a risorse protette devono contenere il `access_token`.
Invia il token di accesso nel campo intestazione `the-Authorization-request`.
