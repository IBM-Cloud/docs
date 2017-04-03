---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

Der {{site.data.keyword.amafull}}-Service wird durch den {{site.data.keyword.appid_full}}-Service ersetzt.

# {{site.data.keyword.amashort}} SDKs, Beispiele und API-Referenz
Wenn Sie Ihrer Client-App {{site.data.keyword.amafull}}-SDKs hinzufügen wollen, wählen Sie die SDKs aus, die Sie verwenden wollen. Konfigurieren Sie anschließend Ihren Abhängigkeitenmanager, sodass er die SDKs in Ihre App aufnimmt.
{:shortdesc}

**Hinweis:** In nachfolgenden Abschnitten erhalten Sie weitere Informationen zur Installation der SDKs.

## Kern-SDK
{: #coresdk}

Das Kern-SDK (Core SDK) enthält die APIs zur Aktivierung einer angepassten Authentifizierung und Protokollierung.

### Android
{: #coresdk-android}

[GitHub-Repository ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}

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

[GitHub-Repository ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security){: new_window}

#### Kern-SDK mit CocoaPods installieren
{: #coresdk-ios-siwft-cocoapods}
Bearbeiten Sie die Podfile und fügen Sie die folgende Zeile zu den erforderlichen Zielen hinzu; führen Sie dann die Datei aus:

```
use_frameworks!
pod 'BMSSecurity'
```
{: codeblock}


### Cordova
{: #coresdk-cordova}

[GitHub-Repository und API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}

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

[GitHub-Repository ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication){: new_window}

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

[GitHub-Repository ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication){: new_window}

#### Facebook-SDK mit CocoaPods installieren
{: #facebooksdk-ios-swift-cocoapods}

Bearbeiten Sie die Podfile und fügen Sie Folgendes zu den erforderlichen Zielen hinzu; führen Sie die Datei dann aus:
```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```
{: codeblock}


### Cordova
{: #facebooksdk-cordova}

[GitHub-Repository und API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}

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

[GitHub-Repository ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication){: new_window}


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

[GitHub-Repository ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication){: new_window}

#### Google+-SDK mit CocoaPods installieren
{: #googlesdk-ios-swift-cocoapods}

Bearbeiten Sie die Podfile und fügen Sie Folgendes hinzu; führen Sie die Datei dann aus:

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```
{: codeblock}


### Cordova
{: #googlesdk-cordova}

[GitHub-Repository und API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}

#### Google+-SDK mit Cordova-CLI installieren
{: #googlesdk-cordova-cli}

Installieren Sie das Plug-in:

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## Server-SDK für Node.js-Server
{: #serversdk}

[GitHub-Repository ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy){: new_window}

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

[GitHub-Repository ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk){: new_window}

#### OAuth-SDK mit npm installieren
{: #oauthsdk}

Führen Sie NPM aus, um das SDK zu installieren:
```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## Angepasster Identitätsprovider - Beispiele
{: #customidprovider}

[GitHub-Repository - einfaches Beispiel ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}

[GitHub-Repository - erweitertes Beispiel ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}
