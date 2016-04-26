---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}

# {{site.data.keyword.amashort}} SDKs, Samples, API references
To add {{site.data.keyword.amashort}} SDKs to your app, choose the SDKs that you want to use and then configure your dependency manager to pull the SDKs into your app.

## Core SDK
{: #coresdk}
The Core SDK includes APIs for enabling custom authentication, monitoring, and logging in your mobile app.

### Android
{: #coresdk-android}
[Git repo](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core),
[API reference](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### Install the Core SDK with Gradle
{: #coresdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'core',
    	version: '1.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (Swift SDK)
{: #coresdk-ios-swift}

[Git repo](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)

#### Install the Core SDK with CocoaPods
{: #coresdk-ios-siwft-cocoapods}

```
use_frameworks!
pod 'BMSCore'
```

### iOS (Objective-C SDK)
{: #coresdk-ios}

[Git repo](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master),
[API reference](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)

#### Install the Core SDK with CocoaPods
{: #coresdk-ios-cocoapods}

```Bash
pod 'IMFCore'
```

### Cordova
{: #coresdk-cordova}

[Git repo and API reference](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Install the Core SDK with the Cordova CLI
{: #coresdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## {{site.data.keyword.amashort}} client SDK for Facebook authentication
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[Git repo](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication),
[API reference](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### Install the Facebook SDK with Gradle
{: #facebooksdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'facebookauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (Swift SDK)
{: #facebooksdk-ios-swift}

[Git repo](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication)

#### Install the Facebook SDK with CocoaPods
{: #facebooksdk-ios-swift-cocoapods}

```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```

### iOS (Objective-C SDK)
{: #facebooksdk-ios}

[Git repo](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[API reference](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

#### Install the Facebook SDK with CocoaPods
{: #facebooksdk-ios-cocoapods}

```Bash
pod 'IMFFacebookAuthentication'
```

### Cordova
{: #facebooksdk-cordova}

[Github repo and API reference](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Install the Facebook SDK with the Cordova CLI
{: #facebooksdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## {{site.data.keyword.amashort}} client SDK for Google Authentication
{: #googlesdk}

### Android
{: #googlesdk-android}

[Github repo](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication),
[API reference](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### Install the Google+ SDK with Gradle
{: #googlesdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'googleauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (Swift SDK)
{: #googlesdk-ios-swift}

[Git repo](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication)

#### Install the Google+ SDK with CocoaPods
{: #googlesdk-ios-swift-cocoapods}

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```

### iOS (Objective-C SDK)
{: #googlesdk-ios}

[Git repo](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[API reference](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### Install the Google+ SDK with CocoaPods
{: #googlesdk-ios-cocoapods}

```Bash
pod 'IMFGoogleAuthentication'
```

### Cordova
{: #googlesdk-cordova}

[Git repo and API reference](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Install the Google+ SDK with the Cordova CLI
{: #googlesdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## {{site.data.keyword.amashort}} server SDK for Node.js servers
{: #serversdk}

[Git repo](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### Install the server SDK with npm
{: #serversdk-npm}

```Bash
npm install -save bms-mca-token-validation-strategy
```

## {{site.data.keyword.amashort}} server SDK for Liberty for Java&trade; server
{: #serverlibertysdk}

[Download TAI artifacts](https://imf-tai.{DomainName}/public/TAI.zip)

## {{site.data.keyword.amashort}} Node.js OAuth SDK
{: #serverlibertysdk-github}

[Git repo](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### Install the OAuth SDK with npm
{: #oauthsdk}

```Bash
npm install -save bms-mca-oauth-sdk
```

## Custom Identity Provider samples
{: #customidprovider}

[Simple sample Git repo](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
[Advanced sample Git repo](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

## IMFURLProtocol
{: #IMFURLProtocol}

[API reference](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### Install the IMFURLProtocol with CocoaPods
{: #IMFURLProtocol-cocoapods}

```Bash
pod 'IMFURLProtocol'
```
