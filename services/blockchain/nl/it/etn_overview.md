---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-09"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Scenario di rete
{: #etn_overview}


I piani IBM Blockchain su Bluemix Starter Developer e High Security Business Network si avvalgono delle funzioni fornite da Hyperledger Fabric v0.6, dal protocollo di consenso PBFT (Practical Byzantine Fault Tolerance) e dall'HFC (Hyperledger Fabric Client) SDK for Node.js. Entrambi i piani sono costituiti da quattro nodi di rete e da un'Autorità di certificazione. L'Autorità di certificazione controlla "Membership Services", che gestisce identità, autorizzazioni di rete e transazioni confidenziali mediante l'emissione di certificati digitali.
{:shortdesc}

Le seguenti funzionalità blockchain sono disponibili in entrambi i piani:

* Il protocollo di consenso PBFT gestisce l'ordinamento di tutte le transazioni scritte nel registro condiviso. Una rete blockchain PBFT di quattro nodi è in grado di raggiungere il consenso nonostante un nodo Byzantine (malfunzionante). Per i dettagli sull'esecuzione di test di consenso PBFT, vedi [Esecuzione di test di consenso e disponibilità](etn_pbft.html).
* L'HFC SDK per Node.js consente alle applicazioni Node.js lato client di interagire con la rete blockchain. Le applicazioni lato client possono completare la registrazione in modo sicuro degli utenti tramite Membership Services, emettere transazioni e scambiare in modo crittografico delle risorse servendosi di tCert. Per ulteriori informazioni su Membership Services e la privacy degli utenti, consulta la sezione [HFC SDK per Node.js](etn_sdk.html) e la [specifica del protocollo](https://github.com/hyperledger/fabric/blob/v0.6/docs/protocol-spec.md) Hyperledger Fabric.
* Ora puoi accedere ai dettagli sull'ambiente di rete blockchain tramite il [dashboard monitor Bluemix](ibmblockchainmonitor.html).  

<br>
## Terminologia

La seguente terminologia, insieme al diagramma successivo, contestualizzano i componenti di una rete IBM Blockchain basata su Hyperledger Fabric v0.6:

**Membro**: un'identità per partecipare alla rete blockchain. Ci sono diverse classi di membri, inclusi utenti, peer, validatori e revisori.

**Membership services**: servizi correlati all'ottenimento e alla gestione di identità membro. Membership Services è controllato dalle autorità di certificazione.  

**Registrazione**: l'atto di aggiungere una nuova identità membro alla rete. Un membro può essere aggiunto dinamicamente alla rete da un utente con il privilegio di 'registrar' (conservatore del registro). Ai membri vengono anche assegnati ruoli e attributi che controllano il loro accesso e la loro autorizzazione sulla rete. Né i ruoli né gli attributi possono essere assegnati dinamicamente; devi invece modificare il file membersrvc.yaml.

**Completamento della registrazione****: completa il processo di registrazione consentendo al nuovo membro di accedere alla rete blockchain. Il completamento della registrazione può essere eseguito dal nuovo membro dopo aver ottenuto un segreto da un conservatore del registro (fuori banda) oppure da un intermediario con l'autorizzazione delegata ad agire per conto del nuovo membro.  

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
## Architettura di rete

La figura 1  e la sua successiva descrizione, illustrano l'architettura di rete di IBM Blockchain e il flusso di dati per i servizi membro, le transazioni, il consenso e l'accodamento al registro:

![Rete dedicata](images/Architecture_BMX_dedicated.png "Architettura di rete IBM Blockchain")
Figura 1.

La seguente procedura descrive in dettaglio il flusso di rete dalla figura 1:

1. Un utente registrato completa la registrazione con la rete tramite il PKI (Membership Services) e riceve un certificato di registrazione completata (eCert) a lungo termine e un batch di certificati transazione (tCert).
2. L'utente distribuisce il chaincode alla rete. Il chaincode (contratto smart) codifica la logica di business, o le regole, che regolano uno specifico tipo di transazione. Ogni transazione, deploy (distribuzione), invoke (richiamo) o query, richiede un tCert univoco e deve essere firmato con la chiave privata dell'utente. L'utente deriva la sua chiave privata dai tCert assegnati.
3. L'utente richiama il contratto smart, che attiva il contratto per eseguirne automaticamente la logica codificata.
4. Una transazione viene inoltrata a un peer di rete. Dopo aver ricevuto la richiesta di transazione, il peer inoltra la richiesta al peer primario della rete (VP1 nella figura 1). Il peer primario ordinerà un blocco di transazioni e trasmetterà questo ordine ai suoi peer.
5. I peer utilizzando il protocollo di consenso di rete (PBFT) per concordare sull'ordine delle transazioni inoltrate. Questo processo di ordinare collettivamente le transazioni è noto come consenso.  
6. Dopo che i peer hanno raggiunto il consenso, le richieste di transazione vengono eseguite e il blocco viene accodato al registro condiviso.  

<!---Both the developer and high-security networks unlock several features in the Hyperledger fabric which robustly enhance security, confidentiality and privacy.  The only fundamental difference between the two is their operating/hosting environment.  The developer network runs in a shared multi-tenant environment on Softlayer, whereas the high-security network exists as an isolated single-tenant running in a secure services container.  Each network leverages the same capabilities from the fabric, including a PBFT consensus protocol and the enhanced Node.js SDK.~~

~~The High-Security business network runs in an isolated and highly secured environment, distinguishing it from other cloud-hosted offerings. The operating system, fabric, and nodes all exist in a secure services container (SSC), providing your enterprise with the security and impregnability that customers have come to expect from system Z technology.  The SSC delivers performance optimization in - peer to peer communication, availability, scalability, hardware encryption, tamper-proof crypto keys, and securely encrypted VMs.  See the [Secure Services Container](etn_ssc.html) section for more details on the security features provided through the SSC.  Additionally, the high security network unlocks numerous features of the Hyperledger fabric (unavailable in the developer service), which robustly enhance security, confidentiality and privacy.  The configuration is such that you are able to test and affirm these features.~~  
{:shortdesc}

~~The high security plan augments the developer plan by delivering several enhancements that help meet the security requirements and concerns of an enterprise-level participant:~~--->

<!---The environment (LinuxONE on z) consists of a four-peer network implementing PBFT with Membership Services enabled, running in an application container.  The application container protects blockchain software, chaincode, and data running within the system. The blockchain software within the secure boot can be signed, attested, and encrypted; and once installed in the application container, is tamper-resistant.  Root users of the platform and system administrators cannot access or see z secure container contents.  In addition, the LinuxOne on z provides you with FIPS compliance, high Evaluation Assurance Level protection, a highly auditable operating environment, and crypto optimization--->
