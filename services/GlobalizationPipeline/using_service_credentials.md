---

copyright:
  years: 2015, 2017
lastupdated: "2016-07-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Using {{site.data.keyword.GlobalizationPipeline_short}} outside of {{site.data.keyword.Bluemix_notm}}
{: #globalizationpipeline_external}

Many {{site.data.keyword.Bluemix_notm}} services, including {{site.data.keyword.GlobalizationPipeline_short}} can be used from an on-premise application hosting environment or even from another cloud platform without having to host the application on {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

To use {{site.data.keyword.GlobalizationPipeline_short}} outside of {{site.data.keyword.Bluemix_notm}}, complete the following steps:

1. Navigate to the {{site.data.keyword.Bluemix_notm}} catalog and select the **{{site.data.keyword.GlobalizationPipeline_short}}** service from the **DevOps** category.

2. From the {{site.data.keyword.GlobalizationPipeline_short}} service catalog page, fill out the required information.  For the **Connect to** field, choose the option to **Leave unbound**.

3. Click **Create** to add the service to your {{site.data.keyword.Bluemix_notm}} organization.  You will be taken to the {{site.data.keyword.GlobalizationPipeline_short}} dashboard.

4. From the dashboard, click the **Service Credentials** tab.  

The **Service Credentials** tab shows all of the credentials that are available for that particular instance of the service.  Using these credentials and the service URL that is provided, you can access the {{site.data.keyword.GlobalizationPipeline_short}} API and make use of its features from your application in any hosting environment.

To learn about the {{site.data.keyword.GlobalizationPipeline_short}} RESTful API, see the [API Reference](https://gp-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}.
