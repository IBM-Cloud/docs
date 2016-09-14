---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Informazioni su {{site.data.keyword.vpn_short}}
{: #vpn_overview}  
*Ultimo aggiornamento: 17 marzo 2016*

Il servizio {{site.data.keyword.vpn_full}} (VPN) fornisce un canale di comunicazione sicuro tra il tuo data center aziendale e le tue risorse nell'ambiente cloud di IBM Bluemix&reg;. La connessione viene stabilita tramite internet.
{:shortdesc}

Il servizio {{site.data.keyword.vpn_short}} fornisce le seguenti funzioni:  
##Sicurezza 
Il servizio IBM VPN utilizza la suite del protocollo IPSec (industry-standard Internet Protocol Security) per autenticare e crittografare la comunicazione IP tra il tuo data center aziendale e le tue risorse nell'ambiente cloud di IBM Bluemix. IPSec fornisce l'autenticazione peer a livello di rete, l'integrità e la riservatezza dei dati (crittografia).

Il servizio IBM VPN supporta i seguenti protocolli e trasformazioni IPSec:

* Algoritmo di autenticazione:
	* HMAC-SHA1-96; la lunghezza della chiave condivisa è 160 bit (predefinito)  
* Algoritmo di crittografia:
	* 3DES-CBC; la lunghezza della chiave condivisa è 192 bit
	* AES-CBC; le lunghezze delle chiavi condivise sono 128 (predefinito), 192, 256 bit
* Protocolli di crittografia e autenticazione:
	* I protocolli Authentication Header (AH) e Encapsulating Security Payload (ESP) sono supportati. AH è utilizzato solo per l'autenticazione. ESP è utilizzato per fornire crittografia e autenticazione.
* Gruppi IKEv1 Diffie-Hellman (DH) Key Exchange 2 (predefinito), 5 e 14

Il servizio IBM VPN supporta la modalità tunnel IPSec. In questa modalità, IPSec protegge l'intero pacchetto IP originale. IPSec crittografa il pacchetto, lo incapsula in un nuovo pacchetto IP e lo inoltra al peer IPSec. 

Il servizio IBM VPN utilizza lo scambio chiavi Diffie-Hellman e la chiave precondivisa per garantire l'associazione tra due peer. L'autenticazione fallisce se una delle due parti non fornisce la chiave precondivisa. 
 
Il servizio IBM VPN è conforme con i seguenti IETF RFC:

* RFCs 2407, 2408 e 2409 per IKEv1
* RFC 4301 per la sicurezza IPv4   
* RFC 4302 per IPv4 Authentication Header  
* RFC 4303 per IPv4 Encapsulating Security Payload (ESP)  
* RFC 2104 HMAC e RFC 2404 HMAC-SHA-1-96 per l'autenticazione  
* RFC 2451 3DES-CBC; RFC 3602 AES128-CBC, AES192-CBC e AES256-CBC per la crittografia
##Semplicità
Puoi creare il servizio IBM VPN utilizzando un'interfaccia grafica intuitiva e semplice. Puoi specificare il tuo indirizzo IP gateway e le tue sottoreti del data center. Puoi utilizzare le politiche IPSec e IKE o personalizzare le politiche per andare incontro ai tuoi bisogni.  
##Gestione
Puoi gestire il servizio IBM VPN utilizzando un'interfaccia grafica, una [interfaccia della riga di comando](../../cli/plugins/vpn/index.html) o le [API](https://new-console.ng.bluemix.net/apidocs/101).

