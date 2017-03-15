---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Creazione e collegamento di un simulatore del dispositivo Node-RED
Utilizza Node-RED per creare un simulatore del dispositivo e per inviare i dati del dispositivo simulato alla tua organizzazione {{site.data.keyword.iot_full}}.  
{:shortdesc}

Node-RED è uno strumento per collegare dispositivi hardware, API o servizi online in modi nuovi e interessanti. Per ulteriori informazioni, consulta il sito web [Node-RED ![icona link esterno](../../icons/launch-glyph.svg)](http://nodered.org/){: new_window}.  

Puoi eseguire la tua istanza Node-RED nel tuo proprio ambiente o utilizzarla come un'applicazione {{site.data.keyword.Bluemix_notm}}. Il seguente processo include le istruzioni per {{site.data.keyword.Bluemix_notm}}.

Per creare e collegare il simulatore del dispositivo Node-RED:

1. Crea il simulatore del dispositivo Node-RED
   Utilizza il simulatore del dispositivo per inviare i messaggi del dispositivo MQTT a {{site.data.keyword.iot_short_notm}}. Il simulatore del dispositivo simula un invio di dati per un contenitore merci a un broker MQTT come {{site.data.keyword.iot_short_notm}}.
    1. Accedi a {{site.data.keyword.Bluemix_notm}} all'indirizzo: https://console.ng.bluemix.net
    2. Seleziona la scheda **Catalog**.
    3. Individua la sezione dei contenitori tipo del catalogo del servizio e fai clic su **Node-RED Starter Community BETA**. **Suggerimento:** fai clic [qui ![icona link esterno](../../icons/launch-glyph.svg)](https://console.ng.bluemix.net/catalog/starters/node-red-starter/){: new_window} per andare direttamente alla pagina starter di Node-RED.
    4. Nella pagina starter di Node-RED, seleziona lo spazio dove desideri distribuire Node-RED, verifica le selezioni per la creazione di un'applicazione e fai clic su **Create** per aggiungere Node-RED alla tua organizzazione Bluemix.  
    Ad esempio:  
     - Spazio: dev
     - Nome: myDevice
     - Host: myDevice

    Lascia il resto delle opzioni con i loro valori predefiniti. Dopo che l'applicazione è stata distribuita, vieni portato alla pagina Start coding with Node-RED.  
    **Nota:** il processo di preparazione può richiedere diversi minuti.

    3. Fai clic sul link Routes per aprire Node-RED.  
    Esempio: `http://simulatedDevice.mybluemix.net`
    4. Fai clic su **Go to your Node-RED flow editor** per aprire l'editor.
    5. Copia il flusso di dati Node-RED che trovi nella sezione [Node-RED node flow data](#flow_data) di questo documento.
    5. Nell'editor del flusso Node-RED, fai clic sul menu nell'angolo in alto a destra e seleziona **Import > Clipboard**.  
    6. Incolla gli appunti nel campo di input dei nodi di importazione e fai clic su **Ok**.
    Il flusso del simulatore del dispositivo viene importato nell'editor del flusso.

2. Registra il tuo dispositivo con {{site.data.keyword.iot_short_notm}}  
Segui queste istruzioni per collegare il dispositivo di esempio Node-RED:
 1. In {{site.data.keyword.Bluemix_notm}}, vai al dashboard
 2. Seleziona lo spazio nel quale hai distribuito {{site.data.keyword.iot_short_notm}}.
 3. Fai clic sul tile **{{site.data.keyword.iot_short_notm}}**.
 4. Fai clic su **Launch dashboard** per aprire il dashboard {{site.data.keyword.iot_short_notm}}.
 5. Seleziona **Devices**
 6. Fai clic su **Add Device**
 7. Fai clic su **Create device type**.
 9. Immetti un nome descrittivo e una descrizione per il tipo di dispositivo, come ad esempio `sample_device`.
 10. Facoltativo: immetti gli attributi per il tipo di dispositivo.
 11. Facoltativo: immetti i metadati per il tipo di dispositivo.
 12. Fai clic su **Create** per aggiungere il nuovo tipo di dispositivo.
 13. Fai clic su **Next** per aggiungere il tuo dispositivo.
 14. Immetti un ID dispositivo, come ad esempio `Device001`.
 15. Facoltativo: immetti i metadati per il dispositivo.
 16. Fai clic su **Next** per aggiungere una connessione del dispositivo con un token di autenticazione generato automaticamente.
 17. Verifica che le informazioni di riepilogo siano corrette e quindi fai clic su **Add** per aggiungere la connessione.
 18. Nella pagina delle informazioni del dispositivo che si apre, copia e salva le informazioni sul dispositivo:  
  <ul>
  <li> ID organizzazione
  <li> Tipo di dispositivo
  <li> ID dispositivo
  <li> Metodo di autenticazione
  <li> Token di autenticazione
  </ul>
  **Suggerimento:** hai bisogno dell'ID organizzazione, del token di autenticazione, del tipo di dispositivo e dell'ID del dispositivo nei successivi pochi passi per finalizzare la configurazione dell'applicazione Node-RED per completare la connessione.

2. Collega il tuo dispositivo a {{site.data.keyword.iot_short_notm}}  
 1. Apri l'editor del flusso Node-RED.
 2. Fai doppio clic su Publish to IoT node.
 3. Verifica che la voce dell'argomento è: `iot-2/evt/event_name/fmt/json` **Suggerimento:** la parte /event_name dell'argomento imposta il nome dell'evento per gli eventi pubblicati.
 4. Fai clic sull'icona di modifica vicino al campo server.
 5. Aggiorna il nome del server in modo che corrisponda alla tua organizzazione {{site.data.keyword.iot_short_notm}}.  
 ```
 {organization_ID}.messaging.internetofthings.ibmcloud.com
 ```  
 Dove {organization_ID} è l'*ID organizzazione* che hai salvato precedentemente.
 6. Aggiorna l'ID client con i tuoi ID organizzazione, tipo di dispositivo e ID del dispositivo:
 ```
 d:{organization_ID}:{device_type}:{device_ID}
   ```  
   Dove {organization_ID}, {device_type} e {device_ID} sono i valori che hai salvato precedentemente.
 7. Fai clic sulla scheda **Security**.
 8. Verifica che il campo nome utente abbia il valore `use-token-auth`.
 9. Aggiorna il campo della password con il *Token di autenticazione* che hai salvato precedentemente.
 10. Fai clic su **Update** e quindi su **OK**.
 12. Nell'angolo in alto a destra dell'editor del flusso Node-RED, fai clic su **Deploy**.
 13. Verifica che lo stato di connessione di Publish to IoT node visualizzi *connected*.  **Suggerimento:** se non viene stabilita la connessione, fai doppio clic sulle impostazioni che hai inserito. Anche un piccolo errore di copia e incolla causerà il malfunzionamento della connessione.

4. Convalida la connessione del dispositivo
 1. In un'altra scheda o finestra del browser, apri il dashboard {{site.data.keyword.iot_short_notm}}.
 2. Seleziona **Devices** e fai clic su **Device001** o sul nome del dispositivo che hai aggiunto, se diverso.  
 Viene visualizzata la pagina delle informazioni sul dispositivo. Questa vista ti consente di controllare lo stato della connessione del tuo dispositivo. Il dispositivo dovrebbe essere visualizzato come scollegato in questa fase.   
 3. Torna al tuo editor del flusso Node-RED, fai clic sul pulsante del nodo Inject per generare un payload asset.  
 Il payload contiene i seguenti punti dati:  
 ```
 {"d":
  { "name":"My Device",
    "location":
    {
      "longitude":-87.90,
      "latitude":43.03
    },
    "velocity":13,
    "type":"GPS"
  }
 }
 ```
  {:codeblock}  

 3. Nella scheda di debug del pannello di destra, verifica che siano stati creati dei messaggi.  
 4. Torna nella pagina delle informazioni sul dispositivo {{site.data.keyword.iot_short_notm}}, il dispositivo dovrebbe essere ora collegato. Verifica di visualizzare gli stessi punti dati ricevuti dal dispositivo.  
 ```
 Event	Datapoint	 Value	Time Received
 event_name	d.name	My Device	May 16, 2016 2:22:18 PM
 event_name	d.location.longitude	-87.90	May 16, 2016 2:22:18 PM
 event_name	d.location.latitude	43.03	May 16, 2016 2:22:18 PM
 event_name	d.velocity	13	May 16, 2016 2:22:18 PM
 event_name	d.type	GPS	May 16, 2016 2:22:18 PM
 ```  
  {:codeblock}  

 Hai ora collegato il tuo dispositivo IoT di esempio a {{site.data.keyword.iot_short_notm}} e puoi visualizzare i dati del dispositivo.

## Dati del flusso del nodo Node-RED
{: #flow_data}  
Copia il seguente testo nei tuoi appunti e quindi incollalo negli appunti di importazione quando importi i nodi nell'editor del flusso Node-RED.   
**Importante:** assicurati di copiare tutto il testo incluse le parentesi quadre iniziali e finali.  

```
[{"id":"e658d1b6.c187e8","type":"mqtt-broker","z":"965c3822.02c558","broker":"organization_ID.messaging.internetofthings.ibmcloud.com","port":"1883","clientid":"d:organization_ID:device_type:device_ID","usetls":false,"verifyservercert":true,"compatmode":true,"keepalive":"60","cleansession":true,"willTopic":"","willQos":"0","willRetain":"false","willPayload":"","birthTopic":"","birthQos":"0","birthRetain":"false","birthPayload":""},{"id":"23f82ce8.126dc4","type":"mqtt out","z":"965c3822.02c558","name":"Publish to IoT","topic":"iot-2/evt/event_name/fmt/json","qos":"","retain":"","broker":"e658d1b6.c187e8","x":480,"y":273,"wires":[]},{"id":"92e2f51f.5126","type":"inject","z":"965c3822.02c558","name":"Send data","topic":"","payload":"","payloadType":"num","repeat":"","crontab":"","once":false,"x":92,"y":265,"wires":[["832b025d.2d24c"]]},{"id":"832b025d.2d24c","type":"function","z":"965c3822.02c558","name":"Device payload","func":"var name1 = \"My Device\";\nvar type1 = \"GPS\";\nvar longitude1 = [-98.49,-97.74,-96.79,-94.20,-90.19,-94.57,-87.62,-87.90,-93.26,-95.99];\nvar latitude1 = [29.42,30.26,32.77,36.37,38.62,39.09,41.87,43.03,44.97,41.25];\nvar velocity1 = context.get('velocity1')||0;\n\n\n\nvelocity1 = velocity1+1;\nif(velocity1 > 20) velocity1=0;\ncontext.set('velocity1',velocity1);\n\nvar counter1 = context.get('counter1')||0;\ncounter1 = counter1+1;\nif(counter1 > 9) counter1 = 0;\ncontext.set('counter1',counter1);\n\nmsg = {\n \tpayload: JSON.stringify(\n \t { d:{\n \"name\" : name1,\n \"location\" : \n {\n \"longitude\" : longitude1[counter1],\n \t \"latitude\" : latitude1[counter1]\n },\n \"velocity\" : velocity1,\n \t \"type\" : type1\n \t }\n \t }\n )\n}\n\nreturn msg;","outputs":1,"noerr":0,"x":270,"y":108,"wires":[["f04ddebd.f55298","23f82ce8.126dc4"]]},{"id":"f04ddebd.f55298","type":"debug","z":"965c3822.02c558","name":"","active":true,"console":"false","complete":"false","x":250,"y":384,"wires":[]},{"id":"d606058f.d3422","type":"comment","z":"965c3822.02c558","name":"Configure Publish to IoT for your environment","info":"1. Double click the node.\n2. Click the edit icon next to the Server field.\n3. Update the Server name to correspond to your Watson IoT Platform organization.\n `organization_ID.messaging.internetofthings.ibmcloud.com`\n\n4. Update the Client ID with your orgainzaiton ID, device type, and device ID:\n `d:organization_ID:device_type:device_ID`\n\n5. Click the Security tab.\n6. Verify that the Username field has the value use-auth-token.\n7. Update the Password field with the Authentication Token that you saved earlier.\n8. Click Update and then OK.\n9. In the upper right corner of the Node-RED flow editor, click Deploy. ","x":570,"y":241,"wires":[]},{"id":"b997cfe2.ebfd7","type":"comment","z":"965c3822.02c558","name":"Function Node","info":"The Function node allows you to pass each message though a JavaScript function.\n\nThe Javascript function creates the message payload that is sent to your Watson IoT Platform organization.","x":271,"y":77,"wires":[]},{"id":"1ce4e378.c5a565","type":"comment","z":"965c3822.02c558","name":"Debug Node","info":"The Debug node causes any message to be displayed in the Debug sidebar. By default, it just displays the payload of the message, but it is possible to display the entire message object.","x":250,"y":414,"wires":[]},{"id":"ba916f5e.695db8","type":"comment","z":"965c3822.02c558","name":"Inject Node","info":"The Inject node allows you to inject messages into a flow, either by clicking the button on the node, or setting a time interval between injects.","x":75,"y":236,"wires":[]}]
```
{:codeblock}
