---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connessione alle applicazioni

Per collegare la tua applicazione a {{site.data.keyword.iot_full}}, devi collegarla utilizzando i token o le chiavi API oppure eseguirne il bind direttamente a {{site.data.keyword.iot_short_notm}} in {{site.data.keyword.Bluemix_notm}}. Utilizza il dashboard di accesso per concedere l'accesso.
{:shortdesc}

## Connessione chiave API
{: #api-key}
Le chiavi API sono utilizzate durante il collegamento delle applicazioni alla tua organizzazione {{site.data.keyword.iot_short_notm}}. Le applicazioni richiedono un chiave API per collegarsi all'organizzazione e un token di autenticazione univoco che deve essere utilizzato con tale chiave API.  

Per ulteriori informazioni sulle connessioni dell'applicazione, consulta [Connettività MQTT per le applicazioni ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.internetofthings.ibmcloud.com/applications/mqtt.html){: new_window} nella documentazione dello sviluppatore.

Per creare una nuova coppia di chiave API e token di autenticazione:  
1.	Nel dashboard {{site.data.keyword.iot_short_notm}}, vai a **Apps > API Keys**.  
2.	Fai clic su **Generate API Key**.  
**Importante:** prendi nota della coppia di chiave API e token. I token di autenticazione non sono ripristinabili. Se perdi o dimentichi questo token, dovrai registrare nuovamente la chiave API per generare un nuovo token di autenticazione.
 - Un esempio di una chiave API è `a-organization_id-a84ps90Ajs`  
 - Un esempio di un token è `MP$08VKz!8rXwnR-Q*`  
3.	Aggiungi un commento per identificare la chiave API nel dashboard, ad esempio: Chiave per collegare la mia applicazione.
4.	Fai clic su **Finish**.



## Connessione bind Bluemix
{: #bluemix-binding}
Puoi eseguire il bind delle applicazioni alla tua organizzazione {{site.data.keyword.iot_short_notm}} da {{site.data.keyword.Bluemix_notm}}. Eseguendo il bind dell'applicazione, è possibile soltanto comunicare con le istanze del servizio nello stesso spazio o organizzazione. Puoi trovare tutti i dati necessari perché l'applicazione comunichi con l'istanza del servizio nella variabile di ambiente VCAP_SERVICES. Se la tua applicazione è associata a più servizi, la variabile VCAP_SERVICES include le informazioni di connessione per ciascuna istanza di servizio.  

Tuttavia, puoi utilizzare le istanze del servizio da altri spazi o organizzazioni nello stesso modo di un'applicazione esterna. Invece di creare un bind, utilizza le credenziali per configurare direttamente la tua istanza dell'applicazione. Per ulteriori informazioni, consulta [Richiesta di una nuova istanza del servizio](https://console.{DomainName}/docs/services/reqnsi.html#req_instance) nella documentazione {{site.data.keyword.Bluemix_notm}}.

Per visualizzare i dettagli delle applicazioni Bluemix associate all'istanza del servizio Bluemix associata alla tua organizzazione, vai a **Apps > Bluemix Apps**.  
