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
Ultimo aggiornamento: 13 ottobre 2016
{: .last-updated}

**ATTENZIONE:** devi riesaminare le seguenti informazioni prima di utilizzare uno dei piani IBM Blockchain su Bluemix: Starter Developer (Beta) o High Security Business Network (GA).
<br><br>

## Istruzione di supporto IBM

IBM vanta una lunga tradizione di leadership nell'innovazione, che continua con le ultime offerte IBM Blockchain. Blockchain è una tecnologia in rapida progressione che andrà a interessare diversi settori, dalla finanza alla logistica. Attraverso vari programmi di adozione iniziali, i clienti e business partner IBM stanno già influenzando la direzione futura della blockchain. IBM Blockchain su Bluemix è uno di questi programmi. **Come con qualsiasi nuova tecnologia, gli utenti di IBM Blockchain su Bluemix devono essere preparati per cambiamenti rapidi e importanti**.  
{:shortdesc}

L'architettura che sta dietro IBM Blockchain è il progetto Hyperledger della Linux Foundation. Hyperledger Fabric è un progetto open source in fase di sviluppo attivo, attualmente in stato di *Incubazione*. Ogni contributo della community open source rende Hyperledger Fabric più robusto, ma può presentare delle difficoltà di adozione. Durante il ciclo di *Incubazione*, i clienti possono utilizzare Hyperledger Fabric v0.5 per i test di rete e la simulazione, ma **IBM mette in guardia contro l'esecuzione di attività finanziarie di valore direttamente su una rete blockchain di Hyperledger Fabric v0.5**.  
<br>

## Istruzione open source

IBM Blockchain su Bluemix &mdash; sia il piano Starter Developer che il piano High Security Business Network &mdash; utilizzano il codice open source di Hyperledger Fabric v0.5 della Linux Foundation. I membri del progetto Hyperledger, compresa IBM, contribuiscono al codice del fabric, che viene revisionato, approvato e testato dalla community. Hyperledger Fabric v0.5 è attualmente nello stato di *Incubazione*; i dettagli sullo stato di *Incubazione* e sull'intero ciclo di vita per il progetto Hyperledger, sono disponibili in https://github.com/hyperledger/hyperledger/wiki/Project-Lifecycle.
<br><br>

## Istruzione di supporto del chaincode

IBM Blockchain non supporta il [chaincode non deterministico](ibmblockchain_tutorials.html#ndcc), che introduce dei rischi per la congruenza e l'integrità dei dati sulle reti blockchain. Prima di distribuire il nuovo chaincode alla tua rete IBM Blockchain su Bluemix, riesamina i dettagli sul [chaincode non deterministico](ibmblockchain_tutorials.html#ndcc).

Oltre al [chaincode non deterministico](ibmblockchain_tutorials.html#ndcc), sulle reti IBM Blockchain NON sono supportate le seguenti prassi di codifica:

1. Utilizzo di array associativi con iterazione (l'ordine è casuale in Go).
2. Lettura di un elenco di voci da una tabella KVS (l'ordine non è garantito).
3. Scrittura del chaincode thread-unsafe (query e richiamo possono essere chiamati in parallelo).
4. Sostituzione della memoria globale o archiviazione cache per le variabili di stato del registro nel chaincode.
5. Accesso ai servizi esterni, ad esempio database, direttamente dal chaincode.
6. Utilizzo di librerie o variabili globali che potrebbero introdurre il non determinismo (ad esempio, l'uso di “random” o "time").
<br><br>

## Come ottenere supporto

Per ottenere supporto e assistenza con la rete IBM Blockchain su Bluemix, vedi [Getting support](ibmblockchain_support.html).
