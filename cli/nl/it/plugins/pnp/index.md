---

copyright:

  years: 2016, 2017

lastupdated: "2017-01-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Plug-in peering della rete privata per la CLI Bluemix
{: #private_network_cli}

Utilizza la CLI (command line interface) per configurare e gestire il peering della rete privata tra gli spazi {{site.data.keyword.Bluemix}}. Il peering della rete privata è supportato per IBM Containers (contenitori docker). Gli spazi Bluemix possono trovarsi in varie zone di disponibilità all'interno della stessa regione oppure in regioni differenti. Il plug-in della CLI peering della rete privata è disponibile per l'utilizzo con il plug-in della CLI Bluemix.

Il plug-in della CLI peering della rete privata è disponibile per i sistemi operativi Windows, MAC e Linux. Assicurati di utilizzare il plug-in adatto a te.

Prima di iniziare, crea gli spazi Bluemix. Assicurati che ogni contenitore all'interno di uno spazio abbia un indirizzo IP da una rete diversa. Per i dettagli, vedi [Using your own private IP address](https://www.{DomainName}/docs/containers/container_security_network.html#container_cli_ips_byoip)

**Nota:** dopo aver utilizzato il peering della rete privata con uno spazio Bluemix, se devi eliminare lo spazio, elimina prima le connessioni peering della rete privata in tale spazio.

Per iniziare, installa la CLI di IBM Bluemix. Per i dettagli, vedi
[CLI Bluemix](http://clis.ng.bluemix.net/ui/home.html).

## Installa il plug-in della CLI peering della rete privata

**Nota**: se disponi del plug-in a una versione precedente, dovrai disinstallarlo. Utilizza il seguente comando per disinstallare il plug-in:

```
bluemix plugin uninstall private-network-peering
```
### Installa in locale
Scarica il plug-in peering della rete privata per la tua piattaforma dal [Repository di plug-in CLI IBM Bluemix](http://plugins.ng.bluemix.net/ui/repository.html#bluemix-plugins).

Installa il plug-in peering della rete privata utilizzando il seguente comando:

**Nota**: puoi passare alla posizione del plug-in o specificarne il percorso.

* Per sistemi operativi Microsoft Windows:

```
bluemix plugin install private-network-peering-windows-amd64.exe
```

* Per sistemi operativi Apple MAC:

```
bluemix plugin install private-network-peering-darwin-amd64
```

* Per sistemi operativi Linux:

```
bluemix plugin install private-network-peering-linux-amd64
```

**Nota**: durante l'installazione del plug-in per il sistema operativo Linux, se visualizzi un messaggio di errore che indica un'autorizzazione negata, immetti il seguente comando per modificare le autorizzazioni:

```
chmod a+x ./private-network-peering-linux-amd64
```

### Installa dal repository Bluemix

Completa questa procedura per installare il plug-in dal repository Bluemix:

1. Aggiungi l'endpoint del registro di plug-in Bluemix:
	```
	bluemix plugin repo-add bluemix-bx http://plugins.ng.bluemix.net
	```

2. Immetti il seguente comando:

	```
	bluemix plugin install private-network-peering -r bluemix-bx
	```

## Elenco di comandi per il peering della rete privata
Sono supportati i seguenti comandi. Utilizza il comando `bluemix network` per visualizzare l'elenco di comandi disponibili:

| Comando     | Descrizione                                    |
|-------------|------------------------------------------------|
| pnp-routers | Elenca tutti i router disponibili per il peering        |
| pnp-create  | Crea una connessione peering della rete privata   |
| pnp-delete  | Elimina una connessione peering della rete privata   |
| pnp-show    | Elenca tutte le connessioni peering della rete privata  |
{: caption="Table 1. Private network peering commands" caption-side="top"}


### Utilizzo dei comandi
Per visualizzare le informazioni di guida per i comandi, esegui: `bluemix network [command] -h`.

#### Elenca tutti i router disponibili per il peering
```
bluemix network pnp-routers [--verbose (or -v)]
```

#####Parametri facoltativi
{: #op1}

* **--verbose (or -v)** (indicatore): visualizza le informazioni di rete dettagliate relative a ciascun router.

######Esempio di comando
{: #ex1}

Per visualizzare le informazioni di rete per tutti i router:

	$ bluemix network pnp-routers
	Listing available routers ...
	OK

	IP              NAME            COMPUTE    REGION          ORGANIZATION    SPACE
	129.41.234.246  default-router  Container  US-South        ywu@us.ibm.com  demo1
	129.41.237.172  default-router  Container  US-South        ywu@us.ibm.com  demo2
	129.41.238.212  default-router  Container  United-Kingdom  ywu@us.ibm.com  demo3


Per visualizzare informazioni di rete dettagliate per tutti i router:


	$ bluemix network pnp-routers -v
	Listing available routers ...
	OK

	Router 'bce1aa25-bad0-4cf1-a831-d53c16463d06':
	FIELD          VALUE
	IP             129.41.234.246
	Name           default-router
	Compute        Container
	Region         US-South
	Organization   ywu@us.ibm.com
	Space          demo1
	Networks       172.31.0.0/16

	Router '9ea160f2-1a30-44cd-bd25-794d441b274b':
	FIELD          VALUE
	IP             129.41.237.172
	Name           default-router
	Compute        Container
	Region         US-South
	Organization   ywu@us.ibm.com
	Space          demo2
	Networks       172.25.0.0/16

	...


#### Crea una connessione peering della rete privata utilizzando indirizzi IP
```
bluemix network pnp-create <ip_router> <ip_router> <nome>
```

#####Parametri
{: #p1}

* **ip_router**: gli indirizzi IP dei due router che vuoi connettere. Puoi trovare gli indirizzi IP utilizzando il seguente comando: `bluemix network pnp-routers`
* **nome**: il nome della connessione peering della rete privata.

######Esempio di comando
{: #ex2}

	$ bluemix network pnp-create 129.41.234.246 129.41.237.172 demo
	Creating private network peering connection 'demo' ...
	Connecting 'default-router(129.41.234.246)' and 'default-router(129.41.237.172)' ...
	OK

	Private network peering connection 'demo' created.


####Crea una connessione peering della rete privata utilizzando il nome della connessione

```
bluemix network pnp-create -i <nome>
```

#####Parametri
{: #p2}

* **--interactive (-i)** (indicatore): modalità interattiva per selezionare i router.
* **nome**: il nome della connessione peering della rete privata.

######Esempio di comando
{: #ex3}

	$ bluemix network pnp-create -i demo
	Creating private network peering connection 'demo' ...
	List of available routers (select TWO for peering):

	#  ROUTER                          COMPUTE    REGION          ORGANIZATION    SPACE
	1  default-router(129.41.234.246)  Container  US-South        ywu@us.ibm.com  demo1
	2  default-router(129.41.237.172)  Container  US-South        ywu@us.ibm.com  demo2
	3  default-router(129.41.238.212)  Container  United-Kingdom  ywu@us.ibm.com  demo3

	Select first router for peering> 1
	Select second router for peering> 2

	Connecting 'default-router(129.41.234.246)' and 'default-router(129.41.237.172)' ...
	OK

	Private network peering connection 'demo' created.


#### Elenca tutte le connessioni peering della rete privata
```
bluemix network pnp-show [--verbose (or -v)]
```

#####Parametri facoltativi
{: #op2}

* **--verbose (or -v)** (indicatore): visualizza le informazioni di rete dettagliate relative a ciascun router.

######Esempio di comando
{: #ex4}

Visualizza informazioni di base:

	$ bluemix network pnp-show
	Listing private network peering connections ...
	OK

	ID                                    NAME  STATUS  ROUTER1                         ROUTER2
	17b1c3c7-d614-4fc5-9afe-961e38ee79f8  demo  Active  default-router(129.41.234.246)  default-router(129.41.237.172)

Visualizza informazioni dettagliate:

	$ bluemix network pnp-show -v
	Listing private network peering connections ...
	OK

	Connection 'bedbc077-8040-41cc-a4aa-d9ce09a2e8ec':
	FIELD              VALUE
	Name               demo
	Status             Active
	Router1 Name       default-router
	Router1 IP         129.41.234.246
	Router1 Networks   172.31.0.0/16
	Router2 Name       default-router
	Router2 IP         129.41.237.172
	Router2 Networks   172.25.0.0/16


#### Elimina una connessione peering della rete privata
```
bluemix network pnp-delete [--force (or -f)] <id_connessione>
```
#####Parametri
{: #p3}
* **id_connessione**: uno o più ID di connessione separati da una virgola.

#####Parametri facoltativi
{: #op3}

* **--force (or -f)** (indicatore): elimina la connessione senza richiedere una conferma.

######Esempio di comando:
{: #ex5}

Elimina una connessione:

	$ bluemix network pnp-delete 17b1c3c7-d614-4fc5-9afe-961e38ee79f8
	Warning: deleted connections cannot be restored.
	Are you sure you want to delete the connection? (yes/no)> yes

	Deleting private network peering connection '17b1c3c7-d614-4fc5-9afe-961e38ee79f8' ...
	OK

	Private network peering connection '17b1c3c7-d614-4fc5-9afe-961e38ee79f8' deleted.


Elimina più connessioni:

```
bluemix network pnp-delete [-f] <id_connessione>,<id_connessione>,<id_connessione>
```
