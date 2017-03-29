---

copyright:
 years: 2015, 2016

---

# Inicialización de SDK Push para aplicaciones iOS
{: #enable-push-ios-notifications-initialize}

Un lugar común para colocar el código de inicialización se encuentra en el delegado de aplicación para la aplicación iOS.
Pulse el enlace **Opciones móviles** en el Panel de control de aplicaciones de Bluemix para obtener la ruta de la aplicación y el GUID.

##Inicialización del SDK principal

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
myBMSClient.defaultRequestTimeout = 10.0 // Timput in seconds
```

##Inicialización del SDK Push del cliente

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

## Ruta, GUID, y región Bluemix

**appRoute**

Especifica la ruta que se asigna a la aplicación de servidor que ha creado en Bluemix.

**GUID**

Especifica la clave exclusiva asignada a la aplicación que ha creado en Bluemix. Este valor distingue entre mayúsculas y minúsculas.

**bluemixRegionSuffix**

Especifica la ubicación en la que se aloja la aplicación. El parámetro `bluemixRegion` especifica qué despliegue de Bluemix está utilizando. Puede establecer este valor con una propiedad estática `BMSClient.REGION` y utilizar uno de estos tres valores:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY
