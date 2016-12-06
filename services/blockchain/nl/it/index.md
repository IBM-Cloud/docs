---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introduzione a IBM {{site.data.keyword.blockchain}}
{: #gettingstartedtemplate}
Ultimo aggiornamento: 10 novembre 2016
{: .last-updated}

**ATTENZIONE:** prima di utilizzare il piano Starter Developer (Beta) o il piano High Security Business Network (GA), leggi le informazioni tecniche e di supporto in [Cosa devi sapere](needtoknow.html).
<br><br>

## Stato dei piani dell'offerta

Il piano Starter Developer è una release Beta e fornisce un ambiente di sviluppo a più tenant. Il piano High Security Business Network è una release GA. Il piano High Security Business Network fornisce un ambiente LinuxONE su z ad elevata protezione e a singolo tenant, con l'isolamento del codice mediante [IBM Secure Service Container](etn_ssc.html).
<br><br>

## IBM Blockchain su Bluemix

Il servizio  {{site.data.keyword.blockchainfull}} su Bluemix&reg; fornisce una scelta tra due reti blockchain diverifica e sviluppo a quattro nodi, con un semplice clic su un pulsante. Invece di creare una rete blockchain da zero, gli sviluppatori possono iniziare immediatamente a scrivere applicazioni e distribuire chaincode. Il servizio IBM Blockchain su Bluemix è una rete con autorizzazioni peer-to-peer, sviluppata sul codice [Hyperledger Fabric v0.6.1](https://github.com/hyperledger/fabric/tree/v0.6) del progetto HyperLedger della Linux Foundation.
{:shortdesc}

Le reti blockchain sono utilizzate per scambiare e tracciare in modo protetto ed efficiente le risorse digitali e per registrare permanentemente tutte le transazioni sul registro condiviso. Per i dettagli sul blockchain, consulta l'argomento [Informazioni sul blockchain](ibmblockchain_overview.html).
<br><br>

## Scegli il tuo piano di rete

Hai una scelta tra due piani IBM Blockchain su Bluemix: **Starter Developer Network** o **High Security Business Network**. Utilizza il grafico di confronto qui di seguito per scegliere l'ambiente giusto per te.

<!-- Commenting our for move to GA status jh 10/07/16
![](images/red_alert.png)  **The High Security Business Network** plan is a limited Beta offering; to select this plan, you must first request preapproval at [IBM Blockchain on IBM Bluemix](http://www-stage.watson.ibm.com/files/blockchain/bluemix.html). -->

| Piano Bluemix:      | Starter Developer Network       | High Security Business Network
| ------------------------- |:--------------------------:|:-----:|
| Stato:    | Beta     | GA |
| Scopo:  |  Sviluppo e test dei livelli di sicurezza, prestazioni e disponibilità |  Simulare una rete aziendale e testare i livelli di sicurezza, prestazioni e disponibilità |
| Nodi:    | 4 nodi + Autorità di certificazione     | 4 nodi + Autorità di certificazione |
| [Monitor dashboard:](ibmblockchainmonitor.html) | Sì | Sì |
| Transazioni confidenziali: | Sì | Sì |
| [Consenso:](etn_pbft.html) | PBFT | PBFT |
| Ambiente:     | A più tenant condiviso | A singolo tenant isolato |
| [IBM Secure Service Container:](etn_ssc.html) | No | Sì |

<br>
## Avvia il tuo piano di rete

Utilizza la seguente procedura per creare e distribuire un'istanza del servizio senza binding della tua rete blockchain.  La tua rete include un ambiente di sviluppo con dei nodi di convalida e un servizio di sicurezza e ti consente di distribuire chaincode, visualizzare log e creare applicazioni:

1. Dalla pagina [Servizio {{site.data.keyword.blockchain}}](https://console.ng.bluemix.net/catalog/services/blockchain/), completa il
modulo **Aggiungi servizio** nel riquadro di destra:
  - **Spazio:** seleziona **dev**.
  - **Applicazione:** seleziona **Lascia senza binding** oppure, per eseguire il binding del tuo servizio a una delle tue applicazioni Bluemix.org, **Seleziona un'applicazione**.
  - **Nome servizio:** immetti un nome o un valore univoci, come **Blockchain Test Net123**.
  - **Nome credenziale:** lascia il valore predefinito.
  - **Piano selezionato:** scegli **Starter Developer** o **High Security**.
  - Fai clic sul pulsante **CREA**.
2.  Sei ora nella schermata **Dashboard del servizio** per il tuo nuovo servizio. Da qui, puoi **gestire** la tua istanza
della rete; fai clic su **AVVIA** per utilizzare il tuo monitor blockchain.
3.  Il monitor blockchain visualizza i dettagli di rete, i log dal vivo, lo stato del registro corrente, le API e i template di chaincode. Utilizza il dashboard per le seguenti funzioni:
  - Accedere alle rotte API e di rilevamento per i peer di rete.
  - Visualizzare i contenitori chaincode in esecuzione.
  - Visualizzare dei log in tempo reale e risolvere i problemi di chaincode.
  - Visualizzare lo stato globale per il registro.
  - Accedere all'IU Swagger e interagire con la tua rete tramite la API REST.
  - Distribuire uno dei tre esempi di chaincode.


# Link correlati
{: #rellinks}
## Esercitazioni ed esempi
{: #samples}
* [Demo IBM Marbles (GitHub)](https://github.com/IBM-Blockchain/marbles)
* [Demo IBM Commercial Paper (GitHub)](https://github.com/IBM-Blockchain/cp-web#readme)
* [Demo IBM Car Lease (Github)](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md)
* [Demo Art Auction (Github)](https://github.com/ITPeople-Blockchain/auction)

## Guida di riferimento alle API
{: #api}
* [IU Swagger](https://obc-service-broker-staging.stage1.mybluemix.net/swagger)
* [API Hyperledger fabric (GitHub)](https://github.com/hyperledger/fabric/tree/v0.6/docs/API)
* [HFC SDK per Node.js](https://github.com/hyperledger/fabric/tree/v0.6/sdk/node)

## Link correlati
{: #general}
* [Codice Fabric](https://github.com/hyperledger/fabric)
* [Whitepaper](https://github.com/hyperledger/hyperledger/wiki/Whitepaper-WG)
* [Protocol Spec & Related Docs](https://github.com/hyperledger/fabric/tree/v0.6/docs)
* [StackOverflow](http://stackoverflow.com/questions/tagged/hyperledger)
* [Linux Foundation](https://www.hyperledger.org/)
* [Novità nei servizi Bluemix](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}


<!--
[Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/)
[IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs) -->
