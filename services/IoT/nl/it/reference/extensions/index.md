---

copyright:
  years: 2015, 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integrazioni del servizio esterno
{: #ref-index}
Ultimo aggiornamento: 26 settembre 2016
{: .last-updated}

L'integrazione del servizio esterno ti consente di accedere ai dati e alle operazioni da servizi di terze parti o esterni nella tua organizzazione {{site.data.keyword.iot_full}}.

## Jasper
{: #jasper}

Jasper è una piattaforma di amministrazione e gestione per i dispositivi SIM. Jasper è integrato nel dashboard {{site.data.keyword.iot_short_notm}}, rende possibile gestire i dispositivi Jasper tramite il dashboard della tua organizzazione {{site.data.keyword.iot_short_notm}}.

### Operazioni supportate per Jasper

L'integrazione Jasper integrata fornita dalla nostra piattaforma fornisce supporto per le seguenti operazioni Jasper:

- Visualizzazione generale dei dati Jasper
  - Mostra: stato, piano tariffario, utilizzo dati da inizio mese, utilizzo SMS da inizio mese, utilizzo voce da inizio mese, limiti in eccedenza, aggiunta data e modifica data.
- Modificare lo stato di attivazione della SIM.
  - Seleziona da: in magazzino, pronto per l'attivazione, attivato, disattivato e ritirato.
- Visualizzare l'utilizzo della SIM
  - Mostra: data di inizio del ciclo, dati totali e fatturabili, SMS totali e fatturabili, voce totale e fatturabile.
  - La data di inizio del ciclo di vita può essere impostata utilizzando un formato YYYY-MM-DD.
- Inviare SMS alla SIM
- Modificare il piano tariffario

Puoi accedere alle operazioni supportate nel drilldown del dispositivo di un dispositivo collegato a Jasper dopo che sono state completate le seguenti istruzioni di configurazione:


### Configurazione di Jasper

Per collegare il tuo servizio Jasper alla tua organizzazione {{site.data.keyword.iot_short_notm}} esistono due fasi di configurazione che devono per prima cosa essere eseguite. In primo luogo, {{site.data.keyword.iot_short_notm}} deve essere collegato al tuo servizio Jasper, quindi i tuoi dispositivi {{site.data.keyword.iot_short_notm}} devono essere configurati.


1. Abilita l'estensione Jasper. Per abilitare l'integrazione Jasper con la tua organizzazione {{site.data.keyword.iot_short_notm}}, completa la seguente procedura:
  1. Dal dashboard {{site.data.keyword.iot_short_notm}}, seleziona **Extensions**.
  2. Nella pagina **Extensions**, fai clic su **Add Extension**.
  3. Fai clic su **Add** vicino a Jasper.
  4. Immetti i tuoi nome utente, password, chiave di accesso e ID dominio Jasper.
  5. Fai clic su **Done**.

2. Configura i tuoi dispositivi
Puoi configurare i dispositivi collegati alla tua organizzazione {{site.data.keyword.iot_short_notm}} e al tuo account Jasper per visualizzare i dati da Jasper nel dashboard {{site.data.keyword.iot_short_notm}}.  
**Importante:** la configurazione di Jasper non può essere applicata come parte del processo di aggiunta del dispositivo, solo i dispositivi precedentemente collegati possono essere configurati con Jasper.  
Per configurare i tuoi dispositivi collegati a Jasper, completa la seguente procedura:
 1. Nella scheda dei dispositivi del tuo dashboard {{site.data.keyword.iot_short_notm}}, trova il dispositivo collegato a Jasper da configurare.
 2. Selezione il dispositivo per aprire la vista *Device Drilldown*.
 3. Scorri verso il basso fino a *Extension Configuration*.
 4. Immetti la configurazione dell'estensione utilizzando il seguente formato JSON e quindi fai clic su **Confirm changes** per salvare la tua configurazione.  

```json
   {
        "jasper": {
            "iccid": "string"
        }
    }

```

Quando l'organizzazione è stata configurata correttamente, viene visualizzata la sezione *Extensions* nella sezione *Extensions Configuration* nella vista *Device Drilldown*.

## AT&T
{: #att}

### Operazioni supportate per AT&T

L'estensione AT&T abilita le seguenti operazioni AT&T:

- Visualizzazione generale dei dati AT&T
  - Mostra: stato, piano tariffario, utilizzo dati da inizio mese, utilizzo SMS da inizio mese, utilizzo voce da inizio mese, limiti in eccedenza, aggiunta data e modifica data.
- Modificare lo stato di attivazione della SIM.
  - Seleziona da: in magazzino, pronto per l'attivazione, attivato, disattivato e ritirato.
- Visualizzare l'utilizzo della SIM
  - Mostra: data di inizio del ciclo, dati totali e fatturabili, SMS totali e fatturabili, voce totale e fatturabile.
  - La data di inizio del ciclo di vita può essere impostata utilizzando un formato YYYY-MM-DD.
- Inviare SMS alla SIM
- Modificare il piano tariffario

### Configurazione di AT&T

Per collegare la tua organizzazione {{site.data.keyword.iot_short_notm}} a AT&T devi completare la configurazione dell'organizzazione e del dispositivo.

Per configurare la tua piattaforma {{site.data.keyword.iot_short_notm}}, completa la seguente procedura.

1. Abilita l'estensione AT&T. Per abilitare l'integrazione AT&T con la tua organizzazione {{site.data.keyword.iot_short_notm}}, completa la seguente procedura:
  1. Dal dashboard {{site.data.keyword.iot_short_notm}}, seleziona **Extensions**.
  2. Nella pagina **Extensions**, fai clic su **Add Extension**.
  3. Fai clic su **Add** vicino a AT&T.
  4. Immetti i tuoi nome utente, password, chiave di accesso e ID dominio AT&T.
  5. Fai clic su **Done**.

Per collegare la tua organizzazione {{site.data.keyword.iot_short_notm}} con il tuo account AT&T, esistono due fasi di configurazione che devono per prima cosa essere eseguite. Completa configurazione della tua organizzazione e quindi configura i tuoi dispositivi.


2. Configura i tuoi dispositivi
Puoi configurare i dispositivi collegati alla tua organizzazione {{site.data.keyword.iot_short_notm}} e al tuo account AT&T per visualizzare i dati da AT&T nel dashboard {{site.data.keyword.iot_short_notm}}.  
**Importante:** la configurazione di AT&T non può essere applicata come parte del processo di aggiunta del dispositivo, solo i dispositivi precedentemente collegati possono essere configurati con AT&T.  
Per configurare i tuoi dispositivi collegati a AT&T, completa la seguente procedura:
 1. Nella scheda dei dispositivi del tuo dashboard {{site.data.keyword.iot_short_notm}}, trova il dispositivo collegato a  AT&T da configurare.
 2. Selezione il dispositivo per aprire la vista *Device Drilldown*.
 3. Scorri verso il basso fino a *Extension Configuration*.
 4. Immetti la configurazione dell'estensione utilizzando il seguente formato JSON e quindi fai clic su **Confirm changes** per salvare la tua configurazione.  

```json
   {
        "atnt": {
            "iccid": "string"
        }
    }

```

Quando l'organizzazione è stata configurata correttamente, viene visualizzata la sezione *Extensions* nella sezione *Extensions Configuration* nella vista *Device Drilldown*.


## Connettore ARM mbed
{: #arm}

Il connettore ARM mbed ti consente di collegare il tuo dispositivo ARM mbed a {{site.data.keyword.iot_short_notm}}. L'estensione ARM mbed è consentita nel portale ARM mbed e {{site.data.keyword.iot_short_notm}} per inviare e ricevere i dati dal portale ARM mbed.

### Configurazione


1. Abilita l'estensione del connettore ARM mbed. Per abilitare l'estensione del connettore ARM mbed completa la seguente procedura:
  1. Dal dashboard {{site.data.keyword.iot_short_notm}}, seleziona **Settings** e naviga a **Extensions**.
  2. Nel menu **Extensions**, fai clic su **Add Extension**.
  3. Fai clic su **Add** vicino all'estensione del connettore ARM mbed .
  4. Immetti i tuoi ID dominio e chiave di accesso ARM mbed. Puoi trovarli utilizzando il portale ARM mbed all'indirizzo https://connector.mbed.com.
  5. Verifica che le credenziali siano corrette facendo clic sul pulsante **Check Connection**.
  6. Fai clic su **Done**.

### Formato payload 

Esistono due tipi di messaggi in entrata dalla piattaforma ARM mbed, le notifiche e le risposte asincrone. {{site.data.keyword.iot_short_notm}} può inviare i comandi ai dispositivi collegati alla piattaforma ARM mbed.

#### Notifiche

Le notifiche vengono generate dalle modifiche nel dispositivo e nei dati del sensore. Dopo che {{site.data.keyword.iot_short_notm}} elabora il messaggio, è presente sull'argomento evento del dispositivo nello stesso modo di un dispositivo direttamente collegato a {{site.data.keyword.iot_short_notm}}. Il tipo di evento utilizzato per le notifiche generate nei dispositivi collegati alla piattaforma ARM mbed è `notify`.

Il seguente esempio di codice mostra il formato del payload per una notifica inviata dall'API della piattaforma ARM mbed:

```
{
  "ep":<endpoint/deviceID>,
  "path":<resource path>,
  "ct":<content type>,
  "payload":<Base64 encoded payload>,
  "max-age":<how long the payload is valid, in seconds>
}
```

#### Risposte asincrone 

Quando {{site.data.keyword.iot_short_notm}} invia un comando a un dispositivo collegato alla piattaforma ARM mbed, il dispositivo restituisce un messaggio di conferma a {{site.data.keyword.iot_short_notm}}. Questo messaggio di conferma viene denominato *risposta asincrona* e utilizza il tipo di evento `asyncResponse`.

Il seguente esempio di codice mostra il formato del payload per una risposta asincrona inviata dal servizio cloud ARM mbed:

```
{
  "id":<transaction id>,
  "status":<200 is command was sucessfully executed. Check other HTTP response codes>,
  "ct":<content type>,
  "max-age":<how long the payload is valid, in seconds>,
  "payload":<base64 encoded payload>,
  "ep":<endpoint/deviceID affected by the command>,
  "path":<resource path affected by the command>
}
```

#### Invio dei comandi alla piattaforma ARM mbed

{{site.data.keyword.iot_short_notm}} può inviare i comandi ai dispositivi collegati alla piattaforma ARM mbed. I comandi inviati alla piattaforma ARM mbed devono utilizzare il seguente formato JSON.

```
{
  "method":<PUT or POST>,
  "deviceId":<endpoint/deviceId>,
  "resourceId":<resource path>,
  "payload": <Base64 encoded payload>
}
```
Il metodo scelto è sensibile al maiuscolo/minuscolo. Il carattere iniziale '/' del percorso della risorsa deve essere ignorato.


Il payload deve essere pubblicato nel seguente argomento:

```
iot-2/type/<device_type>/id/<deviceId>/cmd/<command_type>/fmt/<command_format>
```


## Orange
{: #orange}

L'estensione Orange consente di visualizzare i dati della SIM card dai dispositivi collegati a {{site.data.keyword.iot_short_notm}} e di avere una SIM card Orange installata.

https://developer.ibm.com/iotplatform/2016/03/30/watson-iot-platform-integration-with-orange-beta/

### Operazioni supportate per Orange

Se hai un dispositivo collegato al tuo servizio {{site.data.keyword.iot_short_notm}} e una SIM card Orange, puoi utilizzare l'estensione Orange per visualizzare i seguenti dati della SIM card:

- Numero di serie della SIM
- Stato di attivazione
- Ultima modifica stato
- Ultimo aggiornamento stato
- Stato ubicazione

### Configurazione di Orange



Per abilitare l'estensione Orange:

1. Dal dashboard {{site.data.keyword.iot_short_notm}}, seleziona **Extensions**.
2. Nella pagina **Extensions**, fai clic su **Add Extension**.
3. Fai clic su **Add** vicino all'estensione Orange.
4. Immetti i tuoi nome utente e password Orange.
6. Fai clic su **Done**.

Dopo aver abilitato l'estensione Orange, tutti i dispositivi con una SIM card Orange devono essere configurati per visualizzare i dati della SIM Orange.

1. Nella scheda dei dispositivi del tuo dashboard {{site.data.keyword.iot_short_notm}}, trova il dispositivo SIM Orange da configurare.
2. Selezione il dispositivo e scorri verso il basso fino a *Extension Configuration*.
3. Immetti la configurazione dell'estensione utilizzando il seguente formato JSON e quindi fai clic su **Confirm changes** per salvare la tua configurazione.

```  
    {
        "orange": {
            "serialnumber": "<serial number of Orange SIM>"
        }
    }

```
Quando l'organizzazione è stata configurata correttamente, viene visualizzata la sezione *Extensions* nella sezione *Extensions Configuration* nella vista *Device Drilldown*.

## Spazio di archiviazione dei dati cronologici
{: #historical_data}

L'estensione di archiviazione dei dati cronologici ti permette di individuare e configurare i servizi di archiviazione dei messaggi compatibili come [{{site.data.keyword.cloudantfull}}](../../cloudant_connector.html) o [{{site.data.keyword.messagehub_full}}](../../message_hub.html) per i tuoi dati IoT.

## Pacchetti di gestione del dispositivo personalizzati
{: #device_mgmt}

La gestione del dispositivo è una funzione principale di {{site.data.keyword.iot_short_notm}}, tuttavia, può essere estesa per sviluppare ulteriori funzionalità.

L'estensione di gestione del dispositivo ti consente di installare funzioni personalizzate per la gestione del dispositivo. Per ulteriori informazioni sulle funzioni di gestione del dispositivo personalizzate, consulta [device management custom extensions](../../devices/device_mgmt/custom_actions.html){: new_window}.

## Blockchain
{: #blockchain}

{{site.data.keyword.iot_short_notm}} abilita i dispositivi IoT a fornire dati alle transazioni blockchain, che archiviano i dati nel ledger immutabile di blockchain e li utilizzano nelle regole di business del smart contract. {{site.data.keyword.iot_short_notm}} associa i dati del dispositivo al formato dei dati necessario dallo smart contract di blockchain e li trasmette al fabric blockchain per l'archiviazione nel ledger blockchain.

### Operazioni supportate per Blockchain
- Attivazione degli aggiornamenti smart contract con gli eventi del dispositivo.
- Esecuzione della logica di business del contratto per aggiornare lo stato del ledger con i dati evento del dispositivo.
- Monitoraggio del blockchain, delle transazioni e dello stato del ledger con la IU di monitoraggio.

### Configurazione di Blockchain

L'integrazione blockchain {{site.data.keyword.iot_short_notm}} è un offerta di servizi che non è attivata per impostazione predefinita in {{site.data.keyword.iot_short_notm}}. Per attivare la funzione nel tuo ambiente, completa la seguente procedura:
 1. Dal dashboard {{site.data.keyword.iot_short_notm}}, **Extensions**.
 2. Fai clic sul link **Tell me more** vicino all'estensione blockchain per andare alla pagina IoT Blockchain Services Offering.
 3. Compila e invia il modulo di richiesta del servizio.   
L'approvazione del servizio di solito impiega circa un giorno. Dopo che la tua richiesta è stata approvata, ricevi una email con le istruzioni su come attivare l'integrazione blockchain nella tua organizzazione {{site.data.keyword.iot_short_notm}}.
 5. Ritorna al dashboard {{site.data.keyword.iot_short_notm}} della tua organizzazione per completare la configurazione. Per ulteriori informazioni, consulta [Integrazione blockchain {{site.data.keyword.iot_short_notm}}](../../bl_blockchain_integration.html).

## Weather Company
{: #weathercompany}

L'estensione Weather Company combina i dati meteo con i tuoi dispositivi {{site.data.keyword.iot_short_notm}} esistenti. I dati da Weather Company sono visualizzati nella vista dei dettagli del dispositivo se è stata effettuata una richiesta di ubicazione aggiornata utilizzando l'API o se il dispositivo ha già impostato la sua ubicazione utilizzando un messaggio di gestione del dispositivo.

**Nota:** solo i dispositivi gestiti possono impostare le proprie ubicazioni. Tutti i dispositivi non gestiti devono avere le loro ubicazioni impostate manualmente utilizzando l'API. Per ulteriori informazioni sull'impostazione di un'ubicazione del dispositivo, consulta [Richieste di aggiornamento dell'ubicazione](../../devices/device_mgmt/index.html#update-location).

### Dati meteo

Per visualizzare i dati meteo richiamati per un'ubicazione del dispositivo, trova il dispositivo nel pannello **Devices** e fai clic su di esso. Nella vista del dispositivo dettagliata scorri fino alla sezione **Extensions**. Sono elencati i seguenti dati meteo:

- Meteo corrente.
- Temperatura corrente.
- Temperatura massima e minima previste.
- Umidità relativa. 
- Pressione. 
- Visibilità. 
- Velocità del vento. 
- Direzione del vento. 
- Latitudine.
- Longitudine.

<!-- Weather data from The Weather Company extension can be retrieved by using the API. For information on the Weather Company API, see [The Weather Company API documentation](https://docs.internetofthings.ibmcloud.com/swagger/ext-twc.html). -->
