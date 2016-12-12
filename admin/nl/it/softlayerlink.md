---

 

copyright:

  years: 2016
lastupdated: "2016-11-03"
 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Aggiornamento e unificazione degli account di fatturazione {{site.data.keyword.Bluemix_notm}} e SoftLayer
{: #softlayerlink}

Se disponi di un account {{site.data.keyword.Bluemix_notm}} di prova e vuoi accedere al dashboard Infrastruttura, devi eseguire l'aggiornamento a un account {{site.data.keyword.Bluemix_notm}} con pagamento a consumo. Devi inoltre eseguire l'aggiornamento se desideri utilizzare altre risorse a consumo che non sono disponibili in un account di prova o se il tuo account di prova è terminato. 

Puoi unificare i tuoi account {{site.data.keyword.Bluemix_notm}} e SoftLayer esistenti collegando tali account. Quando colleghi i tuoi account, ricevi la fattura attraverso {{site.data.keyword.Bluemix_notm}} sia per le risorse {{site.data.keyword.Bluemix_notm}} che per le risorse SoftLayer.
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

## Crediti per l'utilizzo di {{site.data.keyword.Bluemix_notm}} con gli account collegati
{: #slcredit}

Quando colleghi il tuo account {{site.data.keyword.Bluemix_notm}} all'account SoftLayer, ricevi un credito di 200 dollari che puoi utilizzare solo all'interno di {{site.data.keyword.Bluemix_notm}}. Il credito deve essere utilizzato entro 30 giorni dal collegamento degli account.

Per informazioni su come visualizzare i crediti e la data di scadenza, vedi [Visualizzazione dei crediti](https://console.ng.bluemix.net/docs/pricing/index.html#credits).

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

L'autenticazione in SoftLayer adesso utilizza l'ID IBM per fornire un singolo accesso in {{site.data.keyword.Bluemix_notm}}. Se disponi di un account SoftLayer esistente, puoi passare a un ID IBM. Una procedura guidata di migrazione ti guiderà in questo passaggio. 
{:shortdesc}

Dopo aver iniziato il passaggio all'ID IBM, finché non si completa il processo, è possibile annullarlo. Tuttavia, ti verrà richiesto di passare all'ID IBM la prossima volta che effettuerai l'accesso.

Per iniziare il passaggio dal tuo nome utente SoftLayer esistente a un ID IBM, completa la seguente procedura:

 1. In {{site.data.keyword.slportal}}, vai alla pagina Modifica profilo utente e fai clic su **Passa a ID IBM**.
 2. Segui le istruzioni della procedura guidata di migrazione per creare il tuo ID IBM. Dopo aver creato il tuo ID IBM, non puoi modificare l'ID, che corrisponde a un indirizzo e-mail. Puoi aggiornare l'e-mail associata al tuo profilo, ma per impostazione predefinita il valore è impostato su quello che hai definito per l'ID IBM. Dopo aver completato la procedura guidata, ti viene inviata un'e-mail.
 3. Quando ricevi l'e-mail, segui il link o copia l'URL in un browser e immetti il codice di registrazione. Il codice è valido per 7 giorni ed è un codice monouso.  Una volta utilizzato, non è possibile riutilizzarlo.
 Dopo aver impostato il collegamento tra l'ID IBM e l'utente SoftLayer, puoi accedere al tuo account solo con l'ID IBM.  Nella finestra di dialogo di accesso, devi utilizzare il pulsante **Accedi con ID IBM** invece di immettere nome utente e password SoftLayer.
 
Se sei un nuovo cliente, quando controlli il tuo ordine ti verrà chiesto un indirizzo e-mail per il tuo account ID IBM esistente o di creare un nuovo account. 

### Associazione di più account SoftLayer a un ID IBM
{: #map_multiple_accounts}

Puoi associare un ID IBM a più account SoftLayer utilizzando un'e-mail ID IBM esistente durante l'impostazione dell'account. È possibile associare un solo utente SoftLayer per ogni account al singolo ID IBM. L'ID IBM deve essere univoco all'interno di ogni account SoftLayer. Tuttavia, un utente con accesso a più account SoftLayer può utilizzare un ID IBM per accedere a diversi account SoftLayer.

Ad esempio, un ID IBM può essere associato all'utente master negli account A e B e a un ulteriore utente negli account C e D. Uno degli account associato a tale ID IBM è l'account predefinito.  Di solito, l'account predefinito è quello che è stato associato per primo all'ID IBM. Tuttavia, puoi cambiare l'account predefinito utilizzando una funzione di passaggio tra account nel portale clienti.

Per un utente che dispone dell'accesso ID IBM a più account e per cui è abilitata l'autenticazione a due fattori, è richiesto un codice di verifica appropriato per tale autenticazione durante l'accesso e il passaggio tra gli account.

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

Rinnova lo sviluppo delle tue applicazioni attraverso contenitori con servizi quali {{site.data.keyword.activedeployshort}} e {{site.data.keyword.deliverypipeline}}. Puoi quindi utilizzare il servizio {{site.data.keyword.vpn_short}} per ricollegarti a SoftLayer per connettere il tuo contenitore appartenente a una rete privata alla rete privata SoftLayer. Tutti gli addebiti di utilizzo dei servizi e delle risorse di calcolo sono riportati nella fattura {{site.data.keyword.Bluemix_notm}}. 

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
* {{site.data.keyword.nlclassifierlshort}}
* {{site.data.keyword.objectstorageshort}}
* {{site.data.keyword.personalityinsightsshort}}
* {{site.data.keyword.presenceinsightsshort}}
* {{site.data.keyword.relationshipextractionshort}}
* {{site.data.keyword.retrieveandrankshort}}
* {{site.data.keyword.servicediscoveryshort}}
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

