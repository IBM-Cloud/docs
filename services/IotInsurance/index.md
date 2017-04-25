---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-25"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Getting started with {{site.data.keyword.iotinsurance_short}}
{: #gettingstarted}

{{site.data.keyword.iotinsurance_full}} is a {{site.data.keyword.Bluemix_notm}} service that you can use to collect, manage, and analyze data from connected policy holders. {{site.data.keyword.iotinsurance_short}} gives you the ability to provide personalized risk assessment, real-time protection, and policy cost reductions.
{:shortdesc}

To get up and running with this service, you must deploy required services and apps, then configure the services. Find an overview of the services and app and an architecture diagram in [About {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html)

**Prerequisites:** Before you begin, ensure that the following prerequisites are in place:
- An instance of the [{{site.data.keyword.iotinsurance_short}} service](https://console.ng.bluemix.net/catalog/services/iot-for-insurance/) must exist in your {{site.data.keyword.Bluemix_notm}} space.
- At least 2 GB of free memory must be available in your {{site.data.keyword.Bluemix_notm}} organization to enable the Deploy function. If you are upgrading from a previous version, you should have at least 2.5 GB.

## Deploying the required services and applications
{: #deploying_services}

1. To deploy all required services and applications, on the [{{site.data.keyword.Bluemix_notm}} console](https://console.ng.bluemix.net/#all-items), click the {{site.data.keyword.iotinsurance_short}} service, then click **Deploy**.

  {{site.data.keyword.iotinsurance_short}} deploys all services and Node.js applications that it requires. It automatically binds the applications to the services.

  Each service instance uses the default service plan. You can upgrade any service plan at a later time by going to the service's console. You can also use an existing instance of a service by deleting the new instance and manually binding the existing instance to the {{site.data.keyword.iotinsurance_short}} service. For more information about the applications, see [About {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html).

  **Important:**  When you deploy the trial version of {{site.data.keyword.iotinsurance_short}}, be aware that the free versions of the other services and application which are also deployed are limited in their functionality. {{site.data.keyword.iot_short_notm}} is limited to a maximum of 500 devices and {{site.data.keyword.cloudant_short_notm}} is limited to one GB of data and has limited read-write threading capabilities.

  **Note**: {{site.data.keyword.iotinsurance_short}} no longer deploys either {{site.data.keyword.amafull}} or {{site.data.keyword.mobilepushfull}}. Earlier versions of {{site.data.keyword.iotinsurance_short}} used the {{site.data.keyword.amashort}} service to process the responses from the mobile app. This process continues to work for all existing instances of {{site.data.keyword.iotinsurance_short}}. However, you must create a custom authentication process to use the mobile app with new instances of
  {{site.data.keyword.iotinsurance_short}}. You can also optionally [create an instance of  {{site.data.keyword.mobilepushshort}}](https://console.ng.bluemix.net/docs/services/mobilepush/index.html), configure it, and bind it to the {{site.data.keyword.iotinsurance_short}} API.

2. Verify that the {{site.data.keyword.iotinsurance_short}} dashboard is functional and that you can access the APIs.
  1. Open the {{site.data.keyword.iotinsurance_short}} dashboard by clicking **Open**. Accept the prefilled credentials by clicking **Login**.
  2. Return to the {{site.data.keyword.iotinsurance_short}} service console and view the APIs by clicking **APIs**.

  **Note:** After deployment, you can access the dashboard or APIs directly by entering their respective URLs in your browser. When you use this method, you must enter your {{site.data.keyword.iotinsurance_short}} service credentials. To locate your credentials, return to the {{site.data.keyword.iotinsurance_short}} service console. Click the **Service Credentials** tab and then click **View Credentials**. Make a note of the User ID and Password.


<!--
## Configuring
{: #iot4i_configservices}



### Configuring {{site.data.keyword.amashort}}
{: #config_ama}
1. Return to your Bluemix console. All apps and services that were deployed by {{site.data.keyword.iotinsurance_short}} are displayed.

2. Copy the URL of the {{site.data.keyword.iotinsurance_short}} API application. Right-click the API application and select **Copy Link Location**.

3. Open the {{site.data.keyword.amashort}} service. The service is available in the Services section of your {{site.data.keyword.Bluemix_notm}} console.

4. Enable authentication by clicking **On**.

5. In the **Custom** section, enter the following authentication credentials:

  - **Realm name**: `IoT4I`

  - **Custom Identity Provider Url**: Paste the URL of the API application that you copied in a previous step.

  - **Your Web Application Redirect URIs**: Leave this field blank.

6. Save your settings. You can now return to the {{site.data.keyword.iotinsurance_short}} service console or your {{site.data.keyword.Bluemix_notm}} console.
-->


## Creating and Configuring {{site.data.keyword.mobilepushshort}}
{: #config_push}

(optional) To enable push notifications for an existing mobile app, you can optionally create an instance of the {{site.data.keyword.mobilepushshort}} service, bind it to the {{site.data.keyword.iotinsurance_short}} API, and add a Public Key Cryptography Standards (PKCS) 12 file. For information about the mobile app, see [Installing and connecting the sample mobile app](iotinsurance_mobile_app.html). For information about {{site.data.keyword.mobilepushshort}}, see [Getting started with Push Notifications](https://console.ng.bluemix.net/docs/services/mobilepush/index.html).

To configure the service after creation, perform the following steps:

  1. Open the {{site.data.keyword.mobilepushshort}} service.
  2. Click **Configure**.
  3. In the Apple Push Notifications Certificate section, upload the PKCS 12 file for your mobile app and enter the password.

## Using Weather Company data
{: #weather_company}

(optional) {{site.data.keyword.iotinsurance_short}} provides a set of static data from the Weather Company that you can view for demonstration purposes. You can also optionally access live data from the Weather Company by creating an instance of the [{{site.data.keyword.weatherfull}} service](../Weather/index.html) and binding it to the  {{site.data.keyword.iotinsurance_short}} weather app.

**Important:** The free version of the {{site.data.keyword.weather_short}} service is limited to 10,000 requests. You can upgrade to a paid version if you need more requests.

What's next?
{: #whats_next}
Learn what you can do with {{site.data.keyword.iotinsurance_short}}.

- Use the instructions and APIs in the Shield Toolkit to create a [user and shield association](iotinsurance_shield_toolkit.html).
<!-- - Install and connect the [sample mobile app](iotinsurance_mobile_app.html). -->
- Download or view all the [API examples on the GitHub site ![External link icon](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}.
