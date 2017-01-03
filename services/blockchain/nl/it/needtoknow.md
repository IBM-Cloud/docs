---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Cosa devi sapere
{: #etn_overview}
Ultimo aggiornamento: 10 novembre 2016
{: .last-updated}

**ATTENZIONE:** devi riesaminare le seguenti informazioni prima di utilizzare uno dei piani IBM Blockchain su Bluemix: Starter Developer (Beta) o High Security Business Network (GA).
<br><br>

## Istruzione di supporto IBM

IBM vanta una lunga tradizione di leadership nell'innovazione, che continua con le ultime offerte IBM Blockchain. Blockchain è una tecnologia in rapida progressione che andrà a interessare diversi settori, dalla finanza alla logistica. Attraverso vari programmi di adozione iniziali, i clienti e business partner IBM stanno già influenzando la direzione futura della blockchain. IBM Blockchain su Bluemix è uno di questi programmi. **Come con qualsiasi nuova tecnologia, gli utenti di IBM Blockchain su Bluemix devono essere preparati per cambiamenti rapidi e importanti**.  
{:shortdesc}

L'architettura che sta dietro IBM Blockchain è il progetto Hyperledger della Linux Foundation. Hyperledger Fabric è un progetto open source in fase di sviluppo attivo, attualmente in stato di *Incubazione*. Ogni contributo della community open source rende Hyperledger Fabric più robusto, ma può presentare delle difficoltà di adozione. Durante il ciclo di *Incubazione*, i clienti possono utilizzare Hyperledger Fabric v0.6 per i test di rete e la simulazione, ma **IBM mette in guardia contro l'esecuzione di attività finanziarie di valore direttamente su una rete blockchain di Hyperledger Fabric v0.6 (o precedenti)**.  
<br>

## Istruzione open source

IBM Blockchain su Bluemix &mdash; sia il piano Starter Developer che il piano High Security Business Network &mdash; utilizzano il codice open source di Hyperledger Fabric v0.6.1 della Linux Foundation. I membri del progetto Hyperledger, compresa IBM, contribuiscono al codice del fabric, che viene revisionato, approvato e testato dalla community. Hyperledger Fabric v0.6.1 è attualmente nello stato di *Incubazione*; i dettagli sullo stato di *Incubazione* e sull'intero ciclo di vita per il progetto Hyperledger, sono disponibili in https://github.com/hyperledger/hyperledger/wiki/Project-Lifecycle.
<br><br>

## Istruzione di supporto del chaincode

IBM Blockchain non supporta il chaincode non deterministico, che introduce dei rischi per la congruenza e l'integrità dei dati sulle reti blockchain. Prima di distribuire il nuovo chaincode alla tua rete IBM Blockchain su Bluemix, riesamina i dettagli sul [chaincode non deterministico](nondeterministic.html).

Oltre al [chaincode non deterministico](nondeterministic.html), sulle reti IBM Blockchain NON sono supportate le seguenti prassi di codifica:

1. Utilizzo di array associativi con iterazione (l'ordine è casuale in Go).
2. Lettura di un elenco di voci da una tabella KVS (l'ordine non è garantito).
3. Scrittura del chaincode thread-unsafe (query e richiamo possono essere chiamati in parallelo).
4. Sostituzione della memoria globale o archiviazione cache per le variabili di stato del registro nel chaincode.
5. Accesso ai servizi esterni, ad esempio database, direttamente dal chaincode.
6. Utilizzo di librerie o variabili globali che potrebbero introdurre il non determinismo (ad esempio, l'uso di "random" o "time").
7. Iterazione utilizzando GetRows.  

Consulta la libreria di esempio per gli esempi chaincode supportati; la directory contiene gli esempi scritti in Go e Java.
<br><br>

## Considerazioni sulla migrazione

Esistono molte modifiche di programmazione che devono essere implementate per poter sviluppare il codice in Hyperledger Fabric v0.5-developer-preview per funzionare con il backend Bluemix (creato con Hyperledger Fabric v0.6.1).  Consulta la sezione [Migration considerations](http://hyperledger-fabric.readthedocs.io/en/v0.6/v0.6_migration/) nella documentazione Hyperledger Fabric per ulteriori dettagli sulle nuove funzioni e sulle modifiche del codice.  

## Problemi noti HSBN

1. Quando si utilizza High Security Business Network, che utilizza Hyperledger Fabric v0.6.1, è suggerita la reimpostazione della rete periodicamente durante una fase di sviluppo se sono presenti grossomodo più di cinquanta distribuzioni chaincode.  La reimpostazione della rete rimuove il chaincode distribuito e i dati che sono stati raccolti.  Ciò fornisce una possibilità di rimuovere i vecchi chaincode che sono stati sostituiti da miglioramenti effettuati durante una fase di distribuzione interattiva.  Se non sei nella fase di post-sviluppo, il numero di distribuzioni di chaincode dovrebbe essere monitorato per lasciare la capacità per il chaincode più importante.
2. Vengono ricevuti degli errori "503 Service Unavailable" e "502 Bad Gateway" sporadici durante l'esecuzione di una query di stato della rete e dei peer.
3. Una sicurezza potenziale per i messaggi "Server.Serve failed to complete security handshake" nei log per vp1. Questo è un errore non irreversibile e non correlato all'operazione di rete.
4. Le **Credenziali del servizio** potrebbero non popolarsi automaticamente; in questo caso, genera le credenziali nel seguente modo:

 a) Dal tuo dashboard del servizio, fai clic sulla scheda **Service Credentials**:

  ![Credenziali di servizio HSBN](images/hsbn.png "Credenziali di servizio HSBN")

 b) Dalla scheda **Service Credentials**, fai clic sul pulsante per **New Credential**:

  ![Nuova credenziale HSBN](images/hsbn1.png "Nuova credenziale HSBN")

c) Viene visualizzata una nuova finestra denominata **Add New Credential**; fai clic sul pulsante **Add** in fondo a questa finestra:

  ![Aggiungi nuova credenziale HSBN](images/hsbn2.png "Aggiungi nuova credenziale HSBN")

 d) Ora la tua schermata dovrebbe essere simile al seguente esempio. Facendo clic su **View Credentials** visualizzerai un payload JSON contenente le credenziali del servizio per la tua istanza HSBN.  

  ![Credenziali generate HSBN](images/hsbn3.png "Credenziali generate")



## Come ottenere supporto

Per ottenere supporto e assistenza con la rete IBM Blockchain su Bluemix, vedi [Getting support](ibmblockchain_support.html).
