---

copyright:
  years: 2017
lastupdated: "2017-04-24"
---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introduzione allo starter {{site.data.keyword.iot_short_notm}}
{: #gettingstartedtemplate}
<!-- Provide an appropriate ID above -->

Introduzione a {{site.data.keyword.iot_full}} utilizzando il progetto il progetto GitHub di {{site.data.keyword.iot_short_notm}}. Mediante lo Starter, puoi facilmente simulare un dispositivo, creare schede, generare dati e iniziare ad analizzare e visualizzare i dati nel dashboard {{site.data.keyword.iot_short_notm}}.  
{:shortdesc}

## Panoramica
{: #overview}  

Lo starter viene distribuito e connesso automaticamente ai seguenti servizi:
<dl>
<dt>**{{site.data.keyword.iot_short_notm}}**</dt>
<dd>Un servizio IoT web che include la gestione di gateway, la gestione dei dispositivi e l'accesso alle applicazioni. Utilizzando {{site.data.keyword.iot_short_notm}}, puoi raccogliere i dati dei dispositivi connessi ed eseguire l'analisi dei dati in tempo reale per la tua organizzazione.</dd>
<dt>**{{site.data.keyword.sdk4nodefull}}**</dt>
<dd>L'ambiente di runtime in cui è in esecuzione Node-RED. </br>Per ulteriori informazioni, vedi la [documentazione di {{site.data.keyword.sdk4nodefull}}](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html).</dd>
<dd>Node-RED è uno strumento per la connessione di dispositivi hardware, API e servizi in linea con nuove e interessanti modalità. Puoi utilizzare Node-RED per creare un termostato simulato che invia dati simulati al tuo servizio {{site.data.keyword.iot_short_notm}}. Puoi creare schede per visualizzare i dati in tempo reale nel dashboard {{site.data.keyword.iot_short_notm}}. </br>Per ulteriori informazioni, vedi la [documentazione Node-RED](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered).</dd>
<dt>**{{site.data.keyword.cloudantfull}}**</dt><dd>Il database in cui Node-RED memorizza i metadati.</dd>
</dl>

## Prima di cominciare
{: #byb}  

- Account richiesti  
Prima di iniziare, avrai bisogno di un [account IBM Bluemix](https://bluemix.net/registration) .

- Esplorazione del prodotto  
Per facilitare lo spostamento tra le attività nel processo che segue, apri il dashboard {{site.data.keyword.Bluemix_notm}}, il dashboard {{site.data.keyword.iot_short_notm}} e l'applicazione Node-RED in diverse schede del tuo browser.
<dl>
<dt>*Dashboard {{site.data.keyword.Bluemix_notm}}*</dt>
<dd>Vedi lo stato della tua distribuzione, leggi la documentazione e avvia i dashboard.</dd>
<dt>*Dashboard {{site.data.keyword.iot_short_notm}}*</dt>
<dd>Definisci i tipi di dispositivi, registra i dispositivi, monitora i dati del sensore in entrata, crea le schede di visualizzazione dei dati e vedi le visualizzazioni dei dati live.</dd>
<dt>*Node-RED*</dt>
<dd>Configura ed esegui il flusso del simulatore del dispositivo e gestisci gli altri flussi per elaborare i dati provenienti da {{site.data.keyword.iot_short_notm}}.</dd>
</dl>

## Passo 1: distribuisci lo starter {{site.data.keyword.iot_short_notm}}
{: #deployStarter}

Completa la seguente procedura per distribuire l'applicazione di esempio starter:

1. Distribuisci l'applicazione starter.
 1. Fai clic su <a href="https://bluemix.net/devops/setup/deploy?repository=https://github.com/ibm-watson-iot/iot-platform-bluemix-starter"><img src="https://bluemix.net/devops/graphics/create_toolchain_button.png" height=25></a> per creare una nuova Toolchain di fornitura continua in Bluemix:  (tramite Continuous Delivery)  
 **Suggerimento:** se preferisci distribuire dalla riga di comando, puoi [trovare lo {{site.data.keyword.iot_short_notm}} starter](https://github.com/ibm-watson-iot/iot-platform-bluemix-starter) nell'organizzazione IBM Watson IoT in GitHub.
 2. Quando richiesto, accedi a IBM Bluemix.
 3. Se necessario, seleziona l'organizzazione Bluemix in cui vuoi distribuire l'applicazione starter.
 4. Mantieni il nome Toolchain o aggiornalo come necessario. Questo è utilizzato come nome applicazione predefinito o come root dell'URL della tua applicazione: `<app-name>.mybluemix.net`
 5. Fai clic su **Crea**.  
**Suggerimento:** fai clic sul tile **Delivery Pipeline** per monitorare l'avanzamento della tua prima distribuzione.
 6. Al completamento della distribuzione, fai clic su **Visualizza applicazione** per aprire la tua nuova applicazione Node-RED in una nuova scheda.
2. Individua i servizi dell'applicazione starter.
 1. Dal menu Bluemix, seleziona **Dashboard**.
 2. Individua i seguenti servizi sotto *Tutti i servizi*:
    - iot-starter
    - iotp-starter-cloudantNoSQLDB
 3. Individua la toolchain sotto *Tutte le applicazioni*:
    - default-toolchain-{id}}


## Passo 2: definisci un dispositivo simulato in {{site.data.keyword.iot_short_notm}}
{: #definingsimdev}

Completa la seguente procedura per simulare uno scenario che utilizza un termostato per monitorare la temperatura, l'umidità e l'ubicazione di un soggiorno.

1.	Avvia il dashboard {{site.data.keyword.iot_short_notm}}.
  1. Nel dashboard Bluemix, sotto *Tutti i servizi*, fai clic sul nome della tua istanza {{site.data.keyword.iot_short_notm}}.
**Suggerimento:** il nome dell'istanza generalmente include `iotp-starter`.
  2. Fai clic su **Launch** per aprire il dashboard {{site.data.keyword.iot_short_notm}} in una nuova scheda del browser.   
Per impostazione predefinita, viene visualizzata la pagina `All Boards`.
2. Crea un tipo di dispositivo.
  1.	Dal menu principale, seleziona **Devices** e fai clic su **Add Device**.
  2.	Nella pagina Add Device, fai clic su **Create device type**.
  3.	Nella pagina per la creazione del tipo di dispositivo, fai clic su **Create device type**.
  4. Immetti un nome univoco (ad esempio `Thermostat`) per il tuo di dispositivo e fai clic su **Next**.
  5. Facoltativo: la definizione di un template e dei metadati nelle due pagine successive è facoltativa e può essere tranquillamente ignorata facendo clic su **Next** in ogni pagina.
  6.	Fai clic su **Create** per aggiungere il tipo di dispositivo.
3.	Aggiungi un dispositivo che utilizza il tipo di dispositivo appena creato.
  1. Nella pagina Add Device, il tipo di dispositivo appena creato viene visualizzato nell'elenco dei tipi di dispositivi. Fai clic su **Next** per aggiungere un dispositivo che utilizza quel tipo di dispositivo.
  2. Immetti un ID dispositivo univoco (ad esempio `LivingRoomThermo1`).
  3. Facoltativo: l'immissione dei dati descrittivi nella pagina Add Device o dei metadati del dispositivo nella pagina successiva è facoltativa e può essere tranquillamente ignorata facendo clic su **Next** in ogni pagina.
  4. Nella pagina Security, fai clic su **Next** per generare un token di autenticazione per il tuo dispositivo.
  5. Nella pagina di riepilogo, verifica che le informazioni siano corrette e fai clic su **Add** per aggiungere il dispositivo. Fai clic su **Back** per ritornare alla pagina precedente.
4.	Prendi nota delle informazioni che vengono visualizzate nella pagina Your Device Credentials.   
Hai bisogno delle seguenti informazioni per configurare il simulatore e visualizzare i dati:
 - ID organizzazione
 - Tipo di dispositivo
 - ID dispositivo
 - Metodo di autenticazione
 - Token di autenticazione

## Passo 3: configura ed esegui il simulatore del dispositivo Node-RED.  
{: #confignodered}  
Configura il simulatore del dispositivo Node-RED per inviare i messaggi del dispositivo MQTT con informazioni su temperatura e umidità a {{site.data.keyword.iot_short_notm}}.

1. Avvia l'editor del flusso Node-RED.
  1. Nel dashboard Bluemix, sotto *Tutte le applicazioni*, fai clic sul nome della tua toolchain.  
**Suggerimento:** il nome della toolchain generalmente include `default-toolchain...`.
  2. Dal dashboard della toolchain, apri la tua istanza Node-RED facendo clic su **Routes** e selezionando il link della rotta.  
  2. Fai clic su **Go to your Node-RED flow editor** per aprire l'editor.
2. Distribuisci il tuo dispositivo.
  1. Nel flusso del simulatore del dispositivo, fai doppio clic sul nodo blu **Send to IBM IoT Platform**.
  2. Verifica che l'autenticazione sia impostata su **Bluemix Service**.
  3. Immetti il **Device Type** e **Device ID** del tuo dispositivo e fai clic su **Done**.
  4. Distribuisci il dispositivo facendo clic su **Deploy**.
3. Configura il flusso del monitor di temperatura Node-RED.
  1. Nel flusso del simulatore del dispositivo, fai doppio clic sul nodo blu **IBM IoT App In**.
  2. In Authentication, seleziona **Bluemix Service**.
  3.	Seleziona **All** per Device Type, Device ID, Event e Format.
  4.	Fai clic su **Done**.
  5.  Distribuisci il tuo monitor facendo clic su **Deploy**.
4. Convalida la connessione del dispositivo.
  1.	Apri il dashboard {{site.data.keyword.iot_short_notm}}.  
**Suggerimento:** se il dashboard {{site.data.keyword.iot_short_notm}} non è già aperto in un'altra scheda, torna al dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sul nome della tua istanza {{site.data.keyword.iot_short_notm}} e fai clic su **Launch Dashboard**.
  2. Dal menu principale, seleziona **Devices**.
  3. Fai clic sul nome del dispositivo che hai aggiunto.   
Le informazioni sul dispositivo visualizzano lo stato della connessione del tuo dispositivo.
  4.	Nell'editor del flusso Node-RED, fai doppio clic sul nodo **Send Data**, imposta il valore Repeat su **Interval** e imposta la frequenza su ogni `3` secondi.
  5. Fai clic su **Done**.
  6. Distribuisci le tue modifiche facendo clic su **Deploy**.  
Il payload contiene i punti dati, come quelli mostrati nel seguente esempio:
```
{"d":{"temp":15,"humidity":50,"location":{"longitude":-98.49,"latitude":29.42}}}
```
  7. Facoltativo: apri la scheda Debug per verificare che i messaggi vengano creati.
    1. Dal menu che si trova nella sezione dell'intestazione, seleziona **View**.
    2. Seleziona **Show Sidebar**.
    3. Fai clic sulla scheda Debug per vedere i messaggi.
  8. Nella pagina {{site.data.keyword.iot_short_notm}} Device Information, verifica di visualizzare i punti dati del dispositivo nella sezione Sensor Information.


## Passo 4: crea le schede in {{site.data.keyword.iot_short_notm}} per visualizzare i dati live  
{: #createcards}  
Crea una tabella e le schede per visualizzare i dati del dispositivo nel dashboard {{site.data.keyword.iot_short_notm}}. Per ulteriori informazioni su tabelle e schede, vedi [Visualizzazione dei dati in tempo reale utilizzando le tabelle e le schede](https://console.ng.bluemix.net/docs/services/IoT/data_visualization.html).

1. Crea una tabella
  1. Apri il dashboard {{site.data.keyword.iot_short_notm}}.  
  **Suggerimento:** se il dashboard {{site.data.keyword.iot_short_notm}} non è già aperto in un'altra scheda, torna al dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sul nome della tua istanza {{site.data.keyword.iot_short_notm}} e fai clic su **Launch Dashboard**.  
  2. Crea una tabella per contenere le schede per i tuoi dispositivi simulati.
    1. Se la pagina All Boards non è già visualizzata, seleziona **Boards** dal menu principale del dashboard {{site.data.keyword.iot_short_notm}} e fai quindi clic su **Create New Board**.
    2. Immetti un nome per la tabella (ad esempio `Home Environment`) e fai clic su **Next**.
    3. Nella pagina successiva, fai clic su **Submit**.  
  3. Fai clic sulla tabella appena creata per aprirla.
2. Crea una scheda per visualizzare la temperatura
  1. Fai clic su **Add New Card**, quindi seleziona il tipo di scheda **Line chart** dalla sezione Devices.
  2. Seleziona il tuo dispositivo dall'elenco e fai clic su **Next**.
  3. Fai clic su **Connect new data set**.
  4. Nella pagina Create Value Card, seleziona o immetti i seguenti valori e fai clic su **Next**.
    - Evento: update
    - Proprietà: temp
    - Nome: Temperature
    - Tipo: Float
    - Unità: °C
    - Precisione: 2
    - Min: 0
    - Max: 50
  5. Nella pagina Card Preview, seleziona **L** per la dimensione del grafico a linee e fai clic su **Next**.
  6. Nella pagina Card Information, modifica il nome della scheda in **Temperature** e fai clic su **Submit**.   
La scheda della temperatura viene visualizzata nel dashboard e include un grafico a linee dei dati sulla temperatura dal vivo.
3. Crea una scheda per visualizzare l'umidità
  1. Fai clic su **Add New Card**, quindi seleziona il tipo di scheda **Gauge** dalla sezione Devices.
  2. Seleziona il tuo dispositivo dall'elenco e fai clic su **Next**.
  3. Fai clic su **Connect new data set**.
  4. Nella pagina Create Value Card, seleziona o immetti i seguenti valori e fai clic su **Next**.
  Evento: update
     - Proprietà: humidity
     - Nome: Humidity
     - Tipo: Float
     - Unità: %
     - Precisione: 1
     - Min: 10
     - Max: 95
  5. Nella pagina Card Preview, seleziona **M** per la dimensione del misuratore e fai clic su **Next**.
  6. Nella pagina Card Information, modifica il nome della scheda in **Humidity** e fai clic su **Submit**.   
La scheda dell'umidità viene visualizzata nel dashboard e include un misuratore che mostra i dati sull'umidità dal vivo.  

<!-- 4. Create a card to display location
  1. Click **Add New Card**, and then select the **Value** card type, which is located in the Devices section.
  2. Select your device from the list, then click **Next**.
  3. Click **Connect new data set**.
  4. In the Create Value Card page, select or enter the following values.
     - Event: update
     - Property: location.latitude
     - Name: Latitude
     - Type: Float
     - Unit: "°N"
     - Precision: 2
     - Min: -180
     - Max: 180
  5. Click **Connect new data set**.
  6. In the Create Value Card page, select or enter the following values and click **Next**.
     - Event: update
     - Property: location.longitude
     - Name: Longitude
     - Type: Float
     - Unit: "°E"
     - Precision: 2
     - Min: -180
     - Max: 180
  7. In the Card Preview page, select **M** as the text size, and click **Next**.
  8. In the Card Information page, change the name of the card to **Location** and click **Submit**.   
The location card appears on the dashboard and shows the live latitude and longitude of the device.-->

## Operazioni successive  
{: #whats-next}  
Ora che il tuo dispositivo simulato invia dati a {{site.data.keyword.iot_short_notm}}, puoi continuare a eseguire l'iterazione sul tuo progetto IoT.
 - Guarda le tue schede che visualizzano i dati generati dal flusso node-RED.  
Node-Red continua a inviare dati finché non li interrompi. Per interrompere i dati simulati, completa la seguente procedura:
    1.	Nell'editor del flusso Node-RED, fai doppio clic sul nodo grigio **Send Data**, imposta il valore Repeat su **Interval** e imposta la frequenza su ogni **3** secondi.
    2. Fai clic su **Done**.
    3. Distribuisci le tue modifiche facendo clic su **Deploy**.

 - Connetti un dispositivo fisico.  
[Cerca le ricette IoT](https://developer.ibm.com/recipes/?post_type=tutorials&s=watson+iot) per connettere un dispositivo fisico come Raspberry Pi e inviare i dati a {{site.data.keyword.iot_short_notm}}.

 - Esplora le opzioni di visualizzazione.  
[Distribuisci un'applicazione node.js di esempio per visualizzare i dati del dispositivo.](https://www.bluemix.net/docs/services/IoT/visualizingdata_sample.html)

 -	Proteggi con password l'editor del flusso Node-RED.   
Per impostazione predefinita, l'editor è aperto a tutti per accedere e modificare i flussi. Per proteggere con password l'editor, completa le seguenti attività:
    1.	Nel dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sul nome della tua applicazione Starter per aprire le pagine dell'applicazione.
    2. Fai clic su **Runtime** per visualizzare la pagina dei runtime.
    3. Fai clic su **Variabile di ambiente** per visualizzare la pagina delle variabili di ambiente.
    4. Nella sezione **Definito dall'utente**, fai clic su **Aggiungi** e immetti le seguenti variabili definite dall'utente:
         -	NODE_RED_USERNAME - il nome utente per proteggere l'editor
         -	NODE_RED_PASSWORD - la password per proteggere l'editor
    3.	Fai clic su **Save**.
