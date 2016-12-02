---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-30"

---

{:shortdesc: .shortdesc}


# {{site.data.keyword.amashort}} SDKs, Beispiele und API-Referenz
Wenn Sie Ihrer Client-App {{site.data.keyword.amafull}}-SDKs hinzufügen wollen, wählen Sie die SDKs aus, die Sie verwenden wollen. Konfigurieren Sie anschließend Ihren Abhängigkeitenmanager, sodass er die SDKs in Ihre App aufnimmt.
{:shortdesc}

**Hinweis:** In nachfolgenden Abschnitten erhalten Sie weitere Informationen zur Installation der SDKs.

## Kern-SDK
{: #coresdk}

Das Kern-SDK (Core SDK) enthält die APIs zur Aktivierung einer angepassten Authentifizierung und Protokollierung.

### Android
{: #coresdk-android}

[GitHub-Repository](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core),
[API-Referenz](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### Kern-SDK mit Gradle installieren
{: #coresdk-android-gradle}

Fügen Sie eine Abhängigkeit 'compile' zur Datei `build.gradle` Ihrer App hinzu:

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'core',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```
{: codeblock}

### iOS (Swift-SDK)
{: #coresdk-ios-swift}

[GitHub-Repository](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security)

#### Kern-SDK mit CocoaPods installieren
{: #coresdk-ios-siwft-cocoapods}
Bearbeiten Sie die Podfile und fügen Sie die folgende Zeile zu den erforderlichen Zielen hinzu; führen Sie dann die Datei aus:

```
use_frameworks!
pod 'BMSSecurity'
```
{: codeblock}

### iOS (Objective-C-SDK)
{: #coresdk-ios}

Das Objective-C-SDK wird zwar weiterhin vollständig unterstützt und gilt noch als primäres SDK für {{site.data.keyword.Bluemix_notm}} Mobile Services, seine Verwendung und Unterstützung sollen jedoch zugunsten des neuen Swift-SDK noch dieses Jahr eingestellt werden (siehe Abschnitt [iOS-Swift-SDK einrichten](getting-started-ios-swift-sdk.html)).

[Git-Repository](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master),
[API-Referenz](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)

#### Kern-SDK mit CocoaPods installieren
{: #coresdk-ios-cocoapods}

Bearbeiten Sie die Podfile und fügen Sie die folgende Zeile zu den erforderlichen Zielen hinzu; führen Sie dann die Datei aus:
```Bash
pod 'IMFCore'
```
{: codeblock}

### Cordova
{: #coresdk-cordova}

[GitHub-Repository und API-Referenz](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Kern-SDK mit der Cordova-Befehlszeilenschnittstelle (CLI) installieren
{: #coresdk-cordova-cli}

Installieren Sie das Cordova-Plug-in für Mobile Client Access:
```Bash
cordova plugin add bms-core
```
{: codeblock}

## Client-SDK für die Facebook-Authentifizierung
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[GitHub-Repository](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication),
[API-Referenz](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### Facebook-SDK mit Gradle installieren
{: #facebooksdk-android-gradle}

Fügen Sie eine Abhängigkeit 'compile' zur Datei `build.gradle` Ihrer App hinzu:
```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'facebookauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```
{: codeblock}

### iOS (Swift-SDK)
{: #facebooksdk-ios-swift}

[GitHub-Repository](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication)

#### Facebook-SDK mit CocoaPods installieren
{: #facebooksdk-ios-swift-cocoapods}

Bearbeiten Sie die Podfile und fügen Sie Folgendes zu den erforderlichen Zielen hinzu; führen Sie die Datei dann aus:
```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```
{: codeblock}

### iOS (Objective-C-SDK)
{: #facebooksdk-ios}

[Git-Repository](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[API-Referenz](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

**Hinweis:** Das Objective-C-SDK wird zwar weiterhin vollständig unterstützt und gilt noch als primäres SDK für {{site.data.keyword.Bluemix_notm}} Mobile Services, Verwendung und Unterstützung dieses SDK sollen jedoch zugunsten des neuen Swift-SDK noch dieses Jahr eingestellt werden. Für neue Anwendungen wird dringend das Swift-SDK empfohlen (siehe Abschnitt 'iOS-Swift-SDK einrichten').
#### Facebook-SDK mit CocoaPods installieren
{: #facebooksdk-ios-cocoapods}

Bearbeiten Sie die Podfile und fügen Sie die folgende Zeile hinzu; führen Sie die Datei dann aus:

```Bash
pod 'IMFFacebookAuthentication'
```
{: codeblock}

### Cordova
{: #facebooksdk-cordova}

[GitHub-Repository und API-Referenz](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Facebook-SDK mit Cordova-CLI installieren
{: #facebooksdk-cordova-cli}

Installieren Sie das Cordova-Plug-in:

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## Client-SDK für die Google-Authentifizierung
{: #googlesdk}

### Android
{: #googlesdk-android}

[GitHub-Repository](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication),
[API-Referenz](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### Google+-SDK mit Gradle installieren
{: #googlesdk-android-gradle}

Fügen Sie eine Abhängigkeit 'compile' zur Datei `build.gradle` Ihrer App hinzu:

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'googleauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```
{: codeblock}

### iOS (Swift-SDK)
{: #googlesdk-ios-swift}

[GitHub-Repository](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication)

#### Google+-SDK mit CocoaPods installieren
{: #googlesdk-ios-swift-cocoapods}

Bearbeiten Sie die Podfile und fügen Sie Folgendes hinzu; führen Sie die Datei dann aus:

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```
{: codeblock}

### iOS (Objective-C-SDK - nicht mehr verwendet)
{: #googlesdk-ios}

[Git-Repository](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[API-Referenz](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### Google+-SDK mit CocoaPods installieren
{: #googlesdk-ios-cocoapods}

Bearbeiten Sie die Podfile und fügen Sie die folgende Zeile hinzu; führen Sie die Datei dann aus:

```Bash
pod 'IMFGoogleAuthentication'
```
{: codeblock}

### Cordova
{: #googlesdk-cordova}

[GitHub-Repository und API-Referenz](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Google+-SDK mit Cordova-CLI installieren
{: #googlesdk-cordova-cli}

Installieren Sie das Plug-in:

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## Server-SDK für Node.js-Server
{: #serversdk}

[GitHub-Repository](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### Server-SDK mit npm installieren
{: #serversdk-npm}

Führen Sie NPM aus, um das SDK zu installieren:

```Bash
npm install -save bms-mca-token-validation-strategy
```
{: codeblock}

## Server-SDK für Liberty for Java&trade;-Server
{: #serverlibertysdk}

[TAI-Artefakte herunterladen](https://imf-tai.{DomainName}/public/TAI.zip)

#### Liberty-SDK installieren
{: #libertysdk}

1. Kopieren Sie die Datei `com.ibm.worklight.oauth.tai_1.0.0.jar` in das Verzeichnis `$<wlp.user.dir>/extensions/lib`.

  **Tipp:** `$<wlp.user.dir>` ist das Benutzerverzeichnis für die Liberty for Java-Laufzeit. Der Standardverzeichnisname ist `usr`.

1. Kopieren Sie das Verzeichnis `OAuthTai-1.0.mf` in das Verzeichnis `$<wlp.user.dir>/extension/lib/features`.


## Node.js-OAuth-SDK
{: #serverlibertysdk-github}

[GitHub-Repository](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### OAuth-SDK mit npm installieren
{: #oauthsdk}

Führen Sie NPM aus, um das SDK zu installieren:
```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## Angepasster Identitätsprovider - Beispiele
{: #customidprovider}

[Einfaches Beispiel - GitHub-Repository](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)

[Erweitertes Beispiel - GitHub-Repository](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

## IMFURLProtocol
{: #IMFURLProtocol}

[API-Referenz](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### IMFURLProtocol mit CocoaPods installieren
{: #IMFURLProtocol-cocoapods}

Bearbeiten Sie die Podfile und fügen Sie die folgende Zeile hinzu; führen Sie die Datei dann aus:

```Bash
pod 'IMFURLProtocol'
```
{: codeblock}
