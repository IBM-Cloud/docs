---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Introduzione allo starter di {{site.data.keyword.iot_short_notm}}
{: #gettingstartedtemplate}
<!-- Provide and appropriate ID above -->
*Ultimo aggiornamento: 27 giugno 2016*
{: .last-updated}

Introduzione a {{site.data.keyword.iot_full}} utilizzando il contenitore tipo dello starter di {{site.data.keyword.iot_short_notm}} . Con lo starter, puoi velocemente simulare un dispositivo, creare schede, generare dati e iniziare l'analisi e la visualizzazione dei dati nel dashboard {{site.data.keyword.iot_short_notm}}.
{: shortdesc}

Lo starter distribuisce e collega automaticamente questi servizi:

{{site.data.keyword.iot_short_notm}} - la piattaforma ti fornisce un toolkit IoT versatile che include i dispositivi gateway, la gestione del dispositivo e un accesso all'applicazione potente. Utilizzando {{site.data.keyword.iot_short_notm}}, puoi raccogliere i dati del dispositivo collegato ed eseguire l'analisi sui dati in tempo reale dalla tua organizzazione.

{{site.data.keyword.sdk4nodefull}} - crea un ambiente di runtime nel quale è in esecuzione Node-RED.

{{site.data.keyword.cloudantfull}} - un database in cui Node-RED archivia i metadati.

## Informazioni su {{site.data.keyword.iot_short_notm}}
{: #about_iotplatform}
{{site.data.keyword.iot_short_notm}} fornisce un accesso all'applicazione potente per i dispositivi e i dati IoT per aiutarti a comporre velocemente le analisi delle applicazioni, a visualizzare i dashboard e le applicazioni IoT mobili.
{{site.data.keyword.iot_short_notm}} ti consente di eseguire potenti operazioni di gestione del dispositivo e archiviare e accedere ai dati del dispositivo, collegare una grande varietà di dispositivi e dispositivi gateway. {{site.data.keyword.iot_short_notm}} fornisce la comunicazione sicura da/ai tuoi dispositivi utilizzando MQTT e TLS.

## Informazioni su Node-RED
{: #about_nodered}
Node-RED è uno strumento per la connessione di dispositivi hardware, API e servizi in linea con nuove e interessanti modalità.  Puoi utilizzare Node-RED per creare un termostato simulato che invia dati simulati al tuo servizio {{site.data.keyword.iot_short_notm}}. Puoi creare schede per visualizzare i dati in tempo reale nel dashboard {{site.data.keyword.iot_short_notm}}. Per ulteriori informazioni, vedi la [Documentazione Node-RED](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered).

## Introduzione
{: #gettingaround}
Nei seguenti passi, utilizzerai tre differenti schede nel tuo browser:
  1. *{{site.data.keyword.Bluemix_notm}} dashboards* - utilizza il dashboard {{site.data.keyword.Bluemix_notm}} per visualizzare lo stato della tua distribuzione, leggere la documentazione e avviare i dashboard.
  2. *{{site.data.keyword.iot_short_notm}} dashboard* - utilizza il dashboard per utilizzare questo servizio. Utilizzerai il dashboard per definire i tipi di dispositivo, registrare i dispositivi, monitorare i dati del sensore in entrata, creare schede di visualizzazione dei dati e visualizzare i dati dal vivo.
  3. *Node-RED* - eseguendo l'applicazione web come un node.js, configurerai ed eseguirai il flusso dell'emulatore del dispositivo e lavorerai con altri flussi per elaborare i dati da {{site.data.keyword.iot_short_notm}}.

## Definizione di un dispositivo simulato in {{site.data.keyword.iot_short_notm}}
{: #definingsimdev}
Registra il tuo dispositivo con {{site.data.keyword.iot_short_notm}}:
  1.	In {{site.data.keyword.Bluemix_notm}}, vai alla scheda della panoramica della tua applicazione distribuita.
  2.	Fai clic sulla casella {{site.data.keyword.iot_short_notm}} nella sezione o scheda delle connessioni.
  3.	Fai clic su avvia dashboard per aprire il dashboard {{site.data.keyword.iot_short_notm}} in una nuova finestra del browser.
  4.	Seleziona Devices
  5.	Fai clic su Add Device
  6.	Fai clic su Create device type nella finestra di dialogo Add Device.
  7.	Fai cli su Create device type nella finestra di dialogo Create Device Type.
  8. Immetti una descrizione e un nome descrittivo per il tipo di dispositivo, come ad esempio termostato.
  9.	Salta: Define Template.
  10.	Salta Metadata.
  11.	Fai clic su Create per aggiungere il nuovo tipo di dispositivo.
  12.	Fai clic su Next per aggiungere il tuo dispositivo (Choose Device Type è preselezionato).
  13.	Immetti un ID del dispositivo come LivingRoomThermo1.
  14.	Salta: Enter device metadata.
  15.	Fai clic su Next per aggiungere una connessione al dispositivo con un token di autenticazione generato automaticamente.
  16.	Verifica che le informazioni di riepilogo siano corrette e quindi fai clic su Add per aggiungere la connessione.
  17.	Nella pagina delle informazioni del dispositivo che viene aperta, copia e salva le informazioni del dispositivo:
      -	Organization ID
      -	Device Type
      -	Device ID
      - Authentication Method
      - Authentication Token

**Suggerimento**: avrai bisogno di Organization ID, Device Type e Device ID nei prossimi passi per finalizzare la configurazione dell'applicazione Node-RED per completare la connessione.

## Configurazione ed esecuzione del simulatore del dispositivo Node-RED.
{: #confignodered}
Configura il simulatore del dispositivo Node-RED. Utilizza il simulatore del dispositivo per inviare messaggi del dispositivo MQTT a {{site.data.keyword.iot_short_notm}}. Il simulatore del dispositivo invia informazioni sulla temperatura e umidità a {{site.data.keyword.iot_short_notm}}.

1. Nel tuo dashboard Bluemix, apri Node-RED selezionando **Visualizza applicazione** o facendo clic sul link (ad esempio, http:// myIoTApp.mybluemix.net).
2.	Fai clic su **Go to your Node-RED flow editor** per aprire l'editor.
3.	Fai doppio clic su **Send** blu al nodo {{site.data.keyword.iot_short_notm}} nel flusso del simulatore del dispositivo.
  1.	Verifica che Authentication = Bluemix Service
  2.	Copia il Device Type dal dispositivo che hai registrato.
  3.	Incolla il Device ID dal dispositivo che hai registrato.
  4.	Fai clic su OK.
4.	Nell'angolo in alto a destra dell'editor del flusso Node-RED, fai clic su **Deploy**.
5.	Configura il flusso Node-RED Temperature Monitor
  1.	Fai doppio clic sull'applicazione IoT IBM blu nel flusso del simulatore del dispositivo.
  2.	Modifica Authentication to Bluemix Service
  3.	Seleziona All per Device Type, Device Id, Event e Format
  4.	Fai clic su OK.
6.	Nell'angolo in alto a destra dell'editor del flusso Node-RED, fai clic su **Deploy**.
7.	Convalida la connessione al dispositivo
  1.	In un'altra scheda o finestra del browser, torna al dashboard {{site.data.keyword.iot_short_notm}}.
  2.	Seleziona Devices e fai clic su LivingRoomThermo1 o sul nome del dispositivo che hai aggiunto, se diverso.  
  Viene aperta la pagina delle informazioni del dispositivo. Questa vista ti permette di visualizzare lo stato della connessione per il tuo dispositivo. Lo stato del dispositivo è disconnesso.
  3.	Torna al tuo editor del flusso Node-RED, fai clic sul pulsante nel nodo Send Data grigio per generare un payload asset.
  Il payload contiene i seguenti punti dati:
  ```
  {"d":{"temp":15,"humidity":50,"location":{"longitude":-98.49,"latitude":29.42}}}
  ```
  4.	Nella scheda di debug del pannello di destra, verifica che siano stati creati dei messaggi.
  5.	Nella pagina delle informazioni del dispositivo {{site.data.keyword.iot_short_notm}}, verifica di visualizzare gli stessi punti dati ricevuti dal dispositivo nella sezione Sensor Information.

8.	Collega il tuo dispositivo IoT di esempio a {{site.data.keyword.iot_short_notm}} per visualizzare i dati del dispositivo.

## Creazione di schede in {{site.data.keyword.iot_short_notm}} per visualizzare i dati dal vivo
{: #createcards}
Per creare schede, completa la seguente procedura:

### Genera automaticamente i dati ogni 3 secondi
1. Nella scheda Node-RED, fai doppio clic sul nodo Send Data
2.	Imposta Repeat to Interval Every 3 seconds
3.	Distribuisci

### Crea nuove schede nel dashboard
1. Vai alla scheda del browser del dashboard {{site.data.keyword.iot_short_notm}}.
2. Seleziona BOARDS.
3. Fai clic su Create New Board.
4. Fornisci un nome come Home Environment.
5. Crea.
6. Fai clic su Add New Card (per la temperatura).
   1.	In Devices, seleziona il grafico Realtime.
   2.	Dati di origine della scheda, controlla il tuo dispositivo "LivingRoomThermo1", quindi fai clic su Next.
   3. Collega un nuovo dataset.
       - Nome: Temperature
       - Evento: update
       - Proprietà: temp
       - Tipe: Float
       - Unità: °C
       - Precisione: 2
       - Min: 0
       - Max: 50
       - Avanti
  4. Anteprima scheda.
       - Seleziona L
       - Avanti
  5. Informazioni sulla scheda.
       - Titolo: Temperature
  6.	Invia.
  7.	La scheda della temperatura appare sul dashboard e include un grafico per i dati della temperatura dal vivo.
7.	Fai clic su Add New Card (per l'umidità).
  1.	In Devices, seleziona Show more.
  2.	Seleziona Gauge.
  3.	Dati di origine della scheda, controlla il tuo dispositivo, quindi fai clic su Next.
  4.	Collega un nuovo dataset.
       -	Nome: Humidity
       -	Evento: update
       -	Proprietà: humidity
       -	Tipe: Float
       -	Unità: "% relative humidity"
       -	Precisione: 1
       -	Min: 10
       -	Max: 95
       -	Avanti
  5.	Anteprima scheda.
       -	Impostazioni
          -	Soglia inferiore: 40 e sereno
          -	Media: good
          -	Soglia superiore: 50% e sereno
       -	Seleziona M
       -	Avanti
  6.	Informazioni sulla scheda.
       -	Titolo: Humidity
  7.	Invia.
  8.	La scheda dell'umidità appare sul dashboard e include un misuratore che mostra i dati sull'umidità dal vivo.
8.	Fai clic su Add New Card (per l'ubicazione).
  1.	In Devices, seleziona Show more.
  2.	Seleziona Value.
  3.	Dati di origine della scheda, controlla il tuo dispositivo. "LivingRoomThermo1", quindi fai clic su Next.
  4.	Collega un nuovo dataset.
       -	Nome: Latitude
       -	Evento: update
       -	Proprietà: location.latitude
       -	Tipe: Float
       -	Unità: "°N"
       -	Precisione: 2
       -	Min: -180
       -	Max: 180
  5. Collega un nuovo dataset.
       -	Nome: Longitude
       -	Evento: update
       -	Proprietà: location.longitude
       -	Tipe: Float
       -	Unità: "°E"
       -	Precisione: 2
       -	Min: -180
       -	Max: 180
       -  Avanti
  6.	Anteprima scheda.
       -	Seleziona L
       -	Avanti
  7.	Informazioni sulla scheda.
       -	Titolo: Location
  8.	Invia.
9.	Controlla l'aggiornamento in tempo reale delle tue nuove schede con i dati del simulatore generati dal flusso Node-RED.
**Nota**: Node-RED continua a inviare dati finché non lo arresti.
10.	Nell'editor del flusso Node-RED, aggiorna il nodo Send Data su Repeat: none.
11.	Distribuisci.

## Operazioni successive
{: #whatsnext}
Ora che il tuo dispositivo simulato invia dati a {{site.data.keyword.iot_short_notm}}, puoi continuare a eseguire l'iterazione sul tuo progetto IoT.

1. [Search our IoT Recipes](https://developer.ibm.com/recipes/?post_type=tutorials&s=watson+iot) per collegare un dispositivo fisico come un Raspberry Pi e inviare dati a {{site.data.keyword.iot_short_notm}}.
2. [Distribuisci un'applicazione node.js di esempio per visualizzare i dati del dispositivo.](https://www.bluemix.net/docs/services/IoT/visualizingdata_sample.html)
3.	Protezione della password dell'editor del flusso Node-RED. Per impostazione predefinita, l'editor è aperto a chiunque acceda e modifichi i flussi. Per proteggere con password l'editor, completa le seguenti attività:
  1.	Nel dashboard Bluemix, seleziona la pagina 'Variabili di ambiente' per la tua applicazione.
  2.	Aggiungi le seguenti variabili definite dall'utente:
       -	NODE_RED_USERNAME - il nome utente per proteggere l'editor
       -	NODE_RED_PASSWORD - la password per proteggere l'editor
  3.	Fai clic su Salva.


# Link correlati
{: #rellinks}

## Esercitazioni ed esempi
{: #samples}
* [Recipes for connecting your devices](https://developer.ibm.com/recipes/?post_type=tutorials&s=iot){:new_window}
* [{{site.data.keyword.iot_short}} Play organization](https://play.internetofthings.ibmcloud.com/){:new_window}
* [Connecting an Intel Galileo to the {{site.data.keyword.iot_short}}](https://developer.ibm.com/recipes/tutorials/connect-an-intel-galileo-to-the-internet-of-things-foundation-connect/){:new_window}
* [Connecting an ARM&reg; mbed&trade; IoT Starter Kit](https://developer.ibm.com/recipes/tutorials/arm-mbed-iot-starter-kit-part-1/){:new_window}
* [Connecting a Raspberry Pi to {{site.data.keyword.iot_short}}](https://developer.ibm.com/recipes/tutorials/raspberry-pi-4/){:new_window}

## Guida di riferimento API
{: #api}
* [Documentazione API {{site.data.keyword.iot_short}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#/){:new_window}


## Link correlati
{: #general}
* [Documentazione {{site.data.keyword.iot_short_notm}}](https://www.bluemix.net/docs/services/IoT/iotplatform_overview.html){:new_window}
* [Documentazione starter {{site.data.keyword.sdk4nodefull}}](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html){:new_window}
