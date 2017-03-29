---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-03-02"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# Risoluzione dei problemi di accesso a {{site.data.keyword.Bluemix_notm}} 
{: #accessing}


I problemi generali con l'accesso a {{site.data.keyword.Bluemix}} potrebbero includere le difficoltà ad accedere a {{site.data.keyword.Bluemix_notm}} o un account che si trova in uno stato di sospensione. In molti casi, puoi risolvere questi problemi seguendo pochi semplici passi.
{:shortdesc}

## Impossibile accedere a {{site.data.keyword.Bluemix_notm}}: password errata
{: #ts_logintobm}

Per accedere alla console {{site.data.keyword.Bluemix_notm}}, devi disporre di una password valida associata al tuo ID IBM.

Per eseguire l'accesso tramite il [Portale del cliente](https://control.softlayer.com), devi disporre di una password valida associata al tuo ID IBM o ID SoftLayer.

Quando tenti di accedere a {{site.data.keyword.Bluemix_notm}}, viene visualizzato il seguente messaggio di errore:
{: tsSymptoms} 

`La password immessa non è corretta.`

L'ID IBM e la password che hai utilizzato per accedere a {{site.data.keyword.Bluemix_notm}} non sono validi.
{: tsCauses} 
 
Utilizza una delle seguenti soluzioni:
{: tsResolve}
 * Immetti la password corretta. Per controllare se il tuo ID IBM e la tua password sono validi, puoi andare alla pagina Il mio profilo IBM, fare clic su **Accedi** e immettere il tuo ID IBM e la relativa password nella pagina di accesso.  
 * Se hai dimenticato la password, fai clic su **Password dimenticata** per reimpostarla. Torna quindi alla [console Bluemix](https://console.{DomainName}) o al [Portale del cliente](https://control.softlayer.com) e accedi di nuovo.
 * Se hai dimenticato il tuo ID IBM o continui ad avere problemi con la tua password, contatta l'Help Desk Worldwide IBM Registration per ottenere assistenza. 
 * Per ottenere un ID IBM e password validi, vai alla pagina Il mio profilo IBM e fai clic su **Registrati**.
  
**Nota:** se ti trovi nella pagina di accesso a IBM e la procedura di accesso viene interrotta per un qualsiasi motivo (ad esempio, la reimpostazione della password), torna alla [console Bluemix](https://console.{DomainName}) o al [Portale del cliente](https://control.softlayer.com) e inizia di nuovo la procedura di accesso.
 

## Impossibile accedere a {{site.data.keyword.Bluemix_notm}}: credenziali di accesso non valide
{: #ts_login_invalid_credentials}

Quando accedi utilizzando il tuo ID IBM, viene visualizzato il seguente messaggio:
{: tsSymptoms}

`Invalid login credentials provided. If you have an IBMid associated with your account, please log in here` 

* Sei passato a un ID IBM, ma hai tentato di effettuare l'accesso tramite il [Portale del cliente](https://control.softlayer.com) utilizzando il tuo nome utente e password SoftLayer precedenti.
{: tsCauses}

* Hai tentato di accedere tramite il [Portale del cliente](https://control.softlayer.com), ma hai immesso il tuo ID IBM e la password nei campi Nome utente e Password. 

Fai clic su **log in here** nel messaggio o vai alla sezione di accesso degli account ID IBM e fai clic su **Accedi con ID IBM**.
{: tsResolve}

Non utilizzare i campi **Nome utente** e **Password** che utilizzavi con il tuo precedente ID Softlayer.


## Impossibile accedere a {{site.data.keyword.Bluemix_notm}}: ID IBM o e-mail non riconosciuti
{: #ts_softlayer_username}

Quando accedi alla console {{site.data.keyword.Bluemix_notm}}, viene visualizzato il seguente messaggio:
{: tsSymptoms} 

`ID IBM o indirizzo e-mail non riconosciuto.`

Hai tentato di accedere alla console {{site.data.keyword.Bluemix_notm}}, ma non hai utilizzato un ID IBM valido. Ad esempio, non hai immesso un indirizzo e-mail completo per l'ID IBM o hai utilizzato un nome utente e password SoftLaywer.
{: tsCauses}
 
Per accedere a {{site.data.keyword.Bluemix_notm}}, devi disporre di un ID IBM e password validi.

 * Assicurati di immettere un indirizzo e-mail completo per l'ID IBM.
 {: tsResolve}
 * Se sei un utente SoftLayer con un ID SoftLayer, devi passare all'autenticazione ID IBM nel Portale del cliente per ogni account a cui hai accesso prima di poter accedere con l'autenticazione ID IBM.
 Per ulteriori informazioni, vedi [Switching to IBMid](/docs/admin/softlayerlink.html#ibmid_switch).


## Impossibile accedere a {{site.data.keyword.Bluemix_notm}}: l'ID IBM non è associato ad alcun account IBM Cloud
{: #ts_login_noswitch}

Quando accedi utilizzando il tuo ID IBM, viene visualizzato il seguente messaggio:
{: tsSymptoms}

`Hai raggiunto questa pagina perché l'autenticazione ha avuto esito positivo, tuttavia questo ID IBM non è associato ad alcun account Bluemix. Se credi che si tratti di un errore, contatta il proprietario dell'account o l'utente master.`

Hai effettuato l'accesso dal [Portale del cliente](https://control.softlayer.com) con un ID IBM valido, ma non sei passato all'autenticazione ID IBM in SoftLayer.
{: tsCauses} 
 
Completa i seguenti controlli, come appropriato:
{: tsResolve}
 * Contatta il tuo utente master o amministratore account per verificare di essere autorizzato a passare all'autenticazione con ID IBM.
 * Assicurati di completare il passo relativo al passaggio all'ID IBM nel tuo account Softlayer. Vedi [Switching to IBMid](/docs/admin/softlayerlink.html#ibmid_switch).
 * Assicurati di seguire i passaggi indicati nell'e-mail per **Associare il tuo account SoftLayer a un ID IBM**. Controlla la cartella della posta in arrivo e quella dello spam per cercare l'e-mail. Per ricevere di nuovo l'e-mail, ad esempio nel caso in cui sia scaduta, vai alla pagina Modifica profilo utente nel Portale del cliente e fai clic su **Invia nuovamente email**. In alternativa, contatta il [Supporto {{site.data.keyword.Bluemix_notm}} ![icona link esterno](../icons/launch-glyph.svg "External link icon")](http://ibm.biz/bluemixsupport.com){: new_window}.

**Nota:** se hai creato il tuo ID IBM direttamente con l'ID IBM, riceverai due e-mail per il processo: una dalla registrazione dell'ID IBM e una da Softlayer. Assicurati di seguire i passaggi indicati in entrambe le e-mail.

A seconda di come è configurato il tuo account, potrebbero essere applicabili alcune di queste opzioni di accesso: 
 * Gli utenti SoftLayer con ID SoftLayer devono eseguire l'accesso tramite il [Portale del cliente](https://control.softlayer.com).
 * Gli utenti SoftLayer con un ID IBM e con o senza un account Bluemix collegato, possono eseguire l'accesso tramite il [Portale del cliente](https://control.softlayer.com) per aprire il portale clienti SoftLayer o tramite la [console Bluemix](https://console.{DomainName}) per aprire il dashboard Infrastruttura. 


## Impossibile accedere a {{site.data.keyword.Bluemix_notm}}: l'ID IBM non è associato ad alcun account {{site.data.keyword.Bluemix_notm}}
{: #ts_unabletologin}

Quando accedi a {{site.data.keyword.Bluemix_notm}}, viene visualizzato il seguente messaggio:
{: tsSymptoms} 
 
`Hai raggiunto questa pagina perché l'autenticazione ha avuto esito positivo, tuttavia questo ID IBM non è associato ad alcun account  {{site.data.keyword.Bluemix_notm}}.`

Hai effettuato l'accesso dalla [console Bluemix](https://console.{DomainName}) con un ID IBM valido, ma non hai ancora creato un account {{site.data.keyword.Bluemix_notm}}.
{: tsCauses} 

Per creare un account {{site.data.keyword.Bluemix_notm}}, segui il processo di registrazione.
{: tsResolve}

A seconda di come è configurato il tuo account, potrebbero essere applicabili alcune di queste opzioni di accesso: 
 * Gli utenti Bluemix senza un account Bluemix collegato devono eseguire l'accesso tramite la console Bluemix.
 * Gli utenti Bluemix con un account Bluemix collegato possono eseguire l'accesso tramite la [console Bluemix](https://console.{DomainName}) o il [Portale del cliente](https://control.softlayer.com).
 

## Impossibile accedere a {{site.data.keyword.Bluemix_notm}}: la console non si apre
{: #ts_login_stalls}

Quando accedi utilizzando il tuo ID IBM, viene visualizzato un messaggio di esito positivo dell'accesso ma non ritorni alla [console Bluemix](https://console.{DomainName}) o al [Portale del cliente](https://control.softlayer.com).
{: tsSymptoms}

Utilizza una delle seguenti soluzioni:
{: tsResolve}
 * Chiudi il browser, cancella la cache e i cookie e riprova a eseguire l'accesso.
 * Assicurati di eseguire l'accesso dalla [console Bluemix](https://console.{DomainName}) o dal [Portale del cliente](https://control.softlayer.com), piuttosto che direttamente dal servizio di autenticazione ID IBM.
 
 
## Impossibile accedere a {{site.data.keyword.Bluemix_notm}}: l'accesso tramite ID IBM non viene completato
{: #ts_login_ibmid}

Quando accedi a {{site.data.keyword.Bluemix_notm}}, l'autenticazione tramite l'ID IBM non viene completata.
{: tsSymptoms}

Potrebbe esserci un problema con il servizio di autenticazione ID IBM.
{: tsCauses}

Controlla lo stato del servizio in [IBM BlueID ![icona link esterno](../icons/launch-glyph.svg "External link icon")](https://new.wind.ibmcloud.com/webapp/#/status/a1a0c5d743d94a6a9597087541564d8e){: new_window} e riprova.
{: tsResolve}


## Impossibile accedere a {{site.data.keyword.Bluemix_notm}}: l'account è in sospeso
{: #ts_accntpding}

Se il tuo account è in sospeso, non puoi accedere a {{site.data.keyword.Bluemix_notm}}.
 
Dopo aver eseguito la registrazione per un account di prova {{site.data.keyword.Bluemix_notm}},
potresti non riuscire ad accedere a {{site.data.keyword.Bluemix_notm}}. Viene visualizzato il seguente messaggio:
{: tsSymptoms}

<code>Your account is pending. Please wait up to 24 hours for email confirmation and also check your
spam folder. If you still have not received your email confirmation, contact <a href="http://ibm.biz/bluemixsupport.com" target="_blank">Bluemix Support</a>.</code>

Dopo aver eseguito la registrazione per un account di prova {{site.data.keyword.Bluemix_notm}},
riceverai un'e-mail di conferma. Dovrai fare clic sul link
che si trova nella email di conferma per completare il processo di registrazione.
{: tsCauses} 

L'e-mail di conferma viene inviata all'indirizzo di posta
da te fornito. Controlla la cartella della posta in arrivo e quella dello spam. Se non hai ricevuto un'e-mail di conferma, contatta il [Supporto {{site.data.keyword.Bluemix_notm}} ![icona link esterno](../icons/launch-glyph.svg "External link icon")](http://ibm.biz/bluemixsupport.com){: new_window}.  
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

## Impossibile aggiungere utenti a un'organizzazione
{: #ts_adduser}

Puoi invitare più di un utente a lavorare nella stessa organizzazione. Puoi invitare utenti nella tua organizzazione solo
se sei il proprietario dell'account o se sei allo stesso tempo un gestore e un membro dell'organizzazione.
 
Non riesci a visualizzare il link **Invita un nuovo utente** nella sezione **Gestisci organizzazioni**.
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

Non puoi invitare utenti nella tua organizzazione se sei un collaboratore, anche se ti è stato assegnato il ruolo di gestore organizzazione.

**Nota:** tutti i gestori organizzazione, compresi quelli che sono collaboratori di un'organizzazione, possono aggiungere, modificare e rimuovere gli utenti già presenti nell'organizzazione.

Se non riesci a inviare utenti nella tua organizzazione e per farlo hai bisogno di un ruolo differente, contatta il gestore della tua organizzazione per modificare il tuo ruolo. Per identificare il gestore della tua organizzazione, completa
la seguente procedura:
{: tsResolve}

  1. Vai al Dashboard {{site.data.keyword.Bluemix_notm}}. Dalla barra dei menu, fai clic sulla voce **Account** e seleziona **Gestisci organizzazioni**.
  2. Vai alla tua organizzazione e visualizza le informazioni del gestore organizzazione
sulla scheda **UTENTI**.  
  
Se non puoi invitare utenti perché sei un collaboratore e non un membro, devi eliminare il tuo account {{site.data.keyword.Bluemix_notm}} precedente ed essere inviato a entrare a far parte dell'account come membro dell'organizzazione. Per eliminare il tuo account precedente ed entrare a far parte dell'account come membro,
completa la seguente procedura: 

  1. Contatta il [Supporto {{site.data.keyword.Bluemix_notm}} ![icona link esterno](../icons/launch-glyph.svg "External link icon")](http://ibm.biz/bluemixsupport){: new_window} per aprire un ticket di supporto e richiedere l'eliminazione del tuo account. Se hai dei dati associati al tuo
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

{{site.data.keyword.Bluemix_notm}} non fornisce la capacità di registrare più utenti contemporaneamente.
{: tsSymptoms}
 
{{site.data.keyword.Bluemix_notm}} non
supporta la registra batch di utenti. Per registrare gli utenti per {{site.data.keyword.Bluemix_notm}},
devi registrare ciascun utente singolarmente.
{: tsCauses}
 
Per registrare più utenti per {{site.data.keyword.Bluemix_notm}}, completa la seguente procedura per ogni utente:
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

Completa una o più delle seguenti azioni, secondo necessità:
{: tsResolve}

  * Aggiorna o riavvia il tuo browser.
  * Disconnettiti da {{site.data.keyword.Bluemix_notm}} e
riesegui l'accesso.
  * Utilizza la modalità di navigazione privata del tuo browser. 
  * Cancella i cookie e la cache del browser.
  * Utilizza un browser differente. Per informazioni sulle versioni dei browser supportati da {{site.data.keyword.Bluemix_notm}}, vedi [Prerequisiti di Bluemix](/docs/overview/whatisbluemix.html#prereqs).
  * Se hai installato l'interfaccia riga di comando cf, immetti il comando `cf apps` per vedere se la tua applicazione è in esecuzione.
