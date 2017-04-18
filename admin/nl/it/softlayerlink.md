---

 

copyright:

  years: 2016, 2017
lastupdated: "2017-01-11"
 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Aggiornamento e unificazione degli account di fatturazione {{site.data.keyword.Bluemix_notm}} e SoftLayer
{: #softlayerlink}

Se disponi di un account {{site.data.keyword.Bluemix_notm}} di prova e vuoi accedere al dashboard Infrastruttura, devi eseguire l'aggiornamento a un account {{site.data.keyword.Bluemix_notm}} con pagamento a consumo. Devi inoltre eseguire l'aggiornamento se desideri utilizzare altre risorse a consumo che non sono disponibili in un account di prova o se il tuo account di prova è terminato. 

Puoi unificare i tuoi account {{site.data.keyword.Bluemix_notm}} e SoftLayer esistenti collegando tali account. Quando colleghi i tuoi account, ricevi la fattura attraverso {{site.data.keyword.Bluemix_notm}} sia per le risorse {{site.data.keyword.Bluemix_notm}} che per le risorse SoftLayer.

**Attenzione:** un account di sottoscrizione {{site.data.keyword.Bluemix_notm}} non può essere collegato a un account SoftLayer. Per accedere al dashboard Infrastruttura, devi creare un account Pagamento a consumo, un secondo account che viene collegato automaticamente a un account SoftLayer. Riceverai quindi due fatture, una per ogni account {{site.data.keyword.Bluemix_notm}}. Anche se le risorse dell'infrastruttura verranno fatturate in un account Pagamento a consumo separato, le risorse possono essere utilizzate con applicazioni e servizi nel tuo account di sottoscrizione. Ad esempio, se attivi un servizio Watson nel tuo account di sottoscrizione, puoi copiare le credenziali del servizio e quindi aggiungerle alla tua applicazione bare metal proveniente dal tuo account Pagamento a consumo. 
{:shortdesc}

## Aggiornamento a un account Pagamento a consumo di {{site.data.keyword.Bluemix_notm}}
{: #upgradetopayg}

Quando ti colleghi a {{site.data.keyword.Bluemix_notm}} utilizzando un account di prova, non puoi accedere al dashboard Infrastruttura {{site.data.keyword.Bluemix_notm}}. Se vuoi che le tue applicazioni utilizzino le risorse dell'infrastruttura, devi eseguire l'aggiornamento a un account Pagamento a consumo.

Per aggiornare il tuo account di prova in un account Pagamento a consumo {{site.data.keyword.Bluemix_notm}}, completa la seguente procedura:

 1. Fai clic su **Account** &gt; **Fatturazione**.
 2. Seleziona **Aggiungi carta di credito**.
 3. Immetti i dettagli di fatturazione richiesti. 
 4. Leggi e accetta i termini e le condizioni per l'account Pagamento a consumo. 
 5. Al termine, fai clic su **Aggiorna**. 
 
Una volta eseguito l'aggiornamento a un account Pagamento a consumo, le opzioni di **Infrastruttura** vengono elencate nel **Catalogo** {{site.data.keyword.Bluemix_notm}}. Se superi la franchigia consentita, riceverai una fattura mensile da parte di {{site.data.keyword.Bluemix_notm}}. La fattura sarà in dollari americani (USD) e verranno descritti gli addebiti delle risorse. 

## Unificazione degli account {{site.data.keyword.Bluemix_notm}} e SoftLayer
{: #unifyingaccounts}

Puoi unificare i tuoi account {{site.data.keyword.Bluemix_notm}} e SoftLayer per utilizzare risorse combinate. Quando colleghi gli account {{site.data.keyword.Bluemix_notm}} e Softlayer, riceverai un'unica fattura {{site.data.keyword.Bluemix_notm}}. Se hai un account {{site.data.keyword.Bluemix_notm}} esistente, la fatturazione tramite {{site.data.keyword.Bluemix_notm}} per le risorse SoftLayer parte dal nuovo ciclo di fatturazione che inizia dopo il collegamento degli account.

**Importante:** tutti gli account collegati in {{site.data.keyword.Bluemix_notm}} devono essere del tipo Pagamento a consumo. Puoi creare un nuovo account Pagamento a consumo o collegarne uno esistente. In alternativa, puoi collegare un account di prova esistente, che verrà tuttavia aggiornato in un account Pagamento a consumo. Gli account Sottoscrizione di {{site.data.keyword.Bluemix_notm}} non possono essere collegati.  

Dopo che gli account sono stati collegati:

* Devi utilizzare le credenziali dell'ID IBM per accedere a entrambi gli account SoftLayer e {{site.data.keyword.Bluemix_notm}}.
* Eventuali sconti SoftLayer esistenti vengono applicati agli addebiti {{site.data.keyword.Bluemix_notm}}. 
* Riceverai un'unica fattura in dollari americani (USD).
* Puoi monitorare l'utilizzo delle tue risorse {{site.data.keyword.BluSoftlayer}} nell'interfaccia utente {{site.data.keyword.Bluemix_notm}}. 

**Attenzione:** una volta collegati, gli account non possono più essere scollegati. 

Se hai un account SoftLayer e desideri collegare gli account SoftLayer e {{site.data.keyword.Bluemix_notm}}, completa la seguente procedura:

 1. Dal {{site.data.keyword.slportal}}, fai clic su **Collega un account {{site.data.keyword.Bluemix_notm}}**.
 2. Leggi e accetta le condizioni di collegamento degli account SoftLayer e {{site.data.keyword.Bluemix_notm}}.
 3. Quando richiesto, fornisci l'indirizzo e-mail associato al tuo account {{site.data.keyword.Bluemix_notm}}. Se non hai un account {{site.data.keyword.Bluemix_notm}}, fornisci l'indirizzo e-mail che desideri utilizzare, quindi segui le istruzioni per ricevere l'invito a {{site.data.keyword.Bluemix_notm}} e crea un account.

Per collegare gli account, devi essere un utente master dell'account SoftLayer.

Dopo aver collegato gli account, nell'intestazione generale di SoftLayer viene visualizzato il link **Vai a {{site.data.keyword.Bluemix_notm}}**. Facendo clic su questo link, arrivi alla pagina di accesso {{site.data.keyword.Bluemix_notm}}. Inoltre, il link **SoftLayer** è ora disponibile nell'intestazione di {{site.data.keyword.Bluemix_notm}}. Facendo clic sul collegamento, accedi attraverso una nuova finestra alla home page di {{site.data.keyword.slportal}}.

Le offerte dell'infrastruttura {{site.data.keyword.Bluemix_notm}} sono collegate a una rete a tre livelli, segmentando il traffico pubblico, privato e di gestione. Le offerte dell'infrastruttura sull'account {{site.data.keyword.Bluemix_notm}} di un cliente potrebbe trasferire i dati da uno all'altro attraverso la rete privata a costo zero. Le offerte dell'infrastruttura, quali i server bare metal, i server virtuali e l'archiviazione cloud, si collegano ad altre applicazioni e altri servizi nel catalogo {{site.data.keyword.Bluemix_notm}}, ad esempio i servizi Watson, contenitori o runtime, attraverso al rete pubblica. Il trasferimento dati tra questi due tipi di offerte viene misurato e addebitato a tariffe di larghezza di banda della rete pubblica standard.

## Come invitare membri del team SoftLayer in {{site.data.keyword.Bluemix_notm}}
{: #invite_users}

Quando colleghi gli account {{site.data.keyword.Bluemix_notm}} e SoftLayer, puoi invitare i membri del tuo team SoftLayer a unirsi a {{site.data.keyword.Bluemix_notm}}. In alternativa, puoi invitare successivamente i membri del team SoftLayer dall'interfaccia utente {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Dall'interfaccia utente {{site.data.keyword.Bluemix_notm}} puoi scegliere di invitare tutti i membri del tuo account SoftLayer oppure puoi selezionare singoli membri. Quando inviti membri del team, devi impostare il ruolo account {{site.data.keyword.Bluemix_notm}} ruolo per gli invitati. Per ulteriori informazioni sui differenti ruoli in {{site.data.keyword.Bluemix_notm}}, vedi [Ruoli utente](https://console.ng.bluemix.net/docs/admin/users_roles.html#userrolesinfo).

Per invitare membri del team a unirsi all'account {{site.data.keyword.Bluemix_notm}}, devi essere un utente master dell'account SoftLayer.

Per invitare membri del team tramite {{site.data.keyword.Bluemix_notm}}, completa la seguente procedura:

 1. Fai clic su **Account** &gt; **Invita membri del team**.
 2. Fai clic su **Aggiungi** per eseguire l'autenticazione nel tuo account SoftLayer e visualizzare un elenco di membri del team dal tuo account {{site.data.keyword.BluSoftlayer}}.
 3. Seleziona i membri del team da invitare e fai clic su **Invia**.
 
Il membro del team riceve un'e-mail che include un link **Unisciti all'organizzazione**. Se il membro del team non dispone di un ID IBM, viene reindirizzato a una pagina di registrazione. Successivamente, il membro del team può immettere alcune informazioni di base e creare il proprio account {{site.data.keyword.Bluemix_notm}}.

Per ulteriori informazioni su come invitare i membri del team attraverso l'interfaccia utente {{site.data.keyword.Bluemix_notm}}, vedi [Come invitare membri del team](https://console.ng.bluemix.net/docs/admin/users_roles.html#inviteteammembers).

## Passaggio all'ID IBM
{: #ibmid_switch}

L'autenticazione in SoftLayer utilizza adesso un ID IBM per fornire un singolo accesso per tutti i {{site.data.keyword.Bluemix_notm}}. Gli account SoftLayer esistenti verranno abilitati a passare all'autenticazione tramite ID IBM. Una procedura guidata di migrazione ti guiderà in questo passaggio.
{:shortdesc}

Se sei un utente master o non visualizzi un prompt per passare a un ID IBM nel {{site.data.keyword.slportal}}, [Contatta il supporto IBM](/docs/support/index.html#contacting-support) per assistenza su come abilitare questa funzione.

Quando inizi a passare a un ID IBM, puoi sempre annullare il passaggio prima di completare il processo. Tuttavia, ogni volta che accedi verrà visualizzato il prompt per passare a un ID IBM. Ogni account SoftLayer che prevedi di collegare a un account {{site.data.keyword.Bluemix_notm}} deve appartenere a un unico ID IBM con un indirizzo e-mail univoco. 

Per passare dal tuo nome utente SoftLayer esistente a un ID IBM, completa la seguente procedura:

 1. Accedi al tuo account SoftLayer. Quando viene visualizzato il prompt per passare a un ID IBM, fai clic su **OK**. 
 
    Se hai già eseguito l'accesso (e hai fatto clic su **Dopo** nel prompt per passare a un ID IBM), ma vuoi passare all'autenticazione con ID IBM nella sessione corrente, vai alla pagina Modifica profilo utente e fai clic su **Passa a ID IBM**.
	
 2. Segui le istruzioni della procedura guidata per creare il tuo ID IBM. 
 
    Per creare un nuovo ID IBM, immetti un indirizzo e-mail che non sia attualmente utilizzato da nessun ID IBM. Il nuovo ID IBM utilizzerà tale indirizzo come nome utente e indirizzo e-mail. Una volta che l'ID IBM è stato creato, puoi aggiornare l'indirizzo e-mail associato all'ID IBM, ma non puoi modificare il nome utente. L'e-mail di invito verrà indirizzata all'indirizzo fornito.
    
    Dopo aver completato la procedura guidata, riceverai un'e-mail con il tuo codice di registrazione.
 
 3. Quando ricevi l'e-mail, segui il link o copia l'URL in un browser e immetti quindi il codice di registrazione. Il codice è valido per 7 giorni e puoi utilizzarlo solo una volta.
 
    Dopo il passaggio all'autenticazione tramite ID IBM, puoi accedere al tuo account solo con il tuo ID IBM. Al prompt di accesso dell'account, vai alla sezione **Accesso account ID IBM** e fai clic su **Accedi con ID IBM**. Non utilizzare i campi **Nome utente** e **Password** che utilizzavi in precedenza con il tuo ID SoftLayer.
 
Se sei un nuovo cliente, quando controlli il tuo ordine ti verrà chiesto il tuo ID IBM esistente o di crearne uno nuovo. 

 * Per utilizzare un ID IBM esistente, immetti il nome utente o l'indirizzo e-mail dell'ID IBM se è univoco (vale a dire, che non sia condiviso tra più ID IBM). 
 
 * Per creare un nuovo ID IBM, immetti un indirizzo e-mail che non sia attualmente utilizzato da nessun ID IBM. Il nuovo ID IBM utilizzerà tale indirizzo come nome utente e indirizzo e-mail. Una volta che l'ID IBM è stato creato, puoi aggiornare l'indirizzo e-mail associato all'ID IBM, ma non puoi modificare il nome utente. L'e-mail di invito verrà indirizzata all'indirizzo fornito.

Per risolvere eventuali problemi di accesso con il tuo ID IBM, vedi [Risoluzione dei problemi di accesso a Bluemix](/docs/troubleshoot/ts_accessing.html#accessing).


### Abilitazione degli utenti al passaggio all'ID IBM
{: #link_accounts_resellers}

In alcuni casi, prima che un utente possa passare a un ID IBM, un rivenditore o un distributore deve abilitare l'account ad utilizzare l'autenticazione tramite ID IBM. 

 * Per abilitare un account esistente con le credenziali legacy SoftLayer per utilizzare l'autenticazione ID IBM, [Contattare il supporto IBM](https://console.ng.bluemix.net/docs/support/index.html#contacting-support) per abilitare la migrazione all'ID IBM. Questa procedura deve essere abilitata per ogni account utente finale esistente che desideri collegare a un account {{site.data.keyword.Bluemix_notm}}.
 
 * Per assicurarti che i nuovi account utente sono stati creati con un ID IBM, l'attributo `CREATE_NEW_ACCOUNT_WITH_IBMid_AUTHENTICATION`       deve essere impostato nell'account utente master immediato. [Contatta il supporto IBM](https://console.ng.bluemix.net/docs/support/index.html#contacting-support) o il tuo fornitore per avere questa impostazione configurata per i tuoi account.
 
### Collegamento dei tuoi account utente
{: #link_user_accounts}
Dopo che i tuoi utenti sono passati all'autenticazione tramite ID IBM, i rivenditori e i distributori possono collegare gli account SoftLayer e {{site.data.keyword.Bluemix_notm}}.

**Nota:** 
  * L'utente master dell'account che sta venendo collegato deve essere un ID IBM.
  * Accedi ad ogni account utente finale come utente master. Vai alla pagina del profilo e fai clic su **Passa a ID IBM**.
  * Ogni account che colleghi all'account {{site.data.keyword.Bluemix_notm}} deve essere gestito da un solo ID IBM univoco con un indirizzo email univoco. Anche se un ID IBM può visualizzare più account SoftLayer, non puoi collegarli agli account {{site.data.keyword.Bluemix_notm}}. Se un ID IBM è l'utente master per più account SoftLayer e desideri collegarli agli account {{site.data.keyword.Bluemix_notm}}, devi modificare gli utenti master in modo che siano un ID IBM univoco per ogni account. Contatta il [Supporto IBM SoftLayer ![icona link esterno](../icons/launch-glyph.svg)](https://knowledgelayer.softlayer.com/topic/support){: new_window} per modificare l'utente master per un account SoftLayer.
  
Completa la seguente procedura per collegare tutti gli account all'account {{site.data.keyword.Bluemix_notm}}: 

 1. Per creare un nuovo account {{site.data.keyword.Bluemix_notm}} o per il collegamento a un account {{site.data.keyword.Bluemix_notm}} esistente, accedi al tuo account SoftLayer come utente master e fai clic sul link **{{site.data.keyword.Bluemix_notm}}**. Questo ti darà la possibilità di creare un nuovo account {{site.data.keyword.Bluemix_notm}} o di collegare un account {{site.data.keyword.Bluemix_notm}} esistente. L'ID IBM che è l'utente master per l'account SoftLayer deve essere il proprietario dell'account Bluemix a cui stati eseguendo il collegamento. Segui le istruzioni nella procedura guidata, inclusa l'aggiunta di utenti nell'account SoftLayer all'account {{site.data.keyword.Bluemix_notm}}. 
 2. Dopo aver collegato l'account, informa gli utenti finali dell'account di migrare all'ID IBM. Gli utenti finali possono quindi accedere ai dashboard Infrastruttura, Applicazioni e Servizi nella console {{site.data.keyword.Bluemix_notm}}.
 3. Quando vengono aggiunti nuovi utenti all'account collegato, dovrai aggiungerli all'account SoftLayer e {{site.data.keyword.Bluemix_notm}} in modo da fornirgli l'accesso a tutte le funzionalità nella console unificata.
 
**Raccomandazione:** migra solo gli account utente finale all'ID IBM. Non migrare gli account dell'azienda che sono account principali per gli account utente finale e non contengono alcuna risorsa. Gli utenti degli account dell'azienda che eseguono la migrazione all'ID IBM perdono la possibilità di accedere al portale BAP (Brand Agent Portal).

<!--
### Mapping multiple SoftLayer accounts to one IBMid
{: #map_multiple_accounts}

You can associate one IBMid with multiple SoftLayer accounts by using an existing IBMid email address when setting up the account. Only one SoftLayer user for each account can be mapped to the single IBMid. The IBMid must be unique within each SoftLayer account. However, one user with access to multiple SoftLayer accounts can use one IBMid to access multiple SoftLayer accounts.

For example, an IBMid can map to the master user in accounts A and B, and to an additional user in accounts C and D. One of the accounts mapped to that IBMid is the default account.  Usually, the default account is the account that was first mapped to the IBMid. However, you can switch which account is the default account  through an account switching feature in the Customer Portal.

For a user with IBMid access to multiple accounts with two-factor authentication enabled, an appropriate two-factored authentication verification code per account is required during account log in and account switching.
-->


## Utilizzo di servizi {{site.data.keyword.Bluemix_notm}} con risorse SoftLayer
{: #bluemix_services}

Puoi utilizzare facilmente servizi {{site.data.keyword.Bluemix_notm}} pubblici basati sull'API insieme alle tue risorse SoftLayer. Tutte le API sono sicure e codificate, cosicché i dati siano protetti.
{:shortdesc}

Ad esempio, hai mai desiderato di aggiungere da SoftLayer capacità cognitive Watson alle tue applicazioni eseguite su server bare metal? Puoi aggiungere un servizio quale {{site.data.keyword.personalityinsightsshort}} per aiutare l'utente delle tue applicazioni in quattro semplici passi:

1. Cerca il servizio nel catalogo {{site.data.keyword.Bluemix_notm}}.
2. Fornisci un'istanza del servizio con pochi clic.
3. Imposta il servizio da eseguire con il codice esistente copiandone le credenziali e aggiungendole alla tua applicazione.
4. Effettuato l'aggiornamento nell'applicazione, distribuisci la nuova versione sulla tua infrastruttura SoftLayer.

Puoi ottenere una conoscenza di *Insights and Cognitive* richiamando le API Watson dalle tue applicazioni in SoftLayer per personalizzarle maggiormente. In alternativa, utilizza i servizi *Data and Analytics* per accedere a un'analisi ad alte prestazioni per le tue applicazioni. In alternativa, selezionare un database-as-a-service in cui tu possa lasciare la gestione a {{site.data.keyword.Bluemix_notm}}.

Rinnova lo sviluppo delle tue applicazioni attraverso contenitori con servizi quali {{site.data.keyword.activedeployshort}} e {{site.data.keyword.deliverypipeline}}. Puoi quindi utilizzare il servizio {{site.data.keyword.vpn_short}} per comunicare con SoftLayer per connettere il tuo contenitore appartenente a una rete privata alla rete privata SoftLayer. Tutti gli addebiti di utilizzo dei servizi e delle risorse di calcolo sono riportati nella fattura {{site.data.keyword.Bluemix_notm}}. 

### Servizi {{site.data.keyword.Bluemix_notm}} basati sull'API
Non tutti i servizi {{site.data.keyword.Bluemix_notm}} possono essere utilizzati con SoftLayer. I seguenti servizi possono essere impostati in modo da essere eseguiti con il codice della tua applicazione:
* {{site.data.keyword.alchemyapishort}}
* {{site.data.keyword.alertnotificationshort}}
* {{site.data.keyword.sparks}}
* {{site.data.keyword.appseccloudshort}}
* {{site.data.keyword.blockchain}}
* {{site.data.keyword.cloudant}}
* {{site.data.keyword.conceptinsightsshort}}
* {{site.data.keyword.iotmapinsights_short}}
* {{site.data.keyword.dashdbshort}}
* {{site.data.keyword.dialogshort}}
* {{site.data.keyword.documentconversionshort}}
* {{site.data.keyword.twittershort}}
* {{site.data.keyword.weather_short}}
* {{site.data.keyword.iotdriverinsights_short}}
* {{site.data.keyword.geospatialshort_Geospatial}}
* {{site.data.keyword.graphshort}}
* {{site.data.keyword.iotelectronics}}
* {{site.data.keyword.languagetranslationshort}}
* {{site.data.keyword.messagehub}}
* {{site.data.keyword.mqa}}
* {{site.data.keyword.mobileappbuilder_short}}
* {{site.data.keyword.mql}}
* {{site.data.keyword.nlclassifiershort}}
* {{site.data.keyword.objectstorageshort}}
* {{site.data.keyword.personalityinsightsshort}}
* {{site.data.keyword.presenceinsightsshort}}
* {{site.data.keyword.relationshipextractionshort}}
* {{site.data.keyword.retrieveandrankshort}}
* {{site.data.keyword.speechtotextshort}}
* {{site.data.keyword.sqldb}}
* {{site.data.keyword.streaminganalyticsshort}}
* {{site.data.keyword.texttospeechshort}}
* {{site.data.keyword.toneanalyzershort}}
* {{site.data.keyword.tradeoffanalyticsshort}}
* {{site.data.keyword.visualinsightsshort}}
* {{site.data.keyword.visualrecognitionshort}}
* {{site.data.keyword.workflow}}
* {{site.data.keyword.workloadscheduler}}

**Nota:** non tutti i piani di questi servizi sono disponibili. Solo i piani abilitati per gli account Pagamento a consumo possono essere utilizzati con gli account collegati. Tuttavia, se disponi di un account {{site.data.keyword.Bluemix_notm}} distinto, fatturato separatamente, puoi utilizzare qualsiasi piano di uno qualsiasi di questi servizi.

## Fatturazione per l'utilizzo di {{site.data.keyword.Bluemix_notm}} con gli account collegati
{: #bill_usage}

Una volta collegati i tuoi account di fatturazione {{site.data.keyword.Bluemix_notm}} e SoftLayer, il successivo ciclo di fatturazione verrà addebitato in un'unica fattura {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Il tuo ciclo di utilizzo di {{site.data.keyword.Bluemix_notm}} si basa sul mese di calendario, perciò l'addebito per il tuo account viene effettuato con cadenza mensile il giorno di fatturazione stabilito nel tuo accordo di addebito. Con SoftLayer, il ciclo di utilizzo inizia nel momento in cui viene avviato e viene pertanto addebitato con cadenza mensile lo stesso giorno del mese in cui hai sottoscritto l'account SoftLayer. 

Quando gli account sono collegati, l'utilizzo di {{site.data.keyword.Bluemix_notm}} continua a essere misurato per il ciclo del mese corrente e viene fatturato con una fattura {{site.data.keyword.Bluemix_notm}}. Dal primo giorno del mese successivo, gli addebiti {{site.data.keyword.Bluemix_notm}} e SoftLayer verranno combinati nella tua fattura {{site.data.keyword.Bluemix_notm}}.

Ad esempio, se hai collegato gli account il 16 aprile, riceverai una fattura Bluemix per l'utilizzo di aprile. A seconda di quando hai collegato i tuoi account, potresti ricevere una fattura separata per l'utilizzo di SoftLayer. L'utilizzo di maggio per SoftLayer e {{site.data.keyword.Bluemix_notm}} verrà fatturato tramite l'account {{site.data.keyword.Bluemix_notm}}.

![Collegamento del riepilogo degli account Bluemix e SoftLayer](images/BluemixSoftLayerBill.svg)

Una volta collegate le fatture, la tua fattura {{site.data.keyword.Bluemix_notm}} elencherà i diversi addebiti per ogni risorsa utilizzata nelle seguenti intestazioni:

* **Server Bare Metal e servizi collegati**
* **Server virtuali e servizi collegati**
* **Servizi non collegati**

Per informazioni sulla visualizzazione dell'utilizzo di {{site.data.keyword.Bluemix_notm}}, vedi [Visualizzazione dei dettagli di utilizzo](https://console.ng.bluemix.net/docs/pricing/index.html#usage).

