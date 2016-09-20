---

Titolo: Abilitazione basata sull'utente di Push Notifications 

Parole chiavi: Push Notifications basato sull'utente, ID utente
copyright:
 years: 2015, 2016

---

# Abilitazione delle notifiche basate sull'utente
{: #user_based_notifications}
Ultimo aggiornamento: 16 agosto 2016
{: .last-updated}

Le {{site.data.keyword.mobilepushshort}} basate su ID utente sono destinate agli utenti dell'applicazione mobile con messaggi personalizzati. Le notifiche basate sull'utente possono coinvolgere utenti specifici a sfruttare i vantaggi delle proprie preferenze e scelte personali.  

## Registrazione del dispositivo con l'ID utente
Per abilitare le notifiche di push indirizzate dall'ID utente, assicurati di aver registrato il dispositivo con un ID utente e inoltre di passare il 'clientSecret' assegnato quando viene eseguito il provisioning dei servizi {{site.data.keyword.mobilepushshort}}. La registrazione del dispositivo avrà esito negativo senza un 'clientSecret' valido.  

L'ID utente può essere una qualsiasi stringa fornita dall'applicazione all'API di registrazione del dispositivo. Normalmente, un'applicazione mobile prima eseguirà un ciclo di autenticazione in cui l'utente dell'applicazione mobile viene autenticato in un servizio di autenticazione come [{{site.data.keyword.amafull}}](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html). Dopo la corretta autenticazione, l'ID dell'utente autenticato viene trasmesso all'API Push Device Registration con un 'clientSecret'.  La presenza di un 'clientSecret' impone solo l'associazione autorizzata di ID utente con le registrazioni del dispositivo mobile.

Mantieni il 'clientSecret' confidenziale e non inserirlo mai nell'applicazione mobile. Esistono vari modelli di inizializzazione dell'applicazione che possono essere utilizzati per estrarre il 'clientSecret' dinamicamente durante il runtime dell'applicazione. Il diagramma della sequenza illustra questo modello.

![Enable_Push](images/init_client_secret.jpg) 

Puoi anche registrare un dispositivo in modo che sia associato con un utente 'anonimo'. Questo richiede che utilizzi una variante dell'API di registrazione del dispositivo che non richiede gli argomenti ID utente e 'clientSecret'.   

## Sincronizzazione di accesso/disconnessione e abilitazione delle notifiche push. 

Puoi scegliere di inviare le notifiche solo se l'utente ha effettuato l'accesso. 

Ad esempio, se un dispositivo è condiviso da una famiglia o da un team di lavoro e hai bisogno di indirizzare utenti specifici nella famiglia o nel team.  In questo caso di utilizzo, dovrebbe esserci una sequenza di accesso e disconnessione utente che sorveglia l'applicazione tracciando l'identità dell'utente presente dell'applicazione. Per assicurarti che le notifiche destinate a un'utente specifico siano sempre ricevute solo da tale utente, dopo un accesso corretto, richiama l'API di registrazione del dispositivo trasmettendo l'ID utente dell'utente che ha eseguito l'accesso. Allo stesso modo, prima della disconnessione, richiama l'API di annullamento della registrazione del dispositivo. La sequenza di queste API push con accesso e disconnessione ti assicurerà che le notifiche push pensate per un utente specifico siano inviate solo a tale utente.
