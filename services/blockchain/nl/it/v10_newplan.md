---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# High Security Business Network (HSBN) vNext Beta
{: #etn_overview}

**HSBN vNext Beta** fornisce una soluzione chiavi in mano per la generazione di una rete di business blockchain.  Il servizio ti fornisce rapidamente la rete e offre un monitor per una facile gestione e manutenzione delle tue risorse. Questo semplice processo di creazione e regolazione di una rete permette di rivolgere più tempo e attenzione allo sviluppo e alla distribuzione delle soluzioni di business.
{:shortdesc}

Le reti **HSBN vNext Beta** vengono eseguite in un ambiente altamente protetto su LinuxONE, dove le risorse di rete (peer, ordinatori, CA, codice di origine, registro)  sono tutte contenute all'interno di un contenitore **IBM Secure Service Container** (SSC). Le funzioni includono:
* Ottimizzazione delle prestazioni per le comunicazioni peer-to-peer
* Elevata disponibilità e framework per la scalabilità 
* Crittografia hardware, chiavi crittografiche a prova di manomissione e macchine virtuali crittografate in modo sicuro
* Avvio protetto con il software resistente alle manomissioni
* Nessun accesso root
* Conformità FIPS, elevata protezione del livello di garanzia della valutazione, controllabilità e ottimizzazione della crittografia

Una sottoscrizione al piano **HSNB vNext Beta** include il supporto per le seguenti risorse di rete:

- Un servizio di ordinamento a tolleranza di errori anomali
- 2 peer per membro
- Fino a 5 ulteriori membri di rete
- 5 chaincode istanziati per membro
- Un'Autorità di certificazione specifica del membro
- Fino a 100 canali
- Politiche di governance predefinite (tutti i membri sono amministratori e possono emettere gli inviti per partecipare alla rete)

Consulta la sezione [IBM Secure Service Container](etn_ssc.html) per ulteriori dettagli sulle funzioni di sicurezza della rete.

## Utilizzo del piano HSBN vNext Beta
{: #use_hsbn}

### Accesso al piano

Il piano IBM Blockchain su Bluemix **HSBN vNext Beta** è concesso su richiesta. Quando selezioni HSBN vNext Beta dal catalogo Bluemix e crei un'istanza del servizio, la tua richiesta di partecipare all'ultima release Beta viene inviata al team di IBM Blockchain. Una volta approvata la richiesta, riceverai un'e-mail di invito a partecipare al piano; segui le istruzioni per avviare il dashboard del piano HSBN vNext Beta.

Sul dashboard HSBN vNext Beta, seleziona una delle tre opzioni:
1. **Network Quick Start**: crea una rete HSBN vNext Beta e invita altre organizzazioni Bluemix a partecipare.
2. **Join Network**: visualizza gli inviti per aderire alle altre reti HSBN vNext Beta.
3. **Monitor Network**: gestisci le tue risorse di rete: peer, canali e chaincode.

<!-- to do - the rest of this page final edit -->

### Scenario di esempio

Supponiamo che tu sia un produttore di marmo e vuoi utilizzare la rete IBM Blockchain per eseguire transazioni con i diversi fornitori. Come procedere?  Potresti creare un canale del consorzio che contiene tutti i membri della rete e lo stato corrente del tuo repository di marmo disponibile al pubblico.  Tutte le transazioni che avvengono su questo canale saranno visibili e disponibili per query a tutti i membri sulla rete.  Tuttavia, potresti creare anche dei "canali secondari" o canali autonomi per soddisfare le esigenze di privacy e riservatezza.  Supponiamo, ad esempio, che offrirai un prezzo migliore a un certo fornitore se risponde a una determinata serie di condizioni.  Questa transazione può essere condotta sul canale secondario e avrà impatto sulla complessiva fornitura di marmo aggiornata sul canale del consorzio.  O magari vuoi commercializzare una specifica classe di marmo che non è disponibile sul canale del consorzio.  Potresti semplicemente effettuare una transazione con la parte necessaria su un canale autonomo e il registro del canale del consorzio rimarrà invariato. I canali forniscono un potente meccanismo per la privacy in quanto hanno tutti dei registri univoci e solo i membri sottoscritti e autenticati a un canale possono interagire con il registro.  

### Creazione di una rete
{: create_a_network}
La rete è composta dai seguenti componenti:
* Un servizio di ordinamento responsabile dell'autenticazione delle transazioni e del loro ordinamento in blocchi per i registri dei canali.
* Un'Autorità di certificazione (CA) specifica del membro responsabile dell'emissione del materiale di identità per i componenti di rete di ciascun membro.
* I peer specifici del membro che eseguono e compiono le transazioni e che mantengono un registro del canale.

Sul dashboard del servizio blockchain, fai clic su **Network Quick Start** e segui la procedura guidata:
1. Nella pagina **Name your Network**, immetti il nome della rete blockchain e il nome della società che rappresenterà la tua identità di membro e fai quindi clic su **Next**;
2. Nella pagina successiva **Invite members**, specifica le informazioni organizzative pertinenti per i partecipanti che desideri invitare. A ognuno verrà fornito un peer e un CA al momento dell'adesione alla rete e tutti i membri della rete manterranno un registro per ogni canale a cui hanno aderito.  <br>
   **Nota:** puoi invitare un massimo di 5 membri in una rete.
3. Nella pagina **Define Governance Rules**, sono visualizzate le impostazioni della politica di rete. Per impostazione predefinita, chiunque nella rete può creare nuovi canali e invitare membri.  
4. Nella pagina **Generate Certificate**, utilizza l'opzione **Auto generated** per creare i certificati per i componenti di rete della tua organizzazione.  Questi certificati X509 non vengono esposti all'utente.  
5. Infine, nella pagina **Review summary**, riesamina la configurazione della tua rete e fai clic su **Done** per avviare la rete.

Questo processo completa la configurazione iniziale della tua rete.

### Adesione a una rete
{: invite_members}

Dopo che la rete è stata inizializzata, i tuoi invitati riceveranno un'e-mail che indica la rete a cui sei stato invitato e le istruzioni per aderire.  Gli invitati vedranno il pulsante **Pending invites** abilitato sul dashboard del piano HSBN vNext. Fai clic sul pulsante per aderire alla rete: 

1. Seleziona la rete sull'elenco e fai clic su **Join Network**.
2. Nella schermata successiva, riesamina le regole di governance e fai clic su **Next**.
3. Nella pagina **Generate Certificate**, immetti il nome della tua organizzazione e seleziona l'opzione **Auto generated**.
4. Nella pagina **Review Network Summary**, riesamina le impostazioni della rete e fai clic su **Done**. Le impostazioni mostrano anche i **Partecipanti invitati** che hanno ricevuto gli inviti ad aderire alla rete.

Vedi [Monitor](v10_dashboard.html) per istruzioni sulla creazione dei canali e sull'istallazione/creazione dell'istanza del chaincode.

<!-- I think all of this is adequately covered in the Monitor Section; and we already tell the story in the Sample Scenario topic above -->


<!-- From Jeff: Agreed. Commenting out all the rest sections on the page.


### Creating new channels
{: prepare_private_channels}

With the latest HSBN vNext plan, you can create a private channel, install a customized chaincode, complete the trade, and update the inventory number upon the other parties in the network make a query or propose a new transaction.

1. On the HSBN vNext plan dashboard, select **Enter Monitor**.
2. Select **Channels**, and click **New Channel**.
3. On the **Create a Channel** page, enter the channel name and choose the company that you want to make trade with by adding members. Then, click **Create** to create another private consortium channel.
4. Select **Chaincode** after you click the **Enter Monitor** button on the dashboard. You can view the chaincode that are already installed on your peer, or install a new chaincode to the peer.<br>
  **Note:** You can install at most 5 chaincode apps per peer.
5. Click **Install Chaincode** to install the smart contract to the peer. A smart contract, also known as chaincode, is the programmatic code installed and instantiated onto a channel’s peers by an appropriately authorized member. End users then invoke chaincode through a client-side application that interfaces with a network peer. Chaincode runs network transactions, which if validated, are appended to the shared ledger and modify world state. Chaincode can be developed for business contracts, asset definitions, and collectively-managed decentralized applications. You can download [this sample code](https://github.com/hyperledger/fabric/blob/master/examples/chaincode/go/marbles02/marbles_chaincode.go){: new_window} to your local environment for testing.

**Note:** After you install the chaincode onto the peer, you must instantiate the chaincode by providing the initial arguments. In the case of the Marbles sample chaincode, you can input `marble1, blue, 35` in a comma separated list to indicate that you have 35 blue marble1 for trade.


### Commencing transactions
{: commence_txs}

To make transactions within your network, the trading parties must:
* Join the same channel within the network.
* Install the same version of the chaincode onto the peer that represents each organization.


Each successful transaction results in a new block appended to the blockchain, and the ledger in the levelDB updated with the new state. Other members in the network can query the ledger or the transaction history to decide the next transaction.



### Monitoring your network
{: monitor_network}

You can perform the following tasks after you click the **Enter Monitor** button on the dashboard:
* Create new channels and invite other members to join your channels to trade privately.
* Install new chaincodes to your peer to initiate or participate into new trade.
* View the changes of blocks, transactions, chaincode invocations.
* View the log on your peer.
* View the information of resources that your organization owns.
* Export a JSON file containing the low-level networking information for each of your components (such as enrollID/enrollSecret for your CA).  

See the [HSBN vNext Beta dashboard](v10_dashboard.md) for more information about the usage of each panel on the dashboard. 


-->
