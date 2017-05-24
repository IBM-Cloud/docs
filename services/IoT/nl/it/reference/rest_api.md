---

copyright:

years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# API
{: #overview}

Sono disponibili molte API per lo sviluppo del codice per i dispositivi, i gateway e le applicazioni collegate a {{site.data.keyword.iot_full}}.

Le API HTTP sono protette con l'autenticazione di base HTTP. Quando generi una chiave API utilizzando il dashboard, ti vengono presentati un token di autenticazione e una chiave. Per maggiori informazioni, consulta


## API REST HTTP

Dopo la registrazione alla tua propria organizzazione, ti sarà fornito un ID dell'organizzazione di 6 caratteri. Questo ID è obbligatorio nel nome host di tutte le chiamate API, è possibile accedere all'URL di base della tua organizzazione al seguente indirizzo:

https://<**orgId**>.internetofthings.ibmcloud.com/api/v0002/

Per autenticare le richieste nell'API dell'applicazione, imposta in nome utente sulla chiave API e la password sul token di autenticazione.

Per le API di messaggistica, utilizza il seguente indirizzo: https://<**orgId**>.messaging.internetofthings.ibmcloud.com:/api/v0002


## Link API

Utilizza i link nella seguente tabella per trovare ulteriori informazioni sulle API fornite da {{site.data.keyword.iot_short_notm}}.

### API HTTP generali

API                     | Utilizzata per ...       
------------- | -------------
[Organization Administration ![Icona link esterno](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html){: new_window} | Configura un'organizzazione (incluse la creazione e l'eliminazione dei dispositivi), controlla l'utilizzo, lo stato del servizio ed esegue la diagnostica dei problemi di connessione del dispositivo.
[Security ![Icona link esterno](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/security.html){: new_window} | Gestisce l'autenticazione egli inviti utente e l'autorizzazione degli utenti, delle chiavi API e dei dispositivi.
[Information Management ![Icona link esterno](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/info-mgmt.html){: new_window} |  Accede ai dati evento del dispositivo, così come all'ubicazione del dispositivo e ottiene le informazioni sul meteo per tale ubicazione. **Nota:** le informazioni sul meteo sono dipendenti dall'integrazione di The Weather Company.
[The Weather Company ![Icona link esterno](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/info-mgmt.html#!/Device_Location_Weather){: new_window} | Integra i dati da The Weather Company con i tuoi dispositivi esistenti.
[Analytics ![Icona link esterno](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/analytics.html){: new_window} | Crea regole, avvisi e azioni per i dati provenienti da {{site.data.keyword.iot_short_notm}} dai dispositivi.
[Device Management ![Icona link esterno](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/device-mgmt.html){: new_window} | Interagisce con i dispositivi gestiti utilizzando il protocollo di gestione del dispositivo.
[Messaging ![Icona link esterno](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}   | Pubblica gli eventi e invia i comandi utilizzando HTTP. **Nota:** per le API di messaggistica, utilizza l'indirizzo https://<**orgId**>.messaging.internetofthings.ibmcloud.com:/api/v0002



### Estensione API HTTP

API                     | Utilizzata per ...       
------------- | -------------
[AT&T Extension ![Icona link esterno](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-atnt.html){: new_window} | Gestisce i dispositivi AT&T.
[Jasper Extension  ![Icona link esterno](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-jasper.html){: new_window} | Gestisce i dispositivi Jasper.
[Orange Extension  ![Icona link esterno](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-orange.html){: new_window} | Visualizza i dati della SIM card dai dispositivi collegati ala tua organizzazione {{site.data.keyword.iot_short_notm}} e ha una SIM card Orange installata.

### API HTTP beta

API                     | Utilizzata per ...       
------------- | -------------
[Gateway Security  ![Icona link esterno](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html){: new_window}   | Controlla e assegna i ruoli ai dispositivi gateway.
[Device Security  ![Icona link esterno](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-devices-beta.html){: new_window} | Controlla e assegna i ruoli ai dispositivi.
[Interface Mapping  ![Icona link esterno](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html){: new_window}   |   Associa ed accede ai dati del dispositivo utilizzando le interfacce.
