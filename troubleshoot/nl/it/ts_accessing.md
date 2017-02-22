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



# Risoluzione dei problemi di accesso a {{site.data.keyword.Bluemix_notm}} 
{: #accessing}


I problemi generali con l'accesso a {{site.data.keyword.Bluemix}} potrebbero includere un utente che non riesce ad accedere a {{site.data.keyword.Bluemix_notm}}, un account bloccato in uno stato In sospeso e così via. Tuttavia, in molti casi, puoi eseguire un ripristino da tali problemi seguendo pochi semplici passi. 
{:shortdesc}

## Impossibile accedere a {{site.data.keyword.Bluemix_notm}}
{: #ts_unabletologin}

Per eseguire l'accesso, devi avere un account {{site.data.keyword.Bluemix_notm}} valido.


Quando tenti di accedere a {{site.data.keyword.Bluemix_notm}}, visualizzi uno dei seguenti messaggi di errore: 
{: tsSymptoms} 

 * Dal portale del cliente
  
   `Hai raggiunto questa pagina perché l'autenticazione ha avuto esito positivo, tuttavia questo ID IBM non è associato ad alcun account Bluemix. Se credi che si tratti di un errore, contatta il proprietario dell'account o l'utente master.`

 * Dalla console {{site.data.keyword.Bluemix_notm}}
  
  `Hai raggiunto questa pagina perché l'autenticazione ha avuto esito positivo, tuttavia questo ID IBM non è associato ad alcun account  {{site.data.keyword.Bluemix_notm}}.`


Uno dei motivi più probabili per cui viene visualizzato questo messaggio di errore è che non hai ancora creato un account {{site.data.keyword.Bluemix_notm}} o devi passare all'autenticazione dell'ID IBM. 
{: tsCauses} 
 

Segui il processo di registrazione per creare un account {{site.data.keyword.Bluemix_notm}} oppure contatta il tuo utente master o amministratore account per passare all'ID IBM. 
{: tsResolve}

A seconda di come è configurato il tuo account, potrebbero essere applicabili alcune di queste opzioni di accesso: 
 * Gli utenti SoftLayer con ID SoftLayer devono eseguire l'accesso tramite il [Portale del cliente ![icona link esterno](../icons/launch-glyph.svg)](https://control.softlayer.com){: new_window}.
 * Gli utenti SoftLayer con un ID IBM e con o senza un account Bluemix collegato, possono eseguire l'accesso tramite il [Portale del cliente ![icona link esterno](../icons/launch-glyph.svg)](https://control.softlayer.com){: new_window} per aprire il portale clienti SoftLayer o tramite la [Bluemix console ![External link icon](../icons/launch-glyph.svg)](https://console.{DomainName}){: new_window} per aprire il dashboard Infrastruttura. 
 * Gli utenti Bluemix senza un account Bluemix collegato devono eseguire l'accesso tramite la console Bluemix.
 * Gli utenti Bluemix con un account Bluemix collegato possono eseguire l'accesso tramite la [console Bluemix ![icona link esterno](../icons/launch-glyph.svg)](https://console.{DomainName}){: new_window}  il [Portale del cliente ![icona link esterno](../icons/launch-glyph.svg)](https://control.softlayer.com){: new_window}.
 

## La password non è valida
{: #ts_logintobm}

Per accedere alla console {{site.data.keyword.Bluemix_notm}}, devi disporre di un ID IBM valido.

Quando tenti di accedere a {{site.data.keyword.Bluemix_notm}}, visualizzi il seguente messaggio di errore: 
{: tsSymptoms} 

`La password immessa non è corretta.`

L'ID IBM e la password da te utilizzati per accedere a {{site.data.keyword.Bluemix_notm}} non sono validi.
{: tsCauses} 
 
Per ottenere un ID IBM e password validi, vai alla pagina Il mio profilo IBM e completa una della seguenti procedure:
{: tsResolve}
  * Se già hai registrato un ID IBM e vuoi controllare se il tuo ID e la tua password sono validi, fai clic su **Accedi** e immetti il tuo ID IBM e la relativa password nella pagina di accesso. Se hai dimenticato la password, fai clic su **Password dimenticata** nella pagina di accesso per reimpostare la password. Se hai dimenticato il tuo ID IBM o continui ad avere problemi con la tua password, contatta l'Help Desk Worldwide IBM Registration per ottenere assistenza. 
  * Se non hai un ID IBM, fai clic su **Registrati** per registrare un ID IBM e password. 



## Impossibile accedere con un nome utente Softlayer
{: #ts_softlayer_username}

Per accedere a {{site.data.keyword.Bluemix_notm}}, devi disporre di un ID IBM e password validi.


Quando tenti di accedere alla console {{site.data.keyword.Bluemix_notm}} con il tuo nome utente Softlayer, ricevi il seguente messaggio: 
{: tsSymptoms} 

`ID IBM o indirizzo e-mail non riconosciuto.`

Devi disporre di un ID IBM per accedere e utilizzare il dashboard Infrastruttura nella console Bluemix.
{: tsCauses} 
 
Se sei un utente SoftLayer che sta utilizzando un ID SoftLayer, devi passare all'autenticazione dell'ID IBM nel portale del cliente di ciascun account a cui hai accesso affinché tu possa accedere utilizzando l'autenticazione dell'ID IBM. 

Contatta il tuo utente master o amministratore account per passare all'ID IBM. 
{: tsResolve}



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
spam folder. If you still have not received your email confirmation, contact <a href="http://ibm.biz/bluemixsupport.com" target="_blank">Bluemix Support <img src="../icons/launch-glyph.svg" alt="External link icon"></a>.</code>


Dopo aver eseguito la registrazione per un account di prova {{site.data.keyword.Bluemix_notm}},
riceverai un'email di conferma. Dovrai fare clic sul link
che si trova nella email di conferma per completare il processo di registrazione.
{: tsCauses} 

L'email di conferma viene inviata all'indirizzo di posta
da te fornito. Controlla la cartella della posta in arrivo e quella della posta indesiderata. Se non hai ricevuto un'e-mail di conferma, contatta il [{{site.data.keyword.Bluemix_notm}} Supporto ![icona link esterno](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport.com){: new_window}.  
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

  1. Vai al Dashboard {{site.data.keyword.Bluemix_notm}}. Dalla barra dei menu, fai clic sulla voce **Supporto** e seleziona **Gestisci organizzazioni**.
  2. Vai alla tua organizzazione e visualizza le informazioni del gestore organizzazione
sulla scheda **UTENTI**.  
  
Se non riesci a invitare utenti perché sei un collaboratore e non
un membro, devi eliminare il tuo account {{site.data.keyword.Bluemix_notm}} precedente
ed essere inviato a entrare a far parte dell'account come membro dell'organizzazione. Per eliminare il tuo account precedente ed entrare a far parte dell'account come membro,
completa la seguente procedura: 

  1. Contatta il [{{site.data.keyword.Bluemix_notm}} Supporto ![icona link esterno](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window} per aprire un ticket di supporto e richiedere l'eliminazione del tuo account. Se hai dei dati associati al tuo
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

  1. Fai clic su **ESEGUI REGISTRAZIONE** nella console {{site.data.keyword.Bluemix_notm}}.
  2. Completa i passi seguendo la procedura guidata.

    

## Impossibile caricare una pagina
{{site.data.keyword.Bluemix_notm}}
{: #ts_err}

Quando usi la console {{site.data.keyword.Bluemix_notm}}, potresti non riuscire a caricare una pagina {{site.data.keyword.Bluemix_notm}}. Potresti visualizzare invece i messaggi di errore BXNUI0001E o BXNUI0016E.
 

Quando usi la console {{site.data.keyword.Bluemix_notm}} potresti visualizzare uno dei seguenti messaggi di errore:
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
  * Utilizza un browser differente. Per informazioni sulle versioni dei browser supportati da {{site.data.keyword.Bluemix_notm}}, consulta [Prerequisiti di {{site.data.keyword.Bluemix_notm}} ![icona link esterno](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}.
  * Se hai installato l'interfaccia riga di comando cf, immetti il comando `cf
apps` per vedere se l'applicazione è in esecuzione.
  
  
  
  
  

