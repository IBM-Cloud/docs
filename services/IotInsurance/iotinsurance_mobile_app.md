---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Installing and connecting the sample mobile app
{: #iot4i_gettingstarted}

The {{site.data.keyword.iotinsurance_full}} sample mobile app is a reference implementation for a mobile client of {{site.data.keyword.iotinsurance_short}}. You can use the app to register new devices in the system and receive alerts for the devices.
{:shortdesc}

**Note**: {{site.data.keyword.iotinsurance_short}} no longer deploys either {{site.data.keyword.amafull}} or {{site.data.keyword.mobilepushfull}}. Earlier versions of {{site.data.keyword.iotinsurance_short}} used the {{site.data.keyword.amashort}} service to process the responses from the mobile app. This process continues to work for all existing instances of {{site.data.keyword.iotinsurance_short}}. However, you must create a custom authentication process to use the mobile app with new instances of
{{site.data.keyword.iotinsurance_short}}. You can also optionally [create an instance of  {{site.data.keyword.mobilepushshort}}](../mobilepush/index.html), configure it, and bind it to the {{site.data.keyword.iotinsurance_short}} API.

**Prerequisites:** Before you begin, ensure that the following prerequisites are in place:
  - Apple Xcode 8 or higher integrated development environment.
  - An iOS 9.0 or higher iPhone mobile device.
  - CocoaPods installed on your computer. See the [CocoaPods website ![External link icon](../../icons/launch-glyph.svg)](https://guides.cocoapods.org/using/getting-started.html){: new_window}.
  - The [parameters](#iot4i_mobileParam) that are required to connect the sample mobile app to your instance of the service.

## Building the sample mobile app
{: #building_mobile}
To try the sample mobile app, perform the following tasks:

1. Clone the [source code repository for the sample mobile app ![External link icon](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-mobile){: new_window} onto a computer on which Xcode 7.3 or above is installed.
2. Install the required packages and generate the IoT4I.xcworkspace file by running a CocoaPods pod install command on your project. CocoaPods must be installed to complete this task.
3. Open the project in Xcode by double-clicking the IoT4I.xcworkspace file.
4. Connect your iPhone to your computer and select it as a build destination.
5. Select the IoT4I file in the list of files to display the Identity dialog box.
6. In the Identity dialog box in Xcode, make the following changes:
  - Change the **Bundle Identifier** to a unique identifier, for example: **myIoT4Ibundle**.
  - Set **Team** to your personal team name and then click **Fix Issue**.
7. To connect your app to your instance of {{site.data.keyword.iotinsurance_short}}, set the following parameters in the **constants.swift** file:  
    - [applicationRoute](#iot4i_mobileParam) = the URL for the {{site.data.keyword.iotinsurance_short}} API application. You can find this value in the Service Credentials tab of the {{site.data.keyword.iotinsurance_short}} service console.
    - [applicationId](#iot4i_mobileParam) = the GUID for your instance of {{site.data.keyword.amashort}}. You can find this value by opening {{site.data.keyword.amashort}}, then clicking **Mobile Options**.  The value is called App GUID / TenantId.
8. On your computer, click the arrow to build and run the current scheme. The sample mobile app is installed on your phone. For more information, see the [Apple developer instructions for running apps on devices from Xcode ![External link icon](../../icons/launch-glyph.svg)](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/LaunchingYourApponDevices/LaunchingYourApponDevices.html){: new_window}.

  **Note:** If an error is displayed when you try to build that says *Could not launch IoT4I because you have not yet verified that your Developer App certificate is trusted on your device*, select yourself as a Trusted Developer, as follows:  
    1. On your phone, go to **Settings > General > Device Management > yourDeveloperID**.
    2. Tap your developer ID account name to establish trust for your developer ID.
    3. When prompted, confirm that the developer ID is trusted.

## Enabling push notifications for the mobile app
{: #iot4i_pushNotification}

Perform the following tasks to enable push notifications for your mobile device. You must have a valid Apple Developer Account membership to use the push notification service.

1. Log in to your [Apple developer account ![External link icon](../../icons/launch-glyph.svg)](https://developer.apple.com/account){: new_window}.

2. Create a certificate file.
  1. Select **Certificates, Identifiers & Profiles**.
  2. Select Identifiers: App IDs.
  3. Click the Add button (+) to create a new App ID.
  4. Enter a description for the App in **Description**.
  5. Select **Explicit App ID** and enter a bundle ID, for example com.YourOrganizationName.iot4i.mobileApp).
  6. Select (V) on **Push Notifications** and click **Continue > Register > Done**.

3. Create a push notification certificate.
  1. Select **Certificates: All**.
  2. Click the Add button (+) to create a new APN certificate.
  3. In the Add iOS Certificate page, select **Apple Push Notification service SSL (Sandbox)** and click **Continue**.
  4. Select the App ID you created in the previous step and click **Continue**.
  5. Create a CSR file by using the instructions that are on the page and click **Continue**.
  6. Select the CSR file that you created and click **Continue**.
  7. Download and run the certificate file.

4. Create a profile.
  1. Select **Provisioning profile: Development**.
  2. Click the Add button (+) to create a new development profile.
  3. Select **iOS App Development** and click **Continue**.
  4. Select the App ID that you created previously.
  5. Select **Developer Certificates: All** and click **Continue**.
  5. Select **All development devices (testing devices)** and click **Continue**.
  6. Specify a Profile Name and click **Continue**.
  7. Download and run the generated profile.

5. Create a Public Key Cryptography Standards (PKCS) 12 file and add it to the {{site.data.keyword.mobilepushshort}} service.
  1. Open Keychain Access and select **My Certificates**.
  2. Right-click **Apple Development IOS Push Service: (bundleID)** and then export, save, and enter a password for the file.
  3. In your {{site.data.keyword.Bluemix_notm}} console, open the {{site.data.keyword.mobilepushshort}} service.
  4. Click **Configure**.
  5. In the Apple Push Notifications Certificate section, upload the PKCS 12 file and enter the password.
  6. In Xcode, change the bundle identifier to the one you created previously.
  7. Run the app and grant permissions for the Push Notification service.
