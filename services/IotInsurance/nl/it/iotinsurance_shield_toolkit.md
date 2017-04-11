---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-01"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Toolkit dello scudo
{: #iot4i_shield_toolkit}
Utilizza gli scudi per proteggere appropriatamente gli utenti identificando i pericoli e crea le risposte automatizzate appropriate. Utilizza o modifica gli scudi inclusi nella libreria degli scudi {{site.data.keyword.iotinsurance_short}} o crea e implementa i tuoi propri scudi utilizzando i seguenti esempi o istruzioni.
{:shortdesc}

## Informazioni sugli scudi.
Uno scudo è una serie di regole e azioni definite che possono essere attivate da condizioni specifiche nell'input che viene ricevuto da un sensore. Ad esempio, potresti creare uno scudo con una regola che crei un messaggio di testo che deve essere inviato se il sensore individua una fuoriuscita d'acqua.

## Utilizzare gli scudi dalla libreria degli scudi {{site.data.keyword.iotinsurance_short}}

Puoi trovare un vasto assortimento di scudi predefiniti nella libreria degli scudi [{{site.data.keyword.iotinsurance_short}} ![icona link esterno](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-shields){: new_window}. Visualizza il file README su tale sito per le istruzioni su come scaricare ed iniziare ad utilizzare gli scudi.

## Creazione del tuo proprio scudo
Questo esempio ti mostra come puoi configurare il tuo ambiente, definire uno scudo, creare un utente e quindi associare lo scudo all'utente.  Puoi inoltre facoltativamente creare promozioni e pericoli simulati.  

Gli esempi di codice per la creazione di un scudo semplice per le fuoriuscite d'acqua vengono illustrate nelle seguenti sezioni. Una serie completa di codici di esempio è disponibile in [iot4i-api-examples-nodejs GitHub repository](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/).

### Prerequisiti
Prima di iniziare, assicurati che siano implementati i seguenti prerequisiti:

- [Node.js](https://nodejs.org/en/) installato sul tuo computer.  
- Un ambiente di runtime abilitato con Node.js come Eclipse.
- Software Git e accesso a [GitHub source code repository for the API examples](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs).   In alternativa, puoi scaricare l'[archivio con i file del codice di origine](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/archive/master.zip).
- Codice di origine pronto.  
  Per preparare il codice di origine, completa la seguente procedura:
  1. Clona o scarica il [GitHub source code repository](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs) sul tuo computer.
  2. Installa i prerequisiti open source del progetto utilizzando una riga di comando per andare alla cartella che contiene i file del codice di origine clonati ed esegui il comando `npm install`.

### Configurazione dell'ambiente
{: #environment}
Per configurare il tuo ambiente per inviare le chiamate API REST, devi configurare l'URL per l'API nel file config.js. L'URL aggregatore può essere ignorato in questo contesto.

```
var config = module.exports = {
  api: "https//iot4insurance-api-<uniqueid>.mybluemix.net",
  aggregator: "https//iot4i-aggregator-<uniqueid>.mybluemix.net",
  credentials : {
    user: "Admin",
    pass: "<password from IoT4I service credentials>"
  }
};
```

### Creazione di una definizione scudo
{: #create_shield_def}

Metodo: POST  
API: /shield  
https://iot4i-docs-api.mybluemix.net/dist/#!/shield/addShield

Crea una definizione scudo nel file createShield.js.  Il seguente esempio mostra uno scudo semplice che rileva una fuoriuscita d'acqua.

```
var shield = {
  "UUID": "26",
  "name": "demoShield",
  "type": "Environmental Measurements",
  "description": "Detect water leaks",
  "image": "shieldWater",
  "canBeDisabled": false,
  "hazardDetectionOnCloud": true,
  "jsCodeMethod": "demoShield",
  "actions": [
     "pushios"
  ],
  "potentialClaimAmount": "10",
  "shieldParameters": []
};

```

dove:
- **UUID** - L'UUID (universal unique identifier) dello scudo.
- **actions** - Un elenco di azioni che vengono attivate quando viene creato un pericolo. In questo esempio, le informazioni sul pericolo vengono inviate all'applicazione dell'utente utilizzando una notifica push iOS.

### Creazione di un codice scudo
{: #create_shield_code}
Crea un codice scudo nel file shieldCode.js per definire come il motore dello scudo elabora un payload.

Il seguente esempio mostra un codice scudo che può essere utilizzato per elaborare un payload di fuoriuscita d'acqua per lo scudo che è stato illustrato negli esempi precedenti.

```
var shieldCode = {
  "name": "demoshield",
  "shieldUUID": "26",
  "type": "shield",
  "code": code.toString()
};

```

Ogni codice scudo contiene le risorse definite nelle istruzioni resource/shield.js. Ognuna delle seguenti risorse include un esempio che può essere utilizzato con lo scudo, il payload e l'utente illustrati negli esempi precedenti.

  - Nome dello scudo  
  ```
  var DEMO_SHIELD_NAME = "demoshield";
  ```

  - Ritardo dello scudo - Il ritardo in millisecondi tra i pericoli.  
  ```
  var DEMO_SHIELD_DELAY = 5000;
  ```

  - UUID (universal unique identifier) dello scudo  
  ```
  var DEMO_SHIELD_UUID = 26;
  ```

  - Condizione iniziale - La condizione e gli attributi obbligatori al motore dello scudo per elaborare il payload. Nell'esempio, la condizione è che il payload debba contenere l'attributo **liquid_detected**.  
  ```
  var demoEntryCondition = function(payload) {
    return (payload.liquid_detected)
  };
  ```

  - Safelet - Il core dello scudo che calcola ed esegue un algoritmo per determinare se è presente un pericolo. Nel seguente esempio, il solo attributo richiesto è **liquid_detected**, ma è possibile utilizzare i safelet per definire algoritmi complessi.  
  ```
  var demoSafelet = function(payload) {
    return (payload.liquid_detected);
  };
  ```

  - Messaggio - Il messaggio inviato all'utente se viene elaborato il pericolo.
  ```
  var demoMessage = function(payload) {
    return (constructMessage(payload, DEMO_SHIELD_UUID, 'demoHazard', 'a demo shield activated!'));
  };
  ```

  - Esecuzione dello scudo - La funzione che viene utilizzata per eseguire direttamente lo scudo, invece di attendere che il motore dello scudo esegua tutti gli scudi pertinenti automaticamente.  
  ```
  var demoShield = function(payload) {
    var shield = getShieldByName(DEMO_SHIELD_NAME);
    return (commonShield (payload, shield));
  };
  ```

  - Scudo registrato - Una funzione predefinita che deve essere richiamata nel codice scudo per registrare lo scudo nel motore dello scudo. Il valore **undefined** nell'esempio rappresenta la funzione pre-elaborata, che non è necessaria in questo esempio in particolare. In alcuni scudi, la funzione pre-elaborata può essere utilizzata per riorganizzare i dati nel payload. Ad esempio, se le letture della temperatura sono riportate in Fahrenheit e il safelet richiede Celsius, è possibile utilizzare la funzione pre-elaborata per convertire le temperature nel valore richiesto.  
  ```
  registerShield(DEMO_SHIELD_UUID, DEMO_SHIELD_NAME, demoEntryCondition, undefined, demoSafelet, demoMessage, DEMO_SHIELD_DELAY);
  ```

### Creazione di un utente
{: #create_user}

Metodo: POST  
API: /user  
https://iot4i-docs-api.mybluemix.net/dist/#!/user/addUser

Crea un utente nel file createUser.js. Il seguente esempio mostra come creare un solo utente.

```
var user = {
  "username": "user1",
  "fullname": "John Doe",
  "firstname": "John",
  "lastname": "Doe",
  "password": "user1234",
  "accessLevel": "100",
  "address": "42 Wallaby Way, Sydney",
  "email": "user@example.com",
  "deviceID": "user1",
  "deviceType": "wink",
  "type": "wink"
};

```

dove:
- **username** - La chiave univoca per l'utente che viene utilizzata per identificare ogni entità associata all'utente, come i dispositivi, gli scudi e le promozioni.
- **password** - Solo l'hash della password viene archiviato nel database.
- **DeviceId** - L'identificativo che viene utilizzato per registrare l'utente in {{site.data.keyword.iot_full}}. Il valore è lo stesso del nome utente.
- **accessLevel** - Il valore definisce gli endpoint dell'API a cui può accedere l'utente:
  - 100 - applicazione mobile
  - 10 - dashboard
  - 1 - amministratore di sistema

### Creazione di un'associazione dello scudo
{: #create_shield_assoc}

Metodo: POST  
API: /user  
https://iot4i-docs-api.mybluemix.net/dist/#!/shieldassociation/addShieldAssociation

Crea un'associazione dello scudo che collega lo scudo all'utente in createUserShieldAssociation.js.

Il seguente esempio mostra un'associazione dello scudo per lo scudo e l'utente che sono stati creati nelle sezioni precedenti.

```
var userShield = {
  "shieldUUID": "26",
  "username": "user1",
  "hazardDetectionOnCloud": true
};

```



### Creazione di un pericolo simulato
{: #create_sim_hazard}

Metodo: POST  
API: /sendPayloadToMQTT  
https://iot4i-docs-api.mybluemix.net/dist/#!/global/sendPayloadToMQTT

Puoi creare un payload di pericolo simulato per verificare i tuoi scudi.

Il seguente esempio mostra come creare un payload che attiva lo scudo creato nell'esempio precedente ed invia un avviso all'utente associato.

```
var parameters {
  "payload": {
    "sensor_pod_id": "190107",
    "name": "Sensor",
    "manufacturer_device_model": "leakSMART",
    "device_manufacturer": "leaksmart",
    "model_name": "leakSMART Sensor",
    "upc_code": "waxman_sensor",
    "hub_id": "379652",
    "lat_lng": [null, null],
    "location": "",
    "status": "online",
    "liquid_detected": true,
    "usr": "user1",
    "activation": "2016-06-20T12:05:02.776Z"
  },
  "outputtype": "evt",
  "devicetype": "wink",
  "deviceid": "wink",
  "type": "wink"
};

```


### Creazione di una promozione
{: #create_promotion}

{{site.data.keyword.iotinsurance_short}} può inviare promozioni ai proprietari di casa utilizzando l'applicazione mobile. Crea le promozioni utilizzando il file createPromotion.js.

Il seguente esempio mostra come creare una promozione per un idraulico autorizzato.

```
var promotion = {
  "title": "Promotion 9",
  "description": "Contact one of our authorized plumbers to install your water leak detection solution.",
  "buttonTitle": "Call Now",
  "type": "1",
  "phone": "+015555555555",
  "username": "user1",  
};

```

Puoi facoltativamente distribuire la tua applicazione mobile ed utilizzare [le istruzioni nel repository GitHub ioti-mobile](https://github.com/ibm-watson-iot/ioti-mobile) per collegarti come un utente creato nella sezione precedente.

# Link correlati
{: #rellinks}

## Riferimento API
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [{{site.data.keyword.iotinsurance_short}} API Examples](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}

## Link correlati
{: #general}
* [Developer support forum](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Stack overflow support forum](http://stackoverflow.com/questions/tagged/ibm-bluemix)
