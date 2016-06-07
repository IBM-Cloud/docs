---

copyright:
  years: 2015, 2016

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 

# Risoluzione dei problemi di accesso a {{site.data.keyword.Bluemix_notm}} 
{: #accessing}

*Ultimo aggiornamento: 16 maggio 2016*

I problemi generali con l'accesso a {{site.data.keyword.Bluemix}} potrebbero includere un utente che non riesce ad accedere a {{site.data.keyword.Bluemix_notm}}, un account bloccato in uno stato In sospeso e così via. Tuttavia, in molti casi, puoi eseguire un ripristino da tali problemi seguendo pochi semplici passi. 
{:shortdesc}

## Impossibile accedere a {{site.data.keyword.Bluemix_notm}}
{: #ts_logintobm}

Per accedere a {{site.data.keyword.Bluemix_notm}}, devi disporre di un ID IBM e password validi.


Quando tenti di accedere a {{site.data.keyword.Bluemix_notm}}, visualizzi il seguente messaggio di errore: 
{: tsSymptoms} 

`L'ID e/o password IBM immessi non sono corretti. Riprova.`


L'ID e la password IBM da te utilizzati per accedere a {{site.data.keyword.Bluemix_notm}} non sono validi.
{: tsCauses} 
 

Per ottenere un ID e una password IBM validi, vai alla pagina Il mio profilo IBM e completa una della seguenti procedure:
{: tsResolve}
  * Se già hai registrato un ID IBM e vuoi controllare se il tuo ID e la tua password sono validi, fai clic su **Accedi** e immetti il tuo ID IBM e la relativa password nella pagina Accedi. Se hai dimenticato la password, fai clic su **Password dimenticata** nella parte destra della pagina di accesso per reimpostare la password. Se hai dimenticato il tuo ID IBM o continui ad avere problemi con la tua password, contatta l'Help Desk Worldwide IBM Registration per ottenere assistenza. 
  * Se non hai un ID IBM, fai clic su **Registrati** per registrare un ID IBM e password. 
  
**Nota:** Per i dipendenti IBM, l'ID IBM potrebbe essere diverso dall'ID di accesso Intranet. 





## Sono presenti modifiche non salvate
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
nslookup mybluemix.net
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

  1. Vai al Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona **Account e supporto** ![Account e supporto](images/account_support.svg) nella barra dei menu superiore e seleziona **Gestisci organizzazioni**.
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

  1. Fai clic su **ESEGUI REGISTRAZIONE** nella parte superiore
destra dell'interfaccia utente
{{site.data.keyword.Bluemix_notm}}.
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
  
  
  
  
  
## La barra dei menu superiore di {{site.data.keyword.Bluemix_notm}}
scompare
{: #ts_topmenubar}

Potresti non riuscire a visualizzare la barra dei menu superiore di {{site.data.keyword.Bluemix_notm}}
quando ridimensioni la finestra del tuo browser o quando utilizzi un dispositivo
mobile.


Quando riduci la dimensione della finestra del tuo browser o
quando utilizzi un dispositivo mobile, la barra dei menu superiore di {{site.data.keyword.Bluemix_notm}}
scompare. Quando la barra dei menu superiore scompare, il menu cassetto laterale
mostrato come icona a linee in pila, viene visualizzato nell'angolo superiore
sinistro. 
{: tsSymptoms}

 

L'interfaccia utente {{site.data.keyword.Bluemix_notm}}
ha un design responsivo. Quando l'ambiente di visualizzazione cambia,
potrebbe cambiare anche il layout dell'interfaccia utente
{{site.data.keyword.Bluemix_notm}}. 
{: tsCauses}
 

Utilizza invece il menu cassetto laterale nell'angolo superiore sinistro.
{: tsResolve}








# Risoluzione dei problemi relativi alla gestione delle applicazioni
{: #managingapps}

I problemi generali con la gestione delle applicazioni potrebbero includere
applicazioni che non possono essere aggiornate o caratteri double-byte che non vengono visualizzati. Tuttavia, in molti casi, puoi eseguire un ripristino da tali problemi seguendo pochi semplici passi.
{:shortdesc}





## Impossibile passare le applicazioni alla modalità di debug
{: #ts_debug}

Potresti non essere in grado di abilitare la modalità di debug se la versione della JVM (Java virtual machine) è 8 o precedente. 


Dopo che hai selezionato **Enable application debug**, gli strumenti tentano di passare l'applicazione alla modalità di debug. Quindi, il workbench di Eclipse avvia una sessione di debug. Quando gli strumenti hanno abilitato correttamente la modalità di debug, lo stato dell'applicazione web visualizza `Updating mode`, `Developing` e `Debugging`. 
{: tsSymptoms}

Tuttavia, quando gli strumenti non riescono ad abilitare la modalità di debug, lo stato dell'applicazione web visualizza solo `Updating mode` e `Developing` e non visualizza `Debugging`. Gli strumenti visualizzano inoltre il seguente messaggio di errore nella vista Console:

```
bluemixMgmgClient - ???? [pool-1-thread-1] .... ERROR --- ClientProxyImpl: Cannot create the websocket connections for MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: The HTTP request to initiate the  WebSocket connection failed
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
at java.util.concurrent.FutureTask.run(FutureTask.java:277)
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
at java.lang.Thread.run(Thread.java:785)
Caused by: javax.websocket.DeploymentException: The HTTP request to initiate the WebSocket connection failed
at  org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
at  com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 more
Caused by: java.util.concurrent.TimeoutException
at org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
at org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 more
[2016-01-15 13:33:51.075] bluemixMgmgClient - ????  [pool-1-thread-1] .... ERROR --- ClientProxyImpl: Cannot create the  websocket connections for MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: The HTTP request to initiate the  WebSocket connection failed
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
at java.util.concurrent.FutureTask.run(FutureTask.java:277)
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
at java.lang.Thread.run(Thread.java:785)
Caused by: javax.websocket.DeploymentException: The HTTP request to initiate the WebSocket connection failed
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 more
Caused by: java.util.concurrent.TimeoutException
at org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
at org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 more
```
 

Le seguenti versioni della JVM (Java virtual machine) non possono stabilire una sessione di debug: IBM JVM 7, IBM JVM 8 e versioni precedenti di Oracle JVM 8.
{: tsCauses}

Se il tuo workbench JVM è di una di queste versioni, potresti avere problemi durante la creazione di una sessione di debug. La versione JVM del workbench è normalmente la JVM di sistema del tuo computer lcoale. La tua JVM di sistema non è la stessa della tua applicazione Java Bluemix in esecuzione. L'applicazione Java Bluemix viene quasi sempre eseguita su JVM IBM e alcune volte su JVM OpenJDK.
  

Per controllare la versione di Java che segue IBM Eclipse Tools for Bluemix, completa la seguente procedura:
{: tsResolve}

  1. In IBM Eclipse Tools for Bluemix, seleziona **Guida** > **Informazioni su Eclipse** > **Dettagli dell'installazione** > **Configurazione**.
  2. Trova la proprietà `eclipse.vm` dall'elenco. La seguente linea è un esempio di una proprietà `eclipse.vm`:
	
	```
	eclipse.vm=C:\Program Files\IBM\ibm-java-sdk-80-win-x86_64\bin\..\jre\bin\j9vm\jvm.dll
	```

  3. Nella riga di comando, immetti `java -version` dalla directory `bin` della tua installazione Java. Vengono visualizzate le informazioni sulla tua versione Java IBM.

Se il JVM workbench JVM è IBM JVM 7 o 8 o una versione precedente di Oracle JVM 8, completa la seguente procedura per passare a Oracle JVM 8:

  1. Scarica e installa Oracle JVM 8, per i dettagli consulta [Java SE Downloads](http://www.oracle.com/technetwork/java/javase/downloads/index.html){: new_window}.
  2. Riavvia Eclipse.
  3. Controlla se la proprietà `eclipse.vm` punta alla tua nuova installazione di Oracle JVM 8.







## Impossibile effettuare le azioni richieste
{: #ts_authority}

Potresti non riuscire a completare delle azioni senza un'appropriata autorità di accesso.

 

Quando tenti di eseguire azioni per un'istanza del servizio o un'istanza dell'applicazione, non riesci a completare le azioni richieste e visualizzai uno dei seguenti messaggi di errore: 
{: tsSymptoms}

`BXNUI0514E: You are not a developer for any of the spaces in the <orgName> organization.`


`Server error, status code: 403, error code: 10003, message: You are not authorized to perform the requested action.`

 

Non disponi di un adeguato livello di autorità necessario per eseguire le azioni. 
{: tsCauses}

  

Per ottenere il livello di autorità appropriato, utilizza uno dei seguenti metodi: 
{: tsResolve}
 * Seleziona un'altra organizzazione e uno spazio per cui disponi del ruolo di sviluppatore. 
 * Chiedi al gestore organizzazione di modificare il tuo ruolo in sviluppatore oppure di creare uno spazio e assegnarti quindi un ruolo sviluppatore. Per i dettagli, vedi [Gestione delle tue organizzazioni](../admin/orgs_spaces.html).
 

 


## Impossibile accedere ai servizi {{site.data.keyword.Bluemix_notm}} a causa di errori di autorizzazione
{: #ts_vcap}

Gli errori di autorizzazione potrebbero verificarsi quando la tua applicazione accede a un servizio {{site.data.keyword.Bluemix_notm}} se le credenziali del servizio sono hardcoded nell'applicazione. 

Dopo aver configurato l'applicazione per comunicare con un servizio {{site.data.keyword.Bluemix_notm}}, distribuisci l'applicazione a {{site.data.keyword.Bluemix_notm}}. Tuttavia, non riesci a utilizzare l'applicazione per accedere al servizio {{site.data.keyword.Bluemix_notm}} e ricevi un messaggio di errore.
{: tsSymptoms}

Le credenziali hardcoded nell'applicazione potrebbero non essere corrette. Ogni volta che il servizio viene ricreato, le credenziali per accedervi cambiano.
{: tsCauses}


Invece di impostare come hardcoded le credenziali nella tua applicazione, utilizza i parametri di connessione dalla variabile di ambiente VCAP_SERVICES. I metodi per utilizzare i parametri di connessione dalla variabile di ambiente VCAP_SERVICES variano a seconda dei linguaggi di programmazione. Ad esempio, per le applicazioni Node.js, puoi utilizzare il seguente comando: 
{: tsResolve}

```
process.env.VCAP_SERVICES
```
Per ulteriori informazioni sui comandi che puoi utilizzare in altri linguaggi di programmazione, vedi [Java](http://docs.run.pivotal.io/buildpacks/java/java-tips.html#env-var){: new_window} e [Ruby](http://docs.run.pivotal.io/buildpacks/ruby/ruby-tips.html#env-var){: new_window}. 
 

 
 




## Impossibile distribuire le applicazioni utilizzando IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}
{: #ts_bm_tools_facet}

Quando al tuo progetto Eclipse viene applicato un facet non supportato, potresti non essere in grado di distribuire le
tue applicazioni a {{site.data.keyword.Bluemix_notm}} utilizzando IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}. 

 

Puoi distribuire correttamente la tua applicazione a {{site.data.keyword.Bluemix_notm}} utilizzando la CLI Cloud Foundry. Tuttavia, non puoi distribuire l'applicazione a {{site.data.keyword.Bluemix_notm}} utilizzando IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, e vedi un messaggio di errore: `Project facet <nome_facet> is not supported.`. Ad esempio, `Project facet Cloud Foundry Standalone Application version 1.0 is not supported.`
{: tsSymptoms}

 

IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} associa i progetti ai runtime {{site.data.keyword.Bluemix_notm}} in base ai facet di progetto. I facet definiscono i requisiti per i progetti Java EE in Eclipse e sono utilizzati come parte della configurazione di runtime, in modo che runtime differenti siano associati a progetti differenti. Se il facet applicato al progetto non è supportato da
IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, potresti non essere in grado di distribuire la tua applicazione utilizzando IBM Eclipse
Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}


Devi rimuovere il facet dal progetto Eclipse in modo da poter distribuire la tua applicazione
utilizzando IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsResolve} 

Per rimuovere il
facet, in IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, fai clic su **Project>Properties>Project Facets** per il progetto. Deseleziona quindi la casella di spunta per il facet non supportato. 



## Ricezione di errori 502 Bad Gateway
{: #ts_502_error}

Se ricevi degli errori 502 Bad Gateway quando interagisci
con le applicazioni su {{site.data.keyword.Bluemix_notm}},
controlla la pagina degli stati di {{site.data.keyword.Bluemix_notm}}
ed effettua le operazioni appropriate.

 

Ricevi dei messaggi di errore che iniziano con 502 Bad Gateway. Ad esempio, potresti vedere `502 Bad Gateway: Registered endpoint failed to handle the request.`
{: tsSymptoms}

 

Un errore
Bad Gateway di solito si verifica quando visiti un sito Web che utilizza
un server proxy per memorizzare e inoltrare i dati dal server principale che
ospita il sito. Il server principale e il server proxy potrebbero non connettersi
correttamente, pertanto visualizzi il codice di stato HTTP 502 nella finestra del
browser. Questo codice di stato indica che il server principale del sito non ha
ricevuto l'implementazione HTTP prevista dal server
proxy.
{: tsCauses}

Altre cause meno comuni di un errore Bad Gateway sono
interruzioni ISP (Internet Service Provider), configurazioni firewall non valide ed
errori della cache del browser. 

 

Se sospetti che un servizio {{site.data.keyword.Bluemix_notm}} sia inattivo, controlla prima la pagina [dello stato di {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#status){: new_window}. Come soluzione alternativa, potresti voler utilizzare questo servizio in un'altra regione
{{site.data.keyword.Bluemix_notm}}. Informazioni dettagliate sono disponibili in [Utilizzo
dei servizi in un'altra regione](../services/reqnsi.html#cross_region_service){: new_window}. Se lo stato del servizio è normale,
prova le seguenti operazioni per risolvere il problema: 
{: tsResolve}

  * Ritenta l'azione:
    * Ricarica la pagina premendo F5 sulla tastiera o facendo clic sul
pulsante di aggiornamento. Se questa operazione non funziona, cancella la cache
e i cookie del tuo browser e ricarica di nuovo la pagina.
	* Utilizza un browser differente.
	* Riavvia il router, il modem e il computer. Il riavvio di questi
dispositivi può cancellare i diversi errori che portano all'errore 502. 
  * Attendi e riprova in seguito. In alcuni casi, possono verificarsi dei
problemi temporanei con il tuo provider dei servizi Internet o con i servizi {{site.data.keyword.Bluemix_notm}}. Puoi attendere finché i problemi non vengono risolti.
  * Se il problema persiste, contatta il supporto {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni, vedi [Come contattare il supporto {{site.data.keyword.Bluemix_notm}}](../support/index.html#contacting-bluemix-support){: new_window}. 




## Quota disco superata
{: #ts_disk_quota}

Se esaurisci lo spazio su disco, puoi modificare manualmente la quota per
ottenere ulteriore spazio sul disco.

  

Se esaurisci lo spazio su disco, potresti visualizzare un messaggio
che indica che la quota di disco è stata superata. Per risolvere il problema,
potresti aver tentato di ridimensionare la tua istanza dell'applicazione per ottenere ulteriore spazio
su disco. Ad esempio, avresti potuto eseguire il ridimensionamento da 256 MB a 1256 MB modificando
la quota di memoria nella pagina dei dettagli dell'applicazione. Tuttavia, poiché la quota di
disco è rimasta la stessa, non hai ottenuto ulteriore spazio su disco. 
{: tsSymptoms}


La quota di disco predefinita assegnata a un'applicazione è 1
GB. Se hai bisogno di più spazio su disco, devi specificare manualmente la
quota di disco. 
{: tsCauses}

 
Utilizza uno dei seguenti metodi per specificare la quota disco. La quota di disco massima che puoi specificare è 2 GB. Se 2 GB non è ancora
sufficiente, prova un servizio esterno come [Object Store](../services/ObjectStorage/index.html){: new_window}.
{: tsResolve}

  * Nel file manifest.yml, aggiungi la seguente voce:
    ```
	disk_quota: <quota_disco>
	```
  * Utilizza l'opzione **-k** con il comando `cf push`
quando distribuisci la tua applicazione a {{site.data.keyword.Bluemix_notm}}:
    ```
	cf push nomeapplicazione -p app_path -k <quota_disco>
	```

	
	
## Impossibile aggiungere il repository Git
{: #ts_cannot_addgit}

Dopo aver creato un'applicazione sul Dashboard, fai clic sul AGGIUNGI GIT per aggiungere un repository Git, ma non riesci a continuare.



Quando fai clic su **AGGIUNGI GIT**, si apre una finestra
e si verifica uno dei seguenti problemi:
{: tsSymptoms} 

  * La finestra si blocca con una schermata vuota.
  * Un messaggio indica che esiste un problema con i cookie di terze parti.



È possibile che il tuo browser sia configurato per impedire l'impostazione
di un cookie. Tale cookie deve essere impostato dal sito di IBM® Bluemix DevOps Services nel dominio Internet hub.jazz.net all'interno del contesto della console {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}  

 

Puoi risolvere questo problema in uno dei seguenti modi:
{: tsResolve}

  * Segui le istruzioni presenti nella finestra che viene visualizzata
dalla console {{site.data.keyword.Bluemix_notm}}. Fai clic sul pulsante. Si aprirà temporaneamente un'altra finestra del browser. In tale
finestra, DevOps Services imposta il cookie di autenticazione.
  * In un'altra scheda del browser, vai all'indirizzo https://hub.jazz.net ed esegui l'accesso. Torna alla console {{site.data.keyword.Bluemix_notm}}
e aggiorna la pagina. Fai di nuovo clic su **AGGIUNGI GIT**.
  * Modifica le impostazioni del tuo browser per abilitare i cookie di terze parti e fai di nuovo clic su AGGIUNGI GIT. Per i dettagli sulla configurazione delle impostazioni,
consulta la documentazione relativa al tuo browser:
    * [Mozilla Firefox](https://support.mozilla.org/en-US/kb/enable-and-disable-cookies-website-preferences#w_how-do-i-change-cookie-settings){: new_window}
	* [Google
Chrome](https://support.google.com/chrome/answer/95647){: new_window}
	* [Apple Safari](https://support.apple.com/kb/PH17191){: new_window}
	* [Microsoft Internet Explorer](http://windows.microsoft.com/en-us/internet-explorer/delete-manage-cookies#ie=ie-11){: new_window}
Se queste soluzioni alternative non risolvono il problema, invia un'email a idslogin@jazz.net.



## Le applicazioni Android non possono ricevere le notifiche di push
{: #ts_push}

In alcune regioni in cui Google non è accessibile, le applicazioni Android
non possono ricevere le notifiche che invii tramite il servizio IBM
Push. In questo caso, puoi utilizzare servizi di terze parti come soluzione alternativa.

 

Esegui il bind di un servizio Push per la tua applicazione Bluemix e invii un messaggio ai dispositivi registrati. Tuttavia, le applicazioni
sviluppate sulla piattaforma Android non possono ricevere le tue notifiche
in determinate regioni. 
{: tsSymptoms}

 
Il servizio IBM Push utilizza il servizio GCM (Google Cloud Messaging)
per inviare notifiche alle applicazioni mobili sviluppate sulla
piattaforma Android. Per consentire alle applicazioni Android di ricevere le notifiche,
è necessario che il servizio GCM (Google Cloud Messaging) sia accessibile dalle applicazioni
mobili. Nelle regioni in cui il servizio GCM non può essere raggiunto dalle applicazioni Android,
tali applicazioni non saranno in grado di ricevere le notifiche di push.
{: tsCauses}

 
Come soluzione alternativa, utilizza servizi di terze parti che non si basano sul servizio GCM,
ad esempio [Pushy](https://pushy.me){: new_window}, [igetui](http://www.getui.com/){: new_window} e [jpush](https://www.jpush.cn/){: new_window}.
{: tsResolve}



## Limite dei servizi dell'organizzazione superato
{: #ts_servicelimit}

Se utilizzi un account utente di prova, potresti non riuscire
a creare un'applicazione in {{site.data.keyword.Bluemix_notm}} se
hai superato il limite dei servizi della tua organizzazione.
 

Quando tenti di creare un'applicazione in {{site.data.keyword.Bluemix_notm}},
visualizzi il seguente messaggio di errore: 
{: tsSymptoms}

`BXNUI2032E: La risorsa <istanze_servizio> non è stata creata. Mentre Cloud Foundry veniva contattato per creare la risorsa, si è verificato un errore. Messaggio di Cloud Foundry: "È stato superato il limite
dei servizi dell'organizzazione."`



Questo errore si verifica quando superi il limite per il
numero di istanze del servizio che puoi avere per l'account. Il
numero massimo di istanze di servizi per un account di prova è 10.
{: tsCauses} 

 

Elimina tutte le istanze dei servizi che non sono necessarie o rimuovi
il limite per il numero di istanze del servizio che puoi avere.
{: tsResolve}
 
  * Per eliminare un'istanza dei servizi, puoi utilizzare l'interfaccia utente di {{site.data.keyword.Bluemix_notm}}
o l'interfaccia riga di comando.
    Per utilizzare l'interfaccia utente di {{site.data.keyword.Bluemix_notm}}
per eliminare un'istanza del servizio, completa la seguente procedura:
	  1. Sul Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic su **SERVIZI** nel riquadro a sinistra. Vengono visualizzati i
tile dei servizi. 
	  2. Sul tile del servizio che vuoi eliminare, fai clic sull'icona **Menu**.
	  3. Fai clic su **Elimina servizio**. Dopo aver eliminato
l'istanza del servizio, ti verrà richiesto di preparare nuovamente l'applicazione
a cui era associata l'istanza del servizio. 
    Per utilizzare l'interfaccia riga di comando per eliminare un'istanza del
servizio, completa la seguente procedura:
	  1. Annulla il bind dell'istanza del servizio da un'applicazione immettendo `cf
unbind-service <nomeapplicazione> <nome_istanza_servizio>`.
	  2. Elimina l'istanza del servizio immettendo `cf delete-service <nome_istanza_servizio>`.
	  3. Dopo aver eliminato l'istanza del servizio, potresti voler preparare nuovamente l'applicazione
a cui era associata l'istanza del servizio immettendo `cf
restage <nomeapplicazione>`.
  * Per rimuovere il limite sul numero di istanze del servizio che puoi avere,
converti il tuo account di prova in un account a pagamento. Per informazioni su come convertire il tuo account di prova in un account a pagamento, vedi [Come modificare il tuo piano](../pricing/index.html#changing){: new_window}.

  
  
## Impossibile eseguire gli eseguibili su {{site.data.keyword.Bluemix_notm}}
{: #ts_executable}

Potresti non riuscire ad eseguire gli eseguibili su {{site.data.keyword.Bluemix_notm}} se
tali eseguibili sono stati sviluppati e creati in un ambiente diverso. 

 

Non riesci ad eseguire gli eseguibili su {{site.data.keyword.Bluemix_notm}} quando
tali eseguibili sono stati sviluppati e creati in un ambiente diverso.
{: tsSymptoms}

 

Se il contenuto che desideri distribuire a {{site.data.keyword.Bluemix_notm}} è
già un eseguibile, il contenuto è stato creato precedentemente e non è necessario
crearlo in {{site.data.keyword.Bluemix_notm}}. In questo caso, non è richiesto alcun pacchetto di build per l'eseguibile da eseguire
su {{site.data.keyword.Bluemix_notm}}. Tuttavia, devi indicare esplicitamente a {{site.data.keyword.Bluemix_notm}} che
non è richiesto alcun pacchetto di build.
{: tsCauses}

 

Quando distribuisci l'eseguibile a {{site.data.keyword.Bluemix_notm}},
devi specificare un pacchetto di build null, che indica che
non è richiesto alcun pacchetto di build. Specifica un pacchetto di build null utilizzando l'opzione **-b**
con il comando `cf push`:
{: tsResolve}

```
cf push nomeapplicazione -p <percorso_applicazione> -c <comando_di_avvio> -b <null-buildpack>
```
Ad esempio:
```
cf push nomeapplicazione -p <percorso_applicazione> -c ./RunMeNow -b https://github.com/ryandotsmith/null-buildpack
```


## Limite di memoria dell'organizzazione superato
{: #ts_outofmemory}

Se utilizzi un account utente di prova, potresti non riuscire a distribuire un'applicazione a {{site.data.keyword.Bluemix_notm}} se hai superato il limite di memoria della tua organizzazione. Puoi
ridurre la memoria utilizzata dalle tue applicazioni o aumentare la quota di memoria
del tuo account. 



Quando distribuisci un'applicazione a {{site.data.keyword.Bluemix_notm}}, visualizzi il seguente messaggio di errore:
{: tsSymptoms} 

`FAILED Server error,
status code: 400, error code: 100005, message: You have exceeded your
organization's memory limit.`

 

Questo errore si verifica quando la quantità di memoria rimanente per la tua organizzazione è inferiore alla quantità di memoria richiesta dall'applicazione che desideri distribuire. La quota massima di memoria
per un account di prova è 2 GB.
{: tsCauses}



Puoi aumentare la quota di memoria del tuo account o ridurre la memoria utilizzata dalle tue applicazioni.
{: tsResolve} 

  * Per aumentare la quota di memoria dell'account,
converti il tuo account di prova in un account a pagamento. Per informazioni
su come convertire il tuo account di prova in un account a pagamento, vedi [Pay
accounts](../pricing/index.html#pay-accounts){: new_window}. 
  * Per ridurre la memoria utilizzata dalle tue applicazioni, utilizza l'interfaccia utente{{site.data.keyword.Bluemix_notm}} o l'interfaccia riga di comando cf.
    Se utilizzi l'interfaccia utente {{site.data.keyword.Bluemix_notm}}, completa la seguente procedura:
	  1. Sul Dashboard {{site.data.keyword.Bluemix_notm}}, seleziona la tua applicazione. Viene visualizzata la pagina dei dettagli dell'applicazione.
	  2. Nel riquadro runtime, puoi ridurre il limite massimo di memoria o il numero di istanze dell'applicazione, o entrambi, per tua applicazione. 
	Se utilizzi l'interfaccia riga di comando cf, completa la seguente procedura:
	  1. Verifica la quantità di memoria utilizzata per le tue applicazioni:
	  ```
	  cf apps
	  ```
	     Il comando cf apps elenca tutte le applicazioni che hai distribuito nel tuo spazio corrente. Viene visualizzato anche lo stato di ciascuna applicazione.
      2. Per ridurre la quantità di memoria utilizzata dalla tua applicazione, riduci il numero di istanze dell'applicazione e/o il limite massimo di memoria.
	  ```
	  cf push <nomeapplicazione> -p <percorso_applicazione> -i <numero_istanza> -m <limite_memoria>
      ```
	  3. Riavvia la tua applicazione per rendere effettive le modifiche.



	  
## Le applicazioni non si riavviano automaticamente
{: #ts_apps_not_auto_restarted}


Un'applicazione non si riavvia automaticamente quando un servizio che associ mediante bind all'applicazione smette di funzionare.	  
	  
 

Quando un servizio che associ mediante bind a un'applicazione viene arrestato in modo anomalo, nell'applicazione potrebbero verificarsi dei problemi come interruzioni, eccezioni ed errori di connessione. {{site.data.keyword.Bluemix_notm}} non
riavvia automaticamente l'applicazione per eseguire un ripristino da tali problemi.
{: tsSymptoms}



Questo è il funzionamento progettato da Cloud Foundry.
{: tsCauses} 

 

Puoi riavviare manualmente l'applicazione immettendo il seguente comando nell'interfaccia riga di comando:
{: tsResolve}

```
cf push <nomeapplicazione> -p <percorso_applicazione>
```
Inoltre, puoi codificare l'applicazione per identificare e risolvere problemi come interruzioni, eccezioni ed errori di connessione. 

	  

## Le variabili definite dall'utente vengono perse dopo la distribuzione di un'applicazione
{: #ts_varsnotretained}

Quando esegui il push di un'applicazione a {{site.data.keyword.Bluemix_notm}} da IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, le variabili che hai specificato vengono reimpostate a meno che non salvi tali variabili nel file
manifest.



Le variabili che hai specificato vengono perse in seguito all'esecuzione del push di un'applicazione a {{site.data.keyword.Bluemix_notm}} da IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms} 


Le variabili specificate vengono mantenute solo se le salvi
nel file manifest.
{: tsCauses} 

 

Quando esegui il push di un'applicazione a {{site.data.keyword.Bluemix_notm}} da IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, seleziona la casella di spunta **Salva nel file manifest** nella pagina Dettagli applicazione della procedura guidata Applicazione. Quindi,
le variabili che hai specificato nella
procedura guidata vengono
salvate nel file manifest della tua applicazione. La prossima volta che apri la procedura guidata, le variabili vengono visualizzate automaticamente.
{: tsResolve}



## Le icone di {{site.data.keyword.Bluemix_notm}} Live
Sync non vengono visualizzate
{: #ts_llz_lkb_3r}

Hai creato un'applicazione in IBM Bluemix DevOps Services, ma le icone IBM Bluemix Live Sync non sono visualizzate nel Web IDE.

 

Quando modifichi un'applicazione Node.js nel DevOps Services Web IDE, le icone di le icone di live edit, riavvio rapido e debug di {{site.data.keyword.Bluemix_notm}} non vengono visualizzate.
{: tsSymptoms}

 

Le icone non sono disponibili nei seguenti casi:
{: tsCauses}

  * Il file `manifest.yml` non è memorizzato al
livello superiore del tuo progetto.
  * La tua applicazione è memorizzata in una sottodirectory anziché al livello superiore
del tuo progetto, ma il percorso della sottodirectory non è specificato
nel file `manifest.yml`.
  * L'applicazione non contiene un file `package.json`.


Per risolvere il problema utilizza uno dei seguenti metodi: 
{: tsResolve} 

  * Se il file `manifest.yml` non è memorizzato al
livello superiore del tuo progetto, memorizzalo lì.
  * Se la tua applicazione è memorizzata in una sottodirectory, specifica il percorso
di tale sottodirectory nel file `manifest.yml`.
  ```
   path: percorso_alla_applicazione
   ```
  * Crea un file `package.json` che si trovi nella stessa
directory della tua applicazione.

  
  
  

  
  

  
  
## Non è possibile trovare le organizzazioni in {{site.data.keyword.Bluemix_notm}}
{: #ts_orgs}

Potresti non riuscire a individuare la tua organizzazione in {{site.data.keyword.Bluemix_notm}} quando
lavori su una regione {{site.data.keyword.Bluemix_notm}}.
  
 

Riesci ad accedere correttamente all'interfaccia utente {{site.data.keyword.Bluemix_notm}} ma non puoi distribuire le applicazioni utilizzando l'interfaccia riga di comando cf o il plug-in Eclipse.
{: tsSymptoms}

Quando tenti di distribuire un'applicazione
a {{site.data.keyword.Bluemix_notm}} utilizzando
l'interfaccia riga di comando cf, puoi visualizzare uno dei seguenti
messaggi di errore in cui viene specificato il nome dell'organizzazione: 

`Error finding org`

`Organization not found`


Quando tenti di distribuire un'applicazione a {{site.data.keyword.Bluemix_notm}}
utilizzando il plug-in Eclipse Cloud Foundry, visualizzi il seguente messaggio di
errore:

`cloudspace not found.`



Questo problema si verifica poiché l'endpoint API della regione
che vuoi utilizzare non è specificato e l'organizzazione che stai
cercando potrebbe trovarsi in una regione differente.
{: tsCauses} 

   
  
Se stai eseguendo il push della tua applicazione a {{site.data.keyword.Bluemix_notm}} utilizzando l'interfaccia riga di comando cf, immetti il comando cf api e specifica l'endpoint API della regione. Ad esempio, immetti il seguente comando per stabilire una connessione alla regione {{site.data.keyword.Bluemix_notm}} Europa
Regno Unito:
{: tsResolve}

```
cf api https://api.eu-gb.bluemix.net
```
Se stai distribuendo la tua applicazione a {{site.data.keyword.Bluemix_notm}} utilizzando
gli strumenti Eclipse, devi prima creare un server {{site.data.keyword.Bluemix_notm}}
e specificare l'endpoint API della regione {{site.data.keyword.Bluemix_notm}} in
cui è stata creata la tua organizzazione. Per ulteriori informazioni sull'utilizzo di strumenti Eclipse, consulta il documento relativo alla [distribuzione di applicazioni con IBM Eclipse Tools for Bluemix](../manageapps/eclipsetools/eclipsetools.html){: new_window}.  
  
  


## Impossibile creare una rotta di applicazione
{: #ts_hostistaken}

Quando distribuisci un'applicazione a {{site.data.keyword.Bluemix_notm}}, la rotta dell'applicazione non può essere creata se il nome host da te specificato è già in uso.



Quando distribuisci un'applicazione a {{site.data.keyword.Bluemix_notm}}, visualizzi il seguente messaggio di errore: 
{: tsSymptoms} 

`Creating route hostname.domainname ... FAILED Server error, status code: 400, error code: 210003, message: The host is taken: hostname`



Questo problema si verifica se il nome host da te specificato
è già in uso.
{: tsCauses} 


  
Il nome host specificato deve essere univoco all'interno
del dominio che stai utilizzando. Per specificare un nome host differente, usa uno dei
seguenti metodi:
{: tsResolve} 

  * Se distribuisci la tua applicazione utilizzando il file `manifest.yml`, specifica il nome host nell'opzione host.	 
    ```
    host: <nomehost>	
	```
  * Se distribuisci la tua applicazione dal prompt dei comandi, utilizza il comando `cf
push` con l'opzione **-n**. 
    ```
    cf push <nomeapplicazione> -p <percorso_applicazione> -n <nome_host>
    ```


## Non è possibile distribuire un'applicazione WAR utilizzando il comando cf push
{: #ts_cf_war}

Potresti non riuscire a utilizzare il comando cf push per distribuire un'applicazione web archiviata a {{site.data.keyword.Bluemix_notm}} se la posizione dell'applicazione non è specificata correttamente.
	


Quando carichi un'applicazione WAR in {{site.data.keyword.Bluemix_notm}} utilizzando il comando `cf push`, visualizzi il messaggio di errore `Staging
error: cannot get instances since staging failed.`
{: tsSymptoms} 

 

Questo problema potrebbe verificarsi se non si specifica il file WAR
o il percorso del file WAR. 
{: tsCauses}

 	
	
Utilizza l'opzione **-p** per specificare
un file WAR o aggiungere il percorso del file WAR. Ad esempio:
{: tsResolve}

```
cf push nomeunivocodellamiaapplicazione01 -p app.war
```

```
cf push nomeunivocodellamiaapplicazione02 -p "./app.war"
```
Per ulteriori informazioni sul comando `cf push` , immettere `cf push -h`. 	





## I caratteri double-byte non sono visualizzati correttamente quando viene eseguito il push di applicazioni Liberty a {{site.data.keyword.Bluemix_notm}}
{: #ts_doublebytes}

I caratteri double-byte potrebbero non essere visualizzati correttamente se il supporto Unicode non è adeguatamente configurato per i file servlet o JSP.

 

Quando un'applicazione Liberty viene distribuita a {{site.data.keyword.Bluemix_notm}}, i caratteri double-byte specificati all'interno dell'applicazione non vengono visualizzati correttamente.
{: tsSymptoms}

 

Il problema può verificarsi se il supporto Unicode non è configurato correttamente per i file servlet o JSP.
{: tsCauses}


Puoi utilizzare il seguente codice all'interno dei tuoi file servlet o JSP:
{: tsResolve} 

  * Nel file di origine servlet 
    ```
	response.setContentType("text/html; charset=UTF-8");
	```
  * Nel JSP 
    ```
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
	```
	
	
	

## Impossibile distribuire le applicazioni Node.js
{: #ts_nodejs_deploy}

Potresti riscontrare dei problemi quando aggiorni un'applicazione Node.js
o quando distribuisci un'applicazione Node.js a {{site.data.keyword.Bluemix_notm}}.



Quando aggiorni un'applicazione Node.js o distribuisci la tua applicazione Node.js
a {{site.data.keyword.Bluemix_notm}},
potresti visualizzare uno dei seguenti messaggi di errore:
{: tsSymptoms} 

`An app was not successfully detected by any available buildpack.`


`Instance (index 0) failed to start accepting connections.`


`Cannot get instances since staging failed.`


 

Di seguito sono indicate le possibili cause del problema:
{: tsCauses}
 
  * Il comando di avvio non è specificato.
  * I file richiesti per distribuire un'applicazione Node.js non sono presenti
nell'applicazione o si trovano in una cartella diversa dalla directory root.
  


	
Effettua le seguenti operazioni in base alla causa del
problema:
{: tsResolve} 

  * Specifica il comando di avvio utilizzando uno dei seguenti metodi: 
      * Utilizza l'interfaccia riga di comando cf. Ad
                                    esempio: 
        ```
		cf push MyUniqueNodejs01 -p app_path -c "node app.js"
		```
	  * Utilizza il file [package.json](https://docs.npmjs.com/json){: new_window}. Ad
esempio:
	    ```
		{
      ...
  	   "scripts": {
	 		 "start": "node app.js"
 	   }
	}
	    ```
	  * Utilizza il file `manifest.yml`. Ad
esempio: 
	    ```
		applications:
  name: MyUniqueNodejs01
  ...
  command: node app.js
  ...
        ```

  * Assicurati che nella tua applicazione Node.js sia presente un file `package.json`
per consentire al pacchetto di build Node.js di riconoscere
l'applicazione. Inoltre, devi inserire questo file nella directory root
della tua applicazione.	
    Il seguente
                                                  esempio mostra un semplice file
                                                  `package.json`:  
	```
	{
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": "3.4.x",
                "jade": "1.1.x"
        },
        "engines": {
                "node": "0.10.x"
        },
        "scripts": {
                  "start": "node app.js"
        }
 }
    ```
	
Per ulteriori suggerimenti relativi alle applicazioni Node.js, vedi [Tips for Node.js Applications](http://docs.cloudfoundry.org/buildpacks/node/node-tips.html){: new_window}.	




## Sono presenti degli errori di configurazione nel file `server.xml` dopo che importi un'applicazione {{site.data.keyword.Bluemix_notm}} Liberty da Bluemix DevOps Services a Eclipse
{: #ts_eclipse}

Se vedi degli errori di configurazione nel file `server.xml` dopo aver importato un'applicazione {{site.data.keyword.Bluemix_notm}} Liberty da IBM Bluemix DevOps Services a Eclipse, potresti dover rimuovere il file `server.xml` dal progetto. 

 

Dopo aver importato un'applicazione {{site.data.keyword.Bluemix_notm}} Liberty da {{site.data.keyword.Bluemix_notm}} DevOps Services in Eclipse, vedi degli errori di configurazione nel file `server.xml` dalla vista Problemi di Eclipse. 
{: tsSymptoms}

 

Il pacchetto di build Liberty utilizza il file `server.xml` per configurare l'applicazione e genera un file `runtime-vars.xml` quando viene eseguito il push dell'applicazione Liberty a {{site.data.keyword.Bluemix_notm}}. Quando importi l'applicazione in Eclipse, il file `runtime-vars.xml` non esiste nel tuo ambiente locale.
{: tsCauses}

 

Puoi risolvere questo problema rimuovendo il file server.xml dal progetto. Il pacchetto di build crea il file `server.xml` dinamicamente quando
esegui il push dell'applicazione come un'applicazione WAR. Per ulteriori informazioni, vedi [Liberty for Java](../runtimes/liberty/index.html){: new_window}.
{: tsResolve}
	
	
## Non è possibile preparare un'applicazione utilizzando un pacchetto di build personalizzato
{: #ts_bp_compilation}

Potresti non riuscire a distribuire un'applicazione a {{site.data.keyword.Bluemix_notm}} utilizzando un pacchetto di build personalizzato se gli script all'interno del pacchetto di build non sono eseguibili.



Quando distribuisci un'applicazione a {{site.data.keyword.Bluemix_notm}} utilizzando un pacchetto di build personalizzato, visualizzi il messaggio di errore `La preparazione  dell'applicazione non è riuscita e, pertanto, non ci sono istanze da visualizzare.`
{: tsSymptoms} 


Questo problema
potrebbe verificarsi se gli script, ad esempio lo script di rilevamento, lo script di compilazione e lo
                script di rilascio, non sono eseguibili.
{: tsCauses}

 

Puoi utilizzare il comando [git
update](http://git-scm.com/docs/git-update-index){: new_window} per modificare l'autorizzazione
di ciascuno script in eseguibile. Ad esempio, puoi immettere `git update --chmod=+x script.sh`.
{: tsResolve}
	
	
	
## Un'applicazione non può essere distribuita da DevOps Services a {{site.data.keyword.Bluemix_notm}}
{: #ts_devops_to_bm}

Potresti non riuscire ad eseguire il push della tua applicazione da IBM Bluemix DevOps Services a {{site.data.keyword.Bluemix_notm}} se il file `manifest.yml` non è presente nella tua applicazione.

 

Quando distribuisci un'applicazione da DevOps Services a {{site.data.keyword.Bluemix_notm}}, potrebbe essere visualizzato un messaggio di errore `Unable to detect a supported application type`.
{: tsSymptoms}

 

Questo problema potrebbe verificarsi perché DevOps Services richiede un file `manifest.yml` per distribuire un'applicazione a {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}

 

Per risolvere questo problema, devi creare un file `manifest.yml`. Per ulteriori informazioni su come creare un file `manifest.yml`,
vedi [Manifest
dell'applicazione](../manageapps/depapps.html#appmanifest){: new_window}.
{: tsResolve}	
	




## Impossibile distribuire le applicazioni Meteor
{: #ts_meteor}

Potresti non riuscire a distribuire un'applicazione Meteor a {{site.data.keyword.Bluemix_notm}} se
il pacchetto di build non è specificato correttamente.

 

Quando distribuisci un'applicazione Meteor a {{site.data.keyword.Bluemix_notm}}, potresti visualizzare il messaggio di errore `La
preparazione dell'applicazione non è riuscita e, pertanto, non ci sono istanze da visualizzare.`
{: tsSymptoms}


Questo problema si verifica perché non viene fornito alcun pacchetto di build integrato per le applicazioni Meteor. Devi utilizzare un pacchetto di build personalizzato.
{: tsCauses} 


 

Per utilizzare un pacchetto di build personalizzato per le applicazioni Meteor, usa uno dei seguenti metodi:
{: tsResolve}

  * Se distribuisci la tua applicazione utilizzando il file `manifest.yml`, specifica l'URL o il nome del pacchetto di build personalizzato usando l'opzione buildpack. Ad
                                    esempio:
  ```
  buildpack: https://github.com/Sing-Li/bluemix-bp-meteor 
  ```
  * Se distribuisci la tua applicazione dal prompt dei comandi, utilizza il comando `cf
push` e specifica il pacchetto di build personalizzato usando
l'opzione **-b**. Ad
                                    esempio:
    ```
	cf push nomeapplicazione -p app_path -b https://github.com/Sing-Li/bluemix-bp-meteor 
	```
	
  

    
## Il pulsante Distribuisci a {{site.data.keyword.Bluemix_notm}}
non distribuisce un'applicazione
{: #deploytobluemixbuttondoesntdeployanapp}

Se fai clic sul pulsante Distribuisci a {{site.data.keyword.Bluemix_notm}}
e rilevi che il repository Git non viene clonato o che l'applicazione
non viene distribuita, prova i metodi di risoluzione per i seguenti problemi.
  * [Impossibile creare il progetto Bluemix DevOps Services](#project-cannot-be-created)
  * [Il repository Git non viene trovato e non può essere clonato in DevOps Services](#repo-not-found)
  * [Il repository Git viene clonato in DevOps Services, ma l'applicazione non viene
distribuita a {{site.data.keyword.Bluemix_notm}}](#repo-cloned-app-not-deployed)
Per ulteriori informazioni su come creare il pulsante, vedi Creazione di un pulsante Distribuisci a {{site.data.keyword.Bluemix_notm}}.

### Impossibile creare il progetto Bluemix DevOps Services
{: #project-cannot-be-created}

Se noti che il progetto DevOps Services non può essere creato, il tuo account {{site.data.keyword.Bluemix_notm}} potrebbe essere scaduto.



Fai clic sul pulsante **Distribuisci a Bluemix**, ma il passo "Creazione del progetto" non viene completato correttamente.
{: tsSymptoms} 


Il tuo account {{site.data.keyword.Bluemix_notm}}
potrebbe essere scaduto.
{: tsCauses} 

Per risolvere il problema utilizza uno dei seguenti metodi:
{: tsResolve}

  * Accedi a {{site.data.keyword.Bluemix_notm}} e
aggiorna le informazioni del tuo account.
  * Fai di nuovo clic sul pulsante **Distribuisci a Bluemix**.


### Il repository Git non viene trovato e non può essere clonato in DevOps Services
{: #repo-not-found}

Se noti che il repository Git non viene clonato, potrebbe esistere
un problema con il repository o con il frammento di pulsante.



Fai clic sul pulsante **Distribuisci a Bluemix**, ma il repository Git non viene trovato e non può essere clonato in DevOps Services. Il passo "Clonazione del repository" non viene completato correttamente. Di conseguenza, l'applicazione non può essere distribuita a {{site.data.keyword.Bluemix_notm}}. 
{: tsSymptoms} 

Questo problema si verifica a causa dei seguenti motivi:
{: tsCauses} 

  * Il repository Git potrebbe non esistere o non essere accessibile.
  * Potrebbe esistere un problema nell'HTML o markdown per il frammento di pulsante.
  * Potrebbe esistere un problema in cui dei caratteri speciali, parametri di query
o frammenti nell'URL impediscono di accedere correttamente al repository
Git.

Per risolvere il problema utilizza uno dei seguenti metodi:
{: tsResolve}

  * Verifica che il repository Git esista e sia accessibile pubblicamente
e che l'URL sia corretto.
  * Verifica che il frammento non contenga errori di HTML o markdown.
  * Se caratteri speciali, parametri di query o frammenti causano problemi con l'URL del repository Git, codifica l'URL nel frammento di pulsante.
  

  
  
### Il repository Git viene clonato in DevOps Services, ma l'applicazione non viene distribuita a {{site.data.keyword.Bluemix_notm}}
{: #repo-cloned-app-not-deployed}

Se noti che l'applicazione non viene distribuita, potrebbero esistere
dei problemi con il codice nel repository.
     


Fai clic sul pulsante **Distribuisci a Bluemix** e il repository Git viene clonato in DevOps Services, ma l'applicazione non viene distribuita a {{site.data.keyword.Bluemix_notm}}. Il passo "Distribuzione a Bluemix" non viene completato correttamente.
{: tsSymptoms} 

Questo problema si verifica a causa dei seguenti motivi:
{: tsCauses}  

  * Nel tuo spazio {{site.data.keyword.Bluemix_notm}} potrebbe non esserci spazio sufficiente
per distribuire un'applicazione. 
  * Un servizio richiesto potrebbe non essere dichiarato nel file `manifest.yml`.
  * Un servizio richiesto potrebbe essere dichiarato nel file `manifest.yml`,
ma il servizio si trova già nello spazio di destinazione.
  * Potrebbe esistere un problema con il codice nel repository.
Per diagnosticare il problema, riesamina i log di creazione e distribuzione
dalla distribuzione:
  1. Quando il passo "Distribuzione a Bluemix" non viene completato correttamente, fai clic sul link nel precedente passo di "Configurazione della pipeline" per aprire Delivery Pipeline.
  2. Identifica la fase di creazione o distribuzione non riuscita.
  3. Nella fase non riuscita, fai clic su **Visualizza log e cronologia**.
  4. Individua il messaggio di errore.
   
Per risolvere il problema utilizza uno dei seguenti metodi:
{: tsResolve}

  * Se il messaggio di errore indica che nello
spazio {{site.data.keyword.Bluemix_notm}} non vi è spazio sufficiente
per distribuire l'applicazione, mira a un altro spazio.
  * Se il messaggio di errore indica che un servizio richiesto non è
dichiarato nel file `manifest.yml`, comunica al proprietario
del repository che è necessario aggiungere il servizio richiesto.
  * Se il messaggio di errore indica che un servizio richiesto esiste
già nello spazio di destinazione, seleziona un spazio differente da utilizzare.
  * Se il messaggio di errore indica che esiste un problema con la creazione,
correggi eventuali problemi con il codice che impediscono la creazione
dell'applicazione. Per verificare che il codice non contenga alcun problema, crea il
codice utilizzando i comandi Git:
    1. Clona il repository Git:
    ```
    git clone <URL_repository_git>
    ```
	2. Apri la directory dell'applicazione:
	```
	cd <nomeapplicazione>
	```
	3. Crea l'applicazione:
	```
	<nomeapplicazione> create
	```
	4. Se necessario, fornisci componenti aggiuntivi.
	5. Aggiungi eventuali variabili di configurazione richieste.
	6. Distribuisci il codice:
	```
	git push <nomeapplicazione> master
	```
	7. Verifica che l'applicazione venga creata correttamente.
	8. Se necessario, esegui il comando di post distribuzione:
	```
	<nomeapplicazione> run
	```
	9. Apri l'applicazione e verifica che funzioni correttamente:
	```
	<nomeapplicazione> open
	```
	



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

 

Per riattivare il tuo account, contatta il [Supporto {{site.data.keyword.Bluemix_notm}}](http://ibm.biz/bluemixsupport.com){: new_window}. Nell'email, devi includere le seguenti informazioni:
{: tsResolve}

  * L'ID IBM da te utilizzato per accedere a {{site.data.keyword.Bluemix_notm}}.
  * Il nome dell'organizzazione in cui verrà creata la tua applicazione. Queste informazioni consentono al team di supporto di determinare se ti sono stati assegnati i ruoli o l'appartenenza appropriati all'interno della tua organizzazione.



## Nessuno spazio associato all'organizzazione corrente
{: #ts_no_space}

Non puoi creare un'applicazione se non vi è alcuno spazio
associato alla tua organizzazione corrente.



Quando tenti di creare un'applicazione in {{site.data.keyword.Bluemix_notm}}, viene visualizzato il seguente messaggio di errore:
{: tsSymptoms} 


`BXNUI0097E: Prima di poter aggiungere un'applicazione, è necessario associare almeno uno spazio alla tua organizzazione e alla tua regione. Sul Dashboard, fai clic su **Crea uno spazio**. Una volta creato lo spazio, prova di nuovo. `



Le applicazioni in {{site.data.keyword.Bluemix_notm}} devono essere create all'interno di uno spazio nella tua organizzazione.
{: tsCauses} 

 

Per creare uno spazio, utilizza uno dei seguenti metodi: 
{: tsResolve}
 
  * Sul Dashboard {{site.data.keyword.Bluemix_notm}}, seleziona l'organizzazione in cui vuoi creare lo spazio e fai quindi clic su **Crea uno spazio**.
  * Nell'interfaccia riga di comando cf, immetti ```cf create-space <nome_spazio> -o <nome_organizzazione>```.
  
  
  
  
## Nomi di dominio uguali per applicazioni diverse
{: #ts_domain_diff}

Potresti notare che diverse applicazioni condividono lo stesso
URL in {{site.data.keyword.Bluemix_notm}}.

 

Questo problema potrebbe verificarsi quando assegni
la stessa rotta URL per applicazioni differenti all'interno di uno spazio.
{: tsCauses}

Ad esempio, esegui il push dell'applicazione myApp1 a {{site.data.keyword.Bluemix_notm}} e imposti il dominio su "mynewapp.mybluemix.net". Esegui quindi il push di un'altra applicazione myApp2 allo stesso spazio e imposti una delle sue rotte URL su "mynewapp.mybluemix.net". La rotta è ora associata a entrambe le applicazioni.

 

Questo è il funzionamento supportato da {{site.data.keyword.Bluemix_notm}} e
puoi utilizzare questa procedura affinché non si verifichino tempi di inattività
per l'aggiornamento della tua applicazione. Per ulteriori informazioni, vedi Distribuzioni Blue-Green.
{: tsResolve}
  
	
	





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





# Risoluzione dei problemi relativi ai runtime
{: #runtimes}

Potresti riscontrare dei problemi quando utilizzi i runtime IBM® Bluemix™. Tuttavia, in molti casi, puoi eseguire un ripristino da tali problemi seguendo pochi semplici passi.
{:shortdesc}


## Un pacchetto di build obsoleto viene caricato dalla cache quando viene eseguito il push di un'applicazione
{: #ts_loading_bp}


Potresti non essere in grado di utilizzare i componenti di pacchetti di build più recenti
quando esegui il push di un'applicazione. Puoi utilizzare i pacchetti di build che hanno dei meccanismi integrati
per impedire il caricamento di componenti obsoleti oppure puoi eliminare il contenuto nella
directory cache della tua applicazione prima di eseguire il push o di preparare di nuovo l'applicazione. 

 

Quando esegui il push o prepari di nuovo un'applicazione
dopo l'aggiornamento del pacchetto di build, i componenti del pacchetto di build più recenti non vengono
caricati automaticamente. Di conseguenza, la tua applicazione utilizza i componenti del pacchetto di build obsoleti. Gli aggiornamenti che
sono stati applicati al pacchetto di build dall'ultima volta che hai eseguito il push
dell'applicazione non vengono implementati. 
{: tsSymptoms}



Alcuni
pacchetti di build non sono configurati per scaricare automaticamente tutti
i componenti aggiornati da Internet per garantire che tu utilizzi sempre
la versione più recente.
{: tsCauses} 

 

Puoi utilizzare dei pacchetti di build che hanno dei meccanismi integrati per evitare il caricamento di componenti obsoleti. I seguenti pacchetti di build sono due esempi: 
{: tsResolve}

  * [Pacchetto di build Java Cloud Foundry](https://github.com/cloudfoundry/java-buildpack){: new_window}. Questo pacchetto di build ha un meccanismo integrato per garantire che venga utilizzata la versione più recente del pacchetto di build. Per ulteriori informazioni sulla modalità
di funzionamento di questo meccanismo, consulta [extending-caches.md](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window}. 
  * [Pacchetto di build Node.js Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}. Questo pacchetto di build ha una funzionalità simile all'utilizzo delle variabili di ambiente. Per abilitare il pacchetto di build Node.js a scaricare i modulo nodo da Internet ogni volta, immetti il
seguente comando nell'interfaccia riga di comando cf: 	
  ```
  set NODE_MODULES_CACHE=false
  ```
Se il pacchetto di build che stai utilizzando non fornisce un meccanismo per caricare i componenti più recenti in modo automatico, puoi eliminare manualmente il contento nella directory cache ed eseguire nuovamente il push della tua applicazione attenendoti alla seguente procedura:
  1. Estrai mediante checkout un ramo di un pacchetto di build null, ad esempio https://github.com/ryandotsmith/null-buildpack. Per informazioni su come estrarre mediante check-out un ramo, consulta [Git Basics - Getting a Git Repository](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window}.  
  2. Aggiungi la seguente riga al file `null-buildpack/bin/compile` ed esegui il commit delle modifiche. Per informazioni su come
eseguire il commit delle modifiche, consulta [Git Basics - Recording Changes to the Repository](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window}.
  ```
  rm -rfv $2/*
  ```
  3. Esegui il push della tua applicazione con il pacchetto di build null che è stato modificato per eliminare
la cache utilizzando il seguente comando. Dopo che hai completato questo passo, tutto il contenuto nella directory
cache della tua applicazione viene eliminato.
  ```
  cf push nomeapplicazione -p app_path -b <pacchetto_build_null_modificato>
  ```
  4. Esegui il push della tua applicazione con il pacchetto di build più recente che vuoi utilizzare servendoti del seguente comando: 
  ```
  cf push nomeapplicazione -p app_path -b <ultimo_pacchetto_build>
  ```
  
	


## Messaggi NOTICE dal pacchetto di build PHP
{: #ts_phplog}

Potresti visualizzare dei messaggi di log che contengono NOTICE. Puoi interrompere la registrazione di questi messaggi modificando il
livello di registrazione.	
	
 

Quando distribuisci un'applicazione a Bluemix utilizzando un pacchetto di build PHP, potresti visualizzare dei messaggi che contengono `NOTICE`:
{: tsSymptoms}

```
• 2015-01-26T15:00:59.70+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: fpm is running, pid 93
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: ready to handle connections
```



Nel pacchetto di build PHP, il parametro error_log è utilizzato per definire il livello di registrazione. Per impostazione predefinita, il valore del parametro `error_log`
è **stderr notice**. Il seguente esempio mostra la configurazione
del livello di registrazione predefinita nel file `nginx-defaults.conf`
del pacchetto di build PHP fornito da Cloud Foundry. Per ulteriori informazioni,
vedi [cloudfoundry/php-buildpack](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window}.
{: tsCauses} 

```
daemon off;
error_log stderr notice;
pid @{HOME}/nginx/logs/nginx.pid;
```

 	
	
I messaggi `NOTICE` sono informativi e non
indicano necessariamente che si è verificato un problema. Puoi interrompere la registrazione di questi messaggi modificando il livello di registrazione da stderr notice a stderr error nel file nginx-defaults.conf del tuo pacchetto di build. Ad
esempio: 	
{: tsResolve}

```
daemon off;
error_log stderr error;
pid @{HOME}/nginx/logs/nginx.pid;
```
Per ulteriori informazioni su come modificare la configurazione di registrazione
predefinita, vedi [error_log](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window}.
	

## Impossibile importare una libreria Python di terze parti in {{site.data.keyword.Bluemix_notm}}
{: #ts_importpylib}

Potresti non riuscire a importare una libreria Python di terze parti
in {{site.data.keyword.Bluemix_notm}}. Puoi risolvere il problema aggiungendo file di configurazione nella directory
root della tua applicazione Python.


Quando tenti di importare una libreria Python di terze parti, come
la libreria `web.py`, il comando `cf push`
non riesce.
{: tsSymptoms}


 

Questo problema si verifica quando mancano delle informazioni di configurazione
per l'applicazione Python.
{: tsCauses}


 

Per risolvere il problema, aggiungi un file `requirements.txt` e un file `Procfile` nella directory root della tua applicazione Python. Le seguenti informazioni presumono che tu stia importando la libreria web.py:
{: tsResolve}

  1. Aggiungi un file `requirements.txt` nella directory root della tua applicazione Python.
     Il file `requirements.txt`
specifica i pacchetti di libreria richiesti per la tua applicazione Python
e la versione dei pacchetti. Il seguente esempio mostra il contenuto del file `requirements.txt`, dove `web.py==0.37` indica
che la versione della libreria `web.py` che verrà scaricata è la 0.37 e `wsgiref==0.1.2` indica che la versione dell'interfaccia gateway del server Web richiesta dalla libreria web.py è la 0.1.2.
	 ```
	 web.py==0.37
     wsgiref==0.1.2
	 ```
	Per ulteriori informazioni su come configurare
il file `requirements.txt`, vedi [Requirements files](https://pip.readthedocs.org/en/1.1/requirements.html). 
	 
  2. Aggiungi un file `Procfile` nella directory root
della tua applicazione Python.
	Il file `Procfile`
deve contenere il comando di avvio per la tua applicazione Python. Nel seguente comando, *ilnomedellatuaapplicazione* è il nome della tua
applicazione Python e *PORT* è il numero di porta che l'applicazione Python dovrà utilizzare per ricevere le richieste dagli utenti
dell'applicazione. *$PORT* è facoltativo. Se non specifichi una PORTA nel comando di avvio, verrà utilizzato
il numero di porta indicato nella variabile di ambiente `VCAP_APP_PORT` che si trova all'interno dell'applicazione. 
	```
	web: python <ilnomedellatuaapplicazione>.py $PORT
	```
Adesso, puoi importare la libreria Python di terze parti
in {{site.data.keyword.Bluemix_notm}}.	



## Il pulsante Azioni nella pagina Dettagli istanza è disabilitato
{: #ts_actionsbutton}



Il pulsante Azioni nella pagina Dettagli istanza è disabilitato.
{: tsSymptoms} 

 

Questo problema si verifica a causa dei seguenti motivi:
{: tsCauses}

  * L'applicazione non è un'applicazione web Java™. RMU (Runtime Management Utilities) supporta solo le applicazioni
Web distribuite con i pacchetti di build Liberty.
  * L'applicazione non viene distribuita con il pacchetto di build Liberty integrato.
  * L'applicazione è stata distribuita con una versione precedente del pacchetto di build
Liberty.



Se il problema è causato da una versione precedente del pacchetto di build Liberty, ridistribuisci l'applicazione in {{site.data.keyword.Bluemix_notm}}. In caso contrario, puoi
fornire i seguenti file di log dell'applicazione client al team
di supporto:
{: tsResolve} 

  * logs/messages.log
  * logs/stdout.log
  * logs/stderr.log
  

  
  
## Credenziali richieste all'apertura della finestra di traccia o di dump
{: #ts_username}


 

Vengono richiesti un nome utente e una password quando si apre la finestra di traccia
e di dump.
{: tsSymptoms}

 

Questo problema si verifica a causa del timeout della sessione di accesso.
{: tsCauses}

 

La soluzione consiste nell'immettere nuovamente il nome utente e la password.
{: tsResolve}




## Si verifica un errore durante l'esecuzione delle operazioni di traccia o di dump
{: #ts_target}

 

Viene visualizzato un messaggio di errore mentre le operazioni di
traccia o di dump sono in esecuzione. Il messaggio indica che un'istanza di destinazione
per un'applicazione non si trova nello stato di In esecuzione:	
{: tsSymptoms}

```
Istanza 0: La specifica di traccia è stata impostata correttamente
Istanza 2: La specifica di traccia è stata impostata correttamente
Istanza 1: L'istanza di destinazione 1 per l'applicazione abcd non si trova nello stato di In esecuzione.
Istanza 3: La specifica di traccia è stata impostata correttamente
Istanza 4: La specifica di traccia è stata impostata correttamente
```



Questo problema si verifica a causa dei seguenti motivi:
{: tsCauses} 

  * Le capacità di gestione della traccia o del dump riguardano solo le istanze dell'applicazione
che sono in esecuzione. Le operazioni di traccia o di dump non possono essere utilizzate
su istanze dell'applicazione arrestate, in fase di avvio o bloccate.
  * Lo stato dell'istanza dell'applicazione cambia quando si apre la finestra di dialogo della traccia o
del dump. 
  


La soluzione consiste nel chiudere la finestra, e quindi
riaprirla.
{: tsResolve} 



## Le istanza hanno una configurazione traceSpecification differente
{: #ts_different_config}

 

Per diverse istanze di un'applicazione, potresti vedere una configurazione traceSpecification differente.
{: tsSymptoms}

 

Questo problema si verifica a causa dei seguenti motivi:
{: tsCauses}

  * Potresti aver modificato la configurazione per una o più istanze, precedentemente. Se modifichi la configurazione traceSpecification per una istanza, essa non si applica ad altre istanze della stessa applicazione. Ad esempio, la tua applicazione utilizza log4j e hai 2 istanze per questa applicazione. Puoi modificare il livello di log dell'istanza 0 da info a debug ma il livello di log dell'istanza 1 rimane info. 
  * Viene eseguito un ridimensionamento incrementale dell'applicazione, che presenta delle nuove istanze. RMU non applica la configurazione traceSpecification dell'istanza esistente alla nuova istanza di cui è stato eseguito il ridimensionamento incrementale. La nuova istanza utilizza la configurazione predefinita. Ad esempio, la tua applicazione utilizza log4j e ha una istanza. Puoi modificare il livello di log di questa istanza da info a debug. Dopo che hai apportato questo modifica, se esegui il ridimensionamento incrementale della tua applicazione in due istanze, il livello di log della nuova istanza è info, invece di debug.
  


Questo è il comportamento previsto.
{: tsResolve} 





## Quota disco superata
{: #ts_diskquota}

Nel log dell'applicazione, potresti notare che la quota del disco è stata superata.

 

Nel log della tua applicazione vedi il messaggio di errore `Disk quota exceeded`.
{: tsSymptoms}



Questo problema è causato da uno dei seguenti motivi: 
{: tsCauses} 

  * I file di dump vengono generati con le istanze dell'applicazione in esecuzione
e i file utilizzano la quota di disco assegnata. Per impostazione predefinita, la quota del disco
per un'istanza dell'applicazione è di 1 GB. Puoi controllare l'utilizzo del
disco facendo clic su **Dashboard>Applicazione>Runtime applicazione**. Il seguente esempio mostra le informazioni di runtime,
incluso l'utilizzo del disco, per due istanze di un'applicazione:
    ```
    Instance	State	CPU	Memory Usage	Disk Usage

	0		Running	1.0%	344.8MB/512MB	236.8MB/1GB
	2		Running	2.3%	361.2MB/512MB	235.7MB/1GB
    ```
  * La quota del disco è limitata dalla quota dell'organizzazione corrente.
  
  


Puoi risolvere il problema utilizzando uno dei seguenti
metodi:
{: tsResolve} 

  * Elimina i file di dump dopo averli scaricati.
  * Ridistribuisci l'applicazione con una quota di disco maggiore includendo
la seguente voce nel manifest di distribuzione:
    ```
	disk_quota: 2048
	```
	
	


