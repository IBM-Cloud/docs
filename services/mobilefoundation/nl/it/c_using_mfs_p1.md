---

copyright:
  years: 2016

---

#	Utilizzo del piano Developer
{: #using_mobilefoundation_p1}

Ultimo aggiornamento: 04 agosto 2016
{: .last-updated}

Dopo aver creato {{site.data.keyword.mobilefoundation_short}}: istanza del servizio dello sviluppatore, in pochi secondi, puoi accedere alla pagina `Panoramica` in {{site.data.keyword.Bluemix_notm}}, la quale ti fornisce le esercitazioni e i video di aiuto per iniziare ad utilizzare il servizio  {{site.data.keyword.mobilefoundation_short}}.

## Avvio del server {{site.data.keyword.mobilefirst}}
{: #start_mobilefoundation_p1}
* Per avviare {{site.data.keyword.mfserver_short_notm}} con le impostazioni predefinite, fai clic su **Avvia server di base**.

Questa selezione fornisce un {{site.data.keyword.mfserver_long_notm}} con le seguenti impostazioni:
*	1 GB di memoria. Questa dimensione è sufficiente per lo sviluppo, per delle attività leggere di test e i carichi di lavoro di produzione su piccola scala. 

*	Il `nome utente` e la `password` ti vengono generati
automaticamente. Disporrai dell'accesso ad essi quando il server è avviato e in esecuzione.

Viene avviato il processo di provisioning. Questo processo impiega circa 10 minuti e una finestra di messaggio
indica l'avanzamento di questa operazione. Al suo completamento, viene visualizzato un dashboard
dove puoi vedere:
*	Lo stato del tuo server in esecuzione (stato, dimensione).

*	La rotta del server creata per te. Utilizza questa rotta nella tua applicazione mobile per collegarti a {{site.data.keyword.mfserver_short_notm}}.

*	I tuoi `nomeutente` e `password` personali per accedere a {{site.data.keyword.mfp_oc_short_notm}}. La `password` è nascosta. Fai clic sull'icona **Mostra password** per visualizzarla.

*	Fai clic su **Avvia console** per avviare {{site.data.keyword.mfp_oc_short_notm}}.


<!--This console runs inside the container.--> Con la console, puoi gestire le tue applicazioni mobili e i tuoi dispositivi mobili, utilizzare il tuo server come un backend mobile, inviare notifiche di push e altro ancora.

## Ricreazione del server {{site.data.keyword.mobilefirst}}
{: #recreate_mobilefoundation_p1}

*	Fai clic su **Ricrea** per ricreare il server.

* Questa azione arresta il tuo server esistente e elimina i dati. Tutti i dati nel tuo server mobile vengono persi. Viene creata una nuova istanza del server con una versione aggiornata, se disponibile. Il completamento di questa azione richiede
alcuni minuti.

##	Impostazione della configurazione avanzata
{: #using_mfs_advanced_p1}

Utilizza **Avvia server con la configurazione avanzata** dalla pagina `Panoramica` per creare il server con le impostazioni avanzate o personalizzate. Puoi inoltre
aggiornare le impostazioni del server per personalizzare la tua configurazione server facendo clic sulla scheda
**Configurazione**. {{site.data.keyword.mobilefoundation_short}} ti dà l'accesso ad alcune impostazioni avanzate.

*	Dalla scheda **Topologia**, puoi selezionare la dimensione del server e il numero di istanze di cui hai bisogno. Il server da 1 GB predefinito è sufficiente per lo sviluppo e una moderata attività di test.

  - Seleziona la dimensione corretta per il tuo server sulla base delle tue necessità.

* **Nodi** visualizza il numero di nodi creati. Questo campo non è modificabile in {{site.data.keyword.mobilefoundation_short}}: Developer. Il numero di nodi <!--in your {{site.data.keyword.IBM_notm}} container group--> è predefinito **1** nel piano Developer.

Fai riferimento alla [documentazione di {{site.data.keyword.mobilefoundation_long}}](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window} per ulteriori dettagli.
