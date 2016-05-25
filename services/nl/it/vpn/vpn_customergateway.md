---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configurazione del gateway nel tuo data center o server SoftLayer
{: #vpn_yourdatacenter}
*Ultimo aggiornamento: 17 marzo 2016*

Hai bisogno di un gateway IPSec VPN nel tuo data center o server SoftLayer per creare una connessione sicura con il servizio {{site.data.keyword.vpn_short}}. Le seguenti configurazioni del gateway VPN sono necessarie nel tuo data center o server SoftLayer:

* Abilita NAT (Network Address Translation) traversal solo nel tuo gateway VPN se è protetto da NAT. 
* Utilizza la stessa chiave precondivisa utilizzata durante la configurazione del servizio IBM VPN.
* Aggiungi la seguente sottorete come sottorete remota:
	* Se hai creato dei contenitori singoli nello spazio IBM Bluemix, aggiungi 172.31.0.0/16.
	* Se hai creato dei gruppi di contenitori nello spazio IBM Bluemix, aggiungi 172.30.0.0/16.
	* Se hai creato dei contenitori singoli e dei gruppi di contenitori nello spazio IBM Bluemix, aggiungi 172.31.0.0/16 e 172.30.0.0/16.
* Verifica che la crittografia, l'autenticazione e le impostazioni del gruppo PFS siano le stesse del gateway IBM VPN gateway nel tuo gateway VPN.
