---

Copyright :
  Années : 2015, 2016

---

# Initialisation du logiciel SDK Push pour les applications iOS
{: #enable-push-ios-notifications-initialize}

Le code d'initialisation se trouve généralement dans le délégué d'application de l'application iOS.
Cliquez sur le lien **Options pour application mobile** dans le tableau de bord de votre application Bluemix pour obtenir la route
de l'application et l'identificateur global unique.

##Initialisation du logiciel SDK de base

###Objective-C

```
// Initialisez le logiciel SDK pour Object-C avec la route et l'identificateur global unique IBM Bluemix
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```

###Swift

```
// Initialisez le logiciel SDK de base pour Swift avec la route, l'identificateur global unique et la région IBM Bluemix
let myBMSClient = BMSClient.sharedInstance

myBMSClient.initializeWithBluemixAppRoute("BluemixAppRoute", bluemixAppGUID: "APPGUID", bluemixRegion:"Location where your app Hosted")
myBMSClient.defaultRequestTimeout = 10.0 // Timput in seconds
```

##Initialisation du logiciel SDK Push du client

###Objective-C

```
//Initialisez le logiciel SDK Push du client pour Objective-C
IMFPushClient _pushService = [IMFPushClient sharedInstance];
```

###Swift

```
//Initialisez le logiciel SDK Push du client pour Swift
let push = BMSPushClient.sharedInstance
```

## Route, identificateur global unique et région Bluemix

**appRoute**

Spécifie la route qui a été affectée à l'application serveur que vous avez créée dans Bluemix.

**GUID**

Spécifie la clé unique qui a été affectée à l'application que vous avez créée dans Bluemix. Cette
valeur est sensible à la casse.

**bluemixRegionSuffix**

Indique l'emplacement où l'appli est hébergée. Le paramètre ```bluemixRegion``` spécifie le déploiement Bluemix que vous utilisez. Vous pouvez définir cette valeur avec une propriété statique ```BMSClient.REGION`` et utiliser l'une des trois valeurs suivantes :

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY
