---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-3-16"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 





# Risoluzione dei problemi relativi alla gestione delle applicazioni
{: #managingapps}


I problemi generali con la gestione delle applicazioni potrebbero includere applicazioni che non possono essere aggiornate o caratteri double-byte che non vengono visualizzati. In molti casi, puoi risolvere questi problemi seguendo pochi semplici passi.
{:shortdesc}


## Impossibile attivare la modalità di debug nelle applicazioni
{: #ts_debug}

Potresti non essere in grado di abilitare la modalità di debug se la versione della JVM (Java virtual machine) è 8 o precedente. 

Dopo aver selezionato **Enable application debug**, gli strumenti tentano di attivare la modalità di debug nell'applicazione. Quindi, il workbench di Eclipse avvia una sessione di debug. Quando gli strumenti hanno abilitato correttamente la modalità di debug, lo stato dell'applicazione web visualizza `Updating mode`, `Developing` e `Debugging`. 
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
 
Le seguenti versioni della JVM (Java virtual machine) non riescono a stabilire una sessione di debug: IBM JVM 7, IBM JVM 8 e versioni precedenti di Oracle JVM 8.
{: tsCauses}

Se la tua JVM del workbench è di una di queste versioni, potresti avere problemi durante la creazione di una sessione di debug. La versione JVM del workbench è normalmente la JVM di sistema del tuo computer locale. La tua JVM di sistema non è uguale a quella della tua applicazione  Java&trade; {{site.data.keyword.Bluemix_notm}} in esecuzione. L'applicazione Java {{site.data.keyword.Bluemix_notm}} viene quasi sempre eseguita sulla JVM IBM e alcune volte sulla JVM OpenJDK.
  
Per controllare la versione di Java eseguita da {{site.data.keyword.eclipsetoolsfull}}, completa la seguente procedura:
{: tsResolve}

  1. In IBM Eclipse Tools for Bluemix, seleziona **Guida** > **Informazioni su Eclipse** > **Dettagli dell'installazione** > **Configurazione**.
  2. Trova la proprietà `eclipse.vm` dall'elenco. La seguente linea è un esempio di una proprietà `eclipse.vm`:
	
	```
	eclipse.vm=C:\Program Files\IBM\ibm-java-sdk-80-win-x86_64\bin\..\jre\bin\j9vm\jvm.dll
	```

  3. Nella riga di comando, immetti `java -version` dalla directory `bin` della tua installazione Java. Vengono visualizzate le informazioni sulla tua versione Java IBM.

Se il JVM workbench JVM è IBM JVM 7 o 8 o una versione precedente di Oracle JVM 8, completa la seguente procedura per passare a Oracle JVM 8:

  1. Scarica e installa Oracle JVM 8; per i dettagli consulta [Java SE Downloads ![icona link esterno](../icons/launch-glyph.svg "External link icon")](http://www.oracle.com/technetwork/java/javase/downloads/index.html){: new_window}.
  2. Riavvia Eclipse.
  3. Controlla se la proprietà `eclipse.vm` punta alla tua nuova installazione di Oracle JVM 8.

  
## Impossibile riutilizzare i nomi di applicazioni eliminate
{: #ts_reuse_appname}
  
Dopo aver eliminato un'applicazione, puoi riutilizzarne il nome solo dopo aver eliminato la rotta dell'applicazione. 

Quando tenti di riutilizzare il nome applicazione, ricevi il seguente messaggio:
{: tsSymptoms}

`Il nome è già utilizzato da un'altra applicazione.`

Quando si elimina un'applicazione, la sua rotta, ossia l'URL dell'applicazione, non viene eliminata automaticamente. Pertanto, non è disponibile per il riutilizzo. Per poterlo riutilizzare, devi accedere allo spazio in cui è stata creata l'applicazione per eliminare la rotta.
{: tsCauses}

Per eliminare la rotta non utilizzata, completa la seguente procedura: 
{: tsResolve}

  1. Controlla se la rotta appartiene allo spazio corrente immettendo il seguente comando: 
     ```
	 cf routes
	 ```
  2. Se la rotta non appartiene allo spazio corrente, passa allo spazio o all'organizzazione a cui appartiene immettendo il seguente comando: 
     ```
	 cf target -o org_name -s space_name
	 ```
  3. Elimina la rotta dell'applicazione immettendo il seguente comando:
     ```
	 cf delete-route domain_name -n host_name
	 ```
	 Ad
esempio:
	 ```
	 cf delete-route mybluemix.net -n app001
	 ```

## Impossibile richiamare gli spazi in un'organizzazione
{: #ts_retrieve_space}

Non puoi creare un'applicazione o un servizio se alla tua organizzazione corrente non è associato alcuno spazio.

Quando tenti di creare un'applicazione in Bluemix, viene visualizzato il seguente messaggio di errore:
{: tsSymptoms}

`BXNUI0515E: Gli spazi nell'organizzazione non sono stati recuperati. Si è verificato un problema di rete oppure la tua organizzazione corrente non dispone di uno spazio associato ad essa.`

Questo errore si verifica spesso la prima volta che si tenta di creare un'applicazione o un servizio dal Catalogo quando ancora non è stato creato uno spazio. 
{: tsCauses}

Assicurati di aver creato uno spazio nella tua organizzazione corrente. Per creare uno spazio, utilizza uno dei seguenti metodi:
{: tsResolve}

  * Dalla barra dei menu, fai clic su **Account** &gt; **Gestisci organizzazioni.** Seleziona l'organizzazione in cui vuoi creare lo spazio e fai clic su **Crea uno spazio**.
  * Nell'interfaccia riga di comando cf, immetti `cf create-space <nome_spazio>
-o <nome_organizzazione>`.

Riprova. Se visualizzi di nuovo questo messaggio, vai alla pagina sugli [stati Bluemix ![icona link esterno](../icons/launch-glyph.svg "External link icon")](http://ibm.biz/bluemixstatus){: new_window} per controllare se un servizio o un componente ha qualche problema.


## Impossibile effettuare le azioni richieste
{: #ts_authority}

Potresti non riuscire a completare delle azioni senza un'appropriata autorità di accesso.

Quando tenti di eseguire azioni per un'istanza del servizio o un'istanza dell'applicazione, non riesci a completare le azioni richieste e visualizzai uno dei seguenti messaggi di errore: 
{: tsSymptoms}

`BXNUI0514E: You are not a developer for any of the spaces in the <orgName> organization.`

`Server error, status code: 403, error code: 10003, message: You are not authorized to perform the requested action.`

Non disponi del livello di autorità adeguato per eseguire le azioni. 
{: tsCauses}

Per ottenere il livello di autorità appropriato, utilizza uno dei seguenti metodi: 
{: tsResolve}
 * Seleziona un'altra organizzazione e uno spazio per cui disponi del ruolo di sviluppatore. 
 * Chiedi al gestore organizzazione di modificare il tuo ruolo in sviluppatore oppure di creare uno spazio e assegnarti quindi un ruolo sviluppatore. Consulta [Gestione di organizzazioni e spazi](/docs/admin/orgs_spaces.html) per i dettagli.
 
## Impossibile accedere ai servizi {{site.data.keyword.Bluemix_notm}} a causa di errori di autorizzazione
{: #ts_vcap}

Gli errori di autorizzazione potrebbero verificarsi quando la tua applicazione accede a un servizio {{site.data.keyword.Bluemix_notm}} e le credenziali del servizio sono hardcoded nell'applicazione. 

Dopo aver configurato l'applicazione per comunicare con un servizio {{site.data.keyword.Bluemix_notm}}, distribuisci l'applicazione a {{site.data.keyword.Bluemix_notm}}. Tuttavia, non riesci a utilizzare l'applicazione per accedere al servizio {{site.data.keyword.Bluemix_notm}} e ricevi un messaggio di errore.
{: tsSymptoms}

Le credenziali hardcoded nell'applicazione potrebbero non essere corrette. Ogni volta che il servizio viene ricreato, le credenziali per accedervi cambiano.
{: tsCauses}

Invece di impostare come hardcoded le credenziali nella tua applicazione, utilizza i parametri di connessione dalla variabile di ambiente VCAP_SERVICES. I metodi per utilizzare i parametri di connessione dalla variabile di ambiente VCAP_SERVICES variano a seconda dei linguaggi di programmazione. Ad esempio, per le applicazioni Node.js, puoi utilizzare il seguente comando: 
{: tsResolve}

```
process.env.VCAP_SERVICES
```
Per ulteriori informazioni sui comandi che puoi utilizzare in altri linguaggi di programmazione, vedi [Java ![icona link esterno](../icons/launch-glyph.svg "External link icon")](http://docs.run.pivotal.io/buildpacks/java/java-tips.html#env-var){: new_window} e [Ruby ![icona link esterno](../icons/launch-glyph.svg "External link icon")](http://docs.run.pivotal.io/buildpacks/ruby/ruby-tips.html#env-var){: new_window}. 
 

## Impossibile distribuire le applicazioni utilizzando IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}
{: #ts_bm_tools_facet}

Quando al tuo progetto Eclipse viene applicato un facet non supportato, potresti non essere in grado di distribuire le
tue applicazioni a {{site.data.keyword.Bluemix_notm}} utilizzando IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}. 

Puoi distribuire correttamente la tua applicazione a {{site.data.keyword.Bluemix_notm}} utilizzando la CLI Cloud Foundry. Tuttavia, non puoi distribuire l'applicazione a {{site.data.keyword.Bluemix_notm}} utilizzando IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} e vedi il messaggio di errore: `Project facet <facet_name> is not supported.` Per esempio:
{: tsSymptoms}
`Project facet Cloud Foundry Standalone Application version 1.0 is not supported.`

IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} associa i progetti ai runtime {{site.data.keyword.Bluemix_notm}} in base ai facet di progetto. I facet definiscono i requisiti per i progetti Java EE in Eclipse e sono utilizzati come parte della configurazione di runtime, in modo che runtime differenti siano associati a progetti differenti. Se il facet applicato al progetto non è supportato da IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, potresti non essere in grado di distribuire la tua applicazione utilizzando IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
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
ospita il sito. Il server principale e il server proxy potrebbero non connettersi correttamente, pertanto visualizzi il codice di stato HTTP 502 nella finestra del browser. Questo codice di stato indica che il server principale del sito non ha ricevuto l'implementazione HTTP prevista dal server proxy.
{: tsCauses}

Altre cause meno comuni di un errore Bad Gateway sono
interruzioni ISP (Internet Service Provider), configurazioni firewall non valide ed
errori della cache del browser. 

Se sospetti che un servizio {{site.data.keyword.Bluemix_notm}} sia inattivo, controlla prima la pagina [Stato di {{site.data.keyword.Bluemix_notm}} ![icona link esterno](../icons/launch-glyph.svg "External link icon")](http://ibm.biz/bluemixstatus){: new_window}. Una soluzione potrebbe essere quella di utilizzare il servizio in un'altra regione {{site.data.keyword.Bluemix_notm}}. Informazioni dettagliate sono disponibili in [Utilizzo dei servizi in un'altra regione ![icona link esterno](../icons/launch-glyph.svg "External link icon")](/docs/services/reqnsi.html#cross_region_service){: new_window}. Se lo stato del servizio è normale,
prova le seguenti operazioni per risolvere il problema: 
{: tsResolve}

  * Ritenta l'azione:
    * Ricarica la pagina premendo F5 sulla tastiera o facendo clic sul
pulsante di aggiornamento. Se questa operazione non funziona, cancella la cache e i cookie del tuo browser e ricarica di nuovo la pagina.
    * Utilizza un browser differente.
    * Riavvia il router, il modem e il computer. Il riavvio di questi
dispositivi può cancellare i diversi errori che portano all'errore 502. 
  * Attendi e riprova in seguito. In alcuni casi, possono verificarsi dei
problemi temporanei con il tuo provider dei servizi Internet o con i servizi {{site.data.keyword.Bluemix_notm}}. Puoi attendere finché i problemi non vengono risolti.
  * Se il problema persiste, contatta il supporto {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni, vedi [Come contattare il supporto {{site.data.keyword.Bluemix_notm}} ![icona link esterno](../icons/launch-glyph.svg "External link icon")](/docs/support/index.html#contacting-bluemix-support){: new_window}. 

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
sufficiente, prova un servizio esterno come [Object Store](/docs/services/ObjectStorage/index.html).
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


## Le applicazioni Android non possono ricevere {{site.data.keyword.mobilepushshort}}
{: #ts_push}

In alcune regioni in cui Google non è accessibile, le applicazioni Android non possono ricevere le notifiche che invii tramite il servizio IBM {{site.data.keyword.mobilepushshort}}. In questo caso, una soluzione potrebbe consistere nell'utilizzare servizi di terze parti.

Esegui il bind di un servizio {{site.data.keyword.mobilepushshort}} per la tua applicazione Bluemix e invii un messaggio ai dispositivi registrati. Tuttavia, le applicazioni
sviluppate sulla piattaforma Android non possono ricevere le tue notifiche
in determinate regioni. 
{: tsSymptoms}

Il servizio IBM {{site.data.keyword.mobilepushshort}} utilizza il servizio GCM (Google Cloud Messaging) per inviare notifiche alle applicazioni mobili sviluppate sulla piattaforma Android. Per consentire alle applicazioni Android di ricevere le notifiche,
è necessario che il servizio GCM (Google Cloud Messaging) sia accessibile dalle applicazioni
mobili. Nelle regioni in cui le applicazioni Android non possono raggiungere il servizio GCM, tali applicazioni non potranno ricevere {{site.data.keyword.mobilepushshort}}.
{: tsCauses}

Come soluzione temporanea, utilizza servizi di terze parti che non si basano sul servizio GCM, ad esempio [Pushy ![icona link esterno](../icons/launch-glyph.svg "External link icon")](https://pushy.me){: new_window}, [igetui ![icona link esterno](../icons/launch-glyph.svg "External link icon")](http://www.getui.com/){: new_window} e [jpush ![icona link esterno](../icons/launch-glyph.svg "External link icon")](https://www.jpush.cn/){: new_window}.
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

Elimina tutte le istanze dei servizi che non sono necessarie o rimuovi il limite per il numero di istanze del servizio che puoi avere.
{: tsResolve}
 
  * Per eliminare un'istanza dei servizi, puoi utilizzare la console {{site.data.keyword.Bluemix_notm}} o l'interfaccia riga di comando.
    Per utilizzare la console {{site.data.keyword.Bluemix_notm}} per eliminare un'istanza del servizio, completa la seguente procedura:
	  1. Nel Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sul servizio che vuoi eliminare.  Il servizio viene visualizzato.
	  2. Nella scheda del servizio, fai clic sull'icona **Menu**.
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
converti il tuo account di prova in un account a pagamento. Per informazioni su come convertire il tuo account di prova in un account a pagamento, vedi [Come modificare il tuo piano](/docs/pricing/index.html#changing).

  
## Impossibile eseguire gli eseguibili su {{site.data.keyword.Bluemix_notm}}
{: #ts_executable}

Potresti non riuscire ad eseguire gli eseguibili su {{site.data.keyword.Bluemix_notm}} se
tali eseguibili sono stati sviluppati e creati in un ambiente diverso. 

Non puoi eseguire gli eseguibili su {{site.data.keyword.Bluemix_notm}} se questi eseguibili sono stati sviluppati e creati in un ambiente diverso.
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
cf push appname -p app_path -c <comando_di_avvio> -b <pacchetto_di_build-null>
```
Per esempio:
```
cf push appname -p app_path -c ./RunMeNow -b https://github.com/ryandotsmith/null-buildpack
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
accounts](/docs/pricing/index.html#pay-accounts). 
  * Per ridurre la memoria utilizzata dalle tue applicazioni, utilizza la console {{site.data.keyword.Bluemix_notm}} o l'interfaccia riga di comando cf.
  
    Se utilizzi la console {{site.data.keyword.Bluemix_notm}}, completa la seguente procedura:
    
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
	  cf push appname -p percorso_applicazione -i numero_istanza -m limite_memoria
      ```
	
    3. Riavvia la tua applicazione per rendere effettive le modifiche.
  
    	  
## Le applicazioni non si riavviano automaticamente
{: #ts_apps_not_auto_restarted}

Un'applicazione non si riavvia automaticamente se un servizio che associ mediante bind all'applicazione smette di funzionare.	  

Quando un servizio che associ mediante bind a un'applicazione viene arrestato in modo anomalo, nell'applicazione potrebbero verificarsi dei problemi come interruzioni, eccezioni ed errori di connessione. {{site.data.keyword.Bluemix_notm}} non riavvia automaticamente l'applicazione per eseguire un ripristino da tali problemi. {: tsSymptoms}

Questo è il funzionamento progettato da Cloud Foundry.
{: tsCauses} 

Puoi riavviare manualmente l'applicazione immettendo il seguente comando nell'interfaccia riga di comando:
{: tsResolve}

```
cf push appname -p percorso_applicazione
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


## Le icone di {{site.data.keyword.Bluemix_notm}} Live Sync non vengono visualizzate
{: #ts_llz_lkb_3r}

Hai creato un'applicazione ma le icone IBM Bluemix Live Sync non sono visualizzate nel Web IDE. 

Quando modifichi un'applicazione Node.js iin Web IDE, le icone di le icone di live edit, riavvio rapido e debug di {{site.data.keyword.Bluemix_notm}} non vengono visualizzate.
{: tsSymptoms}

Le icone non sono disponibili nei seguenti casi:
{: tsCauses}

  * Il file `manifest.yml` non è memorizzato al livello superiore del tuo progetto.
  * La tua applicazione è memorizzata in una sottodirectory anziché al livello superiore del tuo progetto, ma il percorso della sottodirectory non è specificato nel file `manifest.yml`.
  * L'applicazione non contiene un file `package.json`.

Utilizza uno dei seguenti metodi: 
{: tsResolve} 

  * Se il file `manifest.yml` non è memorizzato al livello superiore del tuo progetto, memorizzalo lì.
  * Se la tua applicazione è memorizzata in una sottodirectory, specifica il percorso
di tale sottodirectory nel file `manifest.yml`.
  ```
   path: percorso_alla_applicazione
   ```
  * Crea un file `package.json` che si trovi nella stessa
directory della tua applicazione.   
  
  
## Impossibile trovare le organizzazioni in {{site.data.keyword.Bluemix_notm}}
{: #ts_orgs}

Potresti non riuscire a individuare la tua organizzazione in {{site.data.keyword.Bluemix_notm}} quando
lavori su una regione {{site.data.keyword.Bluemix_notm}}.

Riesci ad accedere correttamente alla console {{site.data.keyword.Bluemix_notm}}, ma non puoi distribuire le applicazioni utilizzando l'interfaccia riga di comando cf o il plug-in Eclipse.
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

Questo problema si verifica poiché l'endpoint API della regione che vuoi utilizzare non è specificato e l'organizzazione che stai cercando potrebbe trovarsi in una regione differente.
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
cui è stata creata la tua organizzazione. Per ulteriori informazioni sull'utilizzo di strumenti Eclipse, consulta il documento relativo alla [distribuzione di applicazioni con IBM Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html).  
  
## Impossibile creare rotte di applicazione
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
    host: nome_host	
	```
  * Se distribuisci la tua applicazione dal prompt dei comandi, utilizza il comando `cf
push` con l'opzione **-n**. 
    ```
    cf push appname -p percorso_applicazione -n nome_host
    ```


## Non è possibile distribuire delle applicazioni WAR utilizzando il comando cf push
{: #ts_cf_war}

Potresti non riuscire a utilizzare il comando cf push per distribuire un'applicazione web archiviata a {{site.data.keyword.Bluemix_notm}} se la posizione dell'applicazione non è specificata correttamente.

Quando carichi un'applicazione WAR in {{site.data.keyword.Bluemix_notm}} utilizzando il comando `cf push`, vedi il seguente messaggio di errore:
{: tsSymptoms} 
`Staging error: cannot get instances since staging failed.`
 
Questo problema potrebbe verificarsi se non si specifica il file WAR o il percorso del file WAR. 
{: tsCauses}
	
Utilizza l'opzione **-p** per specificare
un file WAR o aggiungere il percorso del file WAR. Per esempio:
{: tsResolve}

```
cf push nomeunivocodellamiaapplicazione01 -p app.war
```

```
cf push MyUniqueAppName02 -p "./app.war"
```
Per ulteriori informazioni sul comando `cf push` , immettere `cf push -h`. 	


## I caratteri double-byte non vengono visualizzati correttamente quando si distribuiscono le applicazioni Liberty a {{site.data.keyword.Bluemix_notm}}
{: #ts_doublebytes}

I caratteri double-byte potrebbero non essere visualizzati correttamente se il supporto Unicode non è adeguatamente configurato per i file servlet o JSP.

Quando un'applicazione Liberty viene distribuita a {{site.data.keyword.Bluemix_notm}}, i caratteri double-byte specificati all'interno dell'applicazione non vengono visualizzati correttamente.
{: tsSymptoms}

Il problema può verificarsi se il supporto Unicode non è configurato correttamente per i file servlet o JSP.
{: tsCauses}

Puoi utilizzare il seguente codice nel tuo file servlet o JSP:
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

Potresti riscontrare dei problemi quando aggiorni un'applicazione Node.js o la distribuisci a {{site.data.keyword.Bluemix_notm}}.

Quando aggiorni un'applicazione Node.js o distribuisci la tua applicazione Node.js
a {{site.data.keyword.Bluemix_notm}},
potresti visualizzare uno dei seguenti messaggi di errore:
{: tsSymptoms} 

`An app was not successfully detected by any available buildpack.`

`Instance (index 0) failed to start accepting connections.`

`Cannot get instances since staging failed.`

Di seguito sono riportate le cause possibili:
{: tsCauses}
 
  * Il comando di avvio non è specificato.
  * I file richiesti per distribuire un'applicazione Node.js non sono presenti nell'applicazione o si trovano in una cartella diversa dalla directory root.
	
Utilizza uno dei seguenti metodi in base alla causa del problema:
{: tsResolve} 

  * Specifica il comando di avvio utilizzando uno dei seguenti metodi: 
     * Utilizza l'interfaccia riga di comando cf. Per esempio: 
        ```
		cf push MyUniqueNodejs01 -p app_path -c "node app.js"
		```
    * Utilizza il file [package.json ![icona link esterno](../icons/launch-glyph.svg "External link icon")](https://docs.npmjs.com/json){: new_window}. Per esempio:
	    ```
		{
      ...
  	   "scripts": {
	 		 "start": "node app.js"
 	   }
	}
	    ```
    * Utilizza il file `manifest.yml`. Per esempio: 
	    ```
		applications:
  name: MyUniqueNodejs01
  ...
  command: node app.js
  ...
        ```

  * Assicurati che nella tua applicazione Node.js sia presente un file  `package.json` in modo che il pacchetto di build Node.js possa riconoscere l'applicazione. Assicurati inoltre che questo file si trovi nella directory root della tua applicazione.	
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
	
Per ulteriori suggerimenti relativi alle applicazioni Node.js, vedi [Tips for Node.js Applications](http://docs.cloudfoundry.org/buildpacks/node/node-tips.html ![External link icon](../icons/launch-glyph.svg "icona link esterno"){: new_window}.	


## Sono presenti degli errori di configurazione nel file `server.xml` dopo che importi un'applicazione {{site.data.keyword.Bluemix_notm}} Liberty in Eclipse
{: #ts_eclipse}

Se vedi degli errori di configurazione nel file `server.xml` dopo aver importato un'applicazione {{site.data.keyword.Bluemix_notm}} Liberty in Eclipse, potresti dover rimuovere il file `server.xml` dal progetto. 

Dopo aver importato un'applicazione {{site.data.keyword.Bluemix_notm}} Liberty in Eclipse, vedi degli errori di configurazione nel file `server.xml` dalla vista Problemi di Eclipse.
{: tsSymptoms}

Il pacchetto di build Liberty utilizza il file `server.xml` per configurare l'applicazione e genera un file `runtime-vars.xml` quando viene eseguito il push dell'applicazione Liberty a {{site.data.keyword.Bluemix_notm}}. Quando importi l'applicazione in Eclipse, il file `runtime-vars.xml` non esiste nel tuo ambiente locale.
{: tsCauses}

Puoi risolvere questo problema rimuovendo il file server.xml dal progetto. Il pacchetto di build crea il file `server.xml` dinamicamente quando
esegui il push dell'applicazione come un'applicazione WAR. Per ulteriori informazioni, vedi [Liberty for Java](/docs/runtimes/liberty/index.html).
{: tsResolve}
	
	
## Impossibile preparare l'applicazione utilizzando i pacchetti di build personalizzati
{: #ts_bp_compilation}

Potresti non riuscire a distribuire un'applicazione a {{site.data.keyword.Bluemix_notm}} utilizzando un pacchetto di build personalizzato se gli script in questo pacchetto non sono eseguibili.

Quando distribuisci un'applicazione a {{site.data.keyword.Bluemix_notm}} utilizzando un pacchetto di build personalizzato, visualizzi il messaggio di errore `La preparazione  dell'applicazione non è riuscita e, pertanto, non ci sono istanze da visualizzare.`
{: tsSymptoms} 

Questo problema potrebbe verificarsi se gli script, ad esempio lo script di rilevamento, lo script di compilazione e lo script di rilascio, non sono eseguibili.
{: tsCauses}

Puoi utilizzare il comando [git update ![icona link esterno](../icons/launch-glyph.svg "External link icon")](http://git-scm.com/docs/git-update-index){: new_window} per modificare l'autorizzazione di ciascuno script in eseguibile. Ad esempio, puoi immettere `git update --chmod=+x script.sh`.
{: tsResolve}
	
	
## Non è possibile distribuire un'applicazione da DevOps Services a {{site.data.keyword.Bluemix_notm}}
{: #ts_devops_to_bm}

Potresti non riuscire a distribuire la tua applicazione da IBM Bluemix DevOps Services a {{site.data.keyword.Bluemix_notm}} se il file `manifest.yml` non è presente nella tua applicazione.

Quando distribuisci un'applicazione da DevOps Services a {{site.data.keyword.Bluemix_notm}}, potrebbe essere visualizzato un messaggio di errore `Unable to detect a supported application type`.
{: tsSymptoms}

Questo problema potrebbe verificarsi perché DevOps Services richiede un file `manifest.yml` per distribuire un'applicazione a {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}

Per risolvere questo problema, devi creare un file `manifest.yml`. Per ulteriori informazioni su come creare un file `manifest.yml`,
vedi [Manifest
dell'applicazione](/docs/manageapps/depapps.html#appmanifest).
{: tsResolve}	


## Impossibile distribuire le applicazioni Meteor
{: #ts_meteor}

Potresti non riuscire a distribuire un'applicazione Meteor a {{site.data.keyword.Bluemix_notm}} se il pacchetto di build non è specificato correttamente.

Quando distribuisci un'applicazione Meteor a {{site.data.keyword.Bluemix_notm}}, potresti visualizzare il messaggio di errore `La
preparazione dell'applicazione non è riuscita e, pertanto, non ci sono istanze da visualizzare.`
{: tsSymptoms}

Questo problema si verifica perché non viene fornito alcun pacchetto di build integrato per le applicazioni Meteor. Devi utilizzare un pacchetto di build personalizzato.
{: tsCauses} 

Per utilizzare un pacchetto di build personalizzato per le applicazioni Meteor, usa uno dei seguenti metodi:
{: tsResolve}

  * Se distribuisci la tua applicazione utilizzando il file `manifest.yml`, specifica l'URL o il nome del pacchetto di build personalizzato usando l'opzione buildpack. Per esempio:
  ```
  buildpack: https://github.com/Sing-Li/bluemix-bp-meteor 
  ```
  * Se distribuisci la tua applicazione dal prompt dei comandi, utilizza il comando `cf
push` e specifica il pacchetto di build personalizzato usando
l'opzione **-b**. Per esempio:
    ```
	cf push nomeapplicazione -p app_path -b https://github.com/Sing-Li/bluemix-bp-meteor 
	```
    
## Il pulsante Distribuisci a {{site.data.keyword.Bluemix_notm}}
non distribuisce un'applicazione
{: #ts_deploybutton}

Se fai clic sul pulsante Distribuisci a {{site.data.keyword.Bluemix_notm}} e rilevi che il repository Git non viene clonato o che l'applicazione non viene distribuita, prova i metodi di risoluzione per i seguenti problemi.
  * [Impossibile creare il progetto Bluemix DevOps Services](#ts_project-cant-be-created)
  * [Il repository Git non viene trovato e non può essere clonato in DevOps Services](#ts_repo-not-found)
  * [Il repository Git viene clonato in DevOps Services, ma l'applicazione non viene distribuita a {{site.data.keyword.Bluemix_notm}}](#ts_repo-cloned-app-not-deployed)

Per ulteriori informazioni su come creare il pulsante, vedi Creazione di un pulsante Distribuisci a {{site.data.keyword.Bluemix_notm}}.

### Impossibile creare il progetto Bluemix DevOps Services
{: #ts_project-cant-be-created}

Se non è possibile creare il progetto DevOps Services, il tuo account IBM {{site.data.keyword.Bluemix_notm}} potrebbe essere scaduto.

Fai clic sul pulsante **Distribuisci a Bluemix**, ma il passo "Creazione del progetto" non viene completato correttamente.
{: tsSymptoms} 

Il tuo account {{site.data.keyword.Bluemix_notm}}
potrebbe essere scaduto.
{: tsCauses} 

Utilizza uno dei seguenti metodi:
{: tsResolve}

  * Accedi a {{site.data.keyword.Bluemix_notm}} e
aggiorna le informazioni del tuo account.
  * Fai di nuovo clic sul pulsante **Distribuisci a Bluemix**.

### Il repository Git non viene trovato e non può essere clonato in DevOps Services
{: #ts_repo-not-found}

Se noti che il repository Git non viene clonato, potrebbe esistere un problema con il repository o con il frammento di pulsante.

Fai clic sul pulsante **Distribuisci a Bluemix**, ma il repository Git non viene trovato e non può essere clonato in DevOps Services. Il passo "Clonazione del repository" non viene completato correttamente. Di conseguenza, l'applicazione non può essere distribuita a {{site.data.keyword.Bluemix_notm}}. 
{: tsSymptoms} 

Questo problema si verifica per i seguenti motivi:
{: tsCauses} 

  * Il repository Git potrebbe non esistere o non essere accessibile.
  * Potrebbe esistere un problema nell'HTML o markdown per il frammento di pulsante.
  * Potrebbe esistere un problema in cui dei caratteri speciali, parametri di query
o frammenti nell'URL impediscono di accedere correttamente al repository
Git.

Utilizza uno dei seguenti metodi:
{: tsResolve}

  * Verifica che il repository Git esista e sia accessibile pubblicamente
e che l'URL sia corretto.
  * Verifica che il frammento non contenga errori di HTML o markdown.
  * Se caratteri speciali, parametri di query o frammenti causano problemi con l'URL del repository Git, codifica l'URL nel frammento di pulsante.
  
### Il repository Git viene clonato in DevOps Services, ma l'applicazione non viene distribuita a {{site.data.keyword.Bluemix_notm}}
{: #ts_repo-cloned-app-not-deployed}

Se l'applicazione non viene distribuita, potrebbero esistere dei problemi con il codice nel repository.

Fai clic sul pulsante **Distribuisci a Bluemix** e il repository Git viene clonato in DevOps Services, ma l'applicazione non viene distribuita a {{site.data.keyword.Bluemix_notm}}. Il passo "Distribuzione a Bluemix" non viene completato correttamente.
{: tsSymptoms} 

Questo problema si verifica per i seguenti motivi:
{: tsCauses}  

  * Nel tuo spazio {{site.data.keyword.Bluemix_notm}} potrebbe non esserci spazio sufficiente
per distribuire un'applicazione. 
  * Un servizio richiesto potrebbe non essere dichiarato nel file `manifest.yml`.
  * Un servizio richiesto potrebbe essere dichiarato nel file `manifest.yml`,
ma il servizio si trova già nello spazio di destinazione.
  * Potrebbe esistere un problema con il codice nel repository.

Per diagnosticare il problema, riesamina i log di creazione e distribuzione
dalla distribuzione:
  1. Se il passo "Distribuzione a Bluemix" non viene completato correttamente, fai clic sul link nel precedente passo di "Configurazione della pipeline" per aprire Delivery Pipeline.
  2. Identifica la fase di creazione o distribuzione non riuscita.
  3. Nella fase non riuscita, fai clic su **Visualizza log e cronologia**.
  4. Individua il messaggio di errore.
   
Utilizza uno dei seguenti metodi:
{: tsResolve}

  * Se il messaggio di errore indica che nello spazio {{site.data.keyword.Bluemix_notm}}  non vi è spazio sufficiente per distribuire l'applicazione, scegli un altro spazio.
  * Se il messaggio di errore indica che un servizio richiesto non è dichiarato nel file `manifest.yml`, comunica al proprietario del repository che è necessario aggiungere il servizio richiesto.
  * Se il messaggio di errore indica che un servizio richiesto esiste
già nello spazio di destinazione, seleziona un spazio differente da utilizzare.
  * Se il messaggio di errore indica che esiste un problema con la creazione,
correggi eventuali problemi con il codice che impediscono la creazione
dell'applicazione. Per verificare che il codice non contenga alcun problema, crea il codice utilizzando i comandi Git:
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
	<appname> create
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
	<appname> run
	```
    9. Apri l'applicazione e verifica che funzioni correttamente:
	```
	<appname> open
	```
	
## Impossibile distribuire un'applicazione dalla barra di esecuzione
{: #ts_runbar}

La distribuzione non riesce indicando uno stato "non sincronizzato" di colore giallo. 
{: tsSymptoms} 

L'applicazione che stai distribuendo ha la stessa rotta di un'altra applicazione in esecuzione. 
{: tsCauses}

Modifica la rotta in modo che sia univoca.
{: tsResolve}

## Impossibile trovare la barra di esecuzione in Eclipse
{: #ts_runbar-missing}

Se non visualizzi la barra di esecuzione in Eclipse Orion {{site.data.keyword.webide}}, si è verificato uno dei seguenti problemi:
{: tsCauses}

* {{site.data.keyword.jazzhub}} non riesce a identificare il tuo progetto.
*  {{site.data.keyword.jazzhub_short}} non riesce a determinare in quale cartella si trova la tua applicazione.
* {{site.data.keyword.jazzhub_short}} non riconosce la tua applicazione come applicazione Node.js.
   
Utilizza uno dei seguenti metodi come appropriato:
{: tsResolve}  

* Se {{site.data.keyword.jazzhub}} non riesce a identificare il tuo progetto, crea un file `project.json` nella directory root del tuo progetto.
* Se {{site.data.keyword.jazzhub_short}} non riesce a determinare in quale cartella si trova la tua applicazione, e la tua applicazione non si trova nella directory root del progetto, utilizza uno dei seguenti passi:
  * Crea un file `manifest.yml` nella directory root del tuo progetto, quindi modifica il file in modo che punti alla posizione della tua applicazione. Ad esempio, `path: path_to_your_app`.
  * Sposta la tua applicazione nella directory root del progetto.
* Se {{site.data.keyword.jazzhub_short}} non riconosce la tua applicazione come applicazione Node.js, crea un file `package.json` nella cartella dell'applicazione del tuo progetto.
  
## L'hook GitHub non funziona
{: #ts_githubhookisntworking}

Hai configurato il tuo progetto GitHub per creare link dell'elemento di lavoro quando esegui il push di commit e i link non funzionano nel modo previsto
{: tsSymptoms}

Utilizza la seguente procedura per individuare il problema:
{: tsResolve}

1. Nel repository GitHub, fai clic su **Impostazioni**.
   ![Link alle impostazioni GitHub](images/github_settings.png)

2. Fai clic su **Webhook & servizi**.
   ![Link ai servizi e webhook GitHub](images/github_webhook.png)

3. Per visualizzare il messaggio, passa il puntatore del mouse sull'icona dello stato {{site.data.keyword.jazzhub}}.
   ![Messaggio di errore sull'hook del servizio](images/github_error.png)

4. Risolvi il problema in base al messaggio GitHub.

5. Per verificare che la correzione abbia funzionato, esegui il commit e il push di un'altra modifica o vai alla pagina del servizio per {{site.data.keyword.jazzhub_short}} e fai clic su **Verifica servizio**.
   ![Pulsante Verifica servizio GitHub](images/github_test.png)

6. Verifica che non vi siano errori controllando di nuovo l'icona dello stato.
   ![Icona dello stato senza errori](images/githubResolved_small.png)

Per ulteriori informazioni, vedi [Setting up GitHub for Bluemix DevOps Services projects ![icona link esterno](../icons/launch-glyph.svg "External link icon")](https://hub.jazz.net/docs/githubhooks/){: new_window}.
