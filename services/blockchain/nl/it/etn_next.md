---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Esecuzione di test aggiuntivi
{: #etn_next}


I seguenti test sono stati eseguiti nell'ambiente High Security Business Network (se non diversamente indicato) per verificare la funzione chaincode, il registro, le lunghe esecuzioni, la simultaneità e le transazioni complesse.  I validatori e i nodi Membership Services sono stati eseguiti come guest VM nel contenitore di servizi sicuri sul sistema operativo LinuxONE.  I valori utilizzati di seguito sono stati scelti in base all'input del cliente e non devono essere confusi con i valori massimi. (Nota: alcuni di questi test sono ripetuti nelle sezioni [SDK Node.js](etn_txn.html) e [Esecuzione di test di consenso e disponibilità](etn_pbft.html)).

{:shortdesc}

1. Funzione chaincode - le interfacce chaincode sono state sottoposte a procedure di utilizzo per garantire che le transazioni `Deploy` (distribuzione), `Invoke` (richiamo) e `Query` funzionino correttamente utilizzando la API REST e la CLI. Sia la API REST che la CLI sono state utilizzate per testare tutte le funzioni endpoint, comprese Block (blocco), Blockchain, Chaincode, Network (rete), Registrar (conservatore del registro) e Transactions (transazioni), come descritto nella specifica del protocollo Hyperledger.
2. registro - la creazione di 20.000 record di payload da 1K nel registro basati su diversi ambienti di controllo. I test includevano un client che crea 20.000 record in modo serializzato.
3. Lunghe esecuzioni - questo test è stato eseguito inviando richiami, altezza della catena e query su più nodi per 72 ore utilizzando la chaincode demo example02.
4. SDK Node.js - l'SDK Node.js migliorato è stato utilizzato per registrare e completare la registrazione degli utenti ed eseguire distribuzione, richiami e query sia su un peer in modalità di sviluppo (avviando il peer con: `peer node start –peer -chaincodedev`) sia in modalità di rete (avviando il peer con: `peer node start`).
5. Simultaneità di base - questo test è stato eseguito inviando dei richiami simultanei a ciascuno dei quattro peer per una durata di 10 minuti, con payload da 1KB e misurando l'altezza della catena ed eseguendo query dello stato del registro.
6. Transazioni complesse - questo test è stato eseguito inoltrando casualmente una combinazione di query e richiami di diverse dimensioni di payload, da 10k a 500K, ai peer per una durata di 10 minuti. L'altezza della catena e la query dello stato globale sono state misurate per garantire la sincronizzazione del registro condiviso tra i peer di rete.
