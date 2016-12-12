---

copyright:
  years: 2016
lastupdated: "2016-12-12"

---


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuring mobile connectivity and security
{: #iot4e_configureMCA}

Enable mobile communications and security by configuring {{site.data.keyword.amafull}}. This task is required to use the sample mobile app and only needs to be performed once.
{:shortdesc}

Before you begin, you must deploy an instance of the {{site.data.keyword.iotelectronics}} starter in your {{site.data.keyword.Bluemix_notm}}
 organization. Deploying an instance of the starter automatically deploys the component applications and services, including {{site.data.keyword.amafull}}.

1. If you just deployed the {{site.data.keyword.iotelectronics}} starter, the Getting Started tab of the starter app is displayed, and you should proceed to the next step of these instructions. If the starter app is not displayed, open your {{site.data.keyword.Bluemix_notm}} dashboard and start your {{site.data.keyword.iotelectronics}} starter application by clicking the starter application name.

    ![{{site.data.keyword.iotelectronics}} in the dashboard](images/IoT4E_bm_dashboard.png "{{site.data.keyword.iotelectronics}} in the dashboard")

2. Copy the URL of the {{site.data.keyword.iotelectronics}} web app by right-clicking **View App** and selecting **Copy Link Location**.

3. On the **Connections** tab, click the {{site.data.keyword.amashort}} service to open it.

4. On the {{site.data.keyword.amashort}} Authentication page, enable authentication by clicking **On**.

5. In the **Custom** section, enter the following authentication credentials:

    - **Realm name**: `myRealm`

    - **Custom Identity Provider Url**: Paste the URL of the API application that you copied in the first step in the following format:   **https://<*myIoT4eStarterApp*>.mybluemix.net**.  

    **Important:** Be sure that the URL uses the secure protocol `https` even if the value that you copied uses `http`.

    - **Your Web Application Redirect URIs**: Leave this field blank.

   ![Configure {{site.data.keyword.amashort}}.](images/MCA_config_pg.png "{{site.data.keyword.amashort}} Authentication page")  

5. Save your settings. You can now return to the {{site.data.keyword.iotelectronics}} service console or your {{site.data.keyword.Bluemix_notm}} console.
