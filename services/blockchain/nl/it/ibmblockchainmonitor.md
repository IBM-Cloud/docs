---

copyright:
  years: 2016
lastupdated: "2016-11-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Monitor Dashboard
{: #blockchain_dashboard_monitor}


Il monitor del dashboard fornisce una panoramica del tuo ambiente blockchain, compresi i dati sulle prestazioni e il chaincode distribuito. Utilizza il monitor per visualizzare le informazioni di rete relative a peer, log, stato del registro, API e chaincode.  
{:shortdesc}

Come mostrato nei seguenti esempi, le schede di monitoraggio del dashboard forniscono viste univoche nella tua rete blockchain:
  - Rete
  - Blockchain
  - Chaincode demo
  - API
  - Log
  - Stato
  - Supporto

**Scheda Rete**: monitora lo stato dei tuoi peer e degli eventuali contenitori chaincode in esecuzione, come mostrato nella figura 1. Visualizza le rotte Discovery e API per i tuoi peer di convalida e l'autorità di certificazione, che sono i valori di host e porta di nodo combinati. Ad esempio, il frammento di codice JSON per le tue **Credenziali di servizio** nel **Dashboard Servizio** mostra che `"discovery_host"` e `"discovery_port"` sono equivalenti alla rotta visualizzata nella scheda **Rete**. Questi valori sono utili per stabilire manualmente una connessione a Bluemix.

![](images/Console_Network.png "Scheda Rete")
*Figura 1. Scheda Rete*


**Scheda Blockchain**: visualizza lo stato corrente del tuo blockchain. Come mostrato nella figura 2, puoi visualizzare tutte le transazioni, lo stato del registro e i dati sulle prestazioni correnti per la rete:

![](images/Console_Blockchain.png "Scheda Blockchain")
*Figura 2. Scheda Blockchain*


**Scheda Chaincode demo**: impara e sperimenta con tre template di chaincode di esempio, che puoi distribuire e richiamare sulla tua rete. Sono fornite delle istruzioni per guidarti nel processo, come mostrato nella figura 3. Tutte le distribuzioni e tutti i richiami del chaincode sono scritti nel log e possono anche essere visualizzati nelle schede Log dal vivo, Blockchain e API.  

![](images/Console_DemoChaincode.png "Scheda Chaincode demo")
*Figura 3. Scheda Chaincode demo*


**Scheda API**: utilizza l'IU Swagger per interagire con la tua rete blockchain tramite la API REST, come mostrato nella figura 4:  

![](images/Console_APIs.png "Scheda API")
*Figura 4. Scheda API*


**Scheda Log**:  visualizza i log per i peer di convalida e Membership Services, che includono i risultati di tutte le transazioni sulla rete. Puoi utilizzare le informazioni di log per ispezionare le transazioni e risolvere i problemi del chaincode.  

![](images/Console_Logs.png "Scheda Log")
*Figura 5. Scheda Log*


**Scheda Stato**: visualizza le metriche delle prestazioni per servizio, rete ed esecuzione di test automatizzata, come mostrato nella figura 6. Visualizza i dati per il mese precedente. Questa scheda contiene anche gli annunci di codice, dei forum generali, i problemi noti e le note sulla release per IBM Blockchain.  

![](images/Console_Status.png "Scheda Stato")
*Figura 6. Scheda Stato*


**Scheda Supporto**: segnala un problema e visualizza il tuo stato del servizio, come mostrato nella figura 7:

![](images/Console_Support.png "Scheda Supporto")
*Figura 7. Scheda Supporto*
