---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# IBM Secure Service Container
{: #etn_ssc}

Ultimo aggiornamento: 13 ottobre 2016
{: .last-updated}

L'IBM Blockchain High Security Business Network viene distribuito in forma di applicazione in IBM Secure Service Container, che fornisce l'infrastruttura di base per ospitare i servizi blockchain. L'applicazione combina sistemi operativi, contenitori Docker e componenti middleware e software che operano autonomamente e fornisce i servizi di base e l'infrastruttura con una sicurezza ottimizzata.
{:shortdesc}

IBM Secure Service Container porta la crittografia, la sicurezza e l'affidabilità avanzate della piattaforma z Systems LinuxONE ai servizi blockchain per gestire dati sensibili e regolamentati. Blockchain è protetto tramite una serie di funzioni da IBM Secure Service Container: sistema operativo incapsulato, dischi di applicazioni crittografati, protezione da manomissioni, memoria protetta e forte isolamento LDAP che possono essere configurati in modo da soddisfare i requisiti della certificazione EAL5+.

Il seguente diagramma dell'architettura illustra in che modo sono organizzati IBM Secure Service Container e le applicazioni blockchain:

![Diagramma dell'architettura](images/Architecture_HSBN_SSC.png "IBM Secure Service Container e applicazioni blockchain")
*Figura 1. Panoramica di IBM Secure Service Container e applicazioni blockchain*
<br><br>
## Funzioni di sicurezza chiave
IBM Secure Service Container fornisce le seguenti funzioni di sicurezza ottimizzate per i servizi blockchain:  

### Protezione dagli amministratori di sistema
>Al codice dell'applicazione non possono accedere neanche gli amministratori di piattaforma o sistema.  L'accesso ai dati è controllato dall'applicazione e, pertanto, l'accesso non autorizzato è disabilitato.  Ciò è supportato tramite una combinazione di firma e crittografia di tutti i dati in transito e statici. Viene rimosso anche tutto l'accesso alla memoria. Il firmware supporta ciò con una architettura di avvio protetto.

>Gli amministratori di sistema hanno le seguenti limitazioni quando il blockchain è protetto da IBM Secure Service Container:
>* Non possono accedere ai nodi
>* Non possono visualizzare la rete blockchain

### Protezione da manomissioni  
>IBM Secure Service Container disabilita tutte le interfacce esterne che forniscono accesso alla memoria LPAR. Un caricatore di avvio dell'immagine è firmato per garantire che non possa essere manomesso o scambiato con uno diverso.

### Dischi applicazione crittografati
>Tutto il codice e tutti i dati memorizzati su disco sono sempre crittografati utilizzando il livello di crittografia Linux:  
- Sistema operativo incapsulato
- IP protetto
- Monitoraggio e autocorrezione incorporati  
<br>

## Gestione delle applicazioni tramite le API REST
Le applicazioni software sono preconfigurate per consentirti di farne uso sulla piattaforma z Systems affidabile, protetta e scalabile. Puoi gestire queste applicazioni tramite le API REST senza alcuna configurazione.

Per gestire le risorse blockchain tramite le API REST, puoi utilizzare l'IU Swagger o il dashboard Blockchain su Bluemix oppure gli strumenti di comandi BEST, come `curl` o `Postman`.

Ad esempio, per ottenere informazioni su tutti i peer nella rete, immetti il seguente comando utilizzando `curl`:
```
curl -u <nomeutente>:<password> https://<id_peer>:<porta>/network/peers
```
Vedi il seguente comando curl di esempio e i risultati restituiti:
* Comando:
```
curl -u dashboarduser_type0_2ef27***:89317***https://ad3130e8-4a1a-4ce6-a084-689a345a3308_vp1-api.blockchain.ibm.com:443/network/peers
```
* Informazioni restituite su tutti i peer nella rete:
```
{
	"peers": [{
		"ID": {
			"name": "ad3130e8-4a1a-4ce6-a084-689a345a3308_vp2"
		},
		"address": "ad3130e8-4a1a-4ce6-a084-689a345a3308_vp2-discovery.blockchain.ibm.com:30303",
		"type": 1,
		"pkiID": "rC0uvv0cbSbiT8RUGKPQM3q/o09oyWlcBmRxogi2Cls="
	},
	{
		"ID": {
			"name": "ad3130e8-4a1a-4ce6-a084-689a345a3308_vp1"
		},
		"address": "ad3130e8-4a1a-4ce6-a084-689a345a3308_vp1-discovery.blockchain.ibm.com:30303",
		"type": 1,
		"pkiID": "oeoI+Xa/lW8Xvrvv71A+Nvzit+JDa+oIkthpZHwfaTE="
	}]
}
```
Per ulteriori informazioni su come interagire con blockchain tramite le API REST, consulta [Monitor Dashboard](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchainmonitor.html) e [Esempi ed esercitazioni](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchain_tutorials.html).
