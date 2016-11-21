---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-30"

---

{:shortdesc: .shortdesc}


# {{site.data.keyword.amashort}} SDKs, samples, and API reference


To add {{site.data.keyword.amafull}} SDKs to your client app, choose the SDKs that you want to use. Then configure your dependency manager to pull the SDKs into your app.
{:shortdesc}

**Note:** Subsequent sections give additional information about installing the SDKs.

## Core SDK
{: #coresdk}

The Core SDK includes APIs for enabling custom authentication and logging.

### Android
{: #coresdk-android}

[GitHub repo](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core),
[API reference](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### Install the Core SDK with Gradle
{: #coresdk-android-gradle}

Add a compile dependency to your app's `build.gradle` file:

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'core',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```
{: codeblock}

### iOS (Swift SDK)
{: #coresdk-ios-swift}

[GitHub repo](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security)

#### Install the Core SDK with CocoaPods
{: #coresdk-ios-siwft-cocoapods}
Edit the Podfile and add the following line to the required targets and run:

```
use_frameworks!
pod 'BMSSecurity'
```
{: codeblock}

### iOS (Objective-C SDK)
{: #coresdk-ios}

While the Objective-C SDK remains fully supported, and is still considered the primary SDK for {{site.data.keyword.Bluemix_notm}} Mobile Services, there are plans for discontinuing it later this year in favor of the new Swift SDK (see [Setting up the iOS Swift SDK](getting-started-ios-swift-sdk.html)).

[Git repo](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master),
[API reference](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)

#### Install the Core SDK with CocoaPods
{: #coresdk-ios-cocoapods}

Edit the Podfile and add the following line to the required targets and run:
```Bash
pod 'IMFCore'
```
{: codeblock}

### Cordova
{: #coresdk-cordova}

[GitHub repo and API reference](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Install the Core SDK with the Cordova CLI
{: #coresdk-cordova-cli}

Install the Mobile Client Access Cordova plug-in:
```Bash
cordova plugin add bms-core
```
{: codeblock}

## Client SDK for Facebook authentication
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[GitHub repo](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication),
[API reference](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### Install the Facebook SDK with Gradle
{: #facebooksdk-android-gradle}

Add a compile dependency to your app's `build.gradle` file:
```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'facebookauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```
{: codeblock}

### iOS (Swift SDK)
{: #facebooksdk-ios-swift}

[GitHub repo](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication)

#### Install the Facebook SDK with CocoaPods
{: #facebooksdk-ios-swift-cocoapods}

Edit the Podfile and add the following to the required targets and run:
```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```
{: codeblock}

### iOS (Objective-C SDK)
{: #facebooksdk-ios}

[Git repo](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[API reference](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

**Note:** While the Objective-C SDK remains fully supported, and still considered the primary SDK for {{site.data.keyword.Bluemix_notm}} Mobile Services, there are plans to discontinue this SDK later this year in favor of the new Swift SDK. For new applications we highly recommend the Swift SDK (see Setting up the iOS Swift SDK).
#### Install the Facebook SDK with CocoaPods
{: #facebooksdk-ios-cocoapods}

Edit the Podfile and add the following line and run:

```Bash
pod 'IMFFacebookAuthentication'
```
{: codeblock}

### Cordova
{: #facebooksdk-cordova}

[GitHub repo and API reference](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Install the Facebook SDK with the Cordova CLI
{: #facebooksdk-cordova-cli}

Install the Cordova plug-in:

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## Client SDK for Google Authentication
{: #googlesdk}

### Android
{: #googlesdk-android}

[GitHub repo](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication),
[API reference](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### Install the Google+ SDK with Gradle
{: #googlesdk-android-gradle}

Add a compile dependency to your app's `build.gradle` file:

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'googleauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```
{: codeblock}

### iOS (Swift SDK)
{: #googlesdk-ios-swift}

[GitHub repo](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication)

#### Install the Google+ SDK with CocoaPods
{: #googlesdk-ios-swift-cocoapods}

Edit the Podfile and add the following and run:

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```
{: codeblock}

### iOS (Objective-C SDK - Deprecated)
{: #googlesdk-ios}

[Git repo](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[API reference](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### Install the Google+ SDK with CocoaPods
{: #googlesdk-ios-cocoapods}

Edit the Podfile and add the following line and run:

```Bash
pod 'IMFGoogleAuthentication'
```
{: codeblock}

### Cordova
{: #googlesdk-cordova}

[GitHub repo and API reference](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Install the Google+ SDK with the Cordova CLI
{: #googlesdk-cordova-cli}

Install the plug-in:

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## Server SDK for Node.js servers
{: #serversdk}

[GitHub repo](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### Install the server SDK with npm
{: #serversdk-npm}

Run NPM to install the SDK:

```Bash
npm install -save bms-mca-token-validation-strategy
```
{: codeblock}

## Server SDK for Liberty for Java&trade; server
{: #serverlibertysdk}

[Download TAI artifacts](https://imf-tai.{DomainName}/public/TAI.zip)

#### Install the Liberty SDK
{: #libertysdk}

1. Copy the `com.ibm.worklight.oauth.tai_1.0.0.jar` file to the `$<wlp.user.dir>/extensions/lib` directory.

  **Tip:** `$<wlp.user.dir>` is the user directory for the Liberty for Java runtime. The default directory name is `usr`.

1. Copy the `OAuthTai-1.0.mf` directory to the `$<wlp.user.dir>/extension/lib/features` directory.


## Node.js OAuth SDK
{: #serverlibertysdk-github}

[GitHub repo](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### Install the OAuth SDK with npm
{: #oauthsdk}

Run NPM to install the SDK:
```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## Custom identity provider samples
{: #customidprovider}

[Simple sample GitHub repo](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)

[Advanced sample GitHub repo](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

## IMFURLProtocol
{: #IMFURLProtocol}

[API reference](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### Install the IMFURLProtocol with CocoaPods
{: #IMFURLProtocol-cocoapods}

Edit the Podfile and add the following line and run:

```Bash
pod 'IMFURLProtocol'
```
{: codeblock}
