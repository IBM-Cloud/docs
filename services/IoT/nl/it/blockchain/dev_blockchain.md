---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Sviluppo degli smart contract blockchain
{: #iotblockchain_link}

Utilizza {{site.data.keyword.blockchainfull}} e l'ambiente di sviluppo Hyperledger per creare e verificare i tuoi propri smart contract derivati dai contratti semplici forniti da IBM.
{:shortdesc}

Sviluppo e distribuzione degli smart contract nel formato degli eseguibili chaincode Golang. Utilizza l'integrazione blockchain {{site.data.keyword.iot_short_notm}} per attivare gli aggiornamenti del contratto e per l'esecuzione della logica di business con i dati evento del dispositivo e per scrivere un nuovo stato ledger per il blockchain per ogni transazione.

Un ambiente di sviluppo di integrazione blockchain {{site.data.keyword.iot_short_notm}} è formato dai seguenti componenti:

- L'organizzazione {{site.data.keyword.Bluemix_notm}}:
  - Il servizio {{site.data.keyword.iot_short_notm}} con l'integrazione blockchain IoT abilitata
  - Il fabric {{site.data.keyword.blockchainfull_notm}}
  - L'applicazione Node-RED in esecuzione sul simulatore del dispositivo IoT
   

**Nota:** puoi anche utilizzare un ambiente Node-RED distribuito localmente per eseguire il simulatore.

- L'ambiente locale:
  - L'ambiente di sviluppo Hyperledger per sviluppare e verificare il chaincode del smart contract. L'ambiente include GoLang.
  - La IU di monitoraggio blockchain
- L'ambiente GitHub:
  - Il repository GitHub fornito da IBM per gli smart contract di esempio
  - Il repository GitHub per lo sviluppo degli smart contract per il fabric {{site.data.keyword.blockchainfull_notm}}

Il seguente diagramma illustra l'ambiente di sviluppo dell'integrazione blockchain {{site.data.keyword.iot_short_notm}}:
![L'architettura di integrazione {{site.data.keyword.iot_short_notm}} blockchain IoT.](images/architecture_contracts.svg "IoT blockchain {{site.data.keyword.iot_short_notm}} integrationarchitecture")

## Prima di cominciare

{: #byb}

Ottieni una panoramica di {{site.data.keyword.blockchainfull_notm}}, come si relaziona al concetto di blockchain generale e cosa può fare per te:
- [{{site.data.keyword.blockchainfull_notm}} ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/blockchain/){: new_window} in IBM.com.
- [DOCUMENTI {{site.data.keyword.blockchainfull_notm}}](https://console.ng.bluemix.net/docs/services/blockchain/index.html) -  Introduzione al servizio {{site.data.keyword.blockchainfull_notm}}.
- [{{site.data.keyword.blockchainfull_notm}} HFC SDK for Node.js with API documentation ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/hyperledger/fabric/tree/v0.6/docs/API){: new_window} -  Una panoramica dell'API {{site.data.keyword.blockchainfull_notm}}.
- [{{site.data.keyword.blockchainfull_notm}} for Developers ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/blockchain/for_developers.html){: new_window}  - Una panoramica di come blockchain si adatti al tuo ambiente di sviluppo che include spiegazioni esaurienti con codice e demo live distribuibili per l'esecuzione su {{site.data.keyword.Bluemix_notm}}.

## Smart contract di esempio

{: #samples}

Alcuni contratti di esempio sono disponibili per lo scaricamento dal sito [https://github.com/ibm-watson-iot/blockchain-samples ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-watson-iot/blockchain-samples){: new_window}. Puoi utilizzare i contratti di esempio come base per lo sviluppo dei tuoi propri casi di utilizzo nel chaincode distribuibile:

|Contratto di esempio |Descrizione |
|:---|:---|
|[Basic: Simple Contract ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-watson-iot/blockchain-samples/tree/master/contracts/basic/simple_contract){: new_window} | Una versione semplificata del contratto avanzato che ti consente di tenere traccia e di archiviare i dati dell'asset del dispositivo nel blockchain
|[Advanced: IoT Generic Sample Contract ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-watson-iot/blockchain-samples/tree/master/contracts/advanced/iot_sample_contract){: new_window} | Un contratto di esempio avanzato con molte funzioni e un tipo **commerciale** ai propri funzionamento e modello di dati.|


## Configura il tuo ambiente {{site.data.keyword.blockchainfull_notm}}

{: #configure_environment}
Prima di iniziare a distribuire e verificare gli smart contract, devi configurare il tuo proprio ambiente blockchain.

**Nota:** l'integrazione blockchain {{site.data.keyword.iot_short_notm}} supporta la connessione ai fabric {{site.data.keyword.blockchainfull_notm}} e Hyperledger. I seguenti esempi si basano sull'utilizzo di {{site.data.keyword.blockchainfull_notm}}.

1. Crea e configura il tuo proprio fabric {{site.data.keyword.blockchainfull_notm}}.
L'integrazione blockchain {{site.data.keyword.iot_short_notm}} richiede il fabric {{site.data.keyword.blockchainfull_notm}} per gestire il ledger blockchain, gli smart contract e l'infrastruttura blockchain generale. L'integrazione blockchain {{site.data.keyword.Bluemix_notm}} utilizza {{site.data.keyword.blockchainfull_notm}} per gestire le catene. Se hai accesso a un ambiente {{site.data.keyword.blockchainfull_notm}} esistente, puoi utilizzarlo. Se non hai accesso, devi creare un'istanza di {{site.data.keyword.blockchainfull_notm}} dal catalogo {{site.data.keyword.Bluemix_notm}} [](https://console.ng.bluemix.net/catalog/services/blockchain/).

  1. Dal tuo dashboard dell'account {{site.data.keyword.Bluemix_notm}}, fai clic su **Utilizza servizi o API**.
  2. Individua la sezione Servizi applicazione del catalogo del servizio e seleziona **Blockchain**.  
   **Suggerimento:** Fai clic [qui](https://console.ng.bluemix.net/catalog/services/blockchain/) per andare direttamente alla pagina del servizio {{site.data.keyword.blockchainfull_notm}}.
  3. Nella pagina del servizio {{site.data.keyword.blockchainfull_notm}}, verifica le selezioni di aggiunta del servizio:  
    - Spazio - Se hai più dello spazio `dev` predefinito, verifica che stai distribuendo il servizio nello spazio voluto.
    - Applicazione - Lascia senza bind.
    - Nome servizio - Facoltativamente, modifica il nome del servizio con qualcosa facile da ricordare. Questo nome viene visualizzato nel tile di {{site.data.keyword.blockchainfull_notm}} nel dashboard {{site.data.keyword.Bluemix_notm}}.
    - Piano selezionato - Seleziona il piano gratuito. Il piano gratuito fornisce due peer di convalida e un'autorità del certificato.
  4. Fai clic su **Crea** per distribuire {{site.data.keyword.blockchainfull_notm}} a {{site.data.keyword.Bluemix_notm}}.  
  Il blockchain viene distribuito con due nodi peer iniziali. Puoi aggiungere ulteriori nodi se necessario.

4. Collega {{site.data.keyword.iot_short_notm}} al tuo servizio {{site.data.keyword.blockchainfull_notm}}  
    Per scrivere nel blockchain da {{site.data.keyword.iot_short_notm}}, devi prima collegare i servizi.
     1. In {{site.data.keyword.Bluemix_notm}}, vai al dashboard
     2. Seleziona lo spazio nel quale hai distribuito {{site.data.keyword.blockchainfull_notm}}.
     3. Fai clic sul link **Blockchain** sotto **Servizi**.
     4. Fai clic sulla scheda **Credenziali del servizio**.
     5. Seleziona una serie di credenziali del servizio o fai clic su **Nuova credenziale** per crearne una nuova e fornisci un nome descrittivo, come ad esempio "IoT-Platform-integration."
     6. Nelle credenziali del servizio formattate JSON, prendi nota dei seguenti parametri:  
      - Informazioni peer: `api_host` e `api_port_tls`
      - Informazioni sull'utente del tipo 1 (client): `username` e `secret`  

      Esempio di credenziali del servizio:
     ```json
     {
      "peers": [
      {
        "discovery_host": "fa68cbcbfcec4726932e53e2fa4f3afc-vp0.us.blockchain.ibm.com",
        "discovery_port": 30003,
        "api_host": "fa68cbcbfcec4726932e53e2fa4f3afc-vp0.us.blockchain.ibm.com",
        "api_port_tls": 5003,
        "api_port": 5003,
        "event_host": "fa68cbcbfcec4726932e53e2fa4f3afc-vp0.us.blockchain.ibm.com",
        "event_port": 31003,
        "type": "peer",
        "network_id": "fa68cbcbfcec4726932e53e2fa4f3afc",
        "container_id": "e33f08f85988bf57ccfcf34ccdb80d72489e5bfb46786b570e1a74a6679f804e",
        "id": "fa68cbcbfcec4726932e53e2fa4f3afc-vp0",
        "api_url": "http://fa68cbcbfcec4726932e53e2fa4f3afc-vp0.us.blockchain.ibm.com:5003"
    },
       ...
      ],
      "users": [
      {
        "enrollId": "user_type1_0",
        "enrollSecret": "63c58806d6",
        "affiliation": "group1",
        "username": "user_type1_0",
        "secret": "63c58806d6"
      },
       ...
       ]
      }
     }
     ```  
     **Importante:** l'utente che selezioni non deve essere precedentemente registrato con un peer diverso da quello selezionato.
     7. Fai clic su **Back to Dashboard** per ritornare al tuo dashboard {{site.data.keyword.Bluemix_notm}}.
     8. Seleziona lo spazio nel quale hai distribuito {{site.data.keyword.iot_short_notm}}.
     9. Fai clic sul link **{{site.data.keyword.iot_short_notm}}** sotto **Servizi**.
     10. Fai clic su **Launch** per aprire il dashboard {{site.data.keyword.iot_short_notm}}.
     11. Dal dashboard {{site.data.keyword.iot_short_notm}}, seleziona **Extensions** nella barra laterale del menu.
     12. Nella pagina **Extensions**, nel tile Blockchain, fai clic su **Setup** o su ![Gear icon](../images/gear.png "Configure") se già disponi di fabric collegati.
     13. Nella sezione di configurazione del blockchain, fai clic su **Add Fabric** e immetti quindi le informazioni sul fabric.
    **Nota:** l'integrazione blockchain deve essere abilitata per aggiungere fabric. Per informazioni, consulta [Blockchain](../reference/extensions/index.html#blockchain) nell'argomento delle integrazioni dei servizi esterni.
    1. Nella scheda **Fabric**, immetti un nome che identifica il fabric in {{site.data.keyword.iot_short_notm}}, quindi fai clic su **Next**.   
    2. Nella scheda **Peer**, immetti le informazioni sul peer:  
   <table>
   <thead>
   <tr>
   <th>Parametro</th>
   <th>Valore</th>
   </tr>
   </thead>
   <tbody>
   <tr>
   <td>Nome</td>
   <td>Immetti un nome che identifica il peer in {{site.data.keyword.iot_short_notm}}.</td>
   </tr>
   <tr>
   <td>Host</td>
   <td>L'indirizzo `api_host` per il server di convalida del peer 1</td>
   </tr>
   <tr>
   <td>Porta</td>
   <td>Il numero The `api_port_tls`</td>
   </tr>
   <tr>
   <td>ID utente</td>
   <td>La stringa `username` per l'utente che è stato utilizzato per registrare il smart contract con il blockchain. Puoi anche utilizzare questo ID quando in seguito configurerai a IU semplice.</td>
   </tr>
   <tr>
   <td>Chiave segreta</td>
   <td>La stringa `secret` per l'utente</td>
   </tr>
   <tr>
   <td>Utilizza TLS</td>
   <td>Attivo o Non attivo</br>Utilizza TLS (Transport Layer Security) per codificare la comunicazione tra {{site.data.keyword.iot_short_notm}} e il contratto nel fabric. È necessario abilitare TLS per la connessione a un fabric {{site.data.keyword.blockchainfull_notm}}.</td>
   </tr></tbody>
   </table>  
    3. Fai clic su **Finish**.
     3. Nella sezione di configurazione del blockchain, fai clic su **Done** per salvare le informazioni sul fabric.    

La tabella del fabric viene popolata con la nuova connessione fabric.  

## Crea, verifica e distribuisci i tuoi smart contract
{: #test_contracts}

Puoi ora creare il tuo proprio chaincode del smart contract in GoLang, verificarlo nell'ambiente sandbox e distribuirlo e verificarlo nel tuo proprio fabric {{site.data.keyword.blockchainfull_notm}}.

1. Crea un progetto GitHub per archiviare il tuo chaincode del smart contract.  
Gli smart contract che desideri distribuire devono essere in un repository GitHub pubblico. Per ulteriori informazioni, consulta https://github.com/.
2.  Configura un ambiente di verifica e di sviluppo Hyperledger locale.  
Per sviluppare e verificare il tuo proprio chaincode prima di distribuirlo a {{site.data.keyword.blockchainfull_notm}}, devi configurare un ambiente di sviluppo locale. Questo ambiente include GoLang, che viene utilizzato per scrivere il chaincode per i tuoi contratti.
 1. Configura l'ambiente di sviluppo.  
 L'ambiente di sviluppo include gli strumenti necessari per sviluppare i tuoi smart contract utilizzando il chaincode creato in GoLang. Per ulteriori informazioni, consulta
 [Setting up the development environment ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")]( https://github.com/hyperledger/fabric/blob/master/docs/source/dev-setup/devenv.rst){: new_window} nella documentazione Hyperledger.
 2. Installa un ambiente di debug del chaincode.   
 L'ambiente di debug ti fornisce gli strumenti di cui hai bisogno per verificare ed eseguire il debug dei tuoi smart contract prima di distribuirli a {{site.data.keyword.blockchainfull_notm}}. Per ulteriori informazioni, consulta [Writing, Building, and Running Chaincode in a Development Environment ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/hyperledger/fabric/blob/master/docs/source/Setup/Chaincode-setup.rst){: new_window} nella documentazione Hyperledger.
 3. Configura una rete per lo sviluppo.   
 La rete per lo sviluppo ti fornisce un ambiente rigoroso, simile alla produzione per la verifica finale dei tuoi smart contract.  Utilizza questo ambiente per la verifica finale dei tuoi contratti di debug e verificati prima di distribuirli a {{site.data.keyword.blockchainfull_notm}}. Per ulteriori informazioni, consulta [Setting Up a Network ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/hyperledger/fabric/blob/master/docs/source/Setup/Network-setup.rst){: new_window} nella documentazione Hyperledger.

3. Facoltativo: scarica gli smart contract di esempio forniti da IBM.  
IBM fornisce alcuni smart contract che puoi scaricare e utilizzare direttamente come sono o modificare per adattarsi agli obiettivi della tua organizzazione.  
Per scaricare i contratti di esempio:
 1. Vai nel repository GitHub degli esempi blockchain all'indirizzo: https://github.com/ibm-watson-iot/blockchain-samples/  
 Le cartelle basic_contract_hyperledger e trade_lane_contract_hyperledger contengono rispettivamente i contratti di base e commerciali.
 3. Utilizza `git clone` nel terminale per copiare il progetto https://github.com/ibm-watson-iot/blockchain-samples.  
 **Suggerimento:** puoi anche scaricare un file compresso del progetto facendo clic su **Download ZIP** dalla pagina del progetto.

6. Crea e verifica un smart contract.   
 Utilizzando l'integrazione blockchain {{site.data.keyword.iot_short_notm}}, puoi caricare gli smart contract nel formato degli eseguibili chaincode per {{site.data.keyword.blockchainfull_notm}} per eseguire la logica di business nei dati del dispositivo scritti nel blockchain. Il chaincode del smart contract è sviluppato con GoLang.  
 Il contratto di esempio è incentrato sulla scrittura dei dati del dispositivo IoT per gli eventi di interesse in un blockchain per la condivisione con terze parti o per creare le voci di log resistenti alla manomissione.
2. Crea gli eseguibili del contratto.  
  Il codice del contratto deve essere convertito in un eseguibile prima che possa essere distribuito al blockchain.  
  **Nota:** il contratto di esempio (sample_contract_hyperledger) è stato già generato e può essere distribuito come è.  
  Completa la seguente procedura:
   1. Apri la tua riga di comando e passa alla cartella del contratto.
   2. Esegui il comando `go generate`.  
   Questo comando esegue qualsiasi comando ‘go generate’ che esiste nel codice. Go generate è uno strumento go program che consente di pre-creare la generazione del codice. Nei contratti di esempio forniti da IBM, go generate è utilizzato per creare il file schemas.go che illustra lo schema del contratto e il file del contratto sample.go.  
   **Importante:** il file schemas.go è un componente critico dell'integrazione blockchain {{site.data.keyword.iot_short_notm}}. Il file consente alla piattaforma di confermare che il contratto è conforme con la specifica di integrazione e consente la visualizzazione dell'API del contratto a cui possono essere associati gli eventi del dispositivo.
   2. Esegui il comando `go build`.  
   Questo comando crea un eseguibile con lo stesso nome della cartella. Il file è un eseguibile del contratto che sarà distribuito al blockchain.

6. Verifica il smart contract nel sandbox Hyperledger.  
  Prima di distribuire il tuo smart contract finale a {{site.data.keyword.blockchainfull_notm}}, puoi verificare e distribuire il chaincode nel sandbox Hyperledger che hai installato come parte dell'ambiente di sviluppo.  

6. Distribuisci il chaincode del smart contract a {{site.data.keyword.blockchainfull_notm}}.  
 Dopo il test e la verifica del tuo contratto in locale, puoi distribuirlo al tuo fabric {{site.data.keyword.blockchainfull_notm}} per la verifica.
  1. Carica il tuo contratto nel tuo repository GitHub pubblico.  
  Ad esempio, carica il file sample.go in:
    
  `http://github.com/{my organization}/{my project}/`
  2. Registra il contratto con il peer a cui ti sei collegato precedentemente.  
  Utilizza un client REST come CURL o Postman per inviare la chiamate di registrazione. Per ulteriori informazioni sulla chiamata di registrazione, consulta [POST registrar API documentation ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/hyperledger/fabric/blob/v0.6/docs/API/CoreAPI.md#registrar){: new_window}. Utilizza le seguenti informazioni durante la registrazione:
  <ul>
  <li>URL: `http://api_host:api_port_tls/registrar`
  <li>Tipo: POST
  <li>Intestazione: `Content type: application/json`
  <li>Payload:  
  ```json
   {  
        "enrollId": "{username}",      
        "enrollSecret": "{secret}"    
   }
   ```

  </ul>
  3. Distribuisci il contratto al peer.  
  Per ulteriori informazioni sulla chiamata di disatribuzione, consulta [POST/chaincode API documentation ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/hyperledger/fabric/blob/v0.6/docs/API/CoreAPI.md#chaincode){: new_window}.  
  Utilizza le seguenti informazioni durante la distribuzione:  
  <ul>
  <li>URL: `http://api_host:api_port_tls/chaincode`
  <li>Tipo: POST
  <li>Intestazione: `Accept: application/json`
  <li>Intestazione: `Content type: application/json`
  <li>Payload:  
  ```
  {
    "jsonrpc": "2.0",
    "method": "deploy",
    "params": {
        "type": 1,
        "chaincodeID":{
              "path": "http://github.com/{my organization}/{my project}/sample.go"
        },
        "ctorMsg": {
            "function":"init",
            "args":["{\"version\":\"1.0\",\"nickname\":\"sample_contract\"}"]
        },
        "secureContext": "username"
    },
    "id":1234
}
  ```  
  </ul>  
  Il tuo contratto è stato distribuito al fabric.  
  **Importante:** prendi nota dell'ID del contratto restituito, che è nel formato stringa alfanumerica di 128 caratteri. Hai bisogno dell'ID del contratto per associare i dispositivi al contratto.  

10. Associa i dati del dispositivo al nuovo smart contract.  
  Per iniziare a scrivere i dati del dispositivo nei nuovi smart contract blockchain, devi prima associare i dati del dispositivo ai contratti.  
   1. In {{site.data.keyword.Bluemix_notm}}, vai al dashboard
   2. Seleziona lo spazio nel quale hai distribuito {{site.data.keyword.iot_short_notm}}.
   3. Fai clic sul servizio **{{site.data.keyword.iot_short_notm}}**.
   4. Fai clic su **Launch** per aprire il dashboard {{site.data.keyword.iot_short_notm}}.
   5. Seleziona **Blockchain**  facendo clic su ![Blockchain.](images/platform_blockchain.png "Blockchain") nella barra laterale del menu.
   6. Fai clic su **Map Device Data**.
   7. Seleziona il tipo dispositivo per cui desideri archiviare i dati nel blockchain e il nome dell'evento che desideri archiviare. Fai clic su **Avanti**.
   8. Seleziona il nome del fabric per il fabric che hai precedentemente creato. Fai clic su **Avanti**.
   9. Immetti le seguenti informazioni e fai clic su **Avanti**:
     - ID contratto - Incolla l'ID del contratto di 128 caratteri che hai salvato quando hai distribuito il contratto.
     - Nome contratto - Immetti un nome che identifica il contratto in {{site.data.keyword.iot_short_notm}}.

     **Suggerimento:** per trovare i tipi di evento per un dispositivo, vai alla pagina **Devices** e fai clic sul nome del dispositivo per aprire la pagina dei dettagli del dispositivo. Scorri verso il basso fino alla sezione **Sensor Information** per visualizzare un elenco dei punti dati e degli eventi disponibili per il dispositivo.

   11. Associa le proprietà del dispositivo disponibili ai parametri del contratto.   
   **Importante:** verifica che il tipo di dati per ogni punto dati che associ corrisponda al tipo di dati necessario dal parametro del contratto che associ.  
   Ad esempio, una proprietà del contratto come l'ID asset del tipo stringa deve essere associata a una proprietà del tipo stringa. I requisiti del parametro del contratto sono definiti nelle definizioni `type` nel codice go del contratto.  
   Ad esempio, il contratto fornito da IBM di base dispone dei seguenti requisiti del parametro del contratto:  
    <ul>
    <li>  ID asset - stringa
    <li>  Ubicazione – georilevazione  
    <ul>
    <li> Latitudine - float64
    <li>  Longitudine - float64
    </ul>
    <li>  Temperatura - float64  
    <li>  Vettore - stringa   
    </ul>  
    Per ulteriori informazioni su come associare i dati del dispositivo ai contratti, consulta [Data mapping example ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-watson-iot/blockchain-samples/wiki/Data-mapping-example){: new_window} nei wiki degli esempi Blockchain IoT in GitHub.
   12. Nella pagina di riepilogo, verifica che le informazioni siano corrette.
   13. I dati del dispositivo da associare al contratto sono visualizzati nella pagina Blockchain.

7. Verifica il tuo smart contract in {{site.data.keyword.blockchainfull_notm}}.  
Per verificare il tuo smart contract, esegui un test end-to-end creando un dispositivo in {{site.data.keyword.iot_short_notm}}, collegandolo a {{site.data.keyword.iot_short_notm}}, configurando IoT Blockchain per collegarsi al tuo fabric blockchain e configurando {{site.data.keyword.iot_short_notm}} per associare e archiviare i messaggi del dispositivo nel blockchain. Utilizzando la console {{site.data.keyword.blockchainfull_notm}}, puoi visualizzare il blockchain per controllare i dati del dispositivo nel ledger. Se il tuo contratto supporta la funzione readAsset(), puoi utilizzare la IU di monitoraggio per visualizzare il tuo blockchain e i dati del dispositivo dal tuo proprio scenario che sta venendo archiviato indelebilmente in un blockchain.

5. Configura la IU di monitoraggio per collegarsi a {{site.data.keyword.blockchainfull_notm}}.  
 **Suggerimento:** e la IU di monitoraggio non è ancora stata installata nel tuo ambiente locale, puoi farlo ora. Segui le istruzioni nel documento readme della IU di monitoraggio disponibile nella directory GitHub [Blockchain Monitoring UI ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-watson-iot/blockchain-samples/tree/master/applications/monitoring_ui){: new_window}.  
 Accedi alle impostazioni di sicurezza facendo clic sul pulsante **CONFIGURATION**.   
 Utilizza le seguenti informazioni per il collegamento a un contratto:
<table>
<thead>
<tr>
<th>Parametro</th>
<th>Valore</th>
<th>Commento</th>
</tr>
</thead>
<tbody>
<tr>
<td>Porta e host API</td>
<td>`http://peer_URL:port`</td>
<td>L'host e la porta dell'API REST {{site.data.keyword.blockchainfull_notm}} preceduti da `https://`. Utilizza l'indirizzo  `api_host` e il numero `api_port_tls`. </td>
</tr>
<tr>
<td>ID chaincode</td>
<td>L'ID del contratto che è stato restituito quando hai registrato il contratto.</td>
<td>L'ID del contratto è una stringa alfanumerica di 128 caratteri che corrisponde alla voce dell'ID del contratto.  
**Importante:** quando tagli e incolli l'ID del contratto, assicurati che non sia incluso alcuno spazio nell'ID. Se l'ID viene inserito non correttamente, le voci del ledger blockchain vengono visualizzate ma la funzione di ricerca dell'asset non funziona.
</td>
</tr>
<tr>
<td>Contesto sicuro</td>
<td>Il tuo utente fabric</td>
<td>Questo parametro è obbligatorio per la connessione alle istanze {{site.data.keyword.blockchainfull_notm}} in {{site.data.keyword.Bluemix_notm}}. Utilizza la voce `secureContext`.  
**Importante:** secureContext deve essere il `username` che hai utilizzato durante la configurazione del fabric.
</td>
</tr>
<tr>
<td>Numero di blocchi da visualizzare</td>
<td>Un numero intero positivo. Valore predefinito: 10</td>
<td>Il numero di blocchi blockchain da visualizzare.
</td>
</tr>
</tbody>
</table>

3. Nella IU di monitoraggio, verifica che la tua configurazione stia funzionando come previsto.  
Utilizza i componenti della IU di monitoraggio per interagire con il tuo contratto blockchain:  
 - Operazioni chaincode  
 Verifica che le operazioni chaincode specifiche del contratto possano essere eseguite come previsto. Ad esempio, per il contratto di base, verifica che eseguendo una funzione `createAsset` venga aggiunto un asset al blockchain.
 - Payload della risposta  
 Verifica che le risposte della richiesta peer vengano visualizzate come previsto quando invii le tue richieste REST dalla scheda Chaincode Operations.
 - Blockchain  
Verifica che i blocchi siano aggiunti alla catena quando trasmetti i dati da un dispositivo collegato o quando utilizzi il componente Chaincode Operations.    

## Passo successivo
{: #next_steps}

Hai ora distribuito e esaminato gli smart contract forniti da IBM di esempio. Tuttavia, i contratti di base e commerciali forniscono pochi esempi delle varie possibilità per cui è stato progettato il chaincode del smart contract. È giunto il momento di provare e associare i tuoi scenari di business ai contratti chaincode in {{site.data.keyword.blockchainfull_notm}}. Ora puoi quindi utilizzare {{site.data.keyword.iot_short_notm}} con l'integrazione blockchain IoT per scrivere i dati del dispositivo nel ledger blockchain ed eseguire la logica di business archiviata come smart contract nella risposta ai dati.     


Buon utilizzo di blockchain!
