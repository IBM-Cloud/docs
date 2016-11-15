---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Informazioni su blockchain
{: #ibmblockchain_overview}
Ultimo aggiornamento: 23 settembre 2016
{: .last-updated}

## Cos'è blockchain?
{: #what}

Blockchain è una tecnologia per una nuova generazione di applicazioni transazionali che stabilisce affidabilità, rendicontazione e trasparenza, ottimizzando al tempo stesso i processi di business. La rete blockchain è stata introdotta per la prima volta da bitcoin ma i suoi usi pratici vanno ben oltre gli scambi di criptovaluta. Con blockchain, IBM sta reinventando i più fondamentali scambi di business e aprendo le porte a un nuovo mondo di interazioni digitali.

Blockchain è progettata per ridurre sensibilmente il costo e la complessità dei processi di business tra le aziende. Il suo registro distribuito facilita la creazione di reti di business economicamente vantaggiose, in cui praticamente qualsiasi cosa di valore può essere tracciata ed essere oggetto di scambi commerciali senza un punto di controllo centralizzato. Blockchain si sta già rivelando molto promettente in un'ampia gamma di applicazioni di business. Giusto per fare un esempio, le reti blockchain consentono di regolare le transazioni di titoli in minuti, invece che in giorni. Blockchain sta anche aiutando le aziende a ottimizzare il flusso di merci e pagamenti e sta consentendo ai produttori di ridurre i richiami di prodotti condividendo in modo aperto i log di produzione con i produttori di apparecchiature originali (in inglese OEM, ossia Original Equpment Manufacturer) e gli enti di controllo.  
<br>

## Termini chiave
{: #keyterms}
I seguenti termini sono strumentali per ottenere una comprensione olistica dei concetti della blockchain:

**Operatore economico**: un partecipante alla rete connesso alla rete blockchain tramite un nodo che inoltra transazioni da un client utilizzando un SDK o una API.

**Transazione**: una richiesta da un operatore economico di eseguire una funzione sulla rete blockchain. I tipi di transazione sono distribuzione (deploy), richiamo (invoke) e query, che sono implementati tramite le funzioni chaincode esposte nel contratto API del fabric.

**Registro**: una sequenza di blocchi collegati crittograficamente che contengono transazioni e lo stato globale corrente. Oltre ai dati dalle transazioni precedenti, il registro contiene anche i dati per le applicazioni chaincode attualmente in esecuzione.

**Stato globale**:  database di valori chiave utilizzato dai chaincode per memorizzare il loro stato quando sono eseguiti da una transazione.

**Chaincode**: logica integrata che codifica le regole per specifici tipi di transazioni di rete. Gli sviluppatori scrivono applicazioni chaincode e le distribuiscono nella rete. Gli utenti finali richiamano quindi il chaincode tramite un'applicazione lato client che si interfaccia con un peer di rete, o nodo. Il chaincode esegue le transazioni di rete che, se convalidate, sono accodate al registro condiviso e modificano lo stato globale.

**Peer di convalida**: un nodo di rete che esegue il protocollo di consenso per la rete per convalidare le transazioni e tenere il registro. Le transazioni convalidate vengono accodate al registro, in blocchi. Se il consenso per una transazione ha esito negativo, detta transazione viene eliminata dal blocco e, pertanto, non viene scritta nel registro. Un peer di convalida (o VP, acronimo di validating peer) ha l'autorizzazione per distribuire e richiamare il chaincode ed eseguire query su di esso.

**Peer non di convalida**: un nodo di rete che funge da proxy, connettendo gli operatori economici ai peer di convalida. Un peer non di convalida (o NVP, acronimo di non-validating peer) inoltra le richieste di richiamo al suo peer di convalida (VP) connesso. Ospita anche il server di flussi di evento e il servizio REST.

**Consenso**: un protocollo che gestisce l'ordine delle transazioni di rete blockchain (distribuire e richiamare). I nodi di convalida operano collettivamente per approvare le transazioni implementando il protocollo di consenso. Il consenso garantisce che un quorum di nodi concordi sull'ordine delle transazioni sul registro condiviso. Risolvendo le eventuali discrepanze in quest'ordine, il consenso garantisce che tutti i nodi operino su un registro del blockchain identico. Consultare l'argomento [consenso](etn_pbft.html) per ulteriori informazioni e per gli scenari di test.  

**Rete con autorizzazioni**: una rete blockchain dove a ciascun nodo è richiesto di mantenere un'identità di membro sulla rete e ciascun nodo ha accesso solo alle transazioni consentite dalle sue autorizzazioni.  

<br>
## Concetti chiave
{: #keyconcepts}

**Panoramica**: blockchain è uno specifico tipo di rete su cui i membri tracciano e scambiano risorse digitalizzate. Un registro condiviso contiene il singolo record di tutte le transazioni di rete e viene replicato su tutti i membri della rete. Le applicazioni chaincode contengono dei contratti ad esecuzione automatica e delle applicazioni lato client che si interfacciano con la rete tramite un SDK o una API.

Due o più parti contraenti, come membri di una rete blockchain, concordano implicitamente sui termini del contratto smart che regola la transazione (ad esempio al ricevimento di una risorsa "a", è dovuta la risorsa "b"). Dopo la distribuzione al blockchain, le funzioni nel contratto possono essere richiamate (è ossia possibile attivare una transazione). Il richiamo o i richiami conseguenti vengono ordinati da un nodo principale e trasmessi ai peer di convalida per il consenso. Dopo la convalida, le transazioni vengono eseguite e registrate nel registro in blocchi. Il registro viene quindi distribuito a tutti i nodi di rete tramite la replica. Dopo l'accodamento al registro, le transazioni non possono mai essere modificate o eliminate; il solo modo per annullare o modificare gli effetti di una transazione approvata consiste nell'inoltrare una transazione successiva.

**Rete**: una rete blockchain è caratterizzata da quanto segue:

- una rete peer-to-peer distribuita e decentralizzata, con i nodi che rappresentano i partecipanti alla rete, come banche, agenzie governative, produttori e istituti finanziari.
- Un gruppo di peer che convalidano le transazioni tramite un protocollo di consenso prima di eseguirne il commit a un registro condiviso.

**Registro condiviso**: il registro condiviso è la singola fonte di informazioni attendibili, o l'intera cronologia delle transazioni convalidate, in una rete blockchain. Eventuali discrepanze nel registro condiviso tra i nodi vengono risolte tramite il consenso. Il registro ha i seguenti attributi:
- Registra tutte le transazioni convalidate sulla rete.
- Viene condiviso tra tutti i partecipanti alla rete.
- Viene replicato, in modo che ciascun partecipante abbia la sua copia.
- È disponibile con autorizzazioni, in modo che i partecipanti possano visualizzare solo le loro transazioni.

**Esempio**: la figura 1 rappresenta una rete blockchain di azioni ordinarie di esempio e il registro condiviso:
![Registro condiviso](images/Architecture_shared_ledger.png "Rete blockchain di azioni ordinarie di esempio")
*Figura 1. Un esempio di registro condiviso*

La figura 1 mostra i tipici partecipanti alla rete in un mercato di azioni ordinarie: Depositario della risorsa (banca), Deposito di titoli e operazioni (CSD) e Front office, Operations, securities depository (CSD) e una parte che opera la compensazione (Compensazione/CCP):
1. Utilizzando un'applicazione client, il depositario richiama il chaincode per comprare e vendere blocchi di titoli.  
2. Le transazioni possono essere attivate da qualsiasi nodo di rete ma sono sempre inoltrate al nodo di convalida primario (principale), che ordina le transazioni. Il nodo primario trasmette le transazioni ordinate a tutti i peer di convalida per il consenso, o l'accordo, sull'ordine proposto.
3. In caso di accordo sull'ordine delle transazioni, queste ultime vengono eseguite e accodate al registro su ciascun nodo di convalida. Il registro viene quindi replicato a tutti i nodi di rete.  

## Architettura di rete e applicazioni
{: #architecture}

La figura 2 illustra una rete blockchain con autorizzazioni, che presenta un'architettura peer-to-peer decentralizzata e distribuita e un'Autorità di certificazione che gestisce ruoli utente e autorizzazioni:
![Rete blockchain](images/Architecture_network_and_application.png "Rete blockchain con autorizzazioni di esempio")
*Figura 2. Una rete blockchain con autorizzazioni: l'accesso al flusso di dati e alla rete è regolato dai ruoli dei membri*

Le seguenti descrizioni corrispondono all'architettura e al flusso mostrati nella figura 2, che non rappresentano un processo sequenziale:

**A:** un utente blockchain inoltra una transazione alla rete blockchain con autorizzazioni. La transazione può essere una distribuzione, un richiamo o una query e viene emessa tramite un'applicazione lato client che si avvale di un SDK oppure direttamente tramite una API REST.  

**B:** le reti di business attendibili forniscono l'accesso agli enti di controllo e a quelli di revisione, come la SEC in un mercato azionario statunitense.  

**C:** un operatore di rete blockchain gestisce le autorizzazioni dei membri, come la registrazione dell'ente di controllo (B) come un "ente di revisione" e l'utente blockchain (A) come un "client". È possibile limitare un ente di revisione all'esecuzione di query delle transazioni, mentre un client può essere autorizzato a distribuire, richiamare ed eseguire query di specifici tipi di chaincode.

**D:** uno sviluppatore blockchain scrive il chaincode (contratti smart) e le applicazioni lato client per richiamare i contratti smart. Lo sviluppatore blockchain può distribuire il chaincode direttamente alla rete, tramite un'interfaccia REST. Per includere le credenziali da un'origine dati tradizionale nel chaincode, lo sviluppatore può utilizzare una connessione fuori banda per accedere ai dati (G).

**E:** un utente blockchain stabilisce una connessione alla rete tramite un nodo peer (A). Prima di procedere con eventuali transazioni, il nodo richiama i certificati di registrazione e di transazione dell'utente dall'Autorità di certificazione. Gli utenti devono essere in possesso di tali certificati digitali per eseguire attività di business su una rete con autorizzazioni.

**F:** a un utente che prova a controllare il chaincode potrebbe essere richiesto di verificare le sue credenziali su un'origine dati tradizionale (G). Per confermare l'autorizzazione dell'utente, il chaincode può utilizzare una connessione fuori banda a questi dati tramite una piattaforma di elaborazione tradizionale.

La figura 3 mostra i componenti fondamentali di IBM Blockchain. Membership Services, Blockchain Services e Chaincode Services sono strutture logiche, non un partizionamento fisico di componenti in processi, spazi di indirizzo o macchine virtuali separati: ![Architettura di riferimento](images/Architecture_core_com.png "Reference Architecture")
*Figura 3. Architettura di riferimento del fabric Hyperledger*

**Membership Services**: Membership Services gestisce le identità utente su una rete blockchain con autorizzazioni tramite il peer di Autorità di certificazione. Membership Services fornisce una distinzione dei ruoli combinando elementi di PKI (Public Key Infrastructure) e decentralizzazione (consenso). Le reti senza autorizzazione, invece, non forniscono un'autorizzazione specifica per un membro o una distinzione dei ruoli.

Un blockchain con autorizzazioni richiede che le entità eseguano la registrazione per delle credenziali di identità a lungo termine (certificati di registrazione) che possono essere distinte in base al tipo di entità. Per gli utenti, un certificato di registrazione autorizza l'Autorità di certificazione delle transazioni (TCA) a emettere credenziali pseudonime; tali certificati autorizzano le transazioni inoltrate dall'utente. I certificati delle transazioni persistono sul blockchain e consentono agli enti di controllo autorizzati ad associare delle transazioni altrimenti non collegabili.

**Blockchain Services**: Blockchain Services gestisce il registro condiviso utilizzando un protocollo peer-to-peer, che è sviluppato su HTTP/2. Le strutture dei dati sono altamente ottimizzate per fornire l'algoritmo hash più efficiente per gestire la replica del registro condiviso. PBFT è implementato come protocollo di consenso.    

**Chaincode Services**: Chaincode Services fornisce un metodo leggero e protetto di circoscrivere l'esecuzione del chaincode sui nodi di convalida. L'ambiente è un contenitore “isolato” e protetto, insieme a una serie di immagini di base firmate che contengono i livelli di sistema operativo protetto, linguaggio del chaincode, runtime ed SDK per Go, Java e Node.js. Se necessario è possibile abilitare degli ulteriori linguaggi.

Fai riferimento alla [specifica del protocollo](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric) per Hyperledger Fabric 0.5 per ulteriori informazioni sull'implementazione IBM di blockchain.
