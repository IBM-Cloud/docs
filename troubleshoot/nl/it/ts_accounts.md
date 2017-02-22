---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-11"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 





# Risoluzione dei problemi relativi alla gestione degli account
{: #managingaccounts}


Potrebbero verificarsi dei problemi durante la gestione del tuo account, ad esempio problemi relativi ad applicazioni differenti che condividono lo stesso nome dominio o amministratori che non riescono a visualizzare tutte le organizzazioni. Tuttavia, in molti casi, puoi eseguire un ripristino da tali problemi seguendo pochi semplici passi.
{:shortdesc}


## Account non attivo
{: #ts_accnt_inactive}

Non puoi creare un'applicazione in {{site.data.keyword.Bluemix_notm}} se il tuo account non è attivo. Per risolvere questo problema, devi contattare il team di supporto.



Quando tenti di creare un'applicazione in {{site.data.keyword.Bluemix_notm}}, viene visualizzato il seguente messaggio di errore:
{: tsSymptoms} 

`BXNUI0096E: L'applicazione non è stata creata. Il tuo account non è attivo perché è stato annullato o sospeso.`


Lo stato del tuo account {{site.data.keyword.Bluemix_notm}} diventa inattivo quando l'account viene annullato o sospeso.
{: tsCauses}

 

Per riattivare il tuo account, contatta il [Supporto {{site.data.keyword.Bluemix_notm}} ![icona link esterno](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport.com){: new_window}. Nell'email, devi includere le seguenti informazioni:
{: tsResolve}

  * L'ID IBM utilizzato per accedere a {{site.data.keyword.Bluemix_notm}}.
  * Il nome dell'organizzazione in cui verrà creata la tua applicazione. Queste informazioni consentono al team di supporto di determinare se ti sono stati assegnati i ruoli o l'appartenenza appropriati all'interno della tua organizzazione.



## Nessuno spazio associato alla tua organizzazione corrente
{: #ts_no_space}

Non puoi creare un'applicazione se non vi è alcuno spazio
associato alla tua organizzazione corrente.



Quando tenti di creare un'applicazione in {{site.data.keyword.Bluemix_notm}}, viene visualizzato il seguente messaggio di errore:
{: tsSymptoms} 


`BXNUI0097E: Prima di poter aggiungere un'applicazione, è necessario associare almeno uno spazio alla tua organizzazione e alla tua regione. Sul Dashboard, fai clic su Crea uno
spazio. Una volta creato lo spazio, prova di nuovo. `



Le applicazioni in {{site.data.keyword.Bluemix_notm}} devono essere create all'interno di uno spazio nella tua organizzazione.
{: tsCauses} 

 

Per creare uno spazio, utilizza uno dei seguenti metodi: 
{: tsResolve}
 
  * Sul Dashboard {{site.data.keyword.Bluemix_notm}}, seleziona l'organizzazione in cui vuoi creare lo spazio e fai quindi clic su **Crea uno spazio**.
  * Nell'interfaccia riga di comando cf, immetti `cf create-space <nome_spazio>
-o <nome_organizzazione>`.
  
  
  
  
## Le applicazioni condividono lo stesso nome di dominio
{: #ts_domain_diff}

Potresti notare che diverse applicazioni condividono lo stesso
URL in {{site.data.keyword.Bluemix_notm}}.

 

Questo problema potrebbe verificarsi quando assegni
la stessa rotta URL per applicazioni differenti all'interno di uno spazio.
{: tsCauses}

Ad esempio, esegui il push dell'applicazione myApp1 a {{site.data.keyword.Bluemix_notm}} e imposti il dominio su "mynewapp.stage1.mybluemix.net". Esegui quindi il push di un'altra applicazione myApp2 allo stesso spazio e imposti una delle sue rotte URL su "mynewapp.stage1.mybluemix.net". La rotta è ora associata a entrambe le applicazioni.

 

Questo è il funzionamento supportato da {{site.data.keyword.Bluemix_notm}} e
puoi utilizzare questa procedura affinché non si verifichino tempi di inattività
per l'aggiornamento della tua applicazione. Per ulteriori informazioni, vedi Distribuzioni Blue-Green.
{: tsResolve}
  
	
	
<!-- begin STAGING ONLY --> 
	
	
## Gli amministratori non possono visualizzare tutte le organizzazioni utilizzando l'interfaccia utente {{site.data.keyword.Bluemix_notm}}
{: #ts_ui_org}

In qualità di amministratore, quando utilizzi l'interfaccia utente {{site.data.keyword.Bluemix_notm}}, non riesci a visualizzare tutte le organizzazioni per gestirle. Puoi visualizzare e gestire solo le organizzazioni alle quali appartieni.

 

In qualità di amministratore, non puoi visualizzare tutte le organizzazioni utilizzando l'interfaccia utente {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms}

 

Questa è una limitazione dell'interfaccia utente {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}

 

Puoi utilizzare un comando come `cf orgs`, `cf create-org` e `cf delete-org` dall'interfaccia riga di comando cf per gestire tutte le organizzazioni. Per un elenco completo dei comandi cf, immetti `cf help`.
{: tsResolve}
	
<!-- end STAGING ONLY -->




## Impossibile aggiungere la carta di credito
{: #ts_addcc}

Non riesci a inoltrare le informazioni della tua carta di credito per convertire
il tuo account di prova in un account con pagamento a consumo.

 

Il pulsante Inoltra nella pagina Aggiungi carta di credito è disabilitato.
{: tsSymptoms}

 

Questo problema si verifica se le tue informazioni non sono compilate correttamente nella pagina Aggiungi carta di credito.
{: tsCauses}

 

Per risolvere il problema, completa la seguente procedura:
{: tsResolve}

  1. Nella pagina Aggiungi carta di credito, compila tutti i campi richiesti che si trovano nelle sezioni relative a informazioni di contatto, indirizzo di contatto e indirizzo di fatturazione.
  2. Seleziona **Ho letto e accetto i termini e le condizioni IBM**
e fai clic su **Inoltra**. Viene visualizzata la sezione **Seleziona un
metodo di pagamento**.
  3. Immetti il numero della tua carta di credito, la data di scadenza della carta
e il codice di sicurezza. Quindi, fai clic su **Inoltra**.


