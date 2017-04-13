---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Novità
{: #whatsnew}

Il piano **HSBN vNext Beta** si basa su un commit stabile della base di codice open source [Hyperledger Fabric v1.0](https://www.hyperledger.org/){:new_window}. Hyperledger Fabric v1.0 implementa un'architettura modulare che fornisce un'architettura resiliente, sicura e personalizzabile per la creazione di reti blockchain aziendali.  
{: shortdesc}

Il servizio **HSBN vNext Beta** va oltre il singolo ambiente sandbox per fornire una rete blockchain distribuita con gruppi di risorse che si estendono tra le varie organizzazioni Bluemix.  Consulta l'argomento [Panoramica](v10_netoverview.html) per ulteriori informazioni sull'architettura di rete.

## Nuova architettura nella v1.0
{:why}

L'architettura Hyperledger Fabric si è evoluta in modo significativo nella v1.0 per potenziare le reti di livello
aziendale incentrate sulla sicurezza, scalabilità, riservatezza e prestazioni. I peer vengono suddivisi in
due runtime distinti - **approvazione** e **commit** - e la responsabilità dell'ordinamento delle transazioni
viene astratta in un componente separato.  Le esigenze di privacy e riservatezza vengono risolte tramite i canali, che
forniscono la segregazione dei dati.  Esistono registri per ogni singolo canale, pertanto è possibile personalizzare le
reti in modo da supportare le diverse combinazioni di transazioni bilaterali, multilaterali o pubbliche.

Consulta la sezione sui [dettagli dell'architettura Hyperledger](http://hyperledgerdocs.readthedocs.io/en/latest/arch-deep-dive.html){: new_window} per ulteriori informazioni sulla topologia e interazione di reti.

## Altre modifiche

Il piano HSBN vNext Beta include inoltre le seguenti modifiche:
* Il [nuovo dashboard](v10_dashboard.html) consente ai sottoscrittori di creare una rete blockchain,
invitare membri, aderire ad altre reti e gestire risorse e asset. 
* La [nuova applicazione chaincode Marbles di esempio per la v1.0](https://github.com/hyperledger/fabric/blob/master/examples/chaincode/go/marbles02/marbles_chaincode.go){: new_window} consente la sperimentazione dell'ultima base di codice. 
* Il nuovo [flusso di transazioni](http://hyperledger-fabric.readthedocs.io/en/latest/txflow.html) in Hyperledger Fabric v1.0 garantisce
la congruenza e l'integrità dei dati implementando più punti di controllo in tutto il processo di transazione.
