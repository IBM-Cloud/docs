---

copyright:
  anni: 2015, 2016

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# Risoluzione dei problemi di accesso a {{site.data.keyword.Bluemix_notm}} 
{: #accessing}

Ultimo aggiornamento: 18 agosto 2016
{: .last-updated} 

I problemi generali con l'accesso a {{site.data.keyword.Bluemix}} potrebbero includere un utente che non riesce ad accedere a {{site.data.keyword.Bluemix_notm}}, un account bloccato in uno stato In sospeso e così via. Tuttavia, in molti casi, puoi eseguire un ripristino da tali problemi seguendo pochi semplici passi. 
{:shortdesc}

## Impossibile accedere a {{site.data.keyword.Bluemix_notm}}
{: #ts_logintobm}

Per accedere a {{site.data.keyword.Bluemix_notm}}, devi disporre di un ID IBM e password validi.


Quando tenti di accedere a {{site.data.keyword.Bluemix_notm}}, visualizzi il seguente messaggio di errore: 
{: tsSymptoms} 

`La password immessa non è corretta.`


L'ID IBM e password da te utilizzati per accedere a {{site.data.keyword.Bluemix_notm}} non sono validi.
{: tsCauses} 
 

Per ottenere un ID IBM e una password validi, vai alla pagina Il mio profilo IBM e completa una della seguenti procedure:
{: tsResolve}
  * Se già hai registrato un ID IBM e vuoi controllare se il tuo ID e la tua password sono validi, fai clic su **Accedi** e immetti il tuo ID IBM e la relativa password nella pagina di accesso. Se hai dimenticato la password, fai clic su **Password dimenticata** per reimpostarla. Se hai dimenticato il tuo ID IBM o continui ad avere problemi con la tua password, contatta l'Help Desk Worldwide IBM Registration per ottenere assistenza. 
  * Se non hai un ID IBM, fai clic su **Registrati** per registrare un ID IBM e password. 
  
**Nota:** per i dipendenti IBM, l'ID IBM potrebbe essere diverso dall'ID di accesso Intranet. 



<!-- begin STAGING ONLY --> 

## Problema di accesso al sito Web esterno
{: #ts_bmlinkid}

Non puoi accedere a {{site.data.keyword.Bluemix_notm}} utilizzando il tuo ID Intranet IBM a meno che non colleghi l'ID Intranet ID al tuo ID IBM.


Dopo aver selezionato **Accedi con l'ID Intranet** dalla pagina Accesso {{site.data.keyword.Bluemix_notm}}, potresti visualizzare il seguente messaggio di errore:
{: tsSymptoms} 

`Problema di accesso al sito Web esterno`



Questo problema si verifica quando accedi a {{site.data.keyword.Bluemix_notm}} utilizzando un ID Intranet IBM che non è collegato a un ID IBM. L'ID IBM è l'ID che utilizzi per accedere alla pagina www.ibm.com.
{: tsCauses}


Come dipendente IBM, prima di poter accedere a {{site.data.keyword.Bluemix_notm}} con l'ID Intranet IBM, devi collegare tale ID al tuo ID IBM esterno. Per collegare i due ID, completa la seguente procedura:
{: tsResolve} 

  1. Nella pagina [Accesso centrale](https://w3-03.sso.ibm.com/tools/cso/index.jsp){: new_window}, fai clic su **I miei accessi**.
  2. Nella pagina I miei accessi, fai clic su **Collega ID** e immetti il tuo ID IBM e password nella pagina di accesso {{site.data.keyword.Bluemix_notm}}. Dopo di che, i tuoi ID Intranet e ID IBM verranno collegati automaticamente.
  

<!-- end STAGING ONLY -->




## Non hai salvato delle modifiche
{: #ts_unsaved_changes}


Quando navighi nella pagina dei dettagli dell'applicazione, potresti non riuscire ad eseguire delle azioni ed è possibile che ti venga richiesto di salvare le modifiche prima di continuare. 


Quanto tenti di controllare la tua applicazione o i tuoi servizi nella pagina dei dettagli dell'applicazione, continui a visualizzare il seguente messaggio di errore:
{: tsSymptoms} 

`Sono presenti modifiche non salvate nella pagina nomeapplicazione. Salva o annulla le modifiche.`


Quando passi il mouse sul campo **ISTANZE** o **QUOTA DI MEMORIA** nel riquadro del runtime, i valori cambiano. Questo è il funzionamento previsto; tuttavia, il messaggio di errore di richiede di salvare le impostazioni della memoria o dell'istanza prima di uscire dalla pagina. 
{: tsCauses}


Chiudi la finestra del messaggio, quindi fai clic sul pulsante  **REIMPOSTA** nel riquadro del runtime. 
{: tsResolve} 




    
    
## Il failover automatico tra le regioni {{site.data.keyword.Bluemix_notm}} non è disponibile
{: #ts_failover}

Non riesci a utilizzare il failover automatico tra le regioni {{site.data.keyword.Bluemix_notm}}. Tuttavia, come soluzione alternativa, puoi utilizzare un provider DNS che supporti il failover tra più indirizzi IP.
 

Quando una regione {{site.data.keyword.Bluemix_notm}}  diventa non disponibile, anche le applicazioni in esecuzione in tale regione non saranno più disponibili, anche se le stesse applicazioni sono in esecuzione in un'altra regione {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms}

 
{{site.data.keyword.Bluemix_notm}} non fornisce ancora il failover automatico da una regione all'altra.
{: tsCauses}

 
Puoi utilizzare un provider DNS che supporti il failover intelligente tra più indirizzi IP e configurare manualmente le tue impostazioni
DNS per abilitare il failover automatico tra le regioni {{site.data.keyword.Bluemix_notm}}. I provider DNS con questa capacità comprendono NSONE, Akamai, Dyn.
{: tsResolve}

Quando configuri le tue impostazioni DNS, devi specificare gli indirizzi IP pubblici delle regioni {{site.data.keyword.Bluemix_notm}} in cui sono esecuzione le tue applicazioni. Per ottenere l'indirizzo IP pubblico
di una regione {{site.data.keyword.Bluemix_notm}},
usa il comando `nslookup`. Ad esempio, puoi immettere
il seguente comando in una finestra della riga di comando:
```
nslookup stage1.mybluemix.net
```



## L'account è in sospeso
{: #ts_accntpding}

Se il tuo account è in sospeso, non puoi accedere a {{site.data.keyword.Bluemix_notm}}.

 
Dopo aver eseguito la registrazione per un account di prova {{site.data.keyword.Bluemix_notm}},
potresti non riuscire ad accedere a {{site.data.keyword.Bluemix_notm}}. Invece, visualizzi il seguente messaggio:
{: tsSymptoms}

<code>Your account is pending. Please wait up to 24 hours for email confirmation and also check your
spam folder. If you still have not received your email confirmation, contact <a href="http://ibm.biz/bluemixsupport.com" target="_blank">Bluemix Support</a>.</code>


Dopo aver eseguito la registrazione per un account di prova {{site.data.keyword.Bluemix_notm}},
riceverai un'email di conferma. Dovrai fare clic sul link
che si trova nella email di conferma per completare il processo di registrazione.
{: tsCauses} 

L'email di conferma viene inviata all'indirizzo di posta
da te fornito. Controlla la cartella della posta in arrivo e quella della posta indesiderata. Se non hai ricevuto un'e-mail di conferma, contatta il [Supporto {{site.data.keyword.Bluemix_notm}}](http://ibm.biz/bluemixsupport.com){: new_window}.  
{: tsResolve}



## Impossibile aggiungere utenti a un'organizzazione
{: #ts_adduser}

Puoi invitare più di un utente a lavorare nella stessa organizzazione. Puoi invitare utenti nella tua organizzazione solo
se sei il proprietario dell'account o se sei allo stesso tempo un gestore e un membro dell'organizzazione.
 

Non riesci a visualizzare il link **Invita un nuovo utente**
nella sezione **Gestisci organizzazioni**. 
{: tsSymptoms}

 

Solo i seguenti utenti {{site.data.keyword.Bluemix_notm}}
possono invitare gli utenti in un'organizzazione:
{: tsCauses}
  * Il proprietario dell'account dell'organizzazione
  * I gestori dell'organizzazione che sono anche membri, e non collaboratori,
dell'organizzazione
  
In {{site.data.keyword.Bluemix_notm}},
puoi essere un membro o un collaboratore di un'organizzazione.

<dl><dt>Collaboratore</dt>
<dd>Sei un collaboratore di un'organizzazione se disponi già
di un account {{site.data.keyword.Bluemix_notm}}
e qualcun altro ti invita nell'organizzazione.</dd>
<dt>Membro</dt>
<dd>Sei membro di un'organizzazione se non disponi di un account {{site.data.keyword.Bluemix_notm}},
ma poi qualcuno ti invita nell'organizzazione e ti registri a {{site.data.keyword.Bluemix_notm}}
tramite l'invito.</dd>
</dl>


Non puoi invitare utenti nella tua organizzazione se sei
un collaboratore, anche se ti è stato assegnato il ruolo di
gestore organizzazione.

**Nota:** tutti i gestori organizzazione, compresi quelli che sono collaboratori di un'organizzazione, possono aggiungere, modificare e rimuovere gli utenti già presenti nell'organizzazione.

 

Se non riesci a inviare utenti nella tua organizzazione e per farlo
hai bisogno di un ruolo differente, contatta il gestore della tua organizzazione
per modificare il tuo ruolo. Per identificare il gestore della tua organizzazione, completa
la seguente procedura:
{: tsResolve}

  1. Vai al Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona {{site.data.keyword.avatar}} ![icona Avatar](images/account_support.svg) nella barra dei menu e seleziona **Gestisci organizzazioni**.
  2. Vai alla tua organizzazione e visualizza le informazioni del gestore organizzazione
sulla scheda **UTENTI**.  
  
Se non riesci a invitare utenti perché sei un collaboratore e non
un membro, devi eliminare il tuo account {{site.data.keyword.Bluemix_notm}} precedente
ed essere inviato a entrare a far parte dell'account come membro dell'organizzazione. Per eliminare il tuo account precedente ed entrare a far parte dell'account come membro,
completa la seguente procedura: 

  1. Contatta il [supporto {{site.data.keyword.Bluemix_notm}}](http://ibm.biz/bluemixsupport){: new_window} per aprire un ticket di supporto e richiedere l'eliminazione del tuo account. Se hai dei dati associati al tuo
account precedente che vuoi salvare e passare al nuovo account,
includi queste informazioni nell'email. 
  2. Una volta eliminato il tuo account, fa sì che un utente con il ruolo di gestore
organizzazione ti inviti nell'organizzazione come gestore. Utilizza quindi l'invito per registrarti in
{{site.data.keyword.Bluemix_notm}}. 




## La registrazione batch degli utenti non è supportata
{: #ts_batchregistration}

Quando
registri gli utenti per {{site.data.keyword.Bluemix_notm}},
devi registrare ciascun utente singolarmente.
 

{{site.data.keyword.Bluemix_notm}} non
fornisce la capacità di registrare più utenti
contemporaneamente.
{: tsSymptoms}
 

{{site.data.keyword.Bluemix_notm}} non
supporta la registra batch di utenti. Per registrare gli utenti per {{site.data.keyword.Bluemix_notm}},
devi registrare ciascun utente singolarmente.
{: tsCauses}
 

Per registrare più utenti per {{site.data.keyword.Bluemix_notm}},
devi completare la seguente procedura per ogni utente:
{: tsResolve}

  1. Fai clic su **ESEGUI REGISTRAZIONE** nell'interfaccia utente {{site.data.keyword.Bluemix_notm}}.
  2. Completa i passi seguendo la procedura guidata.

    

## Impossibile caricare una pagina
{{site.data.keyword.Bluemix_notm}}
{: #ts_err}

Durante l'utilizzo dell'interfaccia utente {{site.data.keyword.Bluemix_notm}},
potresti non riuscire a caricare una pagina {{site.data.keyword.Bluemix_notm}}. Potresti visualizzare invece i messaggi di errore BXNUI0001E o BXNUI0016E.
 

Quando utilizzi l'interfaccia utente
{{site.data.keyword.Bluemix_notm}}, potresti visualizzare
uno dei seguenti messaggi di errore:
{: tsSymptoms}

`BXNUI0001E: La pagina non è stata caricata perché Bluemix non ha rilevato se esiste una sessione.`


`BXNUI0016E: Le applicazioni e i servizi non sono stati recuperati perché una pagina di Bluemix non è stata caricata.`

 

Puoi completare una o più delle seguenti azioni,
secondo necessità:
{: tsResolve}

  * Aggiorna o riavvia il tuo browser.
  * Disconnettiti da {{site.data.keyword.Bluemix_notm}} e
riesegui l'accesso.
  * Utilizza la modalità di navigazione privata del tuo browser. 
  * Cancella i cookie e la cache del browser.
  * Utilizza un browser differente. Per informazioni sulle versioni dei browser supportati da {{site.data.keyword.Bluemix_notm}}, consulta [Prerequisiti di {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}.
  * Se hai installato l'interfaccia riga di comando cf, immetti il comando `cf
apps` per vedere se l'applicazione è in esecuzione.
  
  
  
  
  

