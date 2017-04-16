---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Abilitazione dei webhook 
{: #tag_based_notifications}
Ultimo aggiornamento: 23 gennaio 2017
{: .last-updated}


Con il servizio {{site.data.keyword.mobilepushshort}}, puoi scegliere di ricevere avvisi relativi alle modifiche apportate alle informazioni. Le modifiche alle informazioni aziendali creano degli eventi, per i quali puoi ricevere una notifica registrandoli come eventi webhook. Questi eventi webhook attivano un avviso. 

I webhook sono dei callback definiti dall'utente che vengono attivati da un evento, ad esempio la registrazione di un dispositivo o la sottoscrizione a una tag. Nel servizio {{site.data.keyword.mobilepushshort}}, puoi effettuare la registrazione per i seguenti webhook: 

- **onDeviceRegister**: un evento webhook viene attivato per i dispositivi registrati per il push.
- **onDeviceUpdate**: un evento webhook viene attivato quando vengono aggiornate le informazioni su un dispositivo registrato.
- **onDeviceUnregister**: un evento webhook viene attivato quando viene annullata la registrazione di un dispositivo. 
- **onSubscribe**: un evento webhook viene attivato per la sottoscrizione dell'utente a una tag.
- **onUnsubscribe**: un evento webhook viene attivato per l'annullamento della sottoscrizione dell'utente a una tag.
- **onNotificationSend**: un evento webhook viene attivato per una notifica che è stata inviata.
- **onNotificationFailure**: un evento webhook viene attivato per gli errori di notifica.


**Nota**: gli invii delle notifiche vengono effettuati in batch. L'invio di un messaggio può avere più eventi webhook, che possono includere sia errori che esiti positivi. 
Gli eventi webhook hanno lo stesso messageID del messaggio inviato. 

Per ulteriori informazioni sui webhook, vedi [IBM Push Notifications REST API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://mobile.{DomainName}/imfpush/#/webhooks){: new_window}.
