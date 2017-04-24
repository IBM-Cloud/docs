---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-17"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# IBM Cloud Identity and Access Management (IAM)
{: #iam_overview}

IBM Cloud IAM fornisce un modo sicuro di gestire le identità del servizio e dell'utente e l'accesso alle risorse per tali identità. Puoi visualizzare e gestire gli utenti nell'account o organizzazione, a seconda delle opzioni di accesso che sei autorizzato a gestire. Puoi eseguire tutte le operazioni per gli utenti inclusi l'invito e la gestione degli utenti e dei loro ruoli assegnati e gli account o le organizzazioni, o entrambi, a cui possono accedere. Come proprietario di un account, puoi gestire le opzioni di accesso di cui sia tu che gli utenti siete membri, indipendentemente dal ruolo, nell'account corrente.

La gestione dell'identità include quanto segue:
 * Gestione utente 
   * creare, eliminare, aggiornare le informazioni sull'utente
   * Gestione chiave API 
   * scambio, aggiornamento e creazione token
   * autenticazione identità utente
 * Gestione ID servizio
   * creare, eliminare, aggiornare le informazioni sull'utente
   * Gestione chiave API 
   * scambio, aggiornamento e creazione token
   * autenticazione identità servizio 
   
   
La gestione dell'accesso include quanto segue: 
 * Gestione politiche
   * creare, eliminare e aggiornare le politiche 
 * Decisioni sull'accesso alle risorse
 
## Panoramica sull'identità
{: #identity}

Il servizio token IAM cloud è il servizio di autenticazione per IBM Cloud creato su standard aperti specificati da [OAuth 2.0]( https://tools.ietf.org/html/rfc6749), [JWT](https://tools.ietf.org/html/rfc7519), [JWT Profile](https://tools.ietf.org/html/rfc7523) e [JWKS](https://tools.ietf.org/html/rfc7517).

Un obiettivo del servizio token è l'autenticazione degli sviluppatori, degli operatori e degli amministratori per la piattaforma cloud IBM. Per questa autenticazione, il servizio token è collegato al sistema ID IBM per autenticare gli utenti negli ambienti dedicato e locale, può essere collegato a un sistema di autenticazione scelto del cliente come LDAP. 

Per richiamare un token IAM, puoi utilizzare i tipi di concessione OAuth 2.0 standard come `password`, ad esempio:
```
curl 
    -u "<clientid>:<clientsecret>" 
    –H "Content-Type: application/x-www-form-urlencoded" 
    –d "grant_type=password&username=<IBMid>&password=<IBMid password>
       [&ims_account=<ims account>][&bss_account=<bss account>]
       [&response_type=cloud_iam,uaa,ims_portal]"
    "https://iam.ng.bluemix.net/oidc/token[?pretty=true]"
```
{: codeblock}

Come estensione di OAuth 2.0, devi fornire le informazioni sull'account per rendere il token specifico per l'account. Inoltre puoi elencare diversi tipi di risposta per ottenere i token `UAA` o `IMS` per le interazioni con le API CloudFoundry o IMS.

Il servizio token IAM cloud ti consente di creare, aggiornare, eliminare ed utilizzare le chiavi API per gli utenti. Queste chiavi API possono essere create con le chiamate API o la console Bluemix. Per utilizzare una chiave API, un adattatore può utilizzare il seguente tipo di concessione estesa:
```
curl 
    -u "<clientid>:<clientsecret>" 
    –H "Content-Type: application/x-www-form-urlencoded" 
    –d "grant_type=urn:ibm:params:oauth:grant-type:apikey&
       apikey=<apikeyvalue>[&response_type=cloud_iam,uaa,ims_portal]"
    "https://iam.ng.bluemix.net/oidc/token[?pretty=true]"
```
{: codeblock}

Il token risultante può essere utilizzato come uno richiamato con una concessione password o un accesso IU.

Come ulteriore variante, il servizio token IAM cloud ti consente di accedere interattivamente con la IU. Questo è implementato utilizzando il tipo di concessione OAuth 2.0 `authorization_code` ed è anche conosciuto come `OAuth Dance`, perché causa molti reindirizzamenti del browser web durante la fase di autenticazione.

L'altro obiettivo del servizio token è la capacità di creare ID del servizio e le chiavi API per gli ID del servizio. Un ID del servizio è simile a un "ID funzionale" o un "ID applicazione" e viene utilizzato per l'autenticazione dei servizi e non rappresenta un utente.

Gli utenti possono creare gli ID del servizio e associarli per ambiti come un account Bluemix, un'organizzazione o uno spazio CloudFoundry. Questa associazione viene fatta per fornire all'ID del servizio a un contenitore in cui stare. Questo contenitore definisce inoltre chi può aggiornare ed eliminare l'ID del servizio e chi può creare, aggiornare, leggere ed eliminare le chiavi API associate a tale ID del servizio. Un ID del servizio NON è correlato a un utente.

Per ottenere una migliore comprensione di come utilizzare gli ID del servizio, puoi provare la nostra [Applicazione demo](https://iam.ng.bluemix.net/demo) che illustra le API.

## Panoramica sulla gestione dell'accesso 
{: #access_management}

IAM è un sistema Attribute Based Access Control (ABAC) con condizioni ispirate dalla pubblicazione
[NIST](http://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.sp.800-162.pdf).  

IAM utilizza una combinazione di attributi per determinare l'accesso alle risorse. Le politiche IAM hanno regole che vengono applicate ai ruoli, attributi ID utenti/servizio, attributi della risorsa e condizioni. Questo consente un approccio potente e flessibile alla definizione dell'accesso per gli ID del servizio e degli utenti.

Ad esempio, presa una macchina virtuale, VM123 può avere i seguenti attributi: 
```
    resource: {
      'serviceName': 'virtual-machine',
      'region': 'us-south',
      'resourceType': 'vm',
      'resource': 'vm123'
    }
```
{: codeblock}
  
Ogni combinazione di questi attributi della risorsa può essere utilizzata per creare una politica.

Per esempi più dettagliati, consulta [IAM Policy examples](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/policy_examples.html#iam_policy_examples).

ABAC è differente da Role Based Access Control (RBAC), in cui vengono assegnati agli utenti ruoli predefiniti. Questi ruoli predefiniti hanno privilegi specifici e gli utenti con tale ruolo dispongono di tutti i privilegi definiti da esso. 
 
Ad esempio, un ruolo `Amministratore` della macchina virtuale. Questo ruolo implica tutti i privilegi del tipo amministratore su ogni risorsa della macchina virtuale. 

Un modo semplice di pensare a ABAC è:

1. Esistono utenti, risorse, contesti e azioni.
1. Ogni istanza di un utente, una risorsa, un contesto e un'azione ha un identificativo univoco.
1. Ogni istanza ha attributi forniti.
   In pratica ciò significa: "Cosa è vero riguardo l'istanza da un punto di vista dell'autorizzazione".
   Esempi:
   1. L'utente è dei pesci ed è nato nel 1960.
   1. La risorsa è un elenco di squadre di baseball.
   1. Il contenuto è dalle 9:00 AM alle 5:00 PM Eastern Time.
   1. L'azione è "possibile aggiornare".
1. Le politiche sono create per determinare quale serie di attributi ha l'autorizzazione per l'utente di eseguire l'azione nella risorsa.
1. Quando viene effettuata una richiesta da un utente per eseguire un'azione su una risorsa, vengono consultate le politiche per vedere se la richiesta è consentita.

La seguente immagine mostra una vista dettagliata della sequenza di autorizzazione.

![Sequenza di autorizzazione](auth_sequence.png)

## Impostazione del controllo dell'accesso per il tuo servizio
{: #setup_access_mgmt}

Integrazione di un servizio in {{site.data.keyword.Bluemix_notm}} è una serie differente di operazioni che integra un servizio con IAM cloud. Tecnicamente puoi eseguire l'integrazione con {{site.data.keyword.Bluemix_notm}} e IAM cloud indipendentemente e in qualsiasi ordine. Il team IAM cloud sta lavorando con il team di integrazione del servizio {{site.data.keyword.Bluemix_notm}} in modo che il servizio {{site.data.keyword.Bluemix_notm}} nel processo di elaborazione includerà anche l'integrazione IAM cloud.

Per configurare il controllo dell'accesso per il tuo servizio, devi utilizzare i seguenti passi come parte del tuo processo di integrazione:

### Passo 1: Crea un ID del servizio effettuando questa richiesta http:
```
  POST https://iam.ng.bluemix.net/serviceids
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "name": "<service id name>",
    "description": "<service id description>",
    "boundTo": "<crn>"
  }
```
{: codeblock}

Comando Curl:
```  
curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"name": "<service id name>", "description": "<service id description>", "boundTo": "<crn>"}' 'https://iam.ng.bluemix.net/serviceids'
```
{: codeblock}

Quanto segue illustra i valori `ID del servizio` e `Crn del servizio` utilizzati nel comando `curl` in modo più dettagliato:
  
#### ID del servizio 
  
Il nome dell'ID del servizio può essere lo stesso del nome del servizio che compare nei crn per il tuo servizio.
  
Il tuo ID del servizio deve essere associato a un account, un'organizzazione o uno spazio. Questa associazione determina chi può gestire il tuo ID del servizio. Ad esempio, l'amministratore dove è associato il tuo servizio è in grado di aggiornare o eliminare. Il tuo token {{site.data.keyword.Bluemix_notm}} ha bisogno di disporre dell'accesso all'account, all'organizzazione e allo spazio a cui stai associando l'ID. Per associare un account, il crn `boundTo` deve essere simile a quanto segue: 

`crn:v1:::<service name>::a/<account id>:::` 
  
Per un'organizzazione deve essere simile a quanto segue:
`crn:v1:<cname>:<ctype>:<service name>:<region>:o/<organization id>:::` 
  
Per uno spazio deve essere simile a quanto segue:
`crn:v1:<cname>:<ctype>:<service name>:<region>:s/<space id>:::`  
  
Il valore `boundTo` specificato non ha effetto sulle risorse a cui può accedere il tuo ID del servizio. 
  
Le politiche di accesso IAM controllano a quali risorse il tuo ID del servizio può accedere. Anche se il tuo ID del servizio è associato a un'organizzazione BM, le politiche IAM possono essere create per consentire all'ID del servizio di accedere alle risorse all'esterno di tale organizzazione. Quando esegui l'integrazione con IAM, la prima politica di accesso creata dal team IAM consente all'ID del servizio di creare le politiche per tutte le risorse di proprietà del tuo servizio.

Consulta [createServiceid](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/) per ulteriori informazioni su questa API e sulle API correlate.

#### Crn del servizio

Il nome del servizio nel crn `boundTo` deve corrispondere al nome del servizio che compare nel crn del tuo servizio.
  
Consulta [CRN spec](https://github.ibm.com/ibmcloud/builders-guide/blob/master/specifications/crn/CRN.md) per supporto nel completamento di questi campi.

Dalla risposta, salva metadata->uuid e metadata->crn, che sono il tuo ID e crn ID del servizio.


### Passo 2: Contatta la squadra del controllo dell'accesso all'indirizzo [#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 
Il tuo ID del servizio ha fornito il ruolo di amministratore delle politiche per le risorse del tuo servizio.

Utilizza questo formato:
```
IAM adopter service info

service id: uuid from step #1
service name: your service name as it will appear in the crns for your service
```
{: codeblock}

### Passo 3: Devi creare una chiave API dal tuo ID del servizio. Utilizza la seguente richiesta http:
```
  POST https://iam.ng.bluemix.net/apikeys
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "boundTo": "<service id crn>",
    "name": "<api key name>",
    "description": "<api key description>"
  }
```
{: codeblock}

Comando Curl: 
```
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"boundTo": "<service id crn>", "name": "<api key name>", "description": "<api key description>"}' https://iam.ng.bluemix.net/apikeys
```
{: codeblock}

`boundTo` deve essere associato al crn del tuo ID del servizio (campo metadata->crn salvato dalla risposta del primo passo). Il nome e la descrizione possono essere qualsiasi cosa.

Dalla risposta, salva entity->apiKey.

Consulta [createAPIKey](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createAPIKey) per ulteriori informazioni su questa API e sulle API correlate.

### Passo 4: Ottieni un token di accesso per la tua chiave API degli ID del servizio. 

Quando viene stabilita l'autorizzazione, il tuo servizio può effettuare le richieste PAP e PDP dalle risorse del tuo servizio.

Utilizza il campo **apiKey** dell'entità dal passo #3, che rappresenta il tuo valore della chiave API (apikey_value).

  * Quindi ottieni il token con il valore della chiave API (assicurati di stare utilizzando caratteri escape):

    Comando Curl:
```
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<apikey_value>" "https://iam.ng.bluemix.net/oidc/token"
```
{: codeblock}

Utilizza il campo **access_token** nel risultato, che rappresenta il tuo token della chiave API (per il tuo ID del servizio). **access_token** deve essere codificato tramite URL quando utilizzato nel comando curl precedentemente mostrato.


### Passo 5: Registra l'elenco delle azioni del servizio possibili per il nome del servizio.

  a. Associa le azioni del servizio ai ruoli definiti dal sistema IAM. Questa associazione viene utilizzata successivamente durante la registrazione del servizio.

  * Può essere trovato un elenco dei ruoli definiti dal sistema IAM eseguendo la seguente richiesta:
  
Comando Curl:
```
curl -X GET --header 'Accept: application/json' --header 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'
```
{: codeblock}

**Nota:** Utilizza *crn version* dei ruoli definiti dal sistema IAM nel tuo payload di registrazione del servizio.

Il seguente è un esempio di associazione della azioni del servizio ai ruoli. 

  <table>
    <tr>
      <th>Endpoint API</th>
      <th>Azione del servizio</th>
      <th>Ruoli definiti dal sistema IAM</th>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}</td>
      <td>key-protect.keys.create</td>
      <td>Amministratore</td>
    </tr>
    <tr>
      <td>GET /api/keys/{key_id}</td>
      <td>key-protect.keys.read</td>
      <td>Visualizzatore, Editor, Amministratore </td>
    </tr>
    <tr>
      <td>PUT /api/keys/{key_id}</td>
      <td>key-protect.keys.update</td>
      <td>Editor, Amministratore</td>
    </tr>
    <tr>
      <td>DELETE /api/keys/{key_id}</td>
      <td>key-protect.keys.delete</td>
      <td>Amministratore</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/encode</td>
      <td>key-protect.keys.encode</td>
      <td>Editor, Amministratore</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/decode</td>
      <td>key-protect.keys.decode</td>
      <td>Editor, Amministratore</td>
    </tr>
  </table>

  b. Utilizza la seguente riga di comando per registrare il tuo servizio con `PAP`:
```
  curl -X PUT -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'Authorization: <api key token>' -d '{
    "displayName": {
      "default": <service display name>
    },
    "actions": [{
      "id": <service_action>,
      "displayName": {
        "default": <service action display name>
      },
      "roles": [<system_defined_role_crn>]
    }]
  }' 'https://iampap.ng.bluemix.net/acms/v1/services/<service_name>'
  ```
{: codeblock}
  
Le azioni devono essere specificate come definito nel
[Formato azione servizio](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/index.html#action_format).
  
Ad esempio, quando utilizzi il formato standard:

  `<service-name>.<component>.<verb>`
  
  Utilizzando l'azione `key-protect.keys.decode` dall'esempio precedente 
  * service-name = key-protect
  * component = keys
  * verb = decode
  

### Passo 6: Verifica il servizio registrato in base ai dettagli nel passo 5.

```
curl -H "Authorization: <api key token>" "https://iampap.ng.bluemix.net/acms/v1/services/<service_name>"
```

### Passo 7 (Facoltativo): Elimina il servizio registrato nel passo 5.

```
curl -X DELETE -H "Authorization: <api key token>" "https://iampap.ng.bluemix.net/acms/v1/services/<service_name>"
```

### Passo 8: Configura il servizio per utilizzare l'SDK PEP per poter controllare le autorizzazioni con PDP. Scegli il linguaggio SDK corrispondente.

  * [PEP SDK for Java](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Java)
  * [PEP SDK for Nodejs](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Node)
  * [PEP SDK for Python](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Python)
 

## Terminologia
{: #terminology}

### Terminologia identità

* ID IBM - Un'identità fornita e ospitata da IBM per accedere al cloud IBM, alle applicazioni IBM, alle community e al supporto.
* ID utente - L'identificazione che rappresenta una persona reale.
* ID del servizio - L'identificazione che rappresenta un utente tecnico, una macchina, un'applicazione o dei servizi. Simile agli "ID funzionali" o agli "ID dell'applicazione" che rappresenta inoltre un utente tecnico, ma utilizza il tipo di entità "ID utente".
* OAuth 2.0 - Standard aperto per autorizzare l'accesso alle applicazioni e alle API senza fornire le credenziali al servizio di destinazione. OAuth viene anche utilizzato per contenere le informazioni di autenticazione.
* OpenID Connect - Standard aperto creato con OAuth 2.0 che si focalizza sul fornire le informazioni sull'utente autenticato.
* ID client - Le applicazioni che interagiscono con gli endpoint conformi con OAuth 2.0 che richiedono una coppia di ID client segreto / segreto per l'autenticazione. Un'applicazione deve registrarsi con un servizio token per ottenere un ID client.
* Endpoint token - Utilizzato dal client per ottenere uno o più token presentando le informazioni sull'identità come un nome utente o una password, concedere l'autorizzazione o aggiornare il token.
* Endpoint autorizzazione - Utilizzato dal client per autenticare un utente tramite al IU al servizio token.
* Token - Una stringa trasparente o opaca che abilita un'applicazione a richiamare l'autenticazione e/o l'autorizzazione di un'identità.
* Token di accesso - Questo token viene utilizzato per essere inviato come informazioni sull'identità alle API. Contiene le informazioni sull'identità ed è valido solo per poco tempo.
* Token di aggiornamento - Questo token viene archiviato nel client che ha richiesto solo l'autenticazione. Viene utilizzato per ottenere un nuovo token di accesso, (ad es. aggiornare il token di accesso), se il token di accesso scade. Poiché il token di aggiornamento ha una durata molto lunga, non deve lasciare il sistema client ad eccezione di scopi di aggiornamento del token di accesso stesso.
* Cookie di identità - Dopo l'accesso al servizio token cloud di IBM, viene emesso un cookie contenente la tua identità nel tuo browser. Non ti sarà richiesto di accedere finché questo cookie esiste ed è valido. Scade dopo 24 ore, se ti scolleghi dal servizio token cloud IBM o se chiudi il tuo browser.
* Token web JSON - Uno standard basato su JSON (RFC 7519) per rappresentare i token di accesso. Il contenuto del token di accesso è trasparente, (ossia può essere facilmente letto). Un token basato su JWT vene generalmente firmato per essere in grado di verificare la prova di origine di tale token.
* Chiave pubblica - Può essere utilizzata per convalidare una firma di un token web JSON. Se si utilizza la codifica asimmetrica, la chiave pubblica può essere pubblicata in sicurezza per l'utilizzo da parte dei client.
* Chiave privata - Può essere utilizzata per creare una firma per un token web JSON. Questa chiave deve essere mantenuta segreta, altrimenti i token di accesso validi possono essere creati da altre persone.
* realmid - Identificativo per distinguere gli utenti da diversi registri utenti. Al momento i valori utilizzati sono "ID IBM" per gli utenti autenticati dal sistema ID IBM e "iam" per gli ID del servizio autenticati dal servizio token.
* identificativo - L'identificativo che non viene mai modificato e identifica univocamente un utente in un registro utenti (indicato dal parametro `realmid`). La combinazione <realmid>-<identifier> deve sempre dare un utente identificabile univocamente. Nel caso di un ID IBM, viene utilizzato l'identificativo univoco IBM 'IUI'.             
* oggetto - Il nome utente dell'identità. Spesso nello stesso formato di un indirizzo email. Nel caso di un ID IBM, è l'ID IBM l'identità. 
* Attestazioni personalizzate - Ulteriori informazioni non standard in un token web JSON.

### Terminologia della gestione dell'accesso 

* (PAP) Policy Administration Point - Punto che gestisce le politiche dell'autorizzazione di accesso.
* (PDP) Policy Decision Point - Punto che valuta le richieste di accesso per le politiche di autorizzazione prima di emettere le decisioni di accesso.
* (PEP) Policy Enforcement Point - Punto che intercetta la richiesta di accesso dell'utente a una risorsa ed effettua una decisione di accesso al PDP per ottenere la decisione di accesso (ossia se l'accesso alla risorsa viene approvato o rifiutato) e agisce sulla decisione ricevuta.
* (PIP) Policy Information Point - L'entità del sistema che agisce come un'origine dei valori dell'attributo (ossia una risorsa, un oggetto, un ambiente).
* (PRP) Policy Retrieval Point - Punto in cui le politiche dell'autorizzazione di accesso vengono archiviate, normalmente un database o un file system.
* oggetto - L'"oggetto" in una risorsa e in una coppia autorizzazione e oggetto, come una utente o un gruppo. La risorsa nella risorsa in cui può accedere l'oggetto.
* ruolo - Una raccolta di autorizzazioni che possono essere assegnate a un utente, un gruppo di utenti, al sistema, al servizio o all'applicazione che abilitano all'esecuzione di alcune attività.
* risorsa - Un oggetto logico o fisico su cui possono essere eseguite le azioni, come un'organizzazione, uno spazio, un database o una tabella.
* condizioni - Una funzione che viene valutata "True", "False" o “Indeterminato”.
* azioni - Un'attività definita che esegue un'applicazione su un oggetto o una risorsa come risultato di un evento.
* politica- Una serie di regole, un identificativo per l'algoritmo di combinazione delle regole e (facoltativamente) una serie di obblighi o avvisi. Può essere un componente di una serie di politiche.

## Ruoli definiti dal sistema 
{: #system_defined_roles}

I ruoli cloud IBM rappresentano una raccolta di azioni che vengono fornite dai servizi abilitati IAM.

Il raggruppamento delle azioni come ruoli fornisce flessibilità per il supporto delle azioni per ogni servizio
o risorsa utilizzando una serie minima di ruoli
definiti dal sistema. Ad esempio, se hai bisogno di un `Amministratore` per le VM, l'archiviazione e la rete,
puoi utilizzare il ruolo `Amministratore` per tutte e tre ma cambia solo
la destinazione della politica. `Amministratore` per le VM, `Amministratore` per l'archiviazione
e `Amministratore` per la rete.

*Cosa IAM cloud IBM non fa*: un'alternativa che viene utilizzata da altri sistemi di gestione dell'accesso
è di creare le risorse nel ruolo. Questo approccio inavvertitamente crea
un nuovo nome ruolo per ogni tipo di risorsa che viene introdotta nel sistema. Ad esempio,
con questo approccio avrai bisogno di un ruolo `VMAdministrator`, un ruolo
`StorageAdministrator` e un ruolo `NetworkAdministrator`
per coprire la gestione delle risorse per le VM, l'archiviazione e la rete.


La seguente tabella mostra i ruoli definiti dal sistema IAM e gli esempi di azioni da associare ad essi.

|Nome ruolo cloud IBM| Descrizione | Azioni di esempio|
|:-----------------|:-----------------|:-----------------|
|Visualizzatore|le azioni che non modificano lo stato (ad es. in sola lettura)| <ul><li>elencare dispositivi</li><li>lettura dell'oggetto di archiviazione </li><li>eseguire query</li><li>eseguire ricerche</li></ul>|
|Editor|le azioni che possono modificare lo stato e creare/eliminare le risorse secondarie|<ul><li>creare vm</li><li>eliminare vm</li><li>collegare spazio di archiviazione</li><li>riavviare</li><li>avviare/arrestare</li><li>ridenominare</li></ul>|
|Operatore|le azioni obbligatorie per configurare e utilizzare le risorse|<ul><li>aggiornamento della configurazione</li><li>avviare/arrestare vm</li><li>visualizzare log</li><li>backup/ripristino</li></ul>|
|Amministratore|tutte le azioni inclusa la capacità di gestire il controllo dell'accesso |<ul><li>invitare utente</li><li>creare vm</li>aggiornare le politiche di accesso utente </li><li>elencare dispositivi</li><li>creare vm</li><li>eliminare vm</li><li>collegare spazio di archiviazione</li><li>riavviare</li><li>avviare/arrestare</li><li>ridenominare</li><li>backup/ripristino</li></ul>|
|Amministratore fatturazione|le azioni relative alla gestione della fatturazione|<ul><li>aggiornare la carta di credito</li><li>elencare le fatture</li><li>scaricare fatture</li></ul>|

L'elenco più recente di ruoli definiti dal sistema può essere richiesto dal microservizio
PAP:

Comando Curl: 

`curl -X GET --header 'Accept: application/json' --header 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'`
    
    
## Formato azione servizio
{: #action_format}

Le azioni devono essere definite in 1 di 2 formati:
  
* Standard:

    `<service-name>.<component>.<verb>`
* Punto di intercettazione del controllo dell'accesso: 

    `<METHOD> /<api_route>`
  
### Standard
Molti servizi chiamano direttamente IAM PDP e possono modificare il codice di origine per supportare la formattazione dell'azione standard.  
 
 Questo formato deve includere tutte e tre le parti ed è alfanumerico, nessuno spazio o carattere speciale diverso da '-'.

`<service-name>.<component>.<verb>`

Dove 
* service-name - Il nome del servizio definito nel campo nome servizio CRN.
* component - la risorsa o la risorsa secondaria del servizio.
* verb - Verbo che definisce l'azione supportata per il componente nome del servizio. 
  
Ad esempio: `key-protect.keys.decode` 
* service-name = key-protect
* component = keys
* verb = decode

### Punto di intercettazione del controllo dell'accesso API REST
{: intercept_point}

In alcuni casi le richieste API REST vengono indirizzate tramite un gateway che agisce come un punto di intercettazione del controllo dell'accesso. IAM PDP viene richiamato direttamente dal punto di intercettazione prima della chiamata del servizio API REST corrente. Il servizio che elabora la richiesta API REST non richiama mai il IAM PDP.

Il punto di intercettazione conosce solo la rotta API REST e l'endpoint a cui inviare la richiesta. Consulta, [Considerations for Access Control Intercept Points](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/intercept_point.html#intercept_point_overview) per ulteriori dettagli.


 Questo formato deve includere tutte le parti e supportare i caratteri sicuri per gli URL come specificato da [RFC 1738](https://www.ietf.org/rfc/rfc1738.txt).
 
 
`<METHOD> /<api_route>`
  
Dove
* METHOD - Il metodo API REST. 
* api_route - L'URI per l'API REST.

Ad esempio: `GET /v1/things/thing123`
* METHOD = GET
* api_url = /v1/things/thing123

<!---
# Setting up access control for your service
{: #setup_access_mgmt}

Onboarding a service to {{site.data.keyword.Bluemix_notm}} is a different set of operations than onboarding a service with Cloud IAM. Technically you can onboard with {{site.data.keyword.Bluemix_notm}} and Cloud IAM independently and in any order. The Cloud IAM team is working with the {{site.data.keyword.Bluemix_notm}} service onboarding team so that the {{site.data.keyword.Bluemix_notm}} service on boarding process will also include Cloud IAM onboarding.

To setup access control for your service you must use the following steps.

#### Step 1: Create a service id by making this http request:
  ```
  POST https://iam.ng.bluemix.net/serviceids
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "name": "<service id name>",
    "description": "<service id description>",
    "boundTo": "<crn>"
  }
  ```
Curl command:
  ```  
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"name": "<service id name>", "description": "<service id description>", "boundTo": "<crn>"}' 'https://iam.ng.bluemix.net/serviceids'
  ```
  
### Service id 
  
The service id name can be the same as the service name that appears in the crns for your service.
  
Your service id must be bound to an account, organization, or space. This binding determines who can manage your service id. For example, the administrator where your service id is bound are able to update or delete. Your {{site.data.keyword.Bluemix_notm}} token needs to have access to the account, organization, and space you are binding the id to. To bind to an account, the `boundTo` crn must look like the following: 

`crn:v1:::<service name>::a/<account id>:::` 
  
For an organization it must look like the following:
`crn:v1:<cname>:<ctype>:<service name>:<region>:o/<organization id>:::` 
  
For a space it must look like the following:
`crn:v1:<cname>:<ctype>:<service name>:<region>:s/<space id>:::`  
  
The `boundTo` value specified has no affect on which resources your service id can access. 
  
IAM access policies control which resources your service id can access. Even though your service id is bound to an IBM organization, IAM policies can be created that allow your service id to access resources outside of that organization.  When on boarding with IAM the first access policy that is created by the IAM team allows the service id to create policies for any resources owned by your service.

See [createServiceid](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createServiceid) for more information on this api and related apis.

###Service crn

The service-name in the `boundTo` crn must match the service name that appears in the crn for your service.
  
See the [CRN spec](https://github.ibm.com/ibmcloud/builders-guide/blob/master/specifications/crn/CRN.md) for help filling in these fields.

From the response, save metadata&ndash>uuid and metadata&ndash>crn, which are your service id and service id crn.


#### Step 2: Contact the AccessControl Squad at [#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 
Your service id will be given the role of Administrator of policies for your service's resources.

Use this format:
```
IAM adopter service info

service id: uuid from step #1
service name: your service name as it will appear in the crns for your service
```

#### Step 3: You must create an api key from your service id. Use the following http request:
```
  POST https://iam.ng.bluemix.net/apikeys
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "boundTo": "<service id crn>",
    "name": "<api key name>",
    "description": "<api key description>"
  }
```
Curl command: 
```
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"boundTo": "<service id crn>", "name": "<api key name>", "description": "<api key description>"}' https://iam.ng.bluemix.net/apikeys
```
`boundTo` needs to be the crn of your service id (field metadata&ndash>crn saved from step 1’s response). The name and description can be anything.

From the response, save entity&ndash>apiKey.

See [createAPIKey](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createAPIKey) for more information on this api and related apis.

#### Step 4: Get an access token for your service id's API key. 

When the permission is established, your service can make PAP and PDP requests for your service's resources.

Use the entity **apiKey** field from step #3, this is your API key value (apikey_value).

  * Then get the token with the API key value (make sure you use escape characters):

    Curl Command: 
    ```
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<apikey_value>" "https://iam.ng.bluemix.net/oidc/token"
    ```

Use the **access_token** field in the result, this is your api key token(for your service id).


#### Step 5: Register the list of possible service actions for the service name.

  a. Map service actions to IAM System Defined Roles. This mapping is used later during the service registration.

  * A list of IAM System Defined Roles can be found by performing the following request:
Curl command:
```
curl -X GET &ndash&ndashheader 'Accept: application/json' &ndash&ndashheader 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'
```

**Note:** Use the _crn version_ of the IAM System Defined Roles in your service registration payload.

The following is an example of mapping service actions to roles.

  <table>
    <tr>
      <th>API Endpoint</th>
      <th>Service Action</th>
      <th>IAM System Defined Roles</th>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}</td>
      <td>key-protect.keys.create</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>GET /api/keys/{key_id}</td>
      <td>key-protect.keys.read</td>
      <td>Viewer, Editor, Administrator</td>
    </tr>
    <tr>
      <td>PUT /api/keys/{key_id}</td>
      <td>key-protect.keys.update</td>
      <td>Editor, Administrator</td>
    </tr>
    <tr>
      <td>DELETE /api/keys/{key_id}</td>
      <td>key-protect.keys.delete</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/encode</td>
      <td>key-protect.keys.encode</td>
      <td>Editor, Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/decode</td>
      <td>key-protect.keys.decode</td>
      <td>Editor, Administrator</td>
    </tr>
  </table>

  b. Use the following command line to register your service with the `PAP`:
```
  curl -X PUT -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'Authorization: <api key token>' -d '{
    "displayName": {
      "default": <service display name>
    },
    "actions": [{
      "id": <service_action>,
      "displayName": {
        "default": <service action display name>
      },
      "roles": [<system_defined_role_crn>]
    }]
  }' 'https://iampap.ng.bluemix.net/acms/v1/services/<service_name>'
  ```
  
Actions must be defined as specified in the 
[Service Action Format](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/index.html#action_format).
  
For example, using the standard format:

  `<service-name>.<component>.<verb>`
  
  Using action `key-protect.keys.decode` from the previous example 
  * service-name = key-protect
  * component = keys
  * verb = decode
  
  [TODO: Also support REST like action format, yet to be approved]: <>

#### Step 6: Configure the service to use the PEP SDK in order to check permissions with the PDP. Pick the corresponding SDK language.

  * [PEP SDK for Java](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Java)
  * [PEP SDK for Nodejs](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Node)
  * [PEP SDK for Python](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Python)


<!---
# Identity and Access Management Adopter Guidelines
{: #iam_guidelines}

Onboarding a service to {{site.data.keyword.Bluemix_notm}} is a different set of operations than onboarding a service with Cloud IAM. Technically you can onboard with {{site.data.keyword.Bluemix_notm}} and Cloud IAM independently and in any order. The Cloud IAM team is working with the {{site.data.keyword.Bluemix_notm}} service onboarding team so that the {{site.data.keyword.Bluemix_notm}} service on boarding process will also include Cloud IAM onboarding. Until that work is complete please use the following onboarding steps.

- Users are identified with their IBMid.
  - Users authenticate with their IBMid and password.
  - Authentication returns a UAA/OAuth token which is used to access services within the IBM Cloud.
  
- Services are identified by their ServiceIDs.
  - Services authenticate with their ServiceID and APIkey.
  - Authentication returns an OAuth token which is used to access other services within the IBM Cloud.
  
- Services grant access to their resources by creating *Access Policies*.
  - *Roles* can be viewed and *Access Policies* can be managed through the 
  *Policy Administration Point (PAP)*.
  - Actions are permitted or denied through the *Policy Enforcement Point (PEP)* and *Policy Decision Point (PDP)*. 
  

## Creating a ServiceID
{: #create_serviceid}

To create a ServiceID you must use one of the following steps:

Make a one-time request for your ServiceID/APIkey.

 * Create a ServiceID with [swagger](https://iam.ng.bluemix.net/docs).
```
POST /serviceids
```
 * Create a ServiceID using `curl`.
```
curl -X POST -H "Authorization: $CF_TOKEN" -H 'Content-Type: application/json' -d '{"name": "IAMdemo", "description": "IAM demo of adopting service", "boundTo": "crn:v1:staging:public:docker-registry:us-south:o/57666a74-e136-4eb0-a085-220345fac266:::"}' 'https://iam.ng.bluemix.net/serviceids’
```
**Note**
The `boundTo` is the {{site.data.keyword.Bluemix_notm}} Org that is owned by you or your admin.

## Creating a ServiceID metadata response
{: #create_serviceid_metadata}

The following is a ServiceID metadata response using `curl`. Your service ID is expressed with a UUID and CRN format.

```
{"metadata":{\
"uuid":"ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07",\
"crn":"crn:v1:staging:public:iam:us-south:o/57666a74-e136-4eb0-a085-220345fac266::\
serviceid:ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07",\
"version":"1-4d9b1b10ce893f750a2d7e0d6ee34fd7"},"entity":{"boundTo":"crn:v1:staging:public:docker-registry:\
us-south:o/57666a74-e136-4eb0-a085-220345fac266:::","name":"IAMdemo","descripti\
on":"IAM demo of adopting service"}}
```

## Creating an APIkey for your ServiceID
{: #create_apikey_serviceid}

Create an APIkey
```
POST /apikeys
```

The following is a `curl` example of creating an APIkey
```
curl -X POST -H 'Authorization: $CF_TOKEN' -H 'Content-Type: application/json' -d '{"boundTo": "crn:v1:staging:public:iam:us-south:o/57666a74-e136-4eb0-a085-220345fac266::serviceid:ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07", "name": "IAMdemo", "description": "IAM deom of adopting service"}' https://iam.ng.bluemix.net/apikeys
```

## Authenticating with an APIkey
{: #auth_apikey}

The following is a `curl` example of authenticating with an APIkey
```
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H \
"Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-ty\
pe%3Aapikey&apikey=DuE2s….bfRKc=" "https://iam.s\tage1.ng.bluemix.net/oidc/token”
{"access_token":"eyJraWQiOiIyMDE2MTAyNC0wMDowMDowMCIsImFsZyI6IlJTMjU2In0.eyJpZG\
VudGlmaWVyIjoiU2VydmljZUlkLTNlYzBkZDAyLTdhMTAtNDBiZi05MmU3LWI5YTMyOTU0N2MwNyIsI\
nN1YiI6IlNlcnZpY2VJZC0zZWMwZGQwMi03YTEwLTQwYmYtOTJlNy1iOWEzMjk1NDdjMDciLCJzdWJf\
dHlwZSI6IlNlcnZpY2VJZCIsImFjY291bnQiOnsiYnNzIjoiMDY0Zjg3NTZlMzZlODk5MDAyYjliM2M\
wNzZiZTM3OGIifSwibWZhIjp7fSwiaWF0IjoxNDc5Mzk3MTYwLCJleHAiOjE0Nzk0MDA3NjAsImlzcy\
I6Imh0dHBzOi8vaWFtLnN0YWdlMS5uZy5ibHVlbWl4Lm5ldC9vaWRjL3Rva2VuIiwiZ3JhbnRfdHlwZ\
SI6InVybjppYm06cGFyYW1zOm9hdXRoOmdyYW50LXR5cGU6YXBpa2V5Iiwic2NvcGUiOiJvcGVuaWQi\
LCJjbGllbnRfaWQiOiJkZWZhdWx0In0.APRVqQmfUwn6K4Kg2sicT_kGpqSGQXr4Vua8Q5p4B0_dfGE\
tbbe10JqHeE4ovud6u8xjclAIcqCcbjIH4RijnUNGReVse49gS6JlXxmiNGA8OVlNGjiL68ygIpYsj-\
crx8kVuTrXAFqx9lhLEBhAzDneldu-gjSz7wrQKqISikcMXPXQkmLDuoT-OGNq8rG4fCiENBiweUrGf\
_Yw9W5NSiWyQGdWmczS70Krc_hx1iXskmt8pz5_0_vPXY6_tG5rY6KPw-bHO1wux91Q7aTZwCmaL0zI\
F2d3cIuFe1XywJ_926MfwWy65MxC3xv7-_rsZMFoprrLtBsuEnshNWUDhg",
"token_type":"Bearer","expires_in":3600,"expiration":1479400760}
```

## Registering your ServiceID with IAM
{: #register_serviceid}

To complete the on boarding process, contact the AccessControl Squad at
[#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 

Your service id will be given the role of Administrator of policies for your 
service's resources.

Call the `PAP` and `GET` the existing policies
```
curl -X GET -H 'Authorization:<APIkeyToken>' \
'https://iampap.ng.bluemix.net/acms/v1/scopes/global/service_ids/\
ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07/policies'

Response:
{"policies":[]}  <-- no policies yet
```

## Creating access policies
{: #creating_policies}

Now that you are fully on boarded, you can begin creating access policies 
for resources owned by your service.
-->

# ID servizi laboratorio e chiavi API

interconnect-service1:
  * ServiceId-2bc4561c-615f-4ba3-ab50-eba3b70a69d3
  * 7DRDYlbFM8Mpt7cOKS7clQisOItOfFcvItkd4MQsd20M

interconnect-service2:
  * ServiceId-089f58e9-f0a0-4b47-b3db-a2d9036080aa
  * rOB0ZqGR1pbiWxNMbn_OfFDmuJcULhqnYW_G0hNnJj0w

interconnect-service3:
  * ServiceId-9a57c3ed-2a8d-45ff-8b34-a7feb80e81bd
  * 6qZoPsd_V47hQQHHVFR1Z8PeGwTZKmNxHgGlURH7OIPf

interconnect-service4;
  * ServiceId-df633c5f-dee3-4e7b-87c3-7a3ed57d6509
  * 3yICAhsR55nlXJLjPA2nLBcAM1SX7LrXpOabjivVeteQ

interconnect-service5:
  * ServiceId-e3703b76-4f91-4323-9b6d-db3122952a72
  * 1ZD8qf_jqHC7JVOzrrvbuI3Dcr153hkGsr4Ll7EvsXKW

interconnect-service6:
  * ServiceId-2a31b14e-6cad-4597-82cf-04f2cb16c26d
  * XFROeDFVyBnJfecSjNhZngPDOniX-5qXl9QWZrsuNjYY

interconnect-service7:
  * ServiceId-56b98026-bb1c-4166-8128-c4841d10373c
  * cBponeC40MEgPy4mW55kb26XbMFAVmF0y2T3T1fYXJuL

interconnect-service8:
  * ServiceId-7a9cf953-044e-474a-9ffb-e66a1b68f437
  * OEGprDQNk7TLxFNrCbKfvLGxQRrbGS-PvhKSCUYJYn1a

interconnect-service9:
  * ServiceId-147203b6-0156-41c6-a28c-7306f047eebb
  * 2OiRisDKDXYA0_0BtlA7OyBk-7II9NUa709HgbF-D_kY

interconnect-service10:
  * ServiceId-87909073-acb8-403c-ab32-91d632e6c5a6
  * 93eWV_Ns2UrjNGENaaau1yOQmGDvTO2FxEivThGIZUOV

interconnect-service11:
  * ServiceId-0e2ec208-926e-4db7-aab4-c0d3bf44865f
  * gEa6bECSMAVF68cS5AbckIKp47_OX3_q63JNWI6-Q5Y0

interconnect-service12:
  * ServiceId-c793ae24-5f43-4c55-815a-830b8c79d1ee
  * WRSnr-FJZ_mI2DbG-8MNqPdAZHq3IkVZU-WbWL7l7uNC

interconnect-service13:
  * ServiceId-b426e816-6975-47df-ac69-01c08560ef3e
  * MkFJJ_zJDg5MiIRUo78dzCC-Mmw3r9DSzZVMvHZ7A63Z

interconnect-service14:
  * ServiceId-d97a9df4-6dbe-43ab-8b10-a70bb3ff9085
  * N63GX1wfo6UDc5kNrEWYHcPT27bD9V0JLmoB-iKsPfEb

interconnect-service15:
  * ServiceId-c6090a5b-569d-40cc-84f5-12480a9ede60
  * xLuJdPmW5npQMuHs4hyJOWZMaYY7i_DwZOSjWlZjnjjK

interconnect-service16:
  * ServiceId-c1d34878-cac3-43a3-bad6-a5b4992d9ed9
  * UZjSMGF8Aw42lzbHtkgDH14FyJxe0s0aN0O4Qk9uBe8T

interconnect-service17:
  * ServiceId-9ccaba36-6b07-4e9b-8b97-fbe1111f4908
  * CJb3qUI3cQWUiMMSt2RuL3ti9yE-F2-i2-1yIfowOM30

interconnect-service18:
  * ServiceId-84a01c41-8330-49e3-842f-b45eaa368d3d
  * 8-qw4_k5Sbjd1sxAiKksHubfPIlkjK2C9S0DnK-WpPDo

interconnect-service19:
  * ServiceId-2ef5d7ea-7ce0-453d-aa70-fbc5f4b781ef
  * Cz4QHZR_qd_WUZsScF-dVcu31J08dPuF_gszMd4oCLJj

interconnect-service20:
  * ServiceId-9e85525e-fe29-45e1-81b5-0681cd0b7f22
  * -OeamgjtKqnGUmdKFAVOWjKhYJMYP8HstCcPrRKfy4V9

interconnect-service21:
  * ServiceId-62c49423-3205-446e-a4aa-e24deb9b158e
  * N2XQ6MpKTvRJX_2IuDQoOiMK5AIhICUFj2wMVyg8O6Pn

interconnect-service22:
  * ServiceId-2de4c08b-f2cc-4e93-bb8b-eebf2222f93e
  * lEOzJvJJV0EgDjQQa8g5kr_D-PawYqIN-QE1QTNpoD5S

interconnect-service23:
  * ServiceId-49e6dc57-70f2-4a69-aac9-311394454475
  * G7epLqdbohZ8tVs8Jcx4qSjlMzlzrw2piNEnPiP4RZ7A

interconnect-service24:
  * ServiceId-7a4ac3ec-bd69-4dbf-8439-f8f5a2ffb88a
  * I7d2KnqbyeQG1rk1AcKeVXgNT1iqCwhSAhan9g-pWucx

interconnect-service25:
  * ServiceId-542a018b-9248-4bb3-bfc1-e0c9d1e70b46
  * WUl0OMnGkLP1BF3bdkqOJeT3niuwD2p1kWd8In05jpho

interconnect-service26:
  * ServiceId-c94f5b5e-0d43-4843-8153-d402fae7e1b5
  * dBtmioisFz_7gTYBPL1IArA_E9F4HYnYYAKVZJfxIcv3

interconnect-service27:
  * ServiceId-37986f6b-325c-42c3-8973-c88c7d365c0c
  * SY1kOsSpSPSLOocmBMwuPWO7u-60aglBliO2Qa4tu4dv

interconnect-service28:
  * ServiceId-08a48402-a02c-4fe6-9260-635188202aad
  * QFaQPoJaYAcVsVlmnVIlkO1haVY_xg8ZZEt-AkmAzAIn

interconnect-service29:
  * ServiceId-e9414ce2-c8d5-44d6-be68-f6c5176f4482
  * FKiafH2hr8eooB0nS6N-3vDrYkIbltzBZb688U8JxpvD

interconnect-service30:
  * ServiceId-e5caa06b-4087-4f55-b51c-bbbad4d78d84
  * 2hcjXXt2G7hmyqAhWlqhXHL9OwFlNdr2_3NZ3tVkBMF2

interconnect-service31:
  * ServiceId-e71b84e8-fe53-4e40-af46-af26f9e59db3
  * 0vwL6DjNl8ATJJ_mvHrEfuzYt9dyeZulA1nKj_q3zUjf

interconnect-service32:
  * ServiceId-fc200643-5788-4af9-a1a5-847d373331b3
  * gM919kowr90lDhuRNbvc-kt3WOKW0YQLRGYNqLVbwC-B

interconnect-service33:
  * ServiceId-df0898a2-8b19-49fc-a88b-f4868c6d2b18
  * KjDoJ5z2WGv2hIG9PRJuylkh0SPLnvAYLY7mVRkmCGGf

interconnect-service34:
  * ServiceId-1eaa9835-fb15-49a6-b19c-74970795a33f
  * wUXkKrKqJmZO8S4io1QoryPlZml9_G6A4L-6WHftl7Ny

interconnect-service35:
  * ServiceId-14f7e5fc-5be8-49b5-9843-4b338cc0c34e
  * Fi7nwbNHJVU7CXAba-MJR2jiCSG524zQVb5CIFWwAM1D

interconnect-service36:
  * ServiceId-fdfe7ec7-1ec7-4798-bb1d-1815b0d31b57
  * wEj7KGnheNnadxzLTOjOe1TlSqgOB75pEzEV5tz6xxl9

interconnect-service37:
  * ServiceId-4488b45e-992f-4479-8cc1-c7160dafb067
  * weXbJ6CkIgcY0K6Aly3yNmjVb6a7cFWhlphaiD27XMdY

interconnect-service38:
  * ServiceId-5830536e-b38e-47a4-9b2b-d3c996a545dd
  * ElMOFJEGKh6qbq1CLoImqK8gvSP0KQLyxmPlY8bZecbw

interconnect-service39:
  * ServiceId-a03d5d46-d064-41c3-b330-35dfc149333b
  * qR0PIg9jT-cPWbj8ShWmha42qXP5Qijoin8l0TfxBH8w

interconnect-service40:
  * ServiceId-8b7e2cdc-b1c6-4707-8554-7c42c7ff1276
  * VZofAdNllinmi7jQMfQlmvbbJcbpAguunzKKeanweF8c

interconnect-service41:
  * ServiceId-cda9707c-8fee-497d-a514-e593b4e01002
  * Eoj46Od3qp381LaEc5nhYj-CIGZmrJKt4Gc9oRfB1naD

interconnect-service42:
  * ServiceId-c743b5f8-5ba6-464e-86ed-83e8dd3ee1b5
  * nespdN1a1I_TQ7pwgBD2gCgtjWpHJrUigUk_69GJTCDC

interconnect-service43:
  * ServiceId-40513e4d-53e6-4dde-8baf-f3a5c82ba234
  * lYCUBuwNSyW9DNOXcBXfof4znnrZihALfdbTRvytni48

interconnect-service44:
  * ServiceId-afee12ac-c58a-433c-be98-416acbb670e2
  * 2SBqJdVgwwuBBV8k3eDg6_4NVeDBaLynQgImqct4DfFv

interconnect-service45:
  * ServiceId-65a3733a-eb0a-402b-ae91-5a412dc9725f
  * to5dKzNvpNLearwdg0KeJc-zftazx-xlu0yt1uk1Q0VP

interconnect-service46:
  * ServiceId-10413fbe-10aa-4bb5-b641-65a9bbeb9d53
  * kKyrLaYCqbhNxH-Axcv7ABcX0aGdPw-MR2nYjkVORVhY

interconnect-service47:
  * ServiceId-82ead5c9-195a-4780-bbec-b3655a475896
  * -uTIzbpCJSIn45vYZP86YtrKzpgwyQZThibltlL2rRgu

interconnect-service48:
  * ServiceId-c06741b5-0ec8-4131-8b2b-276a4f72c0a1
  * 6FpfmxrQpdD00X4_m8Jhk-r4Bwg4x47BZRnLfA-qVe67

interconnect-service49:
  * ServiceId-ee93887b-11d1-49b9-be63-2764a42beb57
  * 46ZqlkPk_n3QjTbweHa3X4HLQc4N-_O0ODYSfDHu_vui

interconnect-service50:
  * ServiceId-71dd52eb-7bbc-4ff0-aaf3-70816830660e
  * vDhkWd9DzUf7V_5cWaMhmz8IPmyshCJlZcu_tf39EyNm


