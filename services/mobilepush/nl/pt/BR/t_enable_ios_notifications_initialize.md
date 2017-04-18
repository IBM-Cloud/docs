---

copyright:
 years: 2015, 2016

---

# Inicializando apps Push SDK para iOS
{: #enable-push-ios-notifications-initialize}

Um local comum para colocar o código de inicialização é no
aplicativo delegado do aplicativo iOS.
Clique no link **Opções móveis**
em seu Bluemix Application Dashboard
      para obter a rota e GUID de aplicativo.

##Inicializando o SDK principal

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

##Inicializando o SDK de Push do cliente

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

## Rota, GUID e região do Bluemix

**appRoute**

Especifica a rota que é designada ao aplicativo do servidor que você criou no
Bluemix.

**GUID**

Especifica a chave exclusiva que é designada ao aplicativo que você criou no
Bluemix. Esse valor faz
distinção entre maiúsculas e minúsculas.

**bluemixRegionSuffix**

Especifica o local em que o app está hospedado. O parâmetro `bluemixRegion` especifica qual implementação do Bluemix você está usando. É possível configurar esse valor com uma propriedade estática `BMSClient.REGION` e use um dos três valores:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY
