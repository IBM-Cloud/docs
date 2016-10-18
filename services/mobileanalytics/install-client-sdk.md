---

copyright:
  years: 2015, 2016
lastupdated: "2016-09-29"

---

# Installing the {{site.data.keyword.mobileanalytics_short}} Client SDKs
{: #mobileanalytics_sdk}

Last updated: 29 September 2016
{: .last-updated}

The {{site.data.keyword.mobileanalytics_short}}
Client SDKs are currently available for Android, iOS and WatchOS.
{: #shortdesc}

## Installing the Android Client SDK
{: #install-sdk-android}

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics)

The {{site.data.keyword.mobileanalytics_short}} Client SDK is distributed with Gradle, a dependency manager for Android projects. Gradle automatically downloads artifacts from repositories and makes them available to your Android application.

1. Create an [Android Studio](http://developer.android.com/sdk/index.html) project or open an existing project.

2. Open the `build.gradle` file that is in your **app module**.

  **Tip**: Your Android project might have two `build.gradle` files: one for the project and one for the app module. Make sure to use the **app module** file.

3. Find the `Dependencies` section of the `build.gradle` file and add a compile dependency for the {{site.data.keyword.mobileanalytics_short}} Client SDK. Your repositories statement should be similar to the following code example:

	```Gradle
      dependencies {
        compile 'com.ibm.mobilefirstplatform.clientsdk.android:analytics:1.+'
    	// other dependencies  
      }
  ```
  {: codeblock}

4. Synchronize your project with Gradle by clicking **Tools &gt; Android &gt; Sync Project with Gradle Files**.

5. Open the `AndroidManifest.xml` file for your Android project. You can find this file in **app > manifests**. Add internet access permission under the `<manifest>` element:

	```XML
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}
6. You have now installed the Android Client SDK. Next,  [Import and initialize](sdk.html#initalize-ma-sdk-android) the Analytics Client SDK.   

## Installing the Swift SDK
{: #installing-sdk-ios}

![CocoaPods Compatible](https://img.shields.io/cocoapods/v/BMSAnalytics.svg)

The {{site.data.keyword.mobileanalytics_full}} SDK enables you to instrument your mobile application. The Swift SDK is available for iOS and watchOS.

### Before you begin
{: #before-you-begin-ios}

Make sure that you correctly set up Xcode. To learn how to set up your iOS development environment, see the [Apple Developer website](https://developer.apple.com/support/xcode/). Read about the [Xcode requirements](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#requirements) for Client SDK Swift Analytics.

The {{site.data.keyword.mobileanalytics_short}} SDK is distributed with [Cocoapods](https://cocoapods.org/) and [Carthage](https://github.com/Carthage/Carthage#getting-started), which are dependency managers for Cocoa projects. CocoaPods and Carthage automatically download artifacts from repositories and makes them available to your application.

#### Cocoapods
{: #cocoapods}

1. If CocoaPods is not installed, run:

    ```
    sudo gem install cocoapods
    ```
    {: codeblock}
    
    For Xcode 8: `sudo gem install cocoapods --pre`
    
   Make sure that you have the latest version of `BMSAnalytics` by updating your local CocoaPods repository, as follows:
   
    ```
    pod repo update master
    ```
    {: codeblock}

2. Follow the [CocoaPods installation instructions](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#cocoapods) on GitHub.
	
3. After you have installed the iOS Client SDK,  [Import and initialize](sdk.html#init-ma-sdk-ios) the Analytics Client SDK.   

#### Carthage
{: #carthage}

Add frameworks to your project using [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos).

1. Follow the [Carthage installation instructions](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#carthage) on GitHub.

2. After you have installed the iOS Client SDK,  [Import and initialize](sdk.html#init-ma-sdk-ios) the Analytics Client SDK.

# rellinks

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## API Reference
{: #api}
* [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
