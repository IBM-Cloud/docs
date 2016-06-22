---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# About {{site.data.keyword.iotelectronics}}
{: #iotelectronics_about}
*Last updated: 11 June 2016*
{: .last-updated}

{{site.data.keyword.iotelectronics_full}} is a fully integrated IoT production instance that lets your apps communicate with and consume data that is collected by your connected appliances, sensors, and gateways.
{:shortdesc}

{{site.data.keyword.iotelectronics}} uses the {{site.data.keyword.iot_full}} service to connect your smart electronic appliances with the applications you develop. It also uses  {{site.data.keyword.iot_full}} to help you analyze and understand the data from your appliances. You can establish rules to identify conditions that need attention and define automated responses, such as sending email, executing a Node-RED workflow, or connecting to web services.  

## Finding the starter

You can find the {{site.data.keyword.iotelectronics}} starter in the [Boilerplates section](https://console.{DomainName}/catalog/starters/iot-for-electronics-starter/) of the {{site.data.keyword.Bluemix_notm}} catalog.  

## What you can do with {{site.data.keyword.iotelectronics}}
{: #Features_iote}
Quickly explore the features of the {{site.data.keyword.iotelectronics}} solution by using simulated appliances and data.

### Connect simulated appliances
Create simulated appliances and connect them to the platform to see streaming live data. Use a web-based app to simulate how an appliance receives commands and performs operations. Mimic failures to generate notices and alerts.

### Try a sample consumer mobile app
Use an iOS phone to see how an appliance owner can interact with the appliance. Send commands to the appliance and receive updates from the appliance by using the platform and {{site.data.keyword.Bluemix_notm}}. Mimic failure events and view the results in the mobile app.

### Connect your own electronic devices
Connect your own devices securely to the cloud and start customizing your own apps. A set of verified examples and recipes is available that you can modify and use for proofs of concept, testing, and experimentation.

## What's in the {{site.data.keyword.iotelectronics}} starter
{: #whatsInStarter}
The starter boilerplate deploys the integrated {{site.data.keyword.iotelectronics}} solution.  All components are bound and deployed automatically for you. The starter app lets you quickly explore the features of the solution by using simulated appliances and data. The sample mobile app shows you how a consumer can register, receive alerts, and control a connected appliance. You can use the samples as starting points for creating your own applications and collecting data from your own appliances. The following services and applications are included in the solution:

![{{site.data.keyword.iotelectronics}} Architecture](images/IoT4E_architecture.svg "{{site.data.keyword.iotelectronics}} architecture")

**{{site.data.keyword.iotelectronics}} service** supports user and device registration and notifications.

**{{site.data.keyword.iot_full}}** lets your apps communicate with and use data that is collected by your connected devices, sensors, and gateways.

<!-- **{{site.data.keyword.iotrtinsights_full}}** enables you to enrich and monitor data from your devices, visualize what's happening now, and respond to emerging conditions by using automated actions. -->

**{{site.data.keyword.amafull}}** enables users of mobile apps to log in by using existing social accounts and ensures that communications with back-end systems are secure.

**{{site.data.keyword.sdk4nodefull}}** enables you to develop, deploy, and scale server-side JavaScript&reg; apps and provides enhanced performance, security, and serviceability.

**Sample mobile app** lets you view the status and communicate with a simulated appliance by using your iOS phone. Find out how to get the mobile app in [Using the Mobile app](iotelectronics_config_mobile.html).

# Related Links
{: #rellinks}
## Components
{: #general}
* [{{site.data.keyword.iot_short}} documentation](https://new-console.ng.bluemix.net/docs/services/IoT/index.html#gettingstartedtemplate)
* [{{site.data.keyword.amafull}} documentation](https://new-console.ng.bluemix.net/docs/services/mobileaccess/index.html)
* [{{site.data.keyword.sdk4nodefull}} documentation](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)


## API documentation
{: #api}
*  [{{site.data.keyword.iotelectronics}} API](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)  
*  [{{site.data.keyword.iot_short}} API](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)
