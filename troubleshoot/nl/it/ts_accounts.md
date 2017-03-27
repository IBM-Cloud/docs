---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-10"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 


# Risoluzione dei problemi relativi alla gestione degli account
{: #managingaccounts}

I problemi generali con la gestione del tuo account potrebbero riguardare applicazioni diverse che condividono lo stesso nome dominio o amministratori che non riescono a visualizzare tutte le organizzazioni. In molti casi, puoi risolvere questi problemi seguendo pochi semplici passi.
{:shortdesc}


## Account non attivo
{: #ts_accnt_inactive}

Non puoi creare un'applicazione in {{site.data.keyword.Bluemix_notm}} se il tuo account non è attivo. Per risolvere questo problema, devi contattare il team di supporto.

Quando tenti di creare un'applicazione in {{site.data.keyword.Bluemix_notm}}, viene visualizzato il seguente messaggio di errore:
{: tsSymptoms} 

`BXNUI0096E: L'applicazione non è stata creata. Il tuo account non è attivo perché è stato annullato o sospeso.`

Lo stato del tuo account {{site.data.keyword.Bluemix_notm}} diventa inattivo quando l'account viene annullato o sospeso.
{: tsCauses}


Per riattivare il tuo account, contatta il [Supporto {{site.data.keyword.Bluemix_notm}} ![icona link esterno](../icons/launch-glyph.svg "External link icon")](http://ibm.biz/bluemixsupport.com){: new_window}. Includi le seguenti informazioni nell'e-mail:
{: tsResolve}

  * L'ID IBM utilizzato per accedere a {{site.data.keyword.Bluemix_notm}}.
  * Il nome dell'organizzazione in cui verrà creata la tua applicazione. Queste informazioni consentono al team di supporto di determinare se ti sono stati assegnati i ruoli o l'appartenenza appropriati nella tua organizzazione.


## Nessuno spazio associato alla tua organizzazione corrente
{: #ts_no_space}

Non puoi creare un'applicazione se non vi è alcuno spazio associato alla tua organizzazione corrente.

Quando tenti di creare un'applicazione in {{site.data.keyword.Bluemix_notm}}, viene visualizzato il seguente messaggio di errore:
{: tsSymptoms} 

`BXNUI0097E: Prima di poter aggiungere un'applicazione, è necessario associare almeno uno spazio alla tua organizzazione e alla tua regione. Sul Dashboard, fai clic su Crea uno
spazio. Una volta creato lo spazio, prova di nuovo. `

Le applicazioni in {{site.data.keyword.Bluemix_notm}} devono essere create in uno spazio della tua organizzazione.
{: tsCauses} 

Per creare uno spazio, utilizza uno dei seguenti metodi: 
{: tsResolve}
 
  * Sul Dashboard {{site.data.keyword.Bluemix_notm}}, seleziona l'organizzazione in cui vuoi creare lo spazio e fai quindi clic su **Crea uno spazio**.
  * Nell'interfaccia riga di comando cf, immetti `cf create-space <nome_spazio>
-o <nome_organizzazione>`.

  
## Le applicazioni condividono lo stesso nome di dominio
{: #ts_domain_diff}

Potresti notare che diverse applicazioni condividono lo stesso URL in {{site.data.keyword.Bluemix_notm}}.

Questo problema potrebbe verificarsi se assegni la stessa rotta URL per le diverse applicazioni in uno spazio.
{: tsCauses}

Ad esempio, esegui il push dell'applicazione myApp1 a {{site.data.keyword.Bluemix_notm}} e imposta il dominio su "mynewapp.stage1.mybluemix.net". Esegui quindi il push di un'altra applicazione myApp2 allo stesso spazio e imposta una delle sue rotte URL su "mynewapp.stage1.mybluemix.net". La rotta è ora associata a entrambe le applicazioni.

Questo è il funzionamento supportato da {{site.data.keyword.Bluemix_notm}} e puoi utilizzare questa procedura affinché non si verifichino tempi di inattività per l'aggiornamento della tua applicazione. Per ulteriori informazioni, vedi [Using Blue-Green Deployment to Reduce Downtime and Risk ![icona link esterno](../icons/launch-glyph.svg "External link icon")](https://docs.cloudfoundry.org/devguide/deploy-apps/blue-green.html){: new_window}.
{: tsResolve}
  

## Gli amministratori non possono visualizzare tutte le organizzazioni utilizzando l'interfaccia utente {{site.data.keyword.Bluemix_notm}}
{: #ts_ui_org}

In qualità di amministratore, quando utilizzi l'interfaccia utente {{site.data.keyword.Bluemix_notm}}, non riesci a visualizzare tutte le organizzazioni per gestirle. Puoi visualizzare e gestire solo le organizzazioni alle quali appartieni.

In qualità di amministratore, non puoi visualizzare tutte le organizzazioni utilizzando l'interfaccia utente {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms}

Questa è una limitazione dell'interfaccia utente {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}

Puoi utilizzare i comandi come `cf orgs`, `cf create-org` e `cf delete-org` dall'interfaccia riga di comando cf per gestire tutte le organizzazioni. Per un elenco completo dei comandi cf, immetti `cf help`.
{: tsResolve}
	
## Impossibile aggiungere la carta di credito
{: #ts_addcc}

Non puoi inoltrare le informazioni della tua carta di credito per convertire il tuo account di prova in un account con pagamento a consumo.

Il pulsante **Inoltra** nella pagina Aggiungi carta di credito è disabilitato.
{: tsSymptoms}

Questo problema si verifica se non compili correttamente le tue informazioni nella pagina Aggiungi carta di credito.
{: tsCauses}


Completa
la seguente procedura:
{: tsResolve}

  1. Nella pagina Aggiungi carta di credito, compila tutti i campi obbligatori nelle sezioni relative a informazioni di contatto, indirizzo di contatto e indirizzo di fatturazione.
  2. Seleziona **Ho letto e accetto i termini e le condizioni IBM**
e fai clic su **Inoltra**. Viene visualizzata la sezione **Seleziona un
metodo di pagamento**.
  3. Immetti il numero della tua carta di credito, la data di scadenza e il codice di sicurezza indicato sulla carta. Fai quindi clic su **Inoltra**.
