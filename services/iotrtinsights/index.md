---

copyright:
  years: 2015,2016

---

{:new_window: target=_"blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Getting started with {{site.data.keyword.iotrtinsights_full}}
{: #gettingstartedtemplate}
*Last updated: 28 April 2016*

With {{site.data.keyword.iotrtinsights_full}} on {{site.data.keyword.Bluemix_notm}} ({{site.data.keyword.iotrtinsights_short}}), you can perform analytics on real-time data from your Internet of Things devices, and gain insights about their health and the overall state of your operations.
{:shortdesc}

Before you can start using {{site.data.keyword.iotrtinsights_short}} you must set up the {{site.data.keyword.iot_full}} service ({{site.data.keyword.iot_short}}) to connect your analytics engine to your devices.  You can use an existing {{site.data.keyword.iot_short}} service or create a new one. To quickly get up and running your can deploy the Internet of Things phone application and its associated {{site.data.keyword.iot_short}} service to your organization.

To get up and running quickly with this service, follow these steps:
1. Deploy the {{site.data.keyword.iotrtinsights_short}} service to your {{site.data.keyword.Bluemix_notm}} organization.
  1. From your {{site.data.keyword.Bluemix_notm}} account Dashboard, click **Use services or APIs**.
  2. Locate the Internet of Things section of the service catalog and select **{{site.data.keyword.iotrtinsights_short}}**.
  3. On the {{site.data.keyword.iotrtinsights_short}} page, verify the Add Service selections:  
    - Space - Verify that you are deploying the service in the same space that you deployed the {{site.data.keyword.iot_short}} service.
    - App - Leave unbound.
    - Service name - Optionally change the service name to something that is easy to remember. This name is displayed in the IoT {{site.data.keyword.iotrtinsights_short}} tile in the {{site.data.keyword.Bluemix_notm}} dashboard.
    - Selected plan - Select Free or a purchase plan that is suitable for your needs.  
  4. Click **Use** to deploy {{site.data.keyword.iotrtinsights_short}} to your {{site.data.keyword.Bluemix_notm}} services.
2. Optional: Use your phone as an IoT device with IoT {{site.data.keyword.iotrtinsights_short}}.  
Use the Internet of Things phone application to quickly set up your smart phone to act as an IoT device that you can use to verify your {{site.data.keyword.iotrtinsights_short}} environment and begin to define real-time analytics on the data.For more information about the Internet of Things Phone application, see the [Internet of Things phone application](https://github.com/ibm-messaging/IoT-html5-phone) project.

  To create the application and connect your phone to the {{site.data.keyword.iot_full}}:
  1. Click the following button to start the deployment process:   
  [![Deploy to Bluemix icon.](images/deploy_to_bluemix.png "Deploy to Bluemix icon")](https://bluemix.net/deploy?repository=https://github.com/ibm-messaging/iot-html5-phone "Deploy the IoT Phone to Bluemix")  
  **Note:** Deploying the Internet of Things phone application also deploys an {{site.data.keyword.iot_short}} service (*iot-phone-iotf-service*) that automatically binds to the phone application. Add this {{site.data.keyword.iot_short}} as a data source to test the Internet of Things phone application. It also creates a Cloudant NoSQL DB service (*iot-phone-cloudant-cloudantNoSQLDB*) that is used by the application.

  2. Click **Approve** if you are prompted to self approve access for IBM Single Sign On Service (OAuth Consent).  
  **Tip:** If you don't have a {{site.data.keyword.Bluemix_notm}} account you can sign up to activate your free {{site.data.keyword.Bluemix_notm}} trial.
  2. Change the APP NAME field to something easy to remember; we'll call this *phone application* throughout the rest of these instructions. This name will be displayed in an application tile in your {{site.data.keyword.Bluemix_notm}} dashboard and is part of the URL that you will use when connecting your phone to {{site.data.keyword.iot_short}}.
  2. Click **Deploy**.
  2. After the deployment process is complete and you see a 'Success' message, return to your {{site.data.keyword.Bluemix_notm}} dashboard.  
  The *phone application* tile and the *iot-phone-iotf-service* tile are added to your account.
  1. From the {{site.data.keyword.Bluemix_notm}} dashboard, click the *phone application* tile.
  2. From your phone, open a browser and go to the Routes URL that is displayed beneath the application name. When prompted, enter a device ID of your choosing to identify your phone as a device in the {{site.data.keyword.iot_short}} and IoT {{site.data.keyword.iotrtinsights_short}} dashboards.
  3. Click **Connect** to connect your phone to the {{site.data.keyword.iot_short}} *iot-phone-iotf-service*.  
  The view refreshes to display the data that is sent from your phone to your {{site.data.keyword.iot_short}}.
2. Create and configure an Internet of Things service.  
**Tip:** If you deployed the Internet of Things phone application, the  *iot-phone-iotf-service* is already created and you can skip this step.  

  1. Log in to the {{site.data.keyword.Bluemix_notm}} organization and select the space where you want to deploy IoT {{site.data.keyword.iotrtinsights_short}}.
  2. From the {{site.data.keyword.Bluemix_notm}} Dashboard, click **Use services or APIs**.
  3. Locate the Internet of Things section of the service catalog and select **Internet of Things**.
  4. On the {{site.data.keyword.iot_full}} page, verify the Add Service selections and click **Use** to add {{site.data.keyword.iot_short}} to your {{site.data.keyword.Bluemix_notm}} services.  
  After the {{site.data.keyword.iot_short}} service is deployed, you are brought to the service management page.
3. Locate the connection API keys.  
If you created a new {{site.data.keyword.iot_short}} service, you must now create API keys to connect the two services. If you are using an existing service, you can use the existing keys.  
  1. From the {{site.data.keyword.Bluemix_notm}} dashboard, click the Internet of Things tile.  
  **Note:**  If you are using the Internet of Things phone application, click the the *iot-phone-iotf-service* tile.  

  1. Click **Launch dashboard** to open the {{site.data.keyword.iot_full}} dashboard.
  2. Navigate to **Access > API Keys**.
  3. Click **Generate API Key**.
  3. Make a note of the API Key and the Authentication Token.  
  This information, together with the Organization ID, is used in {{site.data.keyword.iotrtinsights_short}} to connect the services.
4. Connect your {{site.data.keyword.iot_short}} service and IoT {{site.data.keyword.iotrtinsights_short}} service.  
**Important:** Each instance of IoT Real-Time Insights supports one data source. To add data sources beyond the first, deploy an additional IoT Real-Time Insights instance from the {{site.data.keyword.Bluemix_notm}} dashboard and add the data source to that instance.
  1. From the {{site.data.keyword.Bluemix_notm}} dashboard, click the IoT {{site.data.keyword.iotrtinsights_short}} tile.  
  2. In the service page, click **Add a data source**.
  2. In the {{site.data.keyword.iotrtinsights_short}} console Manage Data Sources page, click **Add New Data Source**.
  3. Give the data source a descriptive name and provide the following information that you collected earlier:
    - Organization ID
    - API Key
    - Authentication Token
  4. Click ![Create icon.](images/create.png "Create icon") to create the data source and connect to it.
4. Start using {{site.data.keyword.iotrtinsights_short}}.  
You can now start using {{site.data.keyword.iotrtinsights_short}} by adding users, connecting your devices, configuring dashboards to view relevant device data, and setting up alerts.  
**Switching {{site.data.keyword.iotrtinsights_short}} instances:** You can quickly switch between the {{site.data.keyword.iotrtinsights_short}} instances that you have operator or administrator access to by clicking your user name and selecting the instance that you want to access. Each instance is labeled with the {{site.data.keyword.iot_short}} organization ID that is used as data source for the instance.    

# rellinks
## samples
* [Internet of Things phone application](https://github.com/ibm-messaging/IoT-html5-phone)
* [developerWorks Internet of Things Recipes](https://developer.ibm.com/recipes/)
* [Creating apps with the Internet of Things starter application](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html#iot500)

## api
* [API Documentation](https://iotrti-prod.mam.ibmserviceengage.com/apidoc/)

## general
* [About](iotrtinsights_overview.html)   
* [What's new in {{site.data.keyword.Bluemix_notm}} Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category)
* [Getting started with {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html)
* [dW Answers on IBM developerWorks](https://developer.ibm.com/answers/topics/iot-real-time/)
