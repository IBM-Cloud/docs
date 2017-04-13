---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Esecuzione di test di consenso e disponibilità
{: #etn_pbft}

Sia il piano Starter Developer che il piano High Security Business Network ti consentono di testare il protocollo di consenso PBFT (Practical Byzantine Fault Tolerance) su una rete blockchain a quattro nodi. I seguenti argomenti forniscono i dettagli sul consenso in generale e PBFT in particolare. Quando sei pronto a iniziare il test, ti verranno forniti gli scenari di test PBFT.  
{:shortdesc}  

## Cos'è il consenso?

Il consenso è un metodo per convalidare l'ordine delle richieste, o delle transazioni (distribuzione e richiamo) su una rete blockchain. L'ordine corretto delle transazioni è critico perché molte transazioni hanno una dipendenza da una o più transazioni precedenti (gli addebiti in conto spesso hanno una dipendenza su accrediti precedenti, ad esempio).

Su una rete blockchain, non c'è alcuna autorità centralizzata che determina l'ordine delle transazioni; invece, molti nodi di convalida (o peer) implementano il protocollo di consenso di rete. Il consenso garantisce che un quorum di nodi concordi sull'ordine in cui le transazioni sono accodate al registro condiviso. Risolvendo eventuali discrepanze nell'ordine delle transazioni proposto, il consenso garantisce che tutti i nodi della rete blockchain stiano operando su un registro identico. In altre parole, il consenso garantisce* l'integrità e la congruenza di tutte le transazioni della rete blockchain.

* Tale garanzia dipende da variabili quali lo specifico protocollo di consenso implementato e il numero di nodi nella rete blockchain. Entrambi i piani Blockchain su Bluemix implementano il protocollo di consenso PBFT.  

<br>
## Cos'è PBFT?

PBFT (Practical Byzantine Fault Tolerance) è un tipo di protocollo di consenso. La funzione di un protocollo di consenso è quella di mantenere l'ordine delle transazioni su una rete blockchain, nonostante le minacce a tale ordine. Una minaccia possibile, ad esempio, è il malfunzionamento simultaneo e arbitrario (un tipo di errore Byzantine) di più nodi di rete. Utilizzando PBFT, una rete blockchain di (N) nodi può sopportare (f) numero di nodi Byzantine, dove f = (N-1)/3. In altre parole, PBFT garantisce che un minimo di 2\*f + 1 nodi raggiunga il consenso sull'ordine di transazioni prima di accodarle al registro condiviso. Derivare l'una o l'altra formula rivela la regola che una rete PBFT garantisce la congruenza e l'integrità dei dati nonostante gli errori Byzantine su meno di un terzo di tutti i nodi della rete.  

<br>
## PBFT e la tua rete blockchain

La regola PBFT 2\*f + 1 ha le seguenti implicazioni sia per il piano Starter Developer che per il piano High Security Business Network:

1. La rete non può tollerare più di un nodo Byzantine. Ogni rete contiene N=4 nodi, quindi l'applicazione della formula per il numero massimo di nodi Byzantine tollerati dà come risultato: f=(4-1)/3=1. Se esistono due o più nodi Byzantine (f>1), una rete PBFT a 4 nodi non può garantire la congruenza o l'integrità del registro in tutti i nodi. (Per un raffronto, la tolleranza di due nodi Byzantine richiederebbe f=(7-1)/3=2 oppure una rete blockchain PBFT con minimo 7 nodi).
2. Se meno di 2\*f + 1 nodi sono online, la rete smette di accodare al registro poiché PBFT non può garantire la congruenza o l'integrità dei dati nei nodi. La rete riprenderà ad accodare al registro quando almeno 2\*f + 1 nodi sono online (tre o quattro nodi, in questo caso).
3. Poiché solo un minimo di 2\*f + 1 nodi deve raggiungere il consenso prima di procedere al blocco successivo di transazioni, il registro su eventuali nodi aggiuntivi (oltre 2\*f + 1) resterà temporaneamente indietro. Questo ritardo nella sincronizzazione del registro condiviso in tutti i nodi è una limitazione inevitabile di qualsiasi rete PBFT.
<br>

## Scenari di test del consenso
I seguenti scenari di test del consenso sono stati rivisti ed approvati da IBM come rispondenti agli standard di disponibilità di rete per PBFT:

1. [Esecuzione di test PBFT senza nodi Byzantine](pbft_test1.html). Il processo di consenso esegue le transazioni e accoda al registro.
2. [Simulazione di un singolo nodo Byzantine](pbft_test2.html) arrestando un nodo e continuando a inviare transazioni di distribuzione, richiamo e query. Il processo di consenso PBFT esegue le transazioni e accoda al registro. Questo test è stato ripetuto per ciascun nodo in un ambiente a quattro nodi.
3. [Simulazione di due nodi Byzantine](pbft_test3.html) arrestando due nodi e continuando a inviare transazioni di distribuzione, richiamo e query. A causa della impossibilità di raggiungere un consenso PBFT, le transazioni non vengono eseguite o accodate al registro.
4. [Riavvio di un nodo che era stato arrestato](pbft_test4.html) nello scenario di test precedente (Test 3). Il processo di consenso PBFT riprende l'esecuzione delle transazioni e l'accodamento al registro. Il nodo riavviato sincronizza il suo registro con il registro condiviso.  

Attenzione: esamina le seguenti note prima di iniziare il test del consenso:

- Tutti gli scenari di test del consenso utilizzano la API REST per interagire con i peer di rete.
- HTTP/2 è il protocollo per le comunicazioni; gli scenari di test utilizzano gli URL peer. Ad esempio: 'VP0–api.dev.blockchain.ibm.com:80'. I valori simbolici ***VP0, VP1, VP2 e VP3*** sono utilizzati come segnaposto per gli URL peer letterali.
-  Per accedere come un peer, utilizza le credenziali fornite quando hai distribuito il tuo servizio Bluemix. Per gli scenari di test, **test\_user1** e **test\_user1\_enrollSecret** sono utilizzati rispettivamente come valori per *enrollID* e *enrollSecret*.
-  Simula gli arresti anomali dei nodi arrestando e riavviando manualmente i peer con i pulsanti **Azioni** sulla console di rete. La figura 1 di seguito mostra le **Azioni** nella scheda **Rete**:

![](images/stopstartpeer.png "Arresta e avvia i peer")
*Figura 1. Arresta e avvia i peer*

- Gli scenari di test utilizzano **chaincode_example02**, per impostazione predefinita, da: https://github.com/hyperledger/fabric/tree/v0.6/examples/chaincode/go/chaincode_example02. Puoi tuttavia utilizzare un tuo chaincode, o uno qualsiasi degli esempi di chaincode in: https://github.com/hyperledger/fabric/tree/v0.6/examples/chaincode/go.
- Le richieste vengono organizzate in batch in una singola transazione per l'elaborazione. Puoi tuttavia garantire un'immediata elaborazione facendo affidamento sul valore di timeout del batch; attendere almeno due secondi prima di inoltrare la richiesta successiva determinerà un'elaborazione immediata della transazione.
