---

copyright:
 years: 2015, 2016

---

# Inizializzazione di Push SDK per applicazioni Android
{: #android_initialize}

Un posto comune dove inserire il codice di inizializzazione è nel metodo onCreate dell'attività principale nella tua applicazione Android.

Fai clic sul link **Opzioni mobili** nel tuo dashboard dell'applicazione Bluemix per ottenere rotta e applicationGUID dell'applicazione. Utilizza questi valori per la rotta e il GUID dell'applicazione. Modifica il frammento di codice per utilizzare la tua applicazione Bluemix appRoute e i parametri appGUID.


## Inizializza il Core SDK

```
// Inizializza l'SDK for Java (Android) con IBM Bluemix AppGUID e la rotta
BMSClient.getInstance().initialize(getApplicationContext(), "applicationRoute","applicationGUID", bluemixRegion:"Ubicazione in cui è ospitata la tua applicazione");
```


**appRoute**

Specifica la rotta assegnato all'applicazione server creata in Bluemix.

**AppGUID**

Specifica la chiave univoca assegnata all'applicazione creata in Bluemix. Questo valore è
                sensibile al maiuscolo/minuscolo.

**bluemixRegionSuffix**

Specifica l'ubicazione in cui è ospitata l'applicazione. Puoi utilizzare uno dei seguenti tre valori:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

## Inizializza il Push SDK client

```
//Inizializza il Push SDK for Java client
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext());
```
