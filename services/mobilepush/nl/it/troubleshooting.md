---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Risoluzione dei problemi
{: #errors}
Ultimo aggiornamento: 11 gennaio 2017
{: .last-updated}

Utilizza questa sezione come una guida per risolvere i problemi comuni di {{site.data.keyword.mobilepushshort}}.


### Si è verificato un errore server interno. Per favore contatta l'amministratore. (Codice errore interno: PUSHD102E)

**Spiegazione**: questo errore potrebbe verificarsi se hai creato un'istanza di push prima del novembre 2015.  

**Risposta utente**: per risolvere il problema, elimina l'istanza di push e creane una nuova. Nota che quando elimini l'istanza di push, le tue tag non vengono conservate.


### Registrazione non autorizzata

**Spiegazione**: Chrome Web Push non funziona con le chiavi FCM (Firebase Cloud Messaging). Se non puoi ricevere le notifiche push web su Chrome dopo lo spostamento a FCM da GCM, questo succede perché il sito web era stato precedentemente configurato per utilizzare il progetto GCM mentre il nuovo progetto è stato creato in FCM. I token generati che identificano il browser vengono memorizzati nella cache dal browser Chrome.

**Risposta utente**: puoi risolvere questo problema rimuovendo i cookie e reimpostando le autorizzazioni del browser. Questo richiederà alle autorizzazioni di abilitare Push Notifications. 


### I worker del servizio non sono supportati in questo browser

**Spiegazione**: l'SDK che era stato incluso come parte di `BMSPushSDK.js` mediante il worker del servizio non è disponibile. 

**Risposta utente**: si consiglia di passare a un browser che supporti il worker del servizio. Le versioni supportate dei browser sono Firefox versione 49 o successive e Chrome versione 53 (64 bit) o successive.


### SecurityError: l'operazione non è sicura

**Spiegazione**:  si potrebbe visualizzare l'errore durante l'abilitazione della console web in Firefox. Il supporto push web nel servizio Push Notification richiede l'accesso al sito web tramite il protocollo `https` invece di `http`.

**Risposta utente**: si consiglia di provare a connettersi al sito web utilizzando il protocollo `https` dal browser.

