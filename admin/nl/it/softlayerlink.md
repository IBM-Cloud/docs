---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

<!-- draft - staging only -->

#Collegamento degli account di fatturazione SoftLayer e {{site.data.keyword.Bluemix_notm}}
{: #softlayerlink}
*Ultimo aggiornamento: 7 luglio 2016*
{: .last-updated}

È ora possibile collegare gli account di fatturazione SoftLayer e {{site.data.keyword.Bluemix_notm}}. Quando colleghi i tuoi account, ricevi la fatturato attraverso SoftLayer sia per le risorse SoftLayer che per le risorse {{site.data.keyword.Bluemix_notm}}. Se hai già un account, la fatturazione per {{site.data.keyword.Bluemix_notm}} tramite SoftLayer parte dal nuovo ciclo di fatturazione avviato dopo il collegamento degli account.
{:shortdesc}

**Importante:** tutti gli account collegati in {{site.data.keyword.Bluemix_notm}} devono essere del tipo Pagamento a consumo. Puoi creare un nuovo account Pagamento a consumo o collegarne uno esistente. In alternativa, puoi collegare un account di prova esistente, che verrà tuttavia aggiornato in un account Pagamento a consumo.  

Una volta collegati gli account, puoi passare tra gli account facilmente. Puoi ancora monitorare l'utilizzo delle tue risorse {{site.data.keyword.Bluemix_notm}} nell'interfaccia utente {{site.data.keyword.Bluemix_notm}}. Tuttavia, la fatturazione di tali risorse verrà mostrata nella fattura SoftLayer.

Sebbene la tua fatturazione account sia stata collegata, il tuo ID di accesso varierà in base a come il tuo account SoftLayer viene autenticato:
* Per gli utenti negli account SoftLayer che non utilizzano un ID IBM per l'autenticazione, continua a utilizzare il tuo ID SoftLayer per i prodotti e i servizi SoftLayer e il tuo ID IBM per i prodotti e i servizi {{site.data.keyword.Bluemix_notm}}.
* Per gli utenti negli account SoftLayer che utilizzano un ID IBM per l'autenticazione, utilizza il tuo ID IBM per accedere al tuo SoftLayer e ai tuoi account {{site.data.keyword.Bluemix_notm}}.

**Attenzione:** una volta collegati, gli account non possono più essere scollegati.  

Se hai un account SoftLayer e desideri collegare gli account SoftLayer e {{site.data.keyword.Bluemix_notm}}, completa la seguente procedura:
 1. Dal {{site.data.keyword.slportal}}, fai clic su **Collega un account {{site.data.keyword.Bluemix_notm}}**. 
 2. Leggi e accetta le condizioni di collegamento degli account SoftLayer e {{site.data.keyword.Bluemix_notm}}.
 3. Quando richiesto, fornisci l'indirizzo e-mail associato al tuo account {{site.data.keyword.Bluemix_notm}}. Se non hai un account {{site.data.keyword.Bluemix_notm}}, fornisci l'indirizzo e-mail che desideri utilizzare, quindi segui le istruzioni per ricevere l'invito a {{site.data.keyword.Bluemix_notm}} e crea un account.

Per collegare gli account, devi essere un utente master dell'account SoftLayer.

Una volta collegati gli account, nell'intestazione generale di SoftLayer viene visualizzato il link **Vai a {{site.data.keyword.Bluemix_notm}}**. Facendo clic su questo link, arrivi alla pagina di accesso {{site.data.keyword.Bluemix_notm}}. Inoltre, **SoftLayer** è ora disponibile nell'intestazione di {{site.data.keyword.Bluemix_notm}}. Facendo clic sul collegamento, accedi attraverso una nuova finestra alla home page di {{site.data.keyword.slportal}}.


## Crediti per l'utilizzo di {{site.data.keyword.Bluemix_notm}} con gli account collegati
{: #slcredit}

Quando colleghi gli account di fatturazione {{site.data.keyword.Bluemix_notm}} e SoftLayer, ricevi un credito di 200 dollari per l'utilizzo di {{site.data.keyword.Bluemix_notm}}. Il credito deve essere utilizzato entro 30 giorni dal collegamento degli account.

Per informazioni su come visualizzare i crediti e la data di scadenza, vedi [Visualizzazione dei crediti](https://console.ng.bluemix.net/docs/pricing/index.html#credits).

## Come invitare membri del team SoftLayer in {{site.data.keyword.Bluemix_notm}}
{: #invite_users}

Quando colleghi gli account {{site.data.keyword.Bluemix_notm}} e SoftLayer, puoi invitare i membri del tuo team SoftLayer a unirsi a {{site.data.keyword.Bluemix_notm}}. In alternativa, puoi invitare successivamente i membri del team SoftLayer dall'interfaccia utente {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Dall'interfaccia utente {{site.data.keyword.Bluemix_notm}} puoi scegliere di invitare tutti i membri del tuo account SoftLayer oppure puoi selezionare singoli membri. Quando inviti membri del team, devi impostare il ruolo account {{site.data.keyword.Bluemix_notm}} ruolo per gli invitati. Per ulteriori informazioni sui differenti ruoli in {{site.data.keyword.Bluemix_notm}}, vedi [Ruoli utente](https://console.ng.bluemix.net/docs/admin/users_roles.html#userrolesinfo).

Per invitare membri del team a unirsi all'account {{site.data.keyword.Bluemix_notm}}, devi essere un utente master dell'account SoftLayer.

Per invitare membri del team tramite {{site.data.keyword.Bluemix_notm}}:
 1. Passa all'icona **Account e supporto** ![Account e supporto](images/account_support.svg) **Account** **Invita membri del team**.
 2. Fai clic su **Aggiungi** per eseguire l'autenticazione nel tuo account SoftLayer e visualizzare un elenco di membri del team dal tuo account SoftLayer.
 3. Seleziona i membri del team da invitare e fai clic su **Invia**.

Puoi effettuare questa operazione più volte fino ad aggiungere più membri del team al tuo account SoftLayer.
 
Il membro del team riceve un'e-mail che include un link **Unisciti all'organizzazione**. Se il membro non ha un ID IBM, viene reindirizzato a una pagina di registrazione. Successivamente, il membro del team può immettere alcune informazioni di base e creare il proprio account {{site.data.keyword.Bluemix_notm}}.

Per ulteriori informazioni su come invitare i membri del team attraverso l'interfaccia utente {{site.data.keyword.Bluemix_notm}}, vedi [Come invitare membri del team](https://console.ng.bluemix.net/docs/admin/users_roles.html#inviteteammembers).

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

Rinnova lo sviluppo delle tue applicazioni attraverso contenitori con servizi quali {{site.data.keyword.activedeployshort}} e {{site.data.keyword.deliverypipeline}}. Puoi quindi utilizzare il servizio {{site.data.keyword.vpn_short}} per ricollegarti a SoftLayer per connettere il tuo contenitore appartenente a una rete privata alla rete privata SoftLayer. Tutte gli addebiti di utilizzo dei servizi e delle risorse di calcolo sono riportati nella fattura SoftLayer. 

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

Una volta collegati i tuoi account di fatturazione {{site.data.keyword.Bluemix_notm}} e SoftLayer, il successivo ciclo di fatturazione verrà addebitato in un'unica fattura SoftLayer.
{:shortdesc}

Il tuo ciclo di utilizzo di {{site.data.keyword.Bluemix_notm}} si basa sul mese di calendario, perciò l'addebito per il tuo account viene effettuato con cadenza mensile il giorno di fatturazione stabilito nel tuo accordo di addebito. Con SoftLayer, il ciclo di utilizzo inizia nel momento in cui viene avviato e viene pertanto addebitato con cadenza mensile lo stesso giorno del mese in cui hai sottoscritto l'account SoftLayer. 

Quando gli account sono collegati, l'utilizzo di {{site.data.keyword.Bluemix_notm}} continua a essere misurato per il ciclo del mese corrente e viene fatturato con una fattura {{site.data.keyword.Bluemix_notm}}. Dal primo giorno del mese successivo, gli addebiti {{site.data.keyword.Bluemix_notm}} passeranno sulla tua fattura SoftLayer.

Ad esempio, se hai collegato gli account il 16 aprile, riceverai una fattura Bluemix per l'utilizzo di aprile. L'utilizzo di maggio verrà invece fatturato attraverso il tuo account SoftLayer.

![Collegamento del riepilogo degli account Bluemix e SoftLayer](images/BluemixSoftLayerBill.svg)

Una volta combinate le fatture, la tua fattura SoftLayer riporterà una sezione **{{site.data.keyword.Bluemix_notm}}** all'interno della fattura riepilogativa. Nella vista di fatturazione dettagliata, gli addebiti {{site.data.keyword.Bluemix_notm}} vengono indicati come altri servizi e iniziano con *"{{site.data.keyword.Bluemix_notm}} Piano..."*.

Per informazioni sulla visualizzazione dell'utilizzo di {{site.data.keyword.Bluemix_notm}}, vedi [Visualizzazione dei dettagli di utilizzo](https://console.ng.bluemix.net/docs/pricing/index.html#usage).


# rellinks
## generale
* [Video: Link SoftLayer and Bluemix Accounts For a Single Invoice](https://www.youtube.com/watch?v=Xb01idt2NiU&index=1&list=PLzpeuWUENMK2d3L5qCITo2GQEt-7r0oqm)
