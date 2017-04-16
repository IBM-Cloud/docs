---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Abilitazione delle notifiche basate sull'utente
{: #user_based_notifications}
Ultimo aggiornamento: 16 gennaio 2017
{: .last-updated}

Le {{site.data.keyword.mobilepushshort}} basate su ID utente sono destinate agli utenti dell'applicazione mobile con messaggi personalizzati. Con le notifiche basate sull'utente, puoi scegliere di inviare la notifica a delle persone specifiche in base alle rispettive preferenze.

## Registrazione del dispositivo con l'ID utente
Per abilitare le notifiche di push indirizzate dall'ID utente, assicurati di aver registrato il dispositivo con un campo ID utente impostato.     

L'ID utente può essere una qualsiasi stringa fornita dall'applicazione all'API di registrazione del dispositivo. Normalmente, un'applicazione mobile prima eseguirà un ciclo di autenticazione in cui l'utente dell'applicazione mobile viene autenticato in un servizio di autenticazione come [{{site.data.keyword.amafull}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html "Icona link esterno"){: new_window}. Dopo la corretta autenticazione, l'ID dell'utente autenticato viene trasmesso all'API Push Device Registration. 

## Sincronizzazione di accesso/disconnessione dell'utente 

Puoi scegliere di inviare le notifiche solo se l'utente ha effettuato l'accesso. 

Ad esempio, prendi in considerazione un dispositivo condiviso dai membri di una famiglia o un team di lavoro e che ci sia bisogno di indirizzare utenti specifici. In questo caso di utilizzo, dovrebbe esserci una sequenza di accesso e disconnessione utente. Questo meccanismo di autenticazione consente alll'applicazione di tracciare l'identità dell'utente presente dell'applicazione. Questo assicura che le notifiche destinate a un'utente specifico siano sempre ricevute solo da tale utente. Dopo un accesso corretto, richiama l'API di registrazione del dispositivo trasmettendo l'ID utente dell'utente che ha eseguito l'accesso. Allo stesso modo, prima della disconnessione, richiama l'API di annullamento della registrazione del dispositivo. La sequenza di queste API push con accesso e disconnessione ti assicurerà che le notifiche pensate per un utente specifico siano inviate solo a tale utente.
