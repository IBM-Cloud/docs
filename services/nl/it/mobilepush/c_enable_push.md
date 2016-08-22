---

copyright:
 years: 2015, 2016

---

# Abilitazione delle notifiche
{: #c_enable_push-notifications}
*Ultimo aggiornamento: 14 giugno 2016*
{: .last-updated}

Puoi abilitare le applicazioni a ricevere e inviare le notifiche di push ai tuoi dispositivi.

Questa sezione descrive come abilitare le tue applicazioni mobili per ricevere notifiche di push e in che modo dettagliato come creare notifiche di base, ottenere e inizializzare l'SDK o il plugin e come registrare il tuo dispositivo per ricevere notifiche di push. Puoi anche abilitare le tue applicazioni mobili a ricevere notifiche di push utilizzando la [API REST](t_restapi.html).

Nota: per le registrazione dei dispositivi con il push, il Push Notification service conserva un riferimento univoco ai token emessi dai provider di notifica -
APNS per Apple o GCM per Google. I token possono essere annullati dal provider di notifica del Push Notification service per molti motivi. 

Ad esempio, durante la disinstallazione dell'applicazione sul dispositivo. In questo scenario, quando viene tentato l'invio di una notifica in base ai provider, la risposta del dispositivo viene annullata, il Push Notification service rimuoverà le registrazioni del dispositivo. Ciò impedirà i seguenti tentativi di invio della notifica ai dispositivi annullati.
