---

copyright:
 years: 2015, 2016

---

# Push-SDK für Android-Apps initialisieren
{: #android_initialize}

Die Methode 'onCreate' der Hauptaktivität in Ihrer Android-Anwendung ist eine übliche Position für den Initialisierungscode.

Klicken Sie auf den Link **Mobile Systemerweiterungen** in Ihrem Bluemix-Anwendungsdashboard, um
die Anwendungsroute und die Anwendungs-GUID abzurufen. Verwenden Sie diese Werte für Ihre Route und App-GUID. Ändern Sie das Code-Snippet so, dass die Parameter 'appRoute' und 'appGUID' der Bluemix-App verwendet werden.


## Core-SDK initialisieren

```
// Initialize the SDK for Java (Android) with IBM Bluemix AppGUID and route
BMSClient.getInstance().initialize(getApplicationContext(), "applicationRoute","applicationGUID", bluemixRegion:"Location where your app Hosted");
```


**appRoute**

Gibt die Route an, die der Serveranwendung zugewiesen ist, die Sie in Bluemix erstellt haben.

**AppGUID**

Gibt den eindeutigen Schlüssel an, der der Anwendung zugewiesen wird, die Sie in Bluemix erstellt haben. Bei diesem Wert muss die Groß-/Kleinschreibung beachtet werden.

**bluemixRegionSuffix**

Gibt den Standort an, an dem die App gehostet ist. Sie können einen von drei Werten verwenden:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

## Client-Push-SDK initialisieren

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext());
```
