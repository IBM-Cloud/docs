---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}

# {{site.data.keyword.amashort}}-SDKs, Beispiele und API-Referenzen
Wenn Sie Ihrer App {{site.data.keyword.amashort}}-SDKs hinzufügen wollen, wählen Sie die SDKs aus, die Sie verwenden wollen, und konfigurieren anschließend Ihren Abhängigkeitenmanager, sodass er die SDKs in Ihre App aufnimmt.

## Kern-SDK
{: #coresdk}
Das Kern-SDK (Core SDK) enthält die APIs zur Aktivierung einer angepassten Authentifizierung, Überwachung und Protokollierung in Ihrer mobilen App.

### Android
{: #coresdk-android}
[Git-Repository](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core),
[API-Referenz](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### Kern-SDK mit Gradle installieren
{: #coresdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'core',
    	version: '1.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (Swift-SDK)
{: #coresdk-ios-swift}

[Git-Repository](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)

#### Kern-SDK mit CocoaPods installieren
{: #coresdk-ios-siwft-cocoapods}

```
use_frameworks!
pod 'BMSCore'
```

### iOS (Objective-C-SDK)
{: #coresdk-ios}

[Git-Repository](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master),
[API-Referenz](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)

#### Kern-SDK mit CocoaPods installieren
{: #coresdk-ios-cocoapods}

```Bash
pod 'IMFCore'
```

### Cordova
{: #coresdk-cordova}

[Git-Repository und API-Referenz](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Kern-SDK mit der Cordova-Befehlszeilenschnittstelle (CLI) installieren
{: #coresdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## {{site.data.keyword.amashort}}-Client-SDK für die Facebook-Authentifizierung
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[Git-Repository](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication),
[API-Referenz](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### Facebook-SDK mit Gradle installieren
{: #facebooksdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'facebookauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (Swift-SDK)
{: #facebooksdk-ios-swift}

[Git-Repository](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication)

#### Facebook-SDK mit CocoaPods installieren
{: #facebooksdk-ios-swift-cocoapods}

```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```

### iOS (Objective-C-SDK)
{: #facebooksdk-ios}

[Git-Repository](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[API-Referenz](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

#### Facebook-SDK mit CocoaPods installieren
{: #facebooksdk-ios-cocoapods}

```Bash
pod 'IMFFacebookAuthentication'
```

### Cordova
{: #facebooksdk-cordova}

[Github-Repository und API-Referenz](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Facebook-SDK mit der Cordova-Befehlszeilenschnittstelle (CLI) installieren
{: #facebooksdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## {{site.data.keyword.amashort}}-Client-SDK für die Google-Authentifizierung
{: #googlesdk}

### Android
{: #googlesdk-android}

[Github-Repository](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication),
[API-Referenz](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### Google+-SDK mit Gradle installieren
{: #googlesdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'googleauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (Swift-SDK)
{: #googlesdk-ios-swift}

[Git-Repository](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication)

#### Google+-SDK mit CocoaPods installieren
{: #googlesdk-ios-swift-cocoapods}

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```

### iOS (Objective-C-SDK)
{: #googlesdk-ios}

[Git-Repository](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[API-Referenz](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### Google+-SDK mit CocoaPods installieren
{: #googlesdk-ios-cocoapods}

```Bash
pod 'IMFGoogleAuthentication'
```

### Cordova
{: #googlesdk-cordova}

[Git-Repository und API-Referenz](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Google+-SDK mit der Cordova-Befehlszeilenschnittstelle (CLI) installieren
{: #googlesdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## {{site.data.keyword.amashort}}-Server-SDK für Node.js-Server
{: #serversdk}

[Git-Repository](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### Server-SDK mit 'npm' installieren
{: #serversdk-npm}

```Bash
npm install -save bms-mca-token-validation-strategy
```

## {{site.data.keyword.amashort}}-Server-SDK für Liberty for Java&trade;-Server
{: #serverlibertysdk}

[TAI-Artefakte herunterladen](https://imf-tai.{DomainName}/public/TAI.zip)

## {{site.data.keyword.amashort}}-Node.js-OAuth-SDK
{: #serverlibertysdk-github}

[Git-Repository](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### OAuth-SDK mit 'npm' installieren
{: #oauthsdk}

```Bash
npm install -save bms-mca-oauth-sdk
```

## Beispiele für einen angepassten Identitätsprovider
{: #customidprovider}

[Einfaches Beispiel - Git-Repository](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
[Erweitertes Beispiel - Git-Repository](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

## IMFURLProtocol
{: #IMFURLProtocol}

[API-Referenz](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### IMFURLProtocol mit CocoaPods installieren
{: #IMFURLProtocol-cocoapods}

```Bash
pod 'IMFURLProtocol'
```
