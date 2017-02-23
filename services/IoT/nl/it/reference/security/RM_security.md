---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-07"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Gestione della sicurezza e del rischio
{: #RM_security}

Il componente Gestione della sicurezza e del rischio consente alle organizzazioni di migliorare la sicurezza di {{site.data.keyword.iot_full}} creando, definendo e inviando notifiche sulla sicurezza della connessione del dispositivo. Con questo componente aggiuntivo, vengono utilizzati i certificati e l'autenticazione TLS (transport layer security) invece dell'utilizzo di token e ID utente utilizzati da {{site.data.keyword.iot_short_notm}} per determinare come e dove i dispositivi si collegano alla piattaforma. Durante la comunicazione tra i dispositivi e il server, a tutti i dispositivi che non dispongono di certificati validi con l'accesso al server, come configurato nel componente aggiuntivo di gestione della sicurezza e del rischio, non viene consentito l'accesso, anche se utilizzano password e ID utente validi.

## Politica di sicurezza della connessione
{: #connect_policy}

La politica di sicurezza della connessione definisce come i dispositivi si collegano alla piattaforma. Puoi impostare le politiche di connessione predefinite, così come le impostazioni personalizzate per i tipi di dispositivo specifici. La politica può essere impostata per consentire le connessioni non crittografate, per definire solo le connessioni TLS (transport layer security) e per consentire ai dispositivi di autenticarsi con i certificati lato client. Quando vengono utilizzati i certificati lato client, la politica di sicurezza fornisce un'opzione aggiuntiva per utilizzare soltanto il certificato per l'autenticazione client o per utilizzare una combinazione di un certificato client e una coppia di token di autenticazione e ID client.

Per informazioni su come configurare le politiche di connessione, consulta [Configurazione delle politiche di sicurezza](set_up_policies.html).

La sicurezza della connessione può anche essere impostata per i client in modo che utilizzino il proprio certificato invece del certificato predefinito fornito. Questo può essere utile, ad esempio, se i dispositivi dell'utente verranno autenticati per il server durante l'handshake TLS. In questa release iniziale della Gestione della sicurezza e del rischio il nome del dominio del server di {{site.data.keyword.iot_short_notm}} non può essere modificato e deve essere utilizzato nello stato un cui viene fornito nel certificato del server.

## Certificati client
{: #certificates}

Per configurare i certificati client e l'accesso al server per i dispositivi, l'operatore di sistema importa i certificati con autorità di certificazione (CA) e i certificati del server di messaggistica in {{site.data.keyword.iot_short_notm}}. L'analista della sicurezza configura quindi le politiche di sicurezza della connessione in modo che le connessioni tra i dispositivi e la piattaforma utilizzino i livelli di sicurezza Solo certificato o Certificati con token di autenticazione. L'analista può aggiungere diverse politiche per diversi tipi di dispositivo.

Per informazioni su come configurare i certificati, consulta [Configurazione dei certificati](set_up_certificates.html).

## Politiche whitelist e blacklist
{: #wl_bl}

Le politiche whitelist e whitelist forniscono la possibilità di controllare le ubicazioni da cui i dispositivi possono collegarsi all'account dell'organizzazione. Una blacklist identifica tutti gli indirizzi IP, i CIDR o le nazioni a cui non è consentito l'accesso al server, mentre una whitelist fornisce l'accesso esplicito a indirizzi IP specifici.

Per informazioni su come configurare le politiche blacklist e whitelist, consulta [Configurazione delle blacklist e delle whitelist](set_up_policies.html#config_black_white).

## Dashboard di Gestione della sicurezza e del rischio
{: #dashboard}

Infine, l'operatore di sistema e l'analista delle sicurezza possono utilizzare il dashboard di Gestione della sicurezza e del rischio per visualizzare lo stato di sicurezza generale. Le schede nel dashboard posso fornire una panoramica di conformità completa, così come lo stato di connessione dei dispositivi.
