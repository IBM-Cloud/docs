---

copyright:
  years: 2017
lastupdated: "2017-04-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introduzione
{: #gettingstartedtemplate}

**ATTENZIONE:** prima di utilizzare uno dei piani IBM Blockchain su Bluemix, leggi le informazioni tecniche e di supporto in [Dichiarazione di non responsabilità](needtoknow.html).
{:shortdesc}

## IBM Blockchain su Bluemix

Il servizio {{site.data.keyword.blockchainfull}} su Bluemix&reg; consiste in tre piani di rete blockchain. L'ultimo piano, **High Security Business Network (HSBN) vNext Beta**, si basa sul codice Hyperledger Fabric v1.0 e sfrutta un'architettura modulare per fornire nuove funzionalità. I piani IBM Blockchain su Bluemix consentono agli sviluppatori di scrivere e testare immediatamente le applicazioni chaincode, senza dover progettare e configurare una rete blockchain privata.  Il chaincode è il motore che sta dietro lo scambio sicuro ed efficace delle risorse sulle reti Fabric e la registrazione permanente di queste transazioni sul registro.

## Piani dell'offerta

I nuovi sottoscrittori di IBM Blockchain su Bluemix possono ora completare la registrazione al piano **HSBN vNext Beta**. Questa ultima offerta si basa su Hyperledger Fabric v1.0, che fornisce la sicurezza, l'integrità, la scalabilità e le prestazioni di ultima generazione. La tabella 1 descrive i piani Bluemix:

Tabella 1: piani di IBM Blockchain su Bluemix  

| Piano Bluemix      | Stato       | Disponibile per i nuovi sottoscrittori  | Versione Hyperledger Fabric
| ------------------------- |:--------------------------:|:-----:|:-----:|
| **HSBN vNext Beta** (1)   | Beta     | Sì |  v1.0 |
| HSBN (2) |  GA |  Sì |  v0.6 |
| Starter Developer (3)    | Beta     | Sì | v0.6 |

(1) Il piano **High Security Business Network (HSBN) vNext Beta** fornisce un semplice meccanismo per aderire alle organizzazioni Bluemix e creare una rete blockchain distribuita.  
(2) Il piano **High Security Business Network (HSBN) GA** fornisce un ambiente LinuxONE on z Systems ad elevata protezione e a singolo tenant, con l'isolamento del codice mediante [IBM Secure Service Container](etn_ssc.html).  
(3) Il piano Starter Developer Beta fornisce solo un ambiente di sviluppo a più tenant.  

## Dettagli dei piani dell'offerta

La tabella 2 illustra un confronto dettagliato dei piani dell'offerta IBM Blockchain su Bluemix. I nuovi sottoscrittori di IBM Blockchain su Bluemix devono scegliere il piano **HSBN vNext Beta**. I piani HSBN e Starter Developer sono chiusi ai nuovi sottoscrittori, ma rimangono supportati da IBM:

Tabella 2: dettagli dei piani IBM Blockchain su Bluemix  

| Piano Bluemix:      | Starter Developer Network       | High Security Business Network       | High Security Business Network (HSBN) vNext Beta
| ------------------------- |:--------------------------:|:-----:|:-----:|
| Stato:    | Beta     | GA | Beta |
| Scopo:  |  Sviluppo e test dei livelli di sicurezza, prestazioni e disponibilità |  Simulare una rete aziendale e testare i livelli di sicurezza, prestazioni e disponibilità |  Impostare una rete di business aziendale con sicurezza, prestazioni e disponibilità a livello di produzione |
| Nodi:    | 4 peer + Autorità di certificazione     | 4 peer + Autorità di certificazione | gestione dinamica dei componenti di rete |
| Monitor dashboard: | [Sì](ibmblockchainmonitor.html) | [Sì](ibmblockchainmonitor.html) | [Sì](v10_dashboard.html) |
| Ambiente:     | A più tenant condiviso | A singolo tenant isolato | più livelli di isolamento |

# Link correlati
{: #rellinks}
## Esercitazioni ed esempi
{: #samples}
* [Demo IBM Marbles (GitHub)](https://github.com/IBM-Blockchain/marbles) - v0.6 & v1.0
* [Demo IBM Commercial Paper (GitHub)](https://github.com/IBM-Blockchain/cp-web#readme) - v0.6
* [Demo IBM Car Lease (Github)](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md) - v0.6
* [Demo Art Auction (Github)](https://github.com/ITPeople-Blockchain/auction) v0.6 - v1.0 (eseguito localmente)

## Riferimento API
{: #api}
* [API Hyperledger Fabric (GitHub)](https://github.com/hyperledger/fabric/tree/v0.6/docs/API)
* [HFC SDK per Node.js](https://github.com/hyperledger/fabric/tree/v0.6/sdk/node)

## Link correlati
{: #general}
* [Codice Fabric](https://github.com/hyperledger/fabric)
* [Fabric Composer](https://fabric-composer.github.io/)
* [Documentazione di Fabric v1.0](http://hyperledger-fabric.readthedocs.io/en/latest/)
* [Documentazione di Fabric v0.6](https://github.com/hyperledger/fabric/tree/v0.6/docs)
* [StackOverflow](http://stackoverflow.com/questions/tagged/hyperledger)
* [Novità nei servizi Bluemix](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}


<!--
[Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/)
[IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs) -->
