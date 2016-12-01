
---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# Configurazione delle credenziali per il browser web Safari 
{: #configure-credential-for-safari}
Ultimo aggiornamento: 15 novembre 2016
{: .last-updated}

Il servizio IBM {{site.data.keyword.mobilepushshort}} ora estende le funzionalità per inviare le notifiche al tuo browser Safari. 

Assicurati di disporre in un account Apple Developer. Hai bisogno di registrare un ID push sito web e generare un certificato per configurare il tuo browser Safari per ricevere le notifiche. La seguente procedura ti aiuterà ad iniziare.

1. Nel Apple Developer Member center, fai clic su **Certificates, ID & Profiles**. 
2. Fai clic su **Identifiers** e quindi su **Website Push IDs**.
3. Scegli di creare una nuova voce selezionando l'icona più.
  ![Dashboard Push](images/safari_1.jpg)

4. Nel pannello Register Website Push ID, fornisci un ID identificativo e una descrizione Website Push ID appropriati. Ti raccomandiamo che sia nel formato del nome a dominio inverso, e che inizi con 'web'. Ad esempio: web.com.example.dailyweatherreports.
5. Registra l'ID push sito web.
6. Seleziona **Edit** per aggiornare l'ID push sito web.
7. Nella finestra Certificate Assistant per Certificate Information, fornisci il tuo indirizzo email e un nome comune. Lascia l'indirizzo email Certificate Authority vuoto.
8. Fai clic su **Save to disk** e seleziona **Continue**.
9. Scegli di salvare il certificato in una cartella appropriata.

 
