---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# About {{site.data.keyword.iotelectronics}}
{: #iotelectronics_about}
*Last updated: 16 May 2016*

{{site.data.keyword.iotelectronics_full}} is a fully integrated IoT production instance that lets your apps communicate with and consume data that is collected by your connected appliances, sensors, and gateways.
{:shortdesc}

{{site.data.keyword.iotelectronics}} uses the {{site.data.keyword.iot_full}} service to connect your smart electronic appliances with the applications you develop. It also uses  {{site.data.keyword.iotrtinsights_full}} to help you analyze and understand the data from your appliances. You can establish rules to identify conditions that need attention and define automated responses, such as sending email, executing a Node-RED workflow, or connecting to web services.  

## What you can do with {{site.data.keyword.iotelectronics}}
{: #Features_iote}
Quickly explore the features of the {{site.data.keyword.iotelectronics}} solution by using simulated appliances and data.

### Connect simulated appliances
Create simulated appliances and connect them to the platform to see streaming live data. Use a web-based app to simulate how an appliance receives commands and performs operations. Mimic failures to generate notices and alerts.

### Try a sample consumer mobile app
Use an iOS phone to see how an appliance owner can interact with the appliance. Send commands to the appliance and receive updates from the appliance by using the platform and Bluemix. Mimic failure events and view the results in the mobile app.

### Connect your own electronic devices
Connect your own devices securely to the cloud and start customizing your own apps. A set of verified examples and recipes is available that you can modify and use for proofs of concept, testing, and experimentation.

## What's in the {{site.data.keyword.iotelectronics}} Starter
{: #whatsInStarter}
The Starter boilerplate deploys the integrated {{site.data.keyword.iotelectronics}} solution.  All components are bound and deployed automatically for you. The Starter app lets you quickly explore the features of the solution by using simulated appliances and data. The sample mobile app shows you how a consumer can register, receive alerts, and control a connected appliance. You can use the samples as starting points for creating your own applications and collecting data from your own appliances. The following services and applications are included in the solution:

**{{site.data.keyword.iotelectronics}} service** supports user and device registration and notifications.

**{{site.data.keyword.iot_full}}** lets your apps communicate with and use data that is collected by your connected devices, sensors, and gateways.

**{{site.data.keyword.iotrtinsights_full}}** enables you to enrich and monitor data from your devices, visualize what's happening now, and respond to emerging conditions by using automated actions.

**{{site.data.keyword.amafull}}** enables users of mobile apps to log in by using existing social accounts and ensures that communications with back-end systems are secure.

**{{site.data.keyword.sdk4nodefull}}** enables you to develop, deploy, and scale server-side JavaScript&reg; apps and provides enhanced performance, security, and serviceability.

**Sample mobile app** lets you view the status and communicate with a simulated appliance by using your iOS phone. Find out how to get the mobile app [here](iotelectronics_config_mobile.html).

<!--
## Getting started with the sample mobile app
{: #iotforelectronics_getmobileapp}

The {{site.data.keyword.iotelectronics}} sample mobile app lets you receive alerts, send commands, and see the status of your simulated appliances. To get started you must download the app, connect the app to your  {{site.data.keyword.iotelectronics}} Bluemix environment, and then register a simulated appliance. For instructions, see the following sections.

### Downloading the mobile app
To download the mobile app, download and install it on your phone from the Apple App store.  

On your phone, open the App store and search for "ibm iot". Choose **IBM IoT for Electronics** and install. Alternatively, you can install it to your phone by using [iTunes](https://itunes.apple.com/us/app/ibm-iot-for-electronics/id1103404928?ls=1&mt=8).

### Connecting the mobile app
{: #iot4e_connecting_mobile}

To view your simulated devices on your mobile app, you must connect the mobile app to your {{site.data.keyword.iotelectronics}} Bluemix environment.

To connect the mobile app, follow these steps:

  1. On your computer, start your {{site.data.keyword.iotelectronics}} application and click **View App** to display the Starter app.  
  2. Start the consumer app experience by selecting **Consumer App**.
  3. Scroll to the QR code located beneath the heading "In the mobile app on your phone, you'll be asked to scan QR Codes".
  4. On your phone, start the mobile app and tap **Get Started**.
  5. Scroll through the walkthrough, and then click **Try It Out**.
  3. Click the image of a QR code. Enter login credentials when prompted. Your user ID and password can be any length. Be sure to remember what you chose for future sessions.
  4. Select **QR Code scanner**. Scan the QR code on your computer. Your mobile app is now connected to your environment.


### Registering an appliance
{: #iot4e_adding_appliance}

To view appliance status and receive notifications, you must register an  appliance on your mobile app.

To register an appliance, follow these steps:

  1. In the Starter app on your computer, scroll to a simulated washer and click it to display its data and QR code. (If no washer exists, create one by clicking the plus sign.)
  2.	On your phone, register your devices, as follows:
    - To register your first device, select **QR code scanner**.  Scan the QR code of your washer, then click **Register**. The device is displayed in the mobile app.
    - To register another device, click the plus sign on the Appliances Overview page, and then select **QR code scanner**. Scan the QR code of your washer, then click **Register**. The device is displayed in the mobile app.
  3. After your device is registered, you can see the status of the washer on your phone and on your computer.  On your phone, select **Start wash** to start a wash cycle. You can see the changing washer status on both your phone and your computer.
  4. On your computer, select a problem with the washer (such as Board Failure or Strong Vibration).  The problem sends an alert to your iPhone that shows your washer is unavailable.  On your computer, select **Fix machine** to correct the problem. You can see the changing status on both your phone and your computer.
-->

# Related Links
{: #rellinks}
## Components
{: #general}
* [{{site.data.keyword.iot_short}}](https://new-console.ng.bluemix.net/docs/services/IoT/index.html#gettingstartedtemplate)
* [{{site.data.keyword.iotrtinsights_short}}](https://new-console.ng.bluemix.net/docs/services/iotrtinsights/index.html)   
* [{{site.data.keyword.amafull}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/index.html)
* [{{site.data.keyword.sdk4nodefull}}](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)


## API documentation
{: #api}
*  [{{site.data.keyword.iotelectronics}}](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)  
* [{{site.data.keyword.iotrtinsights_short}}](https://iotrti-prod.mam.ibmserviceengage.com/apidoc/)
* [{{site.data.keyword.iot_short}}](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)
