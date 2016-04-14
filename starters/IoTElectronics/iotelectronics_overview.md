{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Getting started with {{site.data.keyword.iotelectronics}}
{: #iotelectronics_about}
*Last updated: 12 April 2016*

{{site.data.keyword.iotelectronics_full}} is a fully integrated IoT production instance that lets your apps communicate with and consume data that is collected by your connected appliances, sensors, and gateways.
{:shortdesc}

{{site.data.keyword.iotelectronics}} uses the {{site.data.keyword.iot_full}} service to connect your smart electronic appliances with the applications you develop. It also uses  {{site.data.keyword.iotrtinsights_full}} to help you analyze and understand the data from your appliances. You can establish rules to identify conditions that need attention and define automated responses, such as sending email, executing a Node-RED workflow, or connecting to web services.  

## What you can do with {{site.data.keyword.iotelectronics}}
{: #Features_iote}
Quickly explore the features of the {{site.data.keyword.iotelectronics}} solution by using simulated appliances and data.

### Connect simulated appliances
Create simulated appliances and connect them to the platform to see streaming live data. Use a web-based app to simulate how an appliance receives commands and performs operations. Mimic failures to generate notices and alerts.

### Try a sample consumer mobile app
Use an iOS phone to see how an appliance owner could interact with the appliance. Send commands to the appliance and receive updates from the appliance via the platform and Bluemix. Mimic failure events and view the results in the mobile app.

### Connect your own electronic devices
Connect your own devices securely to the cloud and start customizing your own apps. We'll provide a set of verified examples and recipes, which you can modify and use for proof of concepts, testing, and experimentation.

## What's in the {{site.data.keyword.iotelectronics}} Starter
{: #whatsInStarter}
The Starter boilerplate deploys the integrated {{site.data.keyword.iotelectronics}} solution.  All components are bound and deployed automatically for you. The Starter app lets you quickly explore the features of the solution by using simulated appliances and data. The sample mobile app shows you how a consumer could register, receive alerts, and control a connected appliance. You can use the samples as starting points for creating your own applications and collecting data from your own appliances. The following services and applications are included in the solution:

**{{site.data.keyword.iotelectronics}} service** supports user and device registration and notifications.

**{{site.data.keyword.iot_full}}** lets your apps communicate with and use data that is collected by your connected devices, sensors, and gateways.

**{{site.data.keyword.iotrtinsights_full}}** enables you to enrich and monitor data from your devices, visualize what's happening now, and respond to emerging conditions through automated actions.

**{{site.data.keyword.amafull}}** enables users of mobile apps to log in with existing social accounts and ensures that communications with back-end systems are secure.

**{{site.data.keyword.sdk4nodefull}}** enables you to develop, deploy, and scale server-side JavaScript&reg; apps, and provides enhanced performance, security, and serviceability.

**Sample mobile app** lets you view the status and communicate with a simulated appliance using your iOS smartphone.  


## Installing the sample mobile app
{: #iotforelectronics_getmobileapp}

The {{site.data.keyword.iotelectronics}} sample mobile app lets you receive alerts, send commands, and see the status of your simulated appliances.   

To install the mobile app, download the source files and follow the instructions in the README.md file located on the [{{site.data.keyword.iotelectronics}} Mobile App GitHub site](https://github.com/ibm-watson-iot/iote-mobile).

# Related Links
{: #rellinks}
## Components
{: #general}
* [{{site.data.keyword.iot_short}}](https://console.ng.bluemix.net/docs/services/IoT/index.html#gettingstartedtemplate)
* [{{site.data.keyword.iotrtinsights_short}}](https://console.ng.bluemix.net/docs/services/iotrtinsights/index.html)   
* [{{site.data.keyword.amafull}}](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html)
* [{{site.data.keyword.sdk4nodefull}}](https://console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)


## API documentation
{: #api}
* [{{site.data.keyword.iotelectronics}}](https://new-console.{DomainName}/apidocs/166)
* [{{site.data.keyword.iotrtinsights_short}}](https://iotrti-prod.mam.ibmserviceengage.com/apidoc/)  
* [{{site.data.keyword.iot_short}}](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)
