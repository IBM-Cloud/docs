---

copyright:
  years: 2017
lastupdated: "2017-03-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Dichiarazione di non responsabilità
{: #etn_overview}

**ATTENZIONE:** devi riesaminare le seguenti informazioni prima di utilizzare uno dei piani IBM Blockchain su Bluemix.

## Istruzione di supporto IBM

IBM vanta una lunga tradizione di leadership nell'innovazione, che continua con i piani dell'offerta IBM Blockchain su Bluemix. Blockchain è una tecnologia in rapido avanzamento che andrà a interessare diversi settori, come finanza, catena di fornitura e logistica. Attraverso vari programmi di adozione iniziali, i clienti e business partner IBM hanno portato attivamente la blockchain a diventare una soluzione industriale. IBM Blockchain su Bluemix è uno di questi programmi. **Come con qualsiasi nuova tecnologia, gli utenti di IBM Blockchain su Bluemix devono essere consapevoli della possibilità di cambiamenti rapidi e importati**.  
{:shortdesc}

L'architettura che sta dietro IBM Blockchain è il progetto Hyperledger Fabric della Linux Foundation. Fabric è attualmente in stato *Attivo* e sottoposto a costante sviluppo. Ogni contributo della community open source apporta miglioramenti a Hyperledger Fabric, ma può presentare delle difficoltà di adozione. Durante il ciclo del progetto *Attivo*, i clienti possono utilizzare Hyperledger Fabric v1.0 per l'esecuzione di test e simulazioni della rete. **IBM mette in guardia dalla definizione o dallo scambio di risorse finanziarie, o di qualsiasi risorsa di valore, direttamente sulle reti blockchain Hyperledger Fabric**.  

## Istruzione open source

Il piano **High Security Business Network (HSBN) vNext Beta** si basa sul codice open source Hyperledger Fabric v1.0 della Linux Foundation. I piani Starter Developer e High Security Business Network (HSBN) si basano sul codice Hyperledger Fabric v0.6. I membri del progetto Hyperledger, compresa IBM, continuano a contribuire al codice di origine, che viene quindi revisionato, approvato e testato dalla community. Hyperledger Fabric v1.0 è attualmente *Attivo*; i dettagli sullo stato *Attivo* e sul ciclo di vita del progetto Hyperledger, sono disponibili all'indirizzo https://wiki.hyperledger.org/community/project-lifecycle.  

## Istruzione di supporto del chaincode

Le seguenti prassi di codifica NON sono supportate sulle reti IBM Blockchain:

1. Utilizzo di array associativi con iterazione (l'ordine è casuale in Go).
2. Lettura di un elenco di voci da una tabella KVS (l'ordine non è garantito).
3. Scrittura del chaincode thread-unsafe (query e richiamo possono essere chiamati in parallelo).
4. Sostituzione della memoria globale o archiviazione cache per le variabili di stato del registro nel chaincode.
5. Accesso ai servizi esterni, ad esempio database, direttamente dal chaincode.
6. Utilizzo di librerie o variabili globali che potrebbero introdurre il non determinismo (ad esempio, l'uso di "random" o "time").
7. Iterazione utilizzando GetRows.  

Inoltre, i piani HSBN e Starter (Hyperledger Fabric v0.6) non supportano il chaincode non deterministico, che introduce dei rischi per la congruenza e l'integrità dei dati; per i dettagli vedi [chaincode non deterministico](nondeterministic.html).
