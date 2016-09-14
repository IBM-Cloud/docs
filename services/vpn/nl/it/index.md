---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Introduzione a {{site.data.keyword.vpn_short}}
{: #vpn}  
*Ultimo aggiornamento: 9 maggio 2016*

Il servizio {{site.data.keyword.vpn_full}} per Bluemix&reg; è disponibile per l'accesso sicuro a IBM Containers (contenitori Docker) nell'ambiente cloud IBM Bluemix. Puoi utilizzare l'ambiente cloud IBM Bluemix come un'estensione del tuo data center aziendale. Puoi inoltre collegarti con i server SoftLayer utilizzando il servizio IBM VPN.
{:shortdesc}

Prima di iniziare, assicurati di avere un contenitore IBM Docker pronto per l'utilizzo. Consulta [IBM Containers for Bluemix](https://www.ng.bluemix.net/docs/containers/container_index.html) per i dettagli su come creare e gestire IBM Containers.  

Per iniziare, seleziona il tile dell'istanza del servizio **VPN (Virtual Private Network)** nel dashboard Bluemix. Completa la seguente procedura:

1. Configura il gateway {{site.data.keyword.vpn_short}} selezionando **CREA GATEWAY**. Viene creato un gateway predefinito. Se necessario, modifica la configurazione del gateway come mostrato nei seguenti passi.  
{: #gateway}  

  1. Seleziona **MODIFICA**.  
  2. Specifica il nome del gateway.  
  3. Seleziona il contenitore e il gruppo di contenitori con cui vuoi utilizzare il servizio VPN.
	**Nota:** i sottoinsiemi privati di contenitori e gruppi di contenitori sono preselezionati per consentirti così di accedere a essi sulla connessione VPN.
  4. Seleziona **SALVA**.  

 Puoi utilizzare le politiche IKE e IPSec predefinite o configurare delle politiche personalizzate. Se desideri utilizzare le politiche predefinite, vai al passo 4.

2. Configura la politica IKE selezionando la scheda **Politiche IKE & IPSec**.
  1. Seleziona **AGGIUNGI NUOVA**.  
  2. Specifica i seguenti dettagli:
	* **Nome**: Nome della politica IKE
	* **Algoritmo di autorizzazione**: sha1; non può essere modificato  
	* **Algoritmo di crittografia**: Seleziona dal menu a discesa. Valori: aes-128 (predefinito), aes-192, aes-256, 3des
	* **Durata della chiave**: Il valore di durata (in secondi) dell'associazione di sicurezza IKE. Intervallo: 60-86400. Valore predefinito: 86400
	* **PFS**: Identificativo del gruppo DH (Diffie-Hellman). Valori: Group2, Group5, Group14. Valore predefinito: Group2
	* **Modalità di negoziazione**: Main; non può essere modificata
	* **Versione**: IKEV1; non può essere modificata
  3. Seleziona **SALVA**.

3. Configura la politica IPSec:
  1. Seleziona **AGGIUNGI NUOVA**.  
  2. Specifica i seguenti dettagli:
  	* **Nome**: Nome della politica IPSec  
  	* **Algoritmo di autorizzazione**: sha1; non può essere modificato  
  	* **Algoritmo di crittografia**: Seleziona dal menu a discesa. Valori: aes-128 (predefinito), aes-192, aes-256, 3des
  	* **Durata della chiave**: Il valore di durata (in secondi) dell'associazione di sicurezza. Intervallo: 60-86400. Valore predefinito: 3600
  	* **PFS**: Identificativo del gruppo DH (Diffie-Hellman). Valori: Group2, Group5, Group14. Valore predefinito: Group2
  	* **Protocollo di trasformazione**: ESP; non può essere modificato
  	* **Modalità di incapsulamento**: Tunnel; non può essere modificata
  3. Seleziona **SALVA**.  

4. Fornisce i dettagli per stabilire una connessione tra il tuo data center o il tuo gateway VPN server SoftLayer e il gateway IBM VPN.  
{: #site}  

  1. Seleziona la scheda **Applicazione gateway**.
  2. Seleziona **Crea connessione** nella sezione **Connessioni sito**.
  3. Specifica i seguenti dettagli di connessione al sito:  
  	* **Nome**: Nome della connessione  
  	* **Descrizione**: Descrizione della connessione (facoltativa)  
  	* **Stringa chiave precondivisa**: Chiave (segreto) precondivisa da utilizzare per l'autenticazione
  	* **Stato ammin**: Stato della connessione VPN. Seleziona dall'elenco a discesa: UP o DOWN. Valore predefinito: UP  
  	* **IP gateway cliente**: Indirizzo IP endpoint remoto del tunnel VPN  
  	* **Sottorete cliente**: Indirizzo di sottorete remoto nel formato CIDR. Seleziona il segno più per aggiungere un altro sottoinsieme.
  4. (Facoltativo) Configura i seguenti parametri delle **Impostazioni avanzate**:  
  	* **Politica IKE**: Seleziona la politica IKE.  
  	* **Intervallo keepalive**: Intervallo keepalive in secondi. Invia i messaggi keepalive all'intervallo configurato per controllare lo stato di attività del peer. Valore predefinito: 15. Intervallo: 5-86399
  	* **Azione per peer inattivo**: Azione da intraprendere quando il peer viene individuato come inattivo.  
    	Valori: 
  		* hold (valore predefinito): l'associazione di sicurezza (SA) viene impostata su hold 
  		* clear: la SA viene eliminata
  		* disabled: la SA viene disabilitata
  		* restart: la SA viene rinegoziata
  		* restart-by-peer: tutte le SA con il peer inattivo vengono rinegoziate  
  	* **Politica IPSec**: Seleziona la politica IPSec.
  	* **Timeout keepalive**: Valore di timeout in secondi dopo il quale la sessione viene terminata. Valore predefinito: 120. Intervallo: 6-86400. Il valore di timeout keepalive deve essere maggiore del valore dell'intervallo keepalive.
  5. Seleziona **SALVA**.

  **Nota:** quando sta venendo stabilita la connessione, lo stato della connessione viene visualizzato come ***pending create***. Quando vedi questo stato, aggiorna la schermata alcune volte per visualizzare lo stato attivo della connessione.

**Importante:** se stai utilizzando un'applicazione web, devi eseguire il bind dall'applicazione web al contenitore Docker che stai utilizzando. Questo bind è necessario in modo che il traffico passi per il tunnel IPSec VPN.

**Importante:** il servizio IBM VPN al momento opera in modalità di risposta. Per iniziare la connessione VPN, deve essere emesso un pacchetto dati dal gateway IBM VPN sul tuo data center o server SoftLayer in loco. Una volta che è stata stabilita la connessione VPN, il traffico può fluire in entrambe le direzioni tra gli endpoint della connessione VPN.

 
# rellinks
## samples 
{: #samples}  
* [Esempio di configurazione gateway strongSwan in loco](vpn_onpremises.html#strongswan){: new_window}
* [Esempio di configurazione gateway Vyatta in loco](vpn_onpremises.html#vyatta){: new_window}
* [Esempio di configurazione GaaS (SoftLayer Gateway Appliance Service) in loco](vpn_onpremises.html#gaas){: new_window}
* [Esempio di configurazione Cisco ASA in loco](vpn_onpremises.html#cisco){: new_window}

## api  
{: #api}  
* [IBM VPN RESTful APIs](https://new-console.ng.bluemix.net/apidocs/101){: new_window}

## general  
{: #general}  
* [IBM VPN Command line Interface](../../cli/plugins/vpn/index.html){: new_window}
* [IBM VPN FAQs](vpn_faq.html#vpn_faq){: new_window}
* [IBM Bluemix Pricing Sheet](https://console.{DomainName}/pricing/){: new_window}
* [IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs)
