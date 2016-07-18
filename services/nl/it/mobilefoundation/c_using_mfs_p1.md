---

copyright:
  years: 2016

---

#	Utilizzo del piano Developer
{: #using_mobilefoundation_p1}

*Ultimo aggiornamento: 15 giugno 2016*
{: .last-updated}

Dopo aver creato l'istanza del servizio {{site.data.keyword.mobilefoundation_short}}: Developer, accetta i termini della licenza di {{site.data.keyword.mfp_full_notm}} V8.0 per iniziare.
Dopo qualche secondo, puoi accedere alla pagina `Panoramica` su {{site.data.keyword.Bluemix_notm}}, che ti fornisce
le esercitazioni e i video per aiutarti a iniziare a lavorare con il servizio {{site.data.keyword.mobilefoundation_short}}.

## Avvio del server {{site.data.keyword.mobilefirst}}
{: #start_mobilefoundation_p1}
* Per avviare {{site.data.keyword.mfserver_short_notm}} con le impostazioni predefinite, fai clic su **Avvia server di base**.

Questa selezione fornisce un {{site.data.keyword.mfserver_long_notm}} con le seguenti impostazioni:
*	1 GB di memoria e 64 GB di archiviazione. Questa dimensione è sufficiente per lo sviluppo e per delle attività
leggere di test.

*	Il `nome utente` e la `password` ti vengono generati
automaticamente. Disporrai dell'accesso ad essi quando il server è avviato e in esecuzione.

Viene avviato il processo di provisioning. Questo processo impiega circa 10 minuti e una finestra di messaggio
indica l'avanzamento di questa operazione. Al suo completamento, viene visualizzato un dashboard
dove puoi vedere:
*	Lo stato del tuo server in esecuzione (stato, dimensione, archiviazione).

*	La rotta del server creata per te. Utilizza questa rotta per raggiungere il server mobile da
internet pubblico. Le tue applicazioni mobili utilizzano questa rotta per accedere al server.

*	I tuoi `nomeutente` e `password` personali per accedere a {{site.data.keyword.mfp_oc_short_notm}}. La `password` è nascosta. Fai clic su **Mostra password** per visualizzarla.

*	Fai clic su **Avvia console** per avviare {{site.data.keyword.mfp_oc_short_notm}}.


Questa console viene eseguita all'interno del contenitore. Con la console, puoi gestire le tue applicazioni mobili e i tuoi dispositivi mobili, utilizzare il tuo server come un backend mobile, inviare notifiche di push e altro ancora.

## Ricreazione del server {{site.data.keyword.mobilefirst}}
{: #recreate_mobilefoundation_p1}

*	Fai clic su **Ricrea** per ricreare il server.

* Questa azione arresta il tuo server esistente e lo elimina. Tutti i dati nel tuo server mobile vengono persi. Viene creata una nuova istanza del server. Il completamento di questa azione richiede
alcuni minuti.

##	Impostazione della configurazione avanzata
{: #using_mfs_advanced_p1}

Utilizza **Avvia server con la configurazione avanzata** dalla pagina `Panoramica` per creare il server con le impostazioni avanzate o personalizzate. Puoi inoltre
aggiornare le impostazioni del server per personalizzare la tua configurazione server facendo clic sulla scheda
**Configurazione**. {{site.data.keyword.mobilefoundation_short}} ti dà l'accesso ad alcune impostazioni avanzate.

*	Dalla scheda **Topologia**, puoi selezionare la dimensione del tuo contenitore. Il server da 1 GB predefinito è sufficiente per lo sviluppo e una moderata attività di test.

  - Seleziona la dimensione corretta per il tuo server sulla base delle tue necessità.


* **Nodi** visualizza il numero di nodi creati. Questo campo non è modificabile in {{site.data.keyword.mobilefoundation_short}}: Developer. Nel piano Developer, il numero predefinito di nodi nel tuo gruppo di contenitori {{site.data.keyword.IBM_notm}} è **1**.

Fai riferimento alla [documentazione di {{site.data.keyword.mobilefoundation_long}}](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window} per ulteriori dettagli.
