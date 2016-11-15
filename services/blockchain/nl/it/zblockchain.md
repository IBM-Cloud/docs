---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Blockchain su z
{: #zblockchain}
Ultimo aggiornamento: 8 luglio 2016
{: .last-updated}



Puoi utilizzare il servizio blockchain nell'offerta dedicata di Bluemix con z/OS per creare risorse digitali private e sicure che possono essere quindi oggetto di scambi commerciali rapidamente e in modo protetto su reti con autorizzazioni.  *(Ulteriori informazioni come parte della descrizione breve)*
{:shortdesc}


* La quantità di contenuto merita questa sezione dedicata?  O volgiamo lasciarlo come un argomento incorporato in "Informazioni su"?
* Attendiamo le informazioni su PBFT, Sicurezza, Prestazioni, Supporto.


## PBFT
{: #PBFT}

PBFT (Practical Byzantine Fault Tolerance) è un protocollo di consenso fondamentale che può essere collegato e configurato per ogni distribuzione. Il pacchetto `obcpbft` è un'implementazione del protocollo di consenso [PBFT](http://dl.acm.org/citation.cfm?id=571640 "PBFT") fondamentale, che fornisce il consenso tra gli enti di convalida a dispetto di una soglia di enti di convalida che fungono da *Byzantine*, ossia dannosi o in errore in un modo imprevedibile. Nella configurazione predefinita, sia PBFT che Sieve sono progettati per essere eseguiti su almeno *3t+1* enti di convalida (repliche), tollerando fino a *t* repliche potenzialmente in errore (comprese quelle dannose o *Byzantine*). Per ulteriori informazioni sulle funzioni principali di PBFT, consulta la sezione [Protocol Specification](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric) del progetto Hyperledger della Linux Foundation. 

Guarda una [![anteprima](http://www.youtube.com/watch?v=EKa5Gh9whgU)(http://img.youtube.com/vi/EKa5Gh9whgU/0.jpg)]

*(Occorre indicare un motivo pratico per cui gli utenti devono conoscere PBFT. Che ruolo ha PBFT nel blockchain sul supporto z e la sua relazione con questo supporto).*


### Casi di errore supportati
{: #failure}

*Quali casi di errore supportiamo e quali non supportiamo qui.*

*(Barry Mosakowski/Raleigh/IBM o Tuan Dang/Raleigh/IBM possono fornire ulteriori dettagli).*

### Disponibilità dell'offerta dedicata con z/OS
{: #Availability}

*Disponibilità e aspettative relative alla disponibilità sulla base dell'esecuzione di test PBFT.*

*(Servono ulteriori dettagli).*

### Verifica della funzionalità di base di PBFT
{: #Test PBFT}

*(Input da Gari. Occorrono ulteriori dettagli da Jason su come eseguire i passi del test, compresi gli screenshot).*

Per verificare la funzionalità PBFT di base, attieniti alla seguente procedura:

1. Inoltra le transazioni a uno o più peer nella rete.
2. Verifica che almeno *2f+1* (3 in questo caso) peer abbiano lo stesso stato. *(Come verificare? Occorrono i dettagli degli scenari di test).*

  *Un esempio utilizzando la API REST*
3. Sul dashboard, fai clic sul pulsante per arrestare il peer 4. *(Utilizza la funzionalità "arresta peer" nel dashboard per arrestare il peer 4. È necessario che lo scenario di test descriva l'operazione dettagliata).*
4. Verifica che la rete continui l'elaborazione. *(Come verificare?)*
5. Sul dashboard, fai clic sul pulsante per arrestare il peer 3.
6. Verifica che la rete arresti l'elaborazione.
7. Sul dashboard, fai clic sul pulsante per riavviare il peer 3.

Se il peer 3 si mette al passo e la rete continua l'elaborazione, puoi utilizzare le funzioni PBFT di base.

**Note:**
* dopo il riavvio del peer 3, devi attendere il timeout prima di inoltrare nuove transazioni al peer 3.

* Le transazioni, che vengono inviate ai peer attivi quando la rete interrompe l'elaborazione, sono memorizzate in buffer e inoltrate alla rete quando la rete continua l'elaborazione.

## Ambiente per blockchain su z
{: #z environment}

Per utilizzare il servizio blockchain nell'offerta dedicata Bluemix con z/OS, assicurati che l'ambiente soddisfi i seguenti requisiti:

* Quattro reti peer che stanno eseguendo PBFT con Membership Services. Per ulteriori informazioni su Membership Services, consulta la sezione [Protocol Specification](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric) del progetto Hyperledger della Linux Foundation. 
* Una rete isolata che non ha computer o memoria condivisi.
* Dei peer isolati nella rete.
* Un sistema protetto dagli amministratori di sistema cloud.

Il monitor blockchain fornisce una panoramica del tuo ambiente blockchain e richiama i dettagli sulla tua rete. Per ulteriori informazioni sul tuo ambiente blockchain e su come monitorarlo, consulta le sezioni relative alla [gestione del chaincode con il monitor blockchain](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchainmonitor.html) e alle [applicazioni di esempio ed esercitazioni per blockchain](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchain_tutorials.html).

## Sicurezza

*Non fornire informazioni sulla sicurezza nel documento?*

## Prestazioni

*Non fornire informazioni sulle prestazioni nel documento?*

## Richiesta di assistenza clienti

Se rilevi dei problemi con il servizio blockchain nell'offerta dedicata Bluemix con z/OS, attieniti al processo di risoluzione dei problemi di IBM Bluemix. Consulta la sezione [Risoluzione dei problemi](https://new-console.ng.bluemix.net/docs/troubleshoot/troubleshoot.html) per ulteriori informazioni su come ottenere assistenza.
