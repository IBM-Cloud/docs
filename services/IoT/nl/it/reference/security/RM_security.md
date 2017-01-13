---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Gestione della sicurezza e del rischio 
{: #RM_security}
Ultimo aggiornamento: 15 novembre 2016
{: .last-updated}

Il componente Gestione della sicurezza e del rischio consente alle organizzazioni di migliorare la sicurezza di IBM Watson IoT Platform creando, definendo e inviando notifiche sulla sicurezza della connessione del dispositivo. Con questo componente aggiuntivo, vengono utilizzati i certificati e l'autenticazione TLS (transport layer security) invece dell'utilizzo di token e ID utente utilizzati da Watson IoT Platform per determinare come e dove i dispositivi si collegano alla piattaforma. Durante la comunicazione tra i dispositivi e il server, a tutti i dispositivi che non dispongono di certificati validi con l'accesso al server, come configurato nel componente aggiuntivo di gestione della sicurezza e del rischio, non viene consentito l'accesso, anche se utilizzano password e ID utente validi.

**Nota:** per registrarti e per abilitare il programma beta di Gestione della sicurezza e del rischio di IBM Watson IoT Platform, vai all'indirizzo https://developer.ibm.com/iotplatform/2016/11/02/experience-the-latest-iot-security-capabilities-sign-up-to-our-november-beta-today/.

## Politica di sicurezza della connessione

La politica di sicurezza della connessione definisce come i dispositivi si collegano alla piattaforma. Puoi impostare le politiche di connessione predefinite, così come le impostazioni personalizzate per i tipi di dispositivo specifici. La politica può essere impostata per consentire le connessioni non crittografate, per definire solo le connessioni TLS (transport layer security) e per consentire ai dispositivi di autenticarsi con i certificati lato client. Quando vengono utilizzati i certificati lato client, la politica di sicurezza fornisce un'opzione aggiuntiva per utilizzare soltanto il certificato per l'autenticazione client o per utilizzare una combinazione di un certificato client e una coppia di token di autenticazione e ID client.   

La sicurezza della connessione può anche essere impostata per i client in modo che utilizzino il proprio certificato invece del certificato predefinito fornito. Questo può essere utile, ad esempio, se i dispositivi dell'utente verranno autenticati per il server durante l'handshake TLS. In questa release iniziale della Gestione della sicurezza e del rischio il nome del dominio del server di Watson IoT Platform non può essere modificato e deve essere utilizzato nello stato un cui viene fornito nel certificato del server.

## Certificati client 

Per configurare i certificati client e l'accesso al server per i dispositivi, l'operatore di sistema importa i certificati con autorità di certificazione (CA) e i certificati del server di messaggistica nella piattaforma Watson IoT. L'analista della sicurezza configura quindi le politiche di sicurezza della connessione in modo che le connessioni tra i dispositivi e la piattaforma utilizzino i livelli di sicurezza Solo certificato o Certificati con token di autenticazione. L'analista può aggiungere diverse politiche per diversi tipi di dispositivo.

## Politiche whitelist e blacklist

Le politiche whitelist e blacklist forniscono la possibilità di controllare le ubicazioni da cui i dispositivi possono collegarsi all'account dell'organizzazione. Una blacklist identifica tutti gli indirizzi IP, i CIDR o le nazioni a cui non è consentito l'accesso al server, mentre una whitelist fornisce l'accesso esplicito a indirizzi IP specifici.

## Dashboard di Gestione della sicurezza e del rischio

Infine, l'operatore di sistema e l'analista delle sicurezza possono utilizzare il dashboard di Gestione della sicurezza e del rischio per visualizzare lo stato di sicurezza generale. Le schede nel dashboard posso fornire una panoramica di conformità completa, così come lo stato di connessione dei dispositivi.
