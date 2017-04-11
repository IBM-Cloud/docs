---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Descrizione dei profili utente
{: #user-profile}

Un profilo utente è un'entità archiviata e conservata da {{site.data.keyword.appid_short}}. Il profilo ospita l'identità e gli attributi dell'utente e può essere anonimo o collegato a un'identità gestita da un provider di identità.
{:shortdesc}

{{site.data.keyword.appid_short_notm}} fornisce un'API per l'accesso, sia in modo anonimo che tramite autenticazione con un IdP OpenId Connect (OIDC), consulta [Configurazione dei provider di identità](/docs/services/appid/identity-providers.html#setting-up-idp). L'endpoint API dell'attributo del profilo utente è una risorsa protetta dal token di accesso generato da {{site.data.keyword.appid_short_notm}} durante il processo di autorizzazione e accesso.


## Memorizzazione, lettura ed eliminazione degli attributi utente
{: #storing-data}



{{site.data.keyword.appid_short_notm}} fornisce un'API REST <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/" target="_blank"> <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per eseguire le operazioni CRUD sugli attributi dell'utente, così come un'SDK per i client mobili <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Android <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> e <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">Swift <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.


## Identità OAuth
{: #oauth}

Quando si richiama l'API di accesso OAuth, {{site.data.keyword.appid_short_notm}} utilizza i protocolli OAuth 2.0 e OIDC per autenticare il chiamante con un provider di identità selezionato. Una volta autenticata, l'identità viene associata a un record utente {{site.data.keyword.appid_short_notm}}. {{site.data.keyword.appid_short_notm}} restituisce un token di accesso che può essere utilizzato per accedere agli attributi dell'utente e un token di identità che ospita le informazioni sull'identità fornite dal provider di identità. È possibile accedere allo stesso record utente e ai relativi attributi ancora da qualsiasi client che si autentica con stessa identità.


## Utente anonimo
{: #anonymous}

Quando esegui l'accesso anonimamente, {{site.data.keyword.appid_short_notm}} crea un record utente ad hoc che viene contrassegnato come anonimo. {{site.data.keyword.appid_short_notm}} restituisce i token di identità e di accesso anonimo al chiamante. Utilizzando il token di accesso anonimo, l'applicazione dell'utente può creare, leggere, aggiornare ed eliminare gli attributi che sono archiviati nel record utente. Ad esempio, uno sviluppatore può creare un'applicazione in cui un utente può immediatamente iniziare ad aggiungere elementi a un carrello d'acquisto senza dover accedere.


## Utente identificato
{: #identified}

Un utente anonimo con un'identità fornita da un provider di identità può diventare un utente identificato. Il flusso per la modifica di un utente anonimo an un utente identificato viene descritto nei seguenti passi: 

* Lo sviluppatore trasmette il token di accesso anonimo all'API di accesso.
* {{site.data.keyword.appid_short_notm}} autentica il chiamante con il provider di identità.
* {{site.data.keyword.appid_short_notm}} trova il record dell'utente anonimo definito dal token di accesso e gli assegna l'identità.

    **Nota**: l'identità può essere assegnata al record anonimo solo se la stessa identità non è già stata assegnata ad un altro utente. Se l'identità è già associata a un altro utente {{site.data.keyword.appid_short_notm}}, i token di accesso e di identità contengono le informazioni di tale record dell'utente e forniscono l'accesso a suoi attributi. Il precedente utente anonimo e suoi attributi non saranno più accessibili tramite il nuovo token di accesso. Finché il token non scade, le informazioni possono ancora essere associate tramite il token di accesso anonimo. Lo sviluppatore può scegliere come vuole unire gli attributi anonimi dell'utente anonimo e dell'utente conosciuto.

* I nuovi token di identità e di accesso ricevuti da {{site.data.keyword.appid_short_notm}} puntano all'utente conosciuto e al token di identità che contiene le informazioni pubbliche ricevute dal provider di identità.
* I token anonimi diventano non validi per l'utente.

Gli attributi contenuti da questo utente mentre era anonimo sono accessibili con il nuovo token di accesso. I nuovi token possono essere aggiunti, modificati o eliminati. In seguito, l'utente e i suoi attributi vengono risolti e sono accessibili quando accedono con la stessa identità per ogni client.


## Codifica e separazione dei dati
{: #data}

{{site.data.keyword.appid_short_notm}} archivia e codifica gli attributi del profilo utente. Come un servizio a più tenant, ogni tenant ha una chiave di codifica e i dati utente in ogni tenant sono codificati con solo tale chiave.

{{site.data.keyword.appid_short_notm}} assicura che le informazioni private siano codificate prima dell'archiviazione.
