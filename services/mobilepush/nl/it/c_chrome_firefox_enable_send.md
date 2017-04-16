---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Invio di notifiche di base ai browser web
{: #web_notifications}
Ultimo aggiornamento: 11 gennaio 2017
{: .last-updated}

Dopo che hai sviluppato le tue applicazioni, puoi inviare una notifica push. 

1. Seleziona **Send Notifications** e componi un messaggio scegliendo **Web Notifications** come l'opzione **Send To**. 
2. Immetti il messaggio che deve essere consegnato nel campo **Message**.
3. Puoi scegliere di fornire delle impostazioni facoltative:
  - **Titolo della notifica**: questo è il testo che deve essere visualizzato nell'intestazione dell'avviso del messaggio.
  - **URL dell'icona di notifica**: se il tuo messaggio deve essere consegnato con un'icona di notifica dell'applicazione, fornisci il link alla tua icona nel campo.
  - **TTL (Time to live)**: notifica al server in merito alla validità dei messaggi.
4. Per le notifiche web inviate al browser Safari, sono richieste delle informazioni aggiuntive:
  - **Azione**: si tratta dell'etichetta del pulsante di azione.
  - **Argomenti URL**: gli argomenti URL che devono essere utilizzati con questa notifica. Assicurati che vengano forniti in forma di array JSON. 
 
La seguente immagine mostra l'opzione delle notifiche web nel dashboard.

  ![Schermata notifiche](images/DashboardWebpush.jpg)


## Fasi successive
  {: #next_steps_tags}

Dopo che hai correttamente configurato le notifiche di base, puoi scegliere di configurare le notifiche basate sulle tag e le opzioni avanzate.

Aggiungi queste funzioni del servizio {{site.data.keyword.mobilepushshort}} alla tua applicazione. Per utilizzare le notifiche basate sulle tag, vedi [Notifiche basate sulle tag](c_tag_basednotifications.html). Per utilizzare le opzioni di notifica avanzate, vedi [Notifiche avanzate](t_advance_badge_sound_payload.html).



