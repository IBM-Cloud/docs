---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Getting started with {{site.data.keyword.iotinsurance_short}}
{: #iotins_gettingstarted}
*Last updated: 20 June 2016*
{: .last-updated}


{{site.data.keyword.iotinsurance_full}}
is an integrated IoT production instance that collects and analyzes full-context data from policy holders to provide personalized risk assessment, real-time protection, and policy cost reductions.
{:shortdesc}

## Prerequisites
{: #iot4i_prereqs}
You must have a node.js runtime environment in which you can run API calls.

## Getting started
{: #iot4i_gettingstarted}
To get up and running with this service, complete the following steps:
1. Locate the credentials of your instance of the {{site.data.keyword.iotinsurance_short}} service, as follows:
  1. From the {{site.data.keyword.Bluemix_notm}} dashboard, click the {{site.data.keyword.iotinsurance_short}} tile.
  2. Select the **Service Credentials** tab.
  3. Make a note of the automatically generated *user name* and *password*. You need them to log onto the {{site.data.keyword.iotinsurance_short}} dashboard and the APIs. Be aware that both the user name and the password are case sensitive.
2. Modify the config.js file with your {{site.data.keyword.iotinsurance_short}} credentials. For sample APIs, see [IoT for Insurance API Examples](https://github.com/ibm-watson-iot/ioti-samples).
3. Create at least one user in the {{site.data.keyword.iotinsurance_short}} system by running `node createUser.js`.
4. Create a shield association for each user by running `node createUserShieldAssociation.js`. For more information about shields, see [Components](iotinsurance_overview.html#components}).
5. Simulate one or more hazard events by running `node simulateHazard.js`.
6. (optional) Create a set of simulated historical data by running `node createHistoricalData.js`.
7. View the users, hazards, and optional simulated data that you created in the previous steps, as follows:
  1. In the {{site.data.keyword.iotinsurance_short}} console, select the **Manage** tab.
  2. Display the {{site.data.keyword.iotinsurance_short}} dashboard by clicking **Open**.
8. (optional) View or try the APIs by clicking **APIs**.
9. Install and connect the [sample mobile starter app](#iot4i_mobile) using the credentials of the user that you created previously.


## Installing and connecting the mobile starter app
{: #iot4i_mobile}

The {{site.data.keyword.iotinsurance_full}} mobile starter app is a reference implementation for a mobile client of the {{site.data.keyword.iotinsurance_short}} solution. By using this app, you can register new devices in the system and receive alerts for these devices.
{:shortdesc}

### Prerequisites
 Required:
  - An [{{site.data.keyword.Bluemix}} account](https://console.ng.bluemix.net/). A 30-day trial account is free.
  - The {{site.data.keyword.iotinsurance_short}} service deployed in {{site.data.keyword.Bluemix_notm}}.
  - Apple Xcode 7.3 or higher integrated development environment.
  - An iOS 9.0 or higher iPhone mobile device.
  - CocoaPods installed on your computer. See the [CocoaPods website](https://guides.cocoapods.org/using/getting-started.html).
  - The [parameters](#iot4i_mobileParam) that are required to connect the mobile starter app to your instance of the service.

### Locating the parameters for your mobile starter app
  {: #iot4i_mobileParam}

To locate the correct values for the parameters that are required in your **constants.swift** file, as follows:
1. In your {{site.data.keyword.Bluemix_notm}} dashboard, select your {{site.data.keyword.iotinsurance_short}} service to display the console.
2. Click **Service Credentials**.  
  - **applicationRoute** - this value is labeled as **uri**.  It is the URL for your instance of {{site.data.keyword.iotinsurance_short}}, for example: https://myIoT4I_instance.mybluemix.net.  
  -   **applicationId** - this value is labeled as **mobile_client_access_id**.

### Building the mobile starter app
To try the mobile starter app, perform the following tasks:

1. Clone the [source code repository for the mobile starter app](https://github.com/ibm-watson-iot/ioti-mobile) onto a computer on which Xcode 7.3 or above is installed.
2. Install the required packages and generate the IoT4I.xcworkspace file by running a CocoaPods pod install command on your project. You must have CocoaPods installed to complete this task.
3. Open the project in Xcode by double-clicking the IoT4I.xcworkspace file.
4. Connect your iPhone to your computer and select it as a build destination.
5. Select the IoT4I file in the list of files to display the Identity dialog.
6. In the Identity dialog box in Xcode, make the following changes:
  - Change the **Bundle Identifier** to a unique identifier, for example: "myIoT4Ibundle".
  - Set **Team** to your personal team name and then click **Fix Issue**.
7. To connect your app to your instance of {{site.data.keyword.iotinsurance_short}}, set the following parameters in the **constants.swift** file:  
    - [applicationRoute](#iot4i_mobileParam) = the URL for your instance of {{site.data.keyword.iotinsurance_short}}
    - [applicationId](#iot4i_mobileParam) = the mobile client access ID for your instance of {{site.data.keyword.iotinsurance_short}}
8. On your computer, click the arrow to build and run the current scheme. The mobile starter app is installed on your phone. For more information, see the [Apple developer instructions for running apps on devices from Xcode](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/LaunchingYourApponDevices/LaunchingYourApponDevices.html).

  **Note:** If an error is displayed when you try to build that says "Could not launch "IoT4I" because you have not yet verified that your Developer App certificate is trusted on your device", select yourself as a Trusted Developer, by completing the following steps:  
    1. On your phone, go to **Settings > General > Device Management > yourDeveloperID**.
    2. Tap your developer ID account name to establish trust for your developer ID.
    3. When prompted, confirm that the developer ID is trusted.

### Locating the parameters required for push notifications
{: #iot4i_pushNotifparam}
You will need to know the Application ID and the Push App Secret to enable push notifications.
To locate the values for the push notifications
  1. In your {{site.data.keyword.Bluemix_notm}} dashboard, select your {{site.data.keyword.iotinsurance_short}} service to display the console.
  2. Click **Service Credentials**.  
  3. Locate the Application ID. This value is the last segment of the `push_url`.  For example, in the following sample push-url, the Application ID is `8d2dd57f-90ca-417a-bd59-85c2df1c03bd`.

  ` "push_url":"http://imfpush.stage1.ng.bluemix.net/imfpush/v1/apps/8d2dd57f-90ca-417a-bd59-85c2df1c03bd"`

  4. Locate the Push App Secret. This value is located in `push_appSecret`.

### Enabling push notifications for the mobile app
{: #iot4i_pushNotification}

Perform the following tasks to enable push notifications for your mobile device. You must have a valid Apple Developer Account membership to use the push notification service.

1. Log into your Apple developer account at https://developer.apple.com/account.
2. Create a certificate file, as follows:
  1. Select **Certificates, Identifiers & Profiles**.
  2. Select Identifiers: App IDs.
  3. Click the Add button (+) to create a new App ID.
  4. Enter a description for the App in **Description**.
  5. Select **Explicit App ID** and enter a bundle ID, for example com.YourOrganizationName.iot4i.mobileApp).
  6. Select (V) on **Push Notifications** and click **Continue > Register > Done**.

3. Create a push notification certificate, as follows:
  1. Select **Certificates: All**.
  2. Click the Add button (+) to create a new APN certificate.
  3. In the Add iOS Certificate page, select **Apple Push Notification service SSL (Sandbox)** and click **Continue**.
  4. Select the App ID you created in the previous step and click **Continue**.
  5. Create a CSR file using the instructions that are on the page and click **Continue**.
  6. Select the CSR file that you created and click **Continue**.
  7. Download and run the certificate file.

4. Create a profile, as follows:
  1. Select **Provisioning profile: Development**.
  2. Click the Add button (+) to create a new development profile.
  3. Select **iOS App Development** and click **Continue**.
  4. Select the App ID that you created previously.
  5. Select **Developer Certificates: All** and click **Continue**.
  5. Select **All development devices (testing devices)** and click **Continue**.
  6. Specify a Profile Name and click **Continue**.
  7. Download and run the generated profile.

5. Create a P12 file and add it to the {{site.data.keyword.Bluemix_notm}} service.
  1. Open Keychain Access and select **My Certificates**.
  2. Right click on **Apple Development IOS Push Service: (bundleID)** and then export, save, and enter a password for the file.

  3. On the [IBM Push Notifications REST API page](https://mobile.ng.bluemix.net/imfpushrestapidocs/#!/applications/put_apps_applicationId_settings_apnsConf), expand the **applications** group and select **/apps/{applicationId}/settings/apnsConf**.

  4. Enter the following values:
     - applicationId. This value is found in your [service credentials](#iot4i_pushNotifparam)
     - password. This is the certificate password.
     - appSecret. This value is found in your [service credentials](#iot4i_pushNotifparam)
     - the certificate file that you created previously
     - issandbox = true  

  5. Click *Try it out* to verify that you have entered the values correctly.
6. In Xcode, change the bundle identifier to the one you created previously.
7. Run the app and grant permisssions for the Push Notification service.

# Related Links
{: #rellinks}

## Tutorials and Samples
{: #samples}
* [Sample mobile starter app](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## API Reference
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API examples](https://github.com/ibm-watson-iot/ioti-samples){:new_window}

## Related Links
{: #general}
* [{{site.data.keyword.iot_full}} documentation](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
