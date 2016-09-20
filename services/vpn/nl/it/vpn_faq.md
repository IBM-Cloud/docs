---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.vpn_short}} Domande frequenti (FAQ)
{: #vpn_faq}
*Ultimo aggiornamento: 17 marzo 2016*

Di seguito sono riportate le domande più frequenti.
{:shortdesc}

1. Quali dispositivi di fornitori di terze parti sono qualificati nei IBM lab per l'interoperabilità con il servizio IBM VPN?

	IBM lab ha verificato i seguenti dispositivi gateway VPN per l'interoperabilità con il servizio IBM VPN :

	* Cisco Adaptive Security Appliance (ASA) Software Versione 8.2(1). [Vedi l'esempio di configurazione](vpn_onpremises.html#cisco) 
	* Brocade Vyatta 5415 vRouter 6.7 R7. [Vedi l'esempio di configurazione](vpn_onpremises.html#vyatta){: new_window}
	* Linux StrongSwan U5.1.2/K3.13.0-55-generic. [Vedi l'esempio di configurazione](vpn_onpremises.html#strongswan){: new_window}
	* Linux StrongSwan U5.2.2/K3.13.0-55-generic. [Vedi l'esempio di configurazione](vpn_onpremises.html#strongswan){: new_window}

	In aggiunta, si ritiene che un dispositivo gateway VPN conforme agli standard IPSec da qualsiasi altro fornitore, funzioni bene con il servizio IBM VPN.

2. Quanto velocemente viene rilevato un peer malfunzionante?
 
	Un peer malfunzionante viene individuato dal valore di timeout keepalive configurato. L'impostazione predefinita è di 60 secondi.

3. Quanti gateway e connessioni VPN posso creare per un servizio VPN?
 
	Puoi creare un'applicazione gateway VPN per servizio VPN in uno spazio Bluemix. Puoi definire fino a 16 connessioni a destinazioni diverse per gateway VPN. 

4. Quando dovrei utilizzare il servizio IBM VPN invece del servizio Bluemix Secure Gateway?

	Entrambi i servizi sono utilizzati per fornire connettività sicura tra le tue risorse Bluemix e il data center in loco. 

	Utilizza il servizio IBM VPN quando ricerchi connettività sicura tra due qualsiasi endpoint. Il sevizio VPN crea una connessione IPSec Layer 3 sicura tra le reti in loco e l'ambiente cloud di IBM Bluemix. Il servizio IBM VPN è disponibile solo per l'accesso sicuro ai contenitori IBM (contenitori Docker). 

	Utilizza il servizio Bluemix Secure Gateway se desideri stabilire una connessione sicura da un endpoint dell'applicazione specifico in Bluemix a un altro endpoint nel tuo data center in loco. 

5. Posso utilizzare il servizio IBM VPN per accedere ai miei contenitori e server virtuali nell'ambiente cloud di IBM Bluemix utilizzando i loro indirizzi IP privati?
 
	Al momento, il servizio IBM VPN è disponibile solo per l'accesso ai contenitori Bluemix.

6. Posso definire il servizio IBM VPN al livello dell'organizzazione Bluemix?

	Al momento, il servizio IBM VPN è disponibile solo al livello dello spazio Bluemix. Se la tua organizzazione Bluemix dispone di più spazi, può quindi essere definito un servizio VPN separato per ogni spazio.

7. Come posso collegare il servizio IBM VPN con il GaaS (SoftLayer Gateway Appliance service)?

	Puoi creare un tunnel IPSec per stabilire una connessione sicura tra il servizio IBM VPN e il SoftLayer GaaS. [Vedi l'esempio di configurazione.](vpn_onpremises.html#gaas){: new_window}
