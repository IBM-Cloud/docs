---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Getting started with {{site.data.keyword.iotinsurance_short}} (Beta)
{: #iotins_gettingstarted}
Last updated: 16 September 2016
{: .last-updated}

{{site.data.keyword.iotinsurance_full}} is a {{site.data.keyword.Bluemix_notm}} service that you can use to collect, manage, and analyze data from connected policy holders. {{site.data.keyword.iotinsurance_short}} gives you the ability to provide personalized risk assessment, real-time protection, and policy cost reductions.
{:shortdesc}

To get up and running with this service, you must deploy required services and apps, then configure the services.

**Prerequisites:** Before you begin, ensure that the following prerequisites are in place:
- An instance of the [{{site.data.keyword.iotinsurance_short}} service](https://console.ng.bluemix.net/catalog/services/iot-for-insurance/) must exist in your {{site.data.keyword.Bluemix_notm}} space.
- At least 2 GB of free memory must be available in your {{site.data.keyword.Bluemix_notm}} organization to enable the Deploy function.

## Deploying the required services and applications
{: #deploying_services}

1. To deploy all required services and applications, on the [{{site.data.keyword.Bluemix_notm}} console](https://console.ng.bluemix.net/#all-items), click the {{site.data.keyword.iotinsurance_short}} service tile, then click **Deploy**.

  {{site.data.keyword.iotinsurance_short}} deploys all services and Node.js applications that it requires. It automatically binds the applications to the services.

  Each service instance uses the default service plan. You can upgrade any service plan at a later time by going to the service's console. You can also use an existing instance of a service by deleting the new instance and manually binding the existing instance to the {{site.data.keyword.iotinsurance_short}} service. For more information about the applications, see [About {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html).

2. Verify that all services and apps are created and functioning properly. In your {{site.data.keyword.Bluemix_notm}} console, check that all apps have a status of `Running`.

3. Verify that the {{site.data.keyword.iotinsurance_short}} dashboard is functional and that you can access the APIs.
  1. Click the {{site.data.keyword.iotinsurance_short}} service tile, then select the **Service Credentials** tab.
  2. Click **View Credentials** and make a note of the User ID and Password. You will use these credentials in the following steps.
  3. Open the {{site.data.keyword.iotinsurance_short}} dashboard by selecting the **Manage** tab and clicking **Open**.
  4. Return to the **Manage** tab. View the APIs, by clicking **APIs**.

## Configuring the services
{: #iot4i_configservices}
Perform the following tasks to configure the services:

### Configuring {{site.data.keyword.amashort}}
{: #config_ama}
1. In your {{site.data.keyword.Bluemix_notm}} console, copy the URL of the {{site.data.keyword.iotinsurance_short}} API application. Right click the API application tile and select **Copy Link Location**.

2. Open the {{site.data.keyword.amashort}} service. The service is available in the Services section of your {{site.data.keyword.Bluemix_notm}} console.

3. In the **Custom** section, click **Configure**, and then enter the following authentication credentials:

  - **Realm name**: `IoT4I`

  - **Custom Identity Provider Url**: Paste the URL of the API application that you copied in the first step.

  - **Your Web Application Redirect URIs**: Leave this field blank.

### Configuring {{site.data.keyword.mobilepushshort}}
{: #config_push}
To enable push notifications for an existing mobile app, you must configure the {{site.data.keyword.mobilepushshort}} service and add a Public Key Cryptography Standards (PKCS) 12 file. For information about the mobile app, see [Installing and connecting the sample mobile app](iotinsurance_mobile_app.html). For information about {{site.data.keyword.mobilepushshort}}, see [Getting started with Push Notifications](https://console.stage1.ng.bluemix.net/docs/services/mobilepush/index.html).

  1. Open the {{site.data.keyword.mobilepushshort}} service.
  2. Click **Setup Push**.
  3. In the Apple Push Notifications Certificate section, upload the PKCS 12 file for your mobile app and enter the password.

What's next?
{: #whats_next}
Learn what you can do with {{site.data.keyword.iotinsurance_short}}.

- Create a [user and shield association](iotinsurance_create_users.html).
- Install and connect the [sample mobile app](iotinsurance_mobile_app.html).
- Improve performance with [advanced services](iotinsurance_advancedservices.html).
- View the [APIs](https://iot4i-docs-api.mybluemix.net/dist/).

# Related Links
{: #rellinks}

## Tutorials and Samples
{: #samples}
* [Sample mobile app code on Github](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## API Reference
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API examples](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs){:new_window}

## Related Links
{: #general}
* [{{site.data.keyword.iot_full}} documentation](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [Developer support forum](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Stack overflow support forum](http://stackoverflow.com/questions/tagged/ibm-bluemix)
