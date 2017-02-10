---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Inviare le notifiche di base alle estensioni e alle applicazioni Chrome 
{: #web_extensions_notifications}
Ultimo aggiornamento: 11 gennaio 2017
{: .last-updated}

Dopo che hai sviluppato le tue applicazioni, puoi inviare una notifica push. 

1. Seleziona **Send Notifications** e componi un messaggio scegliendo **Web Notifications** come l'opzione **Send To**. 
2. Immetti il messaggio che deve essere consegnato nel campo **Message**.
3. Puoi scegliere di fornire delle impostazioni facoltative:
  - **Titolo della notifica**: questo è il testo che deve essere visualizzato nell'intestazione dell'avviso del messaggio.
  - **URL dell'icona di notifica**: se il tuo messaggio deve essere consegnato con un'icona di notifica dell'applicazione, fornisci il link alla tua icona nel campo.
  - **Chiave di compressione**:  le chiavi di compressione solo allegate alle notifiche. Se più notifiche arrivano in sequenza con la stessa chiave di compressione quando il dispositivo è offline, esse vengono compresse. Quando un dispositivo va online, riceve le notifiche dal server FCM/GCM e visualizza solo l'ultima notifica rilevando la stessa chiave di compressione. Se la chiave di compressione non viene inviata, sia il nuovo che il vecchio messaggio vengono archiviati per una consegna successiva.
  - **TTL (Time to live)**: questo valore è impostato in secondi. Se questo parametro non viene specificato, il server FCM/GCM archivia il messaggio per quattro settimane e tenterà di consegnarlo. La validità scade dopo quattro settimane. L'intervallo di valori possibile è compreso tra 0 e 2,419,200 secondi.
  - **Ritarda quando inattivo**: impostando questo valore su `true` si danno istruzioni al server FCM/GCM di non consegnare la notifica se il dispositivo è inattivo. Imposta questo valore su `false`, per assicurati di consegnare la notifica anche se il dispositivo è inattivo.
  - **Payload addizionale**: specifica i valori di payload personalizzati per le tue notifiche.

La seguente immagine mostra l'opzione delle notifiche alle estensioni e applicazioni Chrome nel dashboard.

  ![Schermata notifiche](images/push_chrome_extns.jpg)
  
## Fasi successive
  {: #next_steps_tags}

Dopo che hai correttamente configurato le notifiche di base, puoi scegliere di configurare le notifiche basate sulle tag e le opzioni avanzate.

Aggiungi queste funzioni del servizio {{site.data.keyword.mobilepushshort}} alla tua applicazione. Per utilizzare le notifiche basate sulle tag, vedi [Notifiche basate sulle tag](c_tag_basednotifications.html). Per utilizzare le opzioni di notifica avanzate, vedi [Notifiche avanzate](t_advance_badge_sound_payload.html).
