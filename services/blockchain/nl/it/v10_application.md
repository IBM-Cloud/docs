---

copyright:
  years: 2017
lastupdated: "2017-03-17"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Sviluppo dell'applicazione
{: #v10_dashboard}


Utilizza il chaincode di esempio marbles02 e l'applicazione javascript corrispondente come template per la creazione della tua propria soluzione di business.
{:shortdesc}


L'applicazione si avvale delle API SDK Node.js per interagire con i tuoi componenti di rete forniti e per indirizzare il tuo peer con le richieste di transazione.  Individua gli endpoint API per il tuo peer, l'Autorità di certificazione e il servizio di ordinamento di rete nella scheda **Credenziali del servizio** della schermata **Risorse** del Monitor e inserisci queste stringe in un file di configurazione che accompagna la tua applicazione. Tuttavia, nota che se vuoi indirizzare ulteriori peer nella rete (ossia nel caso in cui richiedi l'approvazione da un peer che non appartiene alla tua organizzazione) dovrai ottenere gli endpoint API corretti per questi peer.  Dovrai anche memorizzare il certificato CA per l'altra organizzazione al fine di verificare le risposte restituite alla tua applicazione.  Queste informazioni non vengono esposte nella tua vista **Risorse** e dovrai pertanto contattare l'amministratore dell'organizzazione Bluemix appropriato e acquisire questi dati in un'operazione fuori banda.  L'URL del servizio di ordinamento è comune all'interno della rete, pertanto non avrai bisogno di alcuna informazione specifica del membro per questo componente.  

Visita il repository GitHub [Marbles](https://github.com/IBM-Blockchain/marbles/tree/v3.0) per informazioni sul codice di origine e sui prerequisiti; segui il file README e dai vita alla tua applicazione.  

Esplora il [repository SDK](https://github.com/hyperledger/fabric-sdk-node) per sperimentare i test end-to-end e acquisire una migliore comprensione delle API.
