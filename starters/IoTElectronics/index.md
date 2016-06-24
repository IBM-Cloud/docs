---

copyright:
  years: 2016

---

{:new_window: target="_blank"}

{:shortdesc: .shortdesc}


# Creating apps with the {{site.data.keyword.iotelectronics}} starter
*Last updated: 14 June 2016*
{: .last-updated}

{{site.data.keyword.iotelectronics_full}} is an integrated, end-to-end solution that enables your apps to communicate with, control, analyze, and update connected appliances. The starter includes a starter app that lets you create and control simulated appliances and a sample mobile app that lets you control those appliances from your mobile device.
{:shortdesc}

**Prerequisite**:  
Ensure that you've deployed the {{site.data.keyword.iotelectronics}} Starter from Boilerplates section of the Bluemix catalog. Doing so automatically deploys the component applications and services of the starter, including {{site.data.keyword.amafull}}.

To get started with {{site.data.keyword.iotelectronics}}, complete these tasks as described in the sections that follow:

1. Enable communications with the sample mobile app by configuring {{site.data.keyword.amashort}}.
2. Create simulated appliances using the {{site.data.keyword.iotelectronics}} starter web application.
3. Install and connect the sample mobile app.

## Configuring {{site.data.keyword.amashort}}
{: #configureMCA}
To use the mobile app, you must configure {{site.data.keyword.amashort}}, as follows:
1. In your {{site.data.keyword.Bluemix_notm}} dashboard, open [{{site.data.keyword.amashort}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html).
2. In the **Custom** section, select **Configure**.
3. Enter the following authentication credentials:
  - **Realm name**: myRealm
  - **URL**: https://<*myIoT4eStarterApp*>.mybluemix.net  

    **Tip:** Be sure to use the secure `https://` prefix in the URL. You can find the URL of your starter app by clicking **Mobile options**.)
4. Save.

  For detailed instructions, see [Configuring {{site.data.keyword.amashort}}](iotelectronics_config_mobile.html#iot4e_configureMCA).

##Creating simulated appliances
To create a simulated appliance, perform the following steps:
1. In your {{site.data.keyword.Bluemix_notm}} dashboard, start your {{site.data.keyword.iotelectronics}} application.
2. Wait for the *Your app is running* status message and then click **View App** to display the starter app.  
3. Select **Remotely control your connected appliances**.
4. Scroll to the section labeled **Next, choose or add new simulated washer** and click the Add (+) button. A new washer is created.

## Installing and connecting the sample mobile app
To install and connect the sample mobile app, perform the following steps:

*Note*: You must have an iOS device to use the sample mobile app.

1. On your phone, open the App Store and search for `ibm iot`. Choose **IBM IoT for Electronics** and install.
2. Connect your phone to your organization by scanning the Connection QR code found in your starter app.
3. Connect your simulated appliance by scanning the Appliance QR code found in your starter app.

  For detailed instructions, see [Connecting the mobile app to your {{site.data.keyword.iotelectronics}} environment](iotelectronics_config_mobile.html#iot4e_connecting_mobile).

##What's next
See what you can do with {{site.data.keyword.iotelectronics}}.

- Explore the starter app to experience how an enterprise manufacturer can monitor appliances that are connected to the {{site.data.keyword.iot_short_notm}}.
- Explore the sample mobile app to experience how appliance owners can register and interact with their appliances.
- Manually cause a device failure to trigger alerts, notifications, and actions to both the manufacturer and the appliance owner.
- Associate operational data with user data to understand how your products and devices are operating and who is operating them.


# Related Links
{: #rellinks}
## API documentation
{: #api}
* [{{site.data.keyword.iotelectronics}} API](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)
* [{{site.data.keyword.iot_short}} API](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)


## Components
{: #general}

* [{{site.data.keyword.iotelectronics}} documentation](iotelectronics_overview.html)
* [{{site.data.keyword.iot_full}} documentation](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
*  [{{site.data.keyword.amashort}} documentation](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html)
* [{{site.data.keyword.sdk4nodefull}} documentation](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)

## Samples
{: #samples}
* [Sample mobile app](https://new-console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html)
