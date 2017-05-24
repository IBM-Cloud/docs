---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connessione dispositivi
{: #iotplatform_task}

Prima di poter iniziare a ricevere i dati dai tuoi dispositivi IoT, devi collegarli a {{site.data.keyword.iot_full}}. La connessione di un dispositivo a {{site.data.keyword.iot_short_notm}} implica la registrazione del dispositivo con {{site.data.keyword.iot_short_notm}} e quindi l'utilizzo delle informazioni di registrazione per configurare il dispositivo da collegare a {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Prima di cominciare
{: #byb}

Prima di iniziare il processo di connessione, devi assicurarti che i tuoi dispositivi rispettino i seguenti requisiti per la comunicazione con {{site.data.keyword.iot_short_notm}}:

- Il tuo dispositivo deve essere in grado di comunicare utilizzando i protocolli HTTP o MQTT.
- I messaggi del dispositivo devono essere conformi ai requisiti del payload del messaggio di {{site.data.keyword.iot_short_notm}}.

Per ulteriori informazioni, consulta [Sviluppo dei dispositivi su Watson IoT Platform](https://console.ng.bluemix.net/docs/services/IoT/devices/device_dev_index.html).

Completa la seguente procedura per collegare il tuo dispositivo a {{site.data.keyword.iot_short_notm}}.

## Passo 1: registrazione del tuo dispositivo con {{site.data.keyword.iot_short_notm}}  
{: #iotplatform_subtask1}

La registrazione di un dispositivo implica la classificazione del dispositivo come un tipo dispositivo, dando al dispositivo un nome e fornendo le informazioni sul dispositivo. Quindi fornisci un token di connessione o accetta un token generato da {{site.data.keyword.iot_short_notm}}.

Puoi aggiungere un dispositivo alla volta dal dashboard {{site.data.keyword.iot_short_notm}} o puoi utilizzare l'API [{{site.data.keyword.iot_short_notm}} ![icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html#!/Device_Bulk_Configuration){: new_window} per aggiungere uno o più dispositivi contemporaneamente.

Per aggiungere un dispositivo dal dashboard {{site.data.keyword.iot_short_notm}}:

1. Fai clic sul tile del servizio {{site.data.keyword.iot_short_notm}} nel tuo dashboard {{site.data.keyword.Bluemix}}.

2. Nella pagina del servizio, fai clic su **Launch** per avviare la gestione della tua organizzazione {{site.data.keyword.iot_short_notm}}.

  Si apre la console web {{site.data.keyword.iot_short_notm}} in una nuova scheda del browser al seguente URL:

 ```
 https://org_id.internetofthings.ibmcloud.com/dashboard/#/overview
 ```

    Dove *org_id* è l'ID della [tua {{site.data.keyword.iot_short_notm}} organizzazione](iotplatform_overview.html#organizations){: new_window}.

3. Nel dashboard della panoramica, dal pannello del menu, seleziona **Devices** e fai clic su **Add Device**.
5. Seleziona o crea un tipo dispositivo per il dispositivo che stai aggiungendo.  
Ogni dispositivo collegato a {{site.data.keyword.iot_short_notm}} deve essere associato a un tipo dispositivo. I tipi di dispositivo sono gruppi di dispositivi che condividono caratteristiche comuni.  
Quando aggiungi il tuo primo dispositivo alla tua organizzazione {{site.data.keyword.iot_short_notm}}, non è disponibile alcun tipo dispositivo nel menu **Device type**. Devi prima creare un tipo dispositivo:
 1. Fai clic su **Create device type**.
 2. Immetti un nome del tipo dispositivo come ad esempio `my_device_type` e una descrizione per il tipo dispositivo.   
 **Importante:** il nome del tipo dispositivo non deve essere più lungo di 36 caratteri e può contenere solo:
 <ul>
  <li>Caratteri alfanumerici (a-z, A-Z, 0-9)</li>
  <li>Trattini (-)</li>
  <li>Caratteri di sottolineatura (&lowbar;)</li>
  <li>Punti (.)</li>
  </ul>
 3. Facoltativo: immetti i metadati e gli attributi per il tipo dispositivo.    
 **Suggerimento:** puoi aggiungere e modificare gli attributi e i metadati successivamente.
 4. Fai clic su **Create** per aggiungere il nuovo tipo dispositivo.
10. Fai clic su **Next** per avviare il processo di aggiunta del tuo dispositivo. con il tipo dispositivo.
11. Immetti un ID dispositivo, come ad esempio `my_first_device`.  
L'ID dispositivo viene utilizzato per identificare il dispositivo nel dashboard {{site.data.keyword.iot_short_notm}} ed è anche un parametro obbligatorio per la connessione del tuo dispositivo a {{site.data.keyword.iot_short_notm}}.  
**Importante:** l'ID del tipo dispositivo non deve essere più lungo di 36 caratteri e può contenere solo:
 <ul>
 <li>Caratteri alfanumerici (a-z, A-Z, 0-9)</li>
 <li>Trattini (-)</li>
 <li>Caratteri di sottolineatura (&lowbar;)</li>
 <li>Punti (.)</li>  
 </ul>
 **Suggerimento:** per i dispositivi collegati alla rete, l'ID del dispositivo può essere ad esempio l'indirizzo MAC del dispositivo senza i due punti di separazione.  
12. Facoltativo: fai clic su **Additional fields** per aggiungere informazioni sul dispositivo, come il numero di serie, il produttore, il modello e così via.  
 **Suggerimento:** puoi aggiungere e modificare le informazioni successivamente.
12. Facoltativo: immetti i metadati JSON del dispositivo.  
 **Suggerimento:** puoi aggiungere e modificare i metadati del dispositivo successivamente.
13. Fai clic su **Next** per completare l'aggiunta del tuo dispositivo.
14. Verifica che le informazioni di riepilogo siano corrette e quindi fai clic su **Add** per aggiungere la connessione.  
**Suggerimento:** hai l'opzione di accettare un token di autenticazione generato automaticamente o di fornirne tu uno.  
Se scegli di creare il tuo proprio token, assicurati che sia compreso tra 8 e 36 caratteri e sia formato solo da caratteri alfanumerici e dai seguenti caratteri speciali:
 - Trattino (-)
 - Carattere di sottolineatura (&lowbar;)
 - Punto esclamativo (!)
 - E commerciale (&)
 - Simbolo chiocciola (@)
 - Punto interrogativo (?)
 - Asterisco (\*)
 - Segno più (+)
 - Punto (.)
 - Parentesi destra e sinistra.  

 **Importante:** il token non deve contenere sequenze di caratteri ripetuti, parole del dizionario, nomi utente o altre sequenze predefinite.
15. Nella pagina delle informazioni del dispositivo, copia e salva le seguenti informazioni sul dispositivo:  
 - ID organizzazione, come ad esempio `tubo8x`
 - Tipo del dispositivo, come ad esempio `my_device_type`
 - ID del dispositivo, come ad esempio `my_first_device`
 - Metodo di autenticazione, come ad esempio `token`
 - Token di autenticazione, come ad esempio `PtBVriRqIg4uh)_-Kl`  
  **Suggerimento:** hai bisogno dell'ID organizzazione, del token di autenticazione, del tipo dispositivo e dell'ID del dispositivo per configurare il tuo dispositivo per il collegamento a {{site.data.keyword.iot_short_notm}}.  

Congratulazioni, hai registrato il tuo dispositivo. Ora puoi configurare il tuo dispositivo per collegarsi a {{site.data.keyword.iot_short_notm}}

## Passo 2: collegamento dei tuoi dispositivi a {{site.data.keyword.iot_short_notm}}
{: #iotplatform_subtask2}

Dopo aver registrato il dispositivo con {{site.data.keyword.iot_short_notm}}, puoi utilizzare le informazioni registrate per collegare il dispositivo e avviare la ricezione dei dati.

{{site.data.keyword.iot_short_notm}} supporta molti tipi di dispositivo. Il processo di base per connettersi a un dispositivo di solito include le seguenti operazioni:
- Configurazione del tuo dispositivo alla messaggistica MQTT e all'utilizzo dell'ID organizzazione, del token di autenticazione, del tipo dispositivo e dell'ID del dispositivo per l'autenticazione.  
- Invio dei messaggi del dispositivo alla tua organizzazione {{site.data.keyword.iot_short_notm}} utilizzando il protocollo MQTT.

**Suggerimento:** molte ricette di connessione sono disponibili per i dispositivi comunemente utilizzati. Per un elenco delle ricette, consulta le
[Device connection recipes ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/){: new_window} disponibili in IBM.com.

Le seguenti informazioni sono necessarie quando colleghi il tuo dispositivo:
- URL: *org_id*.messaging.internetofthings.ibmcloud.com  
Dove *org_id* è l'ID della tua organizzazione {{site.data.keyword.iot_short_notm}}.
- Porta:
 - 1883
 - 8883 (crittografata)
 - 443 (socket web)
- Identificativo del dispositivo: d:*org_id*:*device_type*:*device_id*  
Questa combinazione di parametri identifica univocamente il tuo dispositivo.
- Nome utente: use-token-auth  
Questo valore indica che stai utilizzando l'autorizzazione token.
- Password: *Token di autenticazione*  
Questo valore è il token univoco che hai definito o che è stato assegnato al tuo dispositivo quando lo hai registrato.
- Formato argomento dell'evento: iot-2/evt/*event_id*/fmt/*format_string*  
 Dove *event_id* specifica il nome dell'evento visualizzato in {{site.data.keyword.iot_short_notm}} e *format_string* è il formato dell'evento, come ad esempio JSON.
- Formato del messaggio: JSON
   
 {{site.data.keyword.iot_short_notm}} supporta diversi formati, come JSON e testo.

Per ulteriori informazioni sulla connessione del tuo dispositivo, consulta [Connettività MQTT per i dispositivi](devices/mqtt.html) nella documentazione tecnica.

La documentazione API [Organization Administration ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html){: new_window} contiene inoltre le informazioni richieste.

## Ricette sulla connessione dei dispositivi

Le seguenti ricette descrivono il flusso completo utilizzato per registrare e collegare i dispositivi a Watson IoT Platform.

- [How to Register Devices in IBM Watson IoT Platform ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/recipes/tutorials/how-to-register-devices-in-ibm-iot-foundation/){: new_window}

- [Connecting Raspberry Pi as a Device to Watson IoT using Node-RED ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/recipes/tutorials/deploy-watson-iot-node-on-raspberry-pi/){: new_window}

- [Connect an Arduino Uno device to the IBM Watson IoT Platform ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/recipes/tutorials/connect-an-arduino-uno-device-to-the-ibm-internet-of-things-foundation/){: new_window}

- [Connecting a Sense HAT to Watson IoT using Node-RED ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/recipes/tutorials/connecting-a-sense-hat-to-watson-iot-using-node-red/){: new_window}

- [Connecting Raspberry Pi with Windows IoT Core as a Device to Watson IoT Platform ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/recipes/tutorials/connecting-raspberry-pi-with-windows-iot-core-as-a-device-to-watson-iot-using-node-red/){: new_window}
