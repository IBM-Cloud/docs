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

The {{site.data.keyword.amafull}} service is replaced with the {{site.data.keyword.appid_full}} service.

# {{site.data.keyword.amashort}} SDKs, samples, and API reference


To add {{site.data.keyword.amafull}} SDKs to your client app, choose the SDKs that you want to use. Then configure your dependency manager to pull the SDKs into your app.
{:shortdesc}

**Note:** Subsequent sections give additional information about installing the SDKs.

## Core SDK
{: #coresdk}

The Core SDK includes APIs for enabling custom authentication and logging.

### Android
{: #coresdk-android}

[GitHub repo ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}

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

[GitHub repo ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security){: new_window}

#### Install the Core SDK with CocoaPods
{: #coresdk-ios-siwft-cocoapods}
Edit the Podfile and add the following line to the required targets and run:

```
use_frameworks!
pod 'BMSSecurity'
```
{: codeblock}


### Cordova
{: #coresdk-cordova}

[GitHub repo and API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}

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

[GitHub repo ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication){: new_window},

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

[GitHub repo ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication){: new_window}

#### Install the Facebook SDK with CocoaPods
{: #facebooksdk-ios-swift-cocoapods}

Edit the Podfile and add the following to the required targets and run:
```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```
{: codeblock}


### Cordova
{: #facebooksdk-cordova}

[GitHub repo and API reference![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}

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

[GitHub repo ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication){: new_window},


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

[GitHub repo ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication){: new_window}

#### Install the Google+ SDK with CocoaPods
{: #googlesdk-ios-swift-cocoapods}

Edit the Podfile and add the following and run:

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```
{: codeblock}


### Cordova
{: #googlesdk-cordova}

[GitHub repo and API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}

#### Install the Google+ SDK with the Cordova CLI
{: #googlesdk-cordova-cli}

Install the plug-in:

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## Server SDK for Node.js servers
{: #serversdk}

[GitHub repo ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy){: new_window}

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

[GitHub repo ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk){: new_window}

#### Install the OAuth SDK with npm
{: #oauthsdk}

Run NPM to install the SDK:
```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## Custom identity provider samples
{: #customidprovider}

[Simple sample GitHub repo ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}

[Advanced sample GitHub repo ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}
