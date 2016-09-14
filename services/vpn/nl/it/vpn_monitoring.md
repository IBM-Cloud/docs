---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Monitoraggio dello stato e del flusso del traffico
{: #monitor}  
*Ultimo aggiornamento: 17 marzo 2016*  

Utilizza la funzione di monitoraggio per visualizzare lo stato della connessione e la frequenza del flusso del traffico tra il tuo gateway VPN server SoftLayer o in loco e il gateway {{site.data.keyword.vpn_short}}. 
{:shortdesc}  
##Monitoraggio del dashboard del servizio
{: #dashboard}

Seleziona la scheda **Monitoraggio** per visualizzare le seguenti statistiche della connessione.

* **Stato connessione:** lo stato della connessione VPN tra il tuo sistema il tuo gateway VPN server SoftLayer o in loco e il gateway IBM VPN. Valori: 1=UP, -1=DOWN 
* **Frequenza traffico in uscita in byte/secondo e pacchetti/secondo:** la frequenza del traffico dal gateway IBM VPN al tuo gateway VPN server SoftLayer o in loco.  
* **Frequenza traffico in entrata in byte/secondo e pacchetti/secondo:** la frequenza del traffico dal tuo gateway VPN server SoftLayer o in loco al gateway IBM VPN.  

Le statistiche del monitoraggio vengono visualizzate come grafici con i dati delle ultime 48 ore. I grafici vengono automaticamente aggiornati ogni 20 minuti. Tuttavia, puoi recuperare gli ultimi dati in ogni momento uscendo dalla scheda di monitoraggio e ritornandoci.

**Nota:** i grafici utilizzano l'ora UTC (Coordinated Universal Time) e non l'ora locale.  
##Monitoraggio di Logmet
{: #logmet}

Utilizza [Logmet](https://logmet.{DomainName}) per visualizzare le statistiche di connessione dettagliate. 

1. Accedi con le tue credenziali Bluemix e il nome dell'organizzazione e dello spazio in cui hai creato l'istanza del servizio IBM VPN.  
2. Seleziona l'icona cartella (![](images/folder.png)) in lato a destra.
3. Seleziona **Monitoraggio servizio VPN** dall'elenco dei dashboard per visualizzare i grafici. I grafici utilizzano l'ora locale.  

**Nota:** devi selezionare la scheda **Monitoraggio** nel dashboard del servizio IBM VPN almeno una volta per inviare una query a Logmet per creare il dashboard del servizio VPN in Logmet. Logmet impiega fino a 10 minuti, dopo aver stabilito una connessione VPN, per visualizzare le statistiche di connessione.


