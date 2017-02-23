---

copyright:
  years: 2016, 2017
lastupdated: "2016-06-29"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Visualizzazione dei dati del dispositivo
{: #visualizingdata_data}

Questo esempio ti aiuta a visualizzare i dati cronologici e in tempo reale dai dispositivi registrati nella tua organizzazione {{site.data.keyword.iot_full}}.
{:shortdesc}

## Prima di cominciare
{: #byb}

Prima di poter visualizzare i tuoi dati, devi eseguire le seguenti azioni:

- Registra i tuoi dispositivi nella tua organizzazione {{site.data.keyword.iot_short_notm}}.
- Assicurati che i tuoi dispositivi stiano inviando eventi a {{site.data.keyword.iot_short_notm}}.
- [Scarica l'esempio di visualizzazione](https://github.com/ibm-messaging/iot-visualization/archive/v0.2.0.zip) dal repository github ed estrai il file .zip.
- [Installa lo strumento di riga di comando cf](../../starters/install_cli.html) da {{site.data.keyword.Bluemix_notm}}.

## Esecuzione dell'esempio in {{site.data.keyword.Bluemix_notm}}
{: #running_sample}

1. Crea un'applicazione in {{site.data.keyword.Bluemix_notm}} utilizzando la SDK Node.js. Prendi nota del nome e del nome host dell'applicazione, queste informazioni sono necessarie al caricamento dell'applicazione in {{site.data.keyword.Bluemix_notm}}.
2. Esegui il bind dell'applicazione node.JS alla tua istanza {{site.data.keyword.iot_short_notm}} nel tuo dashboard {{site.data.keyword.Bluemix_notm}} completando i seguenti passi:

  a. Nel tuo dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sull'applicazione Node.JS che hai creato.

  b. Fai clic su **Esegui il bind di un servizio o di una API** e quindi seleziona il tuo servizio {{site.data.keyword.iot_short_notm}} e fai clic su **Aggiungi**.
3. Utilizzando lo strumento di riga di comando cf, modifica la tua directory in quella del pacchetto di esempio di visualizzazione estratto ed esegui il seguente comando per il collegamento a {{site.data.keyword.Bluemix_notm}}.
```
cf api https://api.ng.bluemix.net
```
4. Quindi, accedi a {{site.data.keyword.Bluemix_notm}} utilizzando:
```
cf login -u <your_bluemix_login_id>
```
Se non stai utilizzando lo spazio e l'organizzazione predefiniti, puoi utilizzare:
```
cf target-o <your_bluemix_org> -s dev
```

5. Modifica il file `manifest.yml` e aggiorna i nomi dell'host e dell'applicazione utilizzando il seguente formato:
```
applications:
 - disc quota: 1024M
   host: <your_bluemix_hostname>
   name: <your_bluemix_appname>
   command: node ap.js
   path:
   domain: mybluemix.net
   instances: 1
   memory: 128M
```
6. Distribuisci il tuo esempio di visualizzazione utilizzando il seguente comando:
```
cf push <your_application_name>
```
7. Nel tuo browser, immetti il seguente URL:
```
http://<your_application_name>.mybluemix.net
```

Tutti i dispositivi nella tua organizzazione sono elencati nel menu a discesa del dispositivo. Quando selezionato, dovresti vedere la visualizzazione in tempo reale dei dati che il dispositivo sta inviando al tuo servizio {{site.data.keyword.iot_short_notm}}. Per visualizzare i dati cronologici, fai clic sul pulsante **Dati cronologici**.

## Personalizzazione dell'esempio
{: #customize_sample}

Questa applicazione di esempio è un'applicazione web autonoma, scritta nel framework node.js. L'esempio visualizza gli eventi che sono stati inviati dai dispositivi registrati in {{site.data.keyword.iot_short_notm}}. L'esempio utilizza i seguenti strumenti:

- Express: framework dell'applicazione web Node.js
- JQuery: chiamate IU e Ajax
- Rickshaw: strumento di visualizzazione grafica
- Paho: client MQTT

L'applicazione di esempio è strutturata con le seguenti directory:

- Pubblica
- CSS: fogli di calcolo
- Immagini
- JS: file di logica JavaScript principali
- Storico: codice per la visualizzazione storica
- Tempo reale: codice per la visualizzazione in tempo reale
- Uicontroller.js: codice per il controllo dell'interfaccia utente
- Rotte: instradamento della logica e dell'applicazione web
- Utilità: funzioni di utilità, utilizzate per effettuare le chiamate HTTP
- Viste: file interfaccia utente, scritti in Jade
- La libreria dei grafici Rickshaw è utilizzata per tracciare il grafico per i dati cronologici e in tempo reale.

## Personalizzazione della visualizzazione dei dati in tempo reale
{: #customize_real_time_display}

La directory che contiene il codice di visualizzazione grafica per i dati in tempo reale è `public/ja/realtime`. La logica dei grafici può essere personalizzata modificando `public/js/historian/realtimeGraph.js`.

Il file di riferimento della libreria MQTT Paho per la sottoscrizione agli argomenti del dispositivo e per ricevere gli eventi del dispositivo da {{site.data.keyword.iot_short_notm}} può essere trovato in `public/js/historian/realtime.js`.

Gli eventi del dispositivo trasmessi al file `realtimeGraph.js` per tracciare il grafico.

## Personalizzazione della visualizzazione dei dati cronologici
{: #customize_historical_display}

La directory che contiene il codice di visualizzazione grafica per i dati del dispositivo cronologici è `public/js/historian`. La logica dei grafici può essere personalizzata modificando `public/js/historian/historianGraph.js`.

Il file che controlla le chiamate API ReST per raccogliere i dati del dispositivo cronologici è `public/js/historian/historian.js`.

I dati cronologici sono trasmessi al file `historianGraph.js` per tracciare il grafico.

È disponibile una guida degli sviluppatori più dettagliata nella pagina wiki relativa alla visualizzazione iot Github.
