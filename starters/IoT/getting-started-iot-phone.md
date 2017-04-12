---

copyright:
  years: 2017
lastupdated: "2017-03-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Guide - a mobile web app to get started with {{site.data.keyword.iot_short_notm}} 
In this getting started guide, we'll take you through a simple node.js app that will use your mobile phone to simulate an IoT device and send live accelerometer data to {{site.data.keyword.iot_short_notm}} on Bluemix

## Prerequisites
{: #prereqs}
You'll need the following accounts and tools:
* [{{site.data.keyword.Bluemix_notm}} account](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git-scm.com/downloads){: new_window}
* A mobile phone that can send accelerometer data via a web application to IBM.

If you have another IoT device or want to simulate one without a phone, try one of our [other IoT getting started topics](https://bluemix.net/docs/starters/IoT/iot500.html).
{: tip}


## 1. Deploy {{site.data.keyword.iot_short_notm}}
{: #deploy_watson_iot_platform_service}

You can use the Cloud Foundry CLI to deploy services to {{site.data.keyword.Bluemix_notm}}.

Run the following command to set your API endpoint, replacing the _API-endpoint_ value with the API endpoint for your region.
   ```
cf api <API-endpoint>
   ```
   {: pre}

|API endpoint                    |Region          |
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net     | US South       |
| https://api.eu-gb.bluemix.net  | United Kingdom |
| https://api.au-syd.bluemix.net | Sydney         |

Log in to your {{site.data.keyword.Bluemix_notm}} account.

  ```
cf login
  ```
  {: pre}

Deploy the {{site.data.keyword.iot_short_notm}} to {{site.data.keyword.Bluemix_notm}} calling it `iotp-for-phone`.
  ```
cf create-service iotf-service iotf-service-free iotp-for-phone
  ```
  {: pre}

## 2. Deploy the sample web application
{: #deploy_app}

1. First, clone the Node.js *iot phone* sample app GitHub repo.
  ```
git clone https://github.com/mzuliani-ibm/discover-iot-phone-sample
  ```
  {: pre}
  
2. On the command line, change the directory to where the sample app is located.
  ```
cd discover-iot-phone-sample
  ```
  {: pre}  
  
3. From within the *iot phone* directory, push your app to {{site.data.keyword.Bluemix_notm}} and give it your own name (replace *my-iot-phone-app* in the command below).
  ```
cf push my-iot-phone-app --no-start
  ```
  {: pre}

4. Deploying your application can take a few minutes.


## 3. Bind the app to {{site.data.keyword.iot_short_notm}}
{: #bind_app_to_service}
1. From within the *iot phone* directory, bind your app to your instance of the {{site.data.keyword.iot_short_notm}} using the names you provided for each above.
  ```
cf bind-service my-iot-phone-app iotp-for-phone
  ```
  {: pre}
2. Restage your application for the binding to take effect.
  ```
cf restage my-iot-phone-app
  ```
  {: pre}
  
3.  When deployment completes, you'll see a message that your app is running. View your app at the URL listed in the output of the push command, or view both the app deployment status and the URL by running the following command:
  ```
cf apps
  ```
  {: pre}

You can troubleshoot errors in the deployment process by using the `cf logs <Your-App-Name> --recent` command.
{: tip} 


## 4. Run the web app on your desktop
{: #run_app_desktop}

  . Open the given URL to see your app, it won't work yet, but this will verify that it deployed correctly.
https://*app-name*.mybluemix.net
For example, it could be:
https://my-iot-phone-app.mybluemix.net
  
  2. Send the phone app URL to your phone via QR code or the email link from your desktop browser.
  It will have the URL format:
  �https://*app-name*.mybluemix.net/iot-phone


## 5. Run the web app on your phone
{: #send_iot_data}

  1. Enter a device ID and password for your device.
  2. Open the {{site.data.keyword.iot_short_notm}} to verify the device is registered.
    * Login to your Bluemix dashboard: https://bluemix.net
    * Go to your list of services: 
    * Click on the Watson IoT Platform tile.
    * Open Watson IoT Platform with *Launch* button, it will open in a new browser tab with a URL like https://*iot-org-id*.internetofthings.ibmcloud.com
    * Go to the Devices tab and verify that your device is there.
  3. Shake your phone to send the data.


## 6. See raw data in the {{site.data.keyword.iot_short_notm}}
{: #see_live_data}

1. Open Watson IoT Platform
2. Go to Boards
3. Go to the "Device Centric Analytics" board
4. Select your device on the "Devices I Care About" card.
3. Shake phone and see live text data in the "Device Properties" card.

## 6. Visualize live data in the {{site.data.keyword.iot_short_notm}}
{: #add_card}

Create a dashboard card to see live acceleration data.

1. On the same "Device Centric Analytics" board
2. Add new card button
3. Select Line Chart
4. For Card source data select: Cards > "Devices I Care About" then Next
5. On "Connect data set", select "Connect new data set"
6. Event: sensorData
7. Property: d.ay
8. Name: Accel. Y
9. Type: Float
10. Unit: gs *Next*
11. Card preview > Settings: L *Next*
12. Card information > Title: Acceleration *Submit*
13. Shake your phone to see the live data in your new card!

# Next Steps
1. [Connect your device to {{site.data.keyword.iot_short_notm}}](https://bluemix.net/docs/services/IoT/iotplatform_task.html)
2. [Learn more about {{site.data.keyword.iot_short_notm}}](https://bluemix.net/docs/services/IoT/iotplatform_overview.html)

