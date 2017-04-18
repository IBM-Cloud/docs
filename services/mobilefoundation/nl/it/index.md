---

copyright:
  years: 2016, 2017
lastupdated:  "2017-02-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introduzione a Mobile Foundation
{: #gettingstartedtemplate}

{{site.data.keyword.mobilefoundation_long}} accelera l'impostazione di un ambiente {{site.data.keyword.mfp_full}} da cui puoi sviluppare, testare e operare applicazioni mobili aziendali. {{site.data.keyword.mobilefoundation_short}} è disponibile con due diversi piani di servizio: Developer e Professional 1 Application.
{:shortdesc}

<!-- The Professional 1 Application plan allows the {{site.data.keyword.mobilefoundation_short}} server to be deployed on a scalable container group.--> Mediante il piano Professional 1 Application è possibile gestire una singola applicazione creata on una o tutte le piattaforme operative supportate quali  Android, iOS, Windows o Web mobili. Il piano Developer <!-- does not support {{site.data.keyword.mobilefoundation_short}} deployment on a container group with more than 1 node. This plan --> è consigliato per lo sviluppo e le operazioni di test.

## Introduzione al piano Mobile Foundation: Developer
{: #gettingstartedtemplate_dev}

Dopo aver creato un'istanza di {{site.data.keyword.mobilefoundation_short}}: Developer, puoi iniziare a creare il tuo canale mobile con pochi clic.

*	Per creare un'istanza del {{site.data.keyword.mobilefirst_notm}} Server con la configurazione predefinita, fai clic su **Avvia server di base**.

  `L'istanza del server di base include un singolo nodo, 1 GB di memoria.`

* Per creare un'istanza del server {{site.data.keyword.mobilefirst_notm}} con la configurazione avanzata per topologia, sicurezza e altra configurazione del server, fai clic su **Avvia server con la configurazione avanzata**. Vedi [Impostazione della configurazione avanzata](c_using_mfs_p1.html#using_mfs_advanced_p1) per ulteriori informazioni.

## Introduzione al piano Mobile Foundation: Professional 1 Application
{: #gettingstartedtemplate_prof}

Dopo che hai creato un'istanza del servizio {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application, puoi iniziare a creare il tuo canale mobile completando la seguente procedura.

1.  Collegamento a un servizio {{site.data.keyword.dashdbshort}} for Transactions esistente su {{site.data.keyword.Bluemix_notm}}.

    1.  Seleziona l'`Organizzazione` {{site.data.keyword.Bluemix_notm}} dove è presente l'istanza del servizio {{site.data.keyword.dashdbshort_notm}}.

    + Seleziona lo `Spazio`  {{site.data.keyword.Bluemix_notm}} in cui è presente l'istanza del servizio {{site.data.keyword.dashdbshort_notm}}, dall'elenco di spazi disponibili nell'`Organizzazione` selezionata.

    + Seleziona il `Nome servizio` {{site.data.keyword.dashdbshort_notm}} e le `Credenziali` per connetterti all'istanza del servizio  {{site.data.keyword.dashdbshort_notm}} esistente.

    + Verifica la connessione all'istanza del servizio {{site.data.keyword.dashdbshort_notm}} for Transactions selezionata facendo clic su **Verifica connessione**.

    + Fai clic su **Aggiungi** e su **Continua** nella finestra a comparsa per confermare il servizio {{site.data.keyword.dashdbshort_notm}} for Transactions selezionato. Questa azione crea le tabelle richieste nell'istanza del servizio database {{site.data.keyword.dashdbshort_notm}} configurato.

    **Nota:** dopo aver aggiunto una connessione {{site.data.keyword.dashdbshort_notm}} all'istanza {{site.data.keyword.mobilefoundation_short}} non ti sarà possibile modificarla.

2.  Crea e avvia il server.

    * Per creare un'istanza del {{site.data.keyword.mobilefirst_notm}} Server con la configurazione predefinita, fai clic su **Avvia server di base**.

      `L'istanza del server di base include un singolo nodo, 1 GB di memoria.`

    * Per creare un'istanza del server {{site.data.keyword.mobilefirst_notm}} con la configurazione avanzata per topologia, sicurezza e altra configurazione del server, fai clic su **Avvia server con la configurazione avanzata**. Vedi [Impostazione della configurazione avanzata](c_using_mfs_p2.html#using_mfs_advanced_p2) per ulteriori informazioni.

## Introduzione al piano Mobile Foundation: Developer Pro
{: #gettingstartedtemplate_devpro}

Dopo che hai creato un'istanza del servizio {{site.data.keyword.mobilefoundation_short}}: Developer Pro,
puoi iniziare a creare il tuo canale mobile completando la seguente procedura.

  1.  Collegamento a un servizio {{site.data.keyword.dashdbshort}} for Transactions esistente su {{site.data.keyword.Bluemix_notm}}.

      1.  Seleziona l'`Organizzazione` {{site.data.keyword.Bluemix_notm}} dove è presente l'istanza del servizio {{site.data.keyword.dashdbshort_notm}}.

      + Seleziona lo `Spazio`  {{site.data.keyword.Bluemix_notm}} in cui è presente l'istanza del servizio {{site.data.keyword.dashdbshort_notm}}, dall'elenco di spazi disponibili nell'`Organizzazione` selezionata.

      + Seleziona il `Nome servizio` {{site.data.keyword.dashdbshort_notm}} e le `Credenziali` per connetterti all'istanza del servizio  {{site.data.keyword.dashdbshort_notm}} esistente.

      + Verifica la connessione all'istanza del servizio {{site.data.keyword.dashdbshort_notm}} for Transactions selezionata facendo clic su **Verifica connessione**.

      + Fai clic su **Aggiungi** e su **Continua** nella finestra a comparsa per confermare il servizio {{site.data.keyword.dashdbshort_notm}} for Transactions selezionato. Questa azione crea le tabelle richieste nell'istanza del servizio database {{site.data.keyword.dashdbshort_notm}} configurato.

      **Nota:** dopo aver aggiunto una connessione {{site.data.keyword.dashdbshort_notm}} all'istanza {{site.data.keyword.mobilefoundation_short}} non ti sarà possibile modificarla.

  2.  Crea e avvia il server.

      * Per creare un'istanza del {{site.data.keyword.mobilefirst_notm}} Server con la configurazione predefinita, fai clic su **Avvia server di base**.

      * Questa selezione fornisce un {{site.data.keyword.mfserver_long_notm}} con le seguenti impostazioni:

          - Singolo nodo con 1 GB di memoria. Questa dimensione è sufficiente per lo sviluppo, per delle attività moderate di test e i carichi di lavoro di produzione su piccola scala.

          -	Il `nome utente` e la `password` ti vengono generati automaticamente. Disporrai dell'accesso ad essi quando il server è avviato e in esecuzione.

      * Per creare un'istanza del server {{site.data.keyword.mobilefirst_notm}} con la configurazione avanzata per topologia, sicurezza e altra configurazione del server, fai clic su **Avvia server con la configurazione avanzata**. Vedi [Impostazione della configurazione avanzata](c_using_mfs_p3.html#using_mfs_advanced_p3) per ulteriori informazioni.

## Introduzione al piano Mobile Foundation: Professional Per Capacity
{: #gettingstartedtemplate_profper}

Dopo che hai creato un'istanza del servizio {{site.data.keyword.mobilefoundation_short}}: Professional Per Capacity, puoi iniziare a creare il tuo canale mobile completando la seguente procedura.

  1.  Collegamento a un servizio {{site.data.keyword.dashdbshort}} for Transactions esistente su {{site.data.keyword.Bluemix_notm}}.

      1.  Seleziona l'`Organizzazione` {{site.data.keyword.Bluemix_notm}} dove è presente l'istanza del servizio {{site.data.keyword.dashdbshort_notm}}.

      + Seleziona lo `Spazio`  {{site.data.keyword.Bluemix_notm}} in cui è presente l'istanza del servizio {{site.data.keyword.dashdbshort_notm}}, dall'elenco di spazi disponibili nell'`Organizzazione` selezionata.

      + Seleziona il `Nome servizio` {{site.data.keyword.dashdbshort_notm}} e le `Credenziali` per connetterti all'istanza del servizio  {{site.data.keyword.dashdbshort_notm}} esistente.

      + Verifica la connessione all'istanza del servizio {{site.data.keyword.dashdbshort_notm}} for Transactions selezionata facendo clic su **Verifica connessione**.

      + Fai clic su **Aggiungi** e su **Continua** nella finestra a comparsa per confermare il servizio {{site.data.keyword.dashdbshort_notm}} for Transactions selezionato. Questa azione crea le tabelle richieste nell'istanza del servizio database {{site.data.keyword.dashdbshort_notm}} configurato.

      **Nota:** dopo aver aggiunto una connessione {{site.data.keyword.dashdbshort_notm}} all'istanza {{site.data.keyword.mobilefoundation_short}} non ti sarà possibile modificarla.

  2.  Crea e avvia il server.

      * Per creare un'istanza del {{site.data.keyword.mobilefirst_notm}} Server con la configurazione predefinita, fai clic su **Avvia server di base**.

      * Questa selezione fornisce un {{site.data.keyword.mfserver_long_notm}} con le seguenti impostazioni:
          -  2 nodi con 1 GB di memoria ognuno. Questa dimensione è buona per lo sviluppo, per delle attività moderate di test e i carichi di lavoro di produzione su piccola scala.

          -	Il `nome utente` e la `password` ti vengono generati automaticamente. Disporrai dell'accesso ad essi quando il server è avviato e in esecuzione.

      * Per creare un'istanza del server {{site.data.keyword.mobilefirst_notm}} con la configurazione avanzata per topologia, sicurezza e altra configurazione del server, fai clic su **Avvia server con la configurazione avanzata**. Vedi [Impostazione della configurazione avanzata](c_using_mfs_p4.html#using_mfs_advanced_p4) per ulteriori informazioni.

Vai a [Using the Mobile Foundation service to set up MobileFirst Server<!-- on IBM Containers--> ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/bluemix/using-mobile-foundation/){: new_window} per ulteriori informazioni introduttive a {{site.data.keyword.mobilefoundation_short}}.

##  Limitazioni note
{: #knownlimitations_mfp}

* La IU del servizio {{site.data.keyword.mobilefoundation_short}} non utilizza il modello specifico della locale selezionato dall'utente per visualizzare i numeri.


# Link correlati
{: #rellinks  notoc}

## Link correlati
{: #general notoc}

*	[Documentazione del prodotto IBM MobileFirst Platform Foundation V8.0.0 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}
*	[IBM MobileFirst Platform Developer Center ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://mobilefirstplatform.ibmcloud.com){: new_window}
