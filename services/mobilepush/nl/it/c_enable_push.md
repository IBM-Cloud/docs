---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Abilitazione delle notifiche per i dispositivi mobili
{: #c_enable_push-notifications}
Ultimo aggiornamento: 18 gennaio 2017
{: .last-updated}

Assicurati di aver consultato [Configurazione delle credenziali per un provider di notifica](t__main_push_config_provider.html).

Questa sezione descrive come abilitare le tue applicazioni client - mobili, browser web e anche le estensioni e le applicazioni Chrome per ricevere notifiche di push e in che modo dettagliato come creare notifiche di base, ottenere e inizializzare l'SDK o il plugin e come registrare il tuo dispositivo o browser per ricevere notifiche di push. Puoi anche abilitare le tue applicazioni mobili o browser web a ricevere notifiche di push utilizzando la [API REST](t_restapi.html).

**Nota**: per le registrazioni del dispositivo, del browser, delle estensioni e delle applicazioni Chrome, il servizio {{site.data.keyword.mobilepushshort}} conserva un riferimento univoco ai token emessi dai provider di notifica -
APNs per Apple o FCM per Google. I token possono essere annullati dal provider di notifica del servizio {{site.data.keyword.mobilepushshort}} per molti motivi. 

Ad esempio, durante la disinstallazione d i un'applicazione sul dispositivo. In questo scenario, quando viene tentato l'invio di una notifica in base ai provider, la risposta del dispositivo viene annullata, il servizio {{site.data.keyword.mobilepushshort}} rimuoverà le registrazioni del dispositivo o del browser web. Ciò impedirà i seguenti tentativi di invio della notifica ai dispositivi annullati.
