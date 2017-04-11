---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Gestione della sicurezza e del rischio
{: #RM_security}

Puoi migliorare la sicurezza per abilitare la creazione, la definizione e l'invio di notifiche sulla sicurezza della connessione del dispositivo. Con questa sicurezza avanzata, vengono utilizzati i certificati e l'autenticazione TLS (transport layer security) in aggiunta all'utilizzo di token e ID utente utilizzati da {{site.data.keyword.iot_short_notm}} per determinare come e dove i dispositivi si collegano alla piattaforma. Quando i certificati vengono abilitati durante la comunicazione tra i dispositivi e il server, a tutti i dispositivi che non dispongono di certificati validi con l'accesso al server, come configurato nelle impostazioni di sicurezza, non viene consentito l'accesso, anche se utilizzano password e ID utente validi.

## Certificati client
{: #certificates}

Per configurare i certificati client e l'accesso al server per i dispositivi, l'operatore di sistema importa i certificati con autorità di certificazione (CA) e i certificati del server di messaggistica in {{site.data.keyword.iot_short_notm}}. L'analista della sicurezza configura quindi le politiche di sicurezza della connessione in modo che le connessioni tra i dispositivi e la piattaforma utilizzino i livelli di sicurezza Solo certificato o Certificati con token di autenticazione. L'analista può aggiungere diverse politiche per diversi tipi di dispositivo.

Per informazioni su come configurare i certificati, consulta [Configurazione dei certificati](set_up_certificates.html).

## Piani dell'organizzazione e politiche di sicurezza
Le politiche di sicurezza migliorate abilitano le organizzazioni a determinare come desiderano che i dispositivi si collegano e come vengono autenticati con la piattaforma, utilizzando le politiche di connessione e di blacklist e whitelist. Le opzioni della politica di sicurezza disponibili per un'organizzazione dipendono dal tipo di piano dell'organizzazione, nel seguente modo:

**Piano standard:**
- Gli operatori di sistema possono configurare le politiche di connessione con le seguenti opzioni:
    - TLS facoltativo 
    - TLS con autenticazione token
    - TLS con autenticazione certificato client e token

**Piano di sicurezza avanzato (ASP) o piano lite:** 
- Gli operatori di sistema possono configurare le politiche di connessione con le seguenti opzioni:
    - TLS facoltativo 
    - TLS con autenticazione token
    - TLS con autenticazione certificato client
    - TLS con autenticazione certificato client e token
    - TLS con certificato client o token
- Gli operatori di sistema possono configurare le blacklist o whitelist

## Politiche di connessione
{: #connect_policy}

Le politiche di connessione migliorano come i dispositivi si collegano alla piattaforma. Puoi impostare le politiche di connessione predefinite e creare le impostazioni personalizzate per i tipi di dispositivo specifici. La politica può essere impostata per consentire le connessioni non crittografate, per definire solo le connessioni TLS (transport layer security) e per consentire ai dispositivi di autenticarsi con i certificati lato client.

Per informazioni su come configurare le politiche di connessione, consulta [Configurazione delle politiche di sicurezza](set_up_policies.html).

La sicurezza della connessione può anche essere impostata in modo che gli operatori di sistema possono utilizzare i propri certificati del server di messaggistica invece del certificato predefinito fornito. L'utilizzo di un certificato del server di messaggistica può essere utile se i dispositivi dell'utente verranno autenticati per il server durante l'handshake TLS. Sono supportati solo i certificati del server di messaggistica personalizzati che utilizzano lo stesso dominio che utilizza il server di messaggistica IoTP originale (<orgId>.messaging.internetofthings.ibmcloud.com).

## Politiche whitelist e blacklist
{: #wl_bl}

Le politiche whitelist e whitelist forniscono la possibilità di controllare le ubicazioni da cui i dispositivi possono collegarsi all'account dell'organizzazione. Una blacklist identifica tutti gli indirizzi IP, i CIDR o le nazioni a cui non è consentito l'accesso al server, mentre una whitelist fornisce l'accesso esplicito a indirizzi IP specifici.

Per informazioni su come configurare le politiche blacklist e whitelist, consulta [Configurazione delle blacklist e delle whitelist](set_up_policies.html#config_black_white).

## Dashboard di Gestione della sicurezza e del rischio
{: #dashboard}

Infine, l'operatore di sistema e l'analista delle sicurezza possono utilizzare il dashboard di Gestione della sicurezza e del rischio per visualizzare lo stato di sicurezza generale. Le schede nel dashboard posso fornire una panoramica di conformità completa, così come lo stato di connessione dei dispositivi.
