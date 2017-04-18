---

copyright:
 years: 2015, 2016

---

# Inizializzazione di Push SDK per applicazioni iOS
{: #enable-push-ios-notifications-initialize}

Un posto comune dove inserire il codice di inizializzazione è nel delegato dell'applicazione per l'applicazione iOS.
Fai clic sul link **Opzioni mobili** nel tuo dashboard dell'applicazione Bluemix
      per ottenere rotta e GUID dell'applicazione.

##Inizializzazione dell'SDK Core

###Objective-C

```
// Inizializza l'SDK for Object-C con la rotta e la GUID IBM Bluemix
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```

###Swift

```
// Inizializza l'SDK Core for Swift con l'area, la rotta e la GUID IBM Bluemix
let myBMSClient = BMSClient.sharedInstance

myBMSClient.initializeWithBluemixAppRoute("BluemixAppRoute", bluemixAppGUID: "APPGUID", bluemixRegion:"Ubicazione in cui è ospitata la tua applicazione")
myBMSClient.defaultRequestTimeout = 10.0 // Timput in seconds
```

##Inizializzazione del Push SDK client

###Objective-C

```
//Inizializza il Push SDK for Objective-C client
IMFPushClient _pushService = [IMFPushClient sharedInstance];
```

###Swift

```
//Inizializza il Push SDK for Swift client
let push = BMSPushClient.sharedInstance
```

## Rotta, GUID e area Bluemix

**appRoute**

Specifica la rotta assegnato all'applicazione server creata in Bluemix.

**GUID**

Specifica la chiave univoca assegnata all'applicazione creata in Bluemix. Questo valore è
                sensibile al maiuscolo/minuscolo.

**bluemixRegionSuffix**

Specifica l'ubicazione in cui è ospitata l'applicazione. Il parametro `bluemixRegion` specifica quale distribuzione di Bluemix stati utilizzando. Puoi impostare questo valore con una proprietà statica `BMSClient.REGION` e utilizzare uno dei seguenti tre valori:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY
