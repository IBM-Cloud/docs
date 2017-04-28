---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-28"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Initializing BMSClient
{: #sdk_BMSClient}

`BMSCore` provides the HTTP infrastructure that the other {{site.data.keyword.Bluemix}} Web and Mobile services client SDKs use to communicate with their corresponding {{site.data.keyword.Bluemix_notm}} services.


## Initializing your Android application
{: #init-BMSClient-android}

You can either download and import the `BMSCore` package to your Android Studio project, or use Gradle.

1. Import the Client SDK by adding the following `import` statement at the beginning of your project file:

  ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
  ```
  {: codeblock}

2. Initialize the `BMSClient` SDK in your Android application by adding the initialization code in the `onCreate` method of the main activity in your Android application, or in a location that works best for your project.

  ```Java
  BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // Make sure that you point to your region
  ```
  {: codeblock}

  You must initialize the `BMSClient` with the **bluemixRegion** parameter. In the initializer, the **bluemixRegion** value specifies which {{site.data.keyword.Bluemix_notm}} deployment you are using, for example, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK`, or `BMSClient.REGION_SYDNEY`.


## Initializing your iOS application
{: #init-BMSClient-ios}

You can use [CocoaPods](https://cocoapods.org){: new_window} or [Carthage](https://github.com/Carthage/Carthage){: new_window} to get the `BMSCore` package.

1. To install `BMSCore` by using CocoaPods, add the following lines to your Podfile. If your project does not have a Podfile yet, use the `pod init` command.

  ```Swift
  use_frameworks!

  target 'MyApp' do
    pod 'BMSCore'
  end
  ```
  {: codeblock}

  Then run the `pod install` command, and open the generated `.xcworkspace` file. To update to a newer release of `BMSCore`, use `pod update BMSCore`.

  For more information about using CocoaPods, see the [CocoaPods Guides ![External link icon](../icons/launch-glyph.svg "External link icon")](https://guides.cocoapods.org/using/index.html){: new_window}.

2. To install `BMSCore` by using Carthage, follow these [instructions ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/Carthage/Carthage#getting-started){: new_window}.

  1. Add the following line to your Cartfile:

      ```
      github "ibm-bluemix-mobile-services/bms-clientsdk-swift-core"
      ```
      {: codeblock}

  2. Run the `carthage update` command.

  3. After the build is finished, add `BMSCore.framework` to your project by following [Step 3 ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/Carthage/Carthage#getting-started) in the Carthage instructions.

      For applications that are built with Swift 2.3, use the `carthage update --toolchain com.apple.dt.toolchain.Swift_2_3` command. Otherwise, use the `carthage update` command.

3. Import the module.

  ```Swift
  import BMSCore
  ```
  {: codeblock}

4. Initialize the `BMSClient` class, using the following code.

  Place the initialization code in the `application(_:didFinishLaunchingWithOptions:)` method of your application delegate, or in a location that works best for your project.

  ```Swift
  BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Make sure that you point to your region
  ```
  {: codeblock}

  You must initialize the `BMSClient` with the **bluemixRegion** parameter. In the initializer, the **bluemixRegion** value specifies which {{site.data.keyword.Bluemix_notm}} deployment you are using, for example, `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom`, or `BMSClient.Region.sydney`.


## Initializing your Cordova application
{: #init-BMSClient-cordova}

1. Add the Cordova plugin by running the following command from your Cordova application root directory:

  ```
  cordova plugin add bms-core
  ```
  {: codeblock}

2. Initialize the `BMSClient` class in your Cordova application by adding the initialization code in the main JavaScript file, or in a location that works best for your project.

  ```
  BMSClient.initialize(BMSClient.REGION_US_SOUTH);
  ```
  {: codeblock}
	
  You must initialize the `BMSClient` with the **bluemixRegion** parameter. In the initializer, the **bluemixRegion** value specifies which {{site.data.keyword.Bluemix_notm}} deployment you are using, for example, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK`, or `BMSClient.REGION_SYDNEY`.


# Related Links
{: #rellinks notoc}

## Related Links
{: #general notoc}

* [BMSCore Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [BMSCore iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [BMSCore Cordova Plugin](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}