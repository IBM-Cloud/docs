---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introduzione a {{site.data.keyword.mobilefoundation_short}}
{: #gettingstartedtemplate}

*Ultimo aggiornamento: 15 giugno 2016*
{: .last-updated}

{{site.data.keyword.mobilefoundation_long}} accelera l'impostazione di un ambiente {{site.data.keyword.mfp_full}} da cui puoi sviluppare, testare e operare applicazioni mobili aziendali. {{site.data.keyword.mobilefoundation_short}} è disponibile con due diversi piani di servizio: Developer e Professional 1 Application.
{:shortdesc}

Il piano Professional 1 Application consente di distribuire il server {{site.data.keyword.mobilefoundation_short}} in un gruppo di contenitori scalabile. Mediante il piano Professional 1 Application è possibile gestire una singola applicazione creata in una o tutte le piattaforme operative supportate quali  Android, iOS, Windows o Web mobili. Il piano Developer non supporta la distribuzione di {{site.data.keyword.mobilefoundation_short}} su un gruppo di contenitori con più di 1 nodo. Questo piano è consigliato per lo sviluppo e le operazioni di test. 

## Introduzione al piano {{site.data.keyword.mobilefoundation_short}}: Developer

Dopo aver creato un'istanza di {{site.data.keyword.mobilefoundation_short}}: Developer, puoi iniziare a creare il tuo canale mobile con pochi clic.

*	Per creare un'istanza del {{site.data.keyword.mobilefirst_notm}} Server con la configurazione predefinita, fai clic su **Avvia server di base**.

  `L'istanza del server di base include un singolo nodo,
1 GB di memoria e 64 GB di capacità di archiviazione.`

* Per creare un'istanza del server {{site.data.keyword.mobilefirst_notm}} con la configurazione avanzata per topologia, sicurezza e altra configurazione del server, fai clic su **Avvia server con la configurazione avanzata**. Vedi [Impostazione della configurazione avanzata](c_using_mfs_p1.html#using_mfs_advanced_p1) per ulteriori informazioni.

## Introduzione al piano {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application

Dopo che hai creato un'istanza del servizio {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application, puoi iniziare a creare il tuo canale mobile completando la seguente procedura.

1.  Connettiti a un servizio {{site.data.keyword.dashdbshort}}: Enterprise Transactional esistente su {{site.data.keyword.Bluemix_notm}}.

    1.  Seleziona lo `Spazio`  {{site.data.keyword.Bluemix_notm}} in cui è presente l'istanza del servizio {{site.data.keyword.dashdbshort_notm}}, dall'elenco di spazi disponibili nell'`Organizzazione` corrente.

    2.  Seleziona il `Nome servizio` {{site.data.keyword.dashdbshort_notm}} e le `Credenziali` per connetterti all'istanza del servizio  {{site.data.keyword.dashdbshort_notm}} esistente. 

    3.  Verifica la connessione all'istanza del servizio  {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional selezionata facendo clic su **Verifica connessione**.

    4.  Fai clic su **Aggiungi** e poi su **Continua** nella finestra a comparsa che richiede la conferma sul servizio {{site.data.keyword.dashdbshort_notm}} selezionato. Questa azione crea le tabelle richieste nell'istanza del servizio database {{site.data.keyword.dashdbshort_notm}} configurato.

2.  Crea e avvia il server.

    * Per creare un'istanza del {{site.data.keyword.mobilefirst_notm}} Server con la configurazione predefinita, fai clic su **Avvia server di base**.

      `L'istanza del server di base include un singolo nodo,
1 GB di memoria e 64 GB di capacità di archiviazione.`

    * Per creare un'istanza del server {{site.data.keyword.mobilefirst_notm}} con la configurazione avanzata per topologia, sicurezza e altra configurazione del server, fai clic su **Avvia server con la configurazione avanzata**. Vedi [Impostazione della configurazione avanzata](c_using_mfs_p2.html#using_mfs_advanced_p2) per ulteriori informazioni.

Vai a [Using the Mobile Foundation service to set up MobileFirst Server on IBM Containers](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibm-containers/using-mobile-foundation/) per ulteriori informazioni introduttive a {{site.data.keyword.mobilefoundation_short}}.

# Link correlati
{: #rellinks}

## Link correlati
{: #general}

*	[Documentazione del prodotto IBM MobileFirst Platform Foundation V8.0.0](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}
*	[IBM MobileFirst Platform Developer Center](https://mobilefirstplatform.ibmcloud.com){: new_window}
