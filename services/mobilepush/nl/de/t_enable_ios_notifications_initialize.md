---

copyright:
 years: 2015, 2016

---

# Push-SDK für iOS-Apps initialisieren
{: #enable-push-ios-notifications-initialize}

Das Anwendungs-Delegat für die iOS-Anwendung ist eine übliche Position für den
Initialisierungscode.
Klicken Sie auf den Link **Mobile Systemerweiterungen** in Ihrem Bluemix-Anwendungsdashboard, um
die Anwendungsroute und die GUID abzurufen.

##Core-SDK initialisieren

###Objective-C

```
// Initialize the SDK for Object-C with IBM Bluemix GUID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```

###Swift

```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstance

myBMSClient.initializeWithBluemixAppRoute("BluemixAppRoute", bluemixAppGUID: "APPGUID", bluemixRegion:"Location where your app Hosted")
myBMSClient.defaultRequestTimeout = 10.0 // Timeout in seconds
```

##Client-Push-SDK initialisieren

###Objective-C

```
//Initialize client Push SDK for Objective-C
IMFPushClient _pushService = [IMFPushClient sharedInstance];
```

###Swift

```
//Initialize client Push SDK for Swift
let push = BMSPushClient.sharedInstance
```

## Route, GUID und Bluemix-Region

**appRoute**

Gibt die Route an, die der Serveranwendung zugewiesen ist, die Sie in Bluemix erstellt haben.

**GUID**

Gibt den eindeutigen Schlüssel an, der der Anwendung zugewiesen wird, die Sie in Bluemix erstellt haben. Bei diesem Wert muss die Groß-/Kleinschreibung beachtet werden.

**bluemixRegionSuffix**

Gibt den Standort an, an dem die App gehostet ist. Der Parameter `bluemixRegion` gibt an, welche Bluemix-Bereitstellung verwendet wird. Sie können diesen Wert mit der statischen Eigenschaft `BMSClient.REGION` angeben und einen von drei Werten verwenden:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY
