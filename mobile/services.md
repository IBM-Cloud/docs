---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-11"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# Services
{: #services}

From the {{site.data.keyword.Bluemix}} Mobile dashboard **Services** view, you can view your existing services or create new services. The Mobile dashboard provides a single location to view all of the Bluemix services that are being managed by projects.  

If you delete services from the **Services** view, you will disconnect the service from the project that it is associated with. Create a new service instance if you want to reconnect the service to the project.

## {{site.data.keyword.Bluemix_notm}} Mobile services overview
{: #mobile_services_overview}

The following table depicts  {{site.data.keyword.Bluemix_notm}} Mobile services. You can use individual services from the {{site.data.keyword.Bluemix_notm}} catalog, or you can integrate them into your mobile project.

<table summary="This table describes {{site.data.keyword.Bluemix_notm}} Mobile services and provides links to the service documentation">
<caption>Table 1. {{site.data.keyword.Bluemix_notm}} Mobile services</caption>
<th>{{site.data.keyword.Bluemix_notm}} Mobile service</th>
<th>Description</th>
<tr>
<td> <img src="images/mobile_analytics_icon.png" alt="{{site.data.keyword.mobileanalytics_short}} icon"><br/>{{site.data.keyword.mobileanalytics_short}}</td>
<td valign="top">Use the {{site.data.keyword.mobileanalytics_full}} service to gain insight into how your mobile apps are performing and how they are being used.<br/><br/>
Read more about operating this service in the <a href="/docs/services/mobileanalytics/index.html" alt="{{site.data.keyword.mobileanalytics_short}} documentation link">{{site.data.keyword.mobileanalytics_short}} documentation</a>.
</td>
</tr>
<tr>
<td><img src="images/authentication_icon
.png" alt="{{site.data.keyword.amashort}} service icon"><br/>{{site.data.keyword.amashort}}</td>
<td valign="top">Use the {{site.data.keyword.amafull}} service to add security functionality to your mobile app. You can configure client authentication and identity providers so that users can log in to the app with their existing Google or Facebook accounts.<br/><br/>
Read more about operating this service in the <a href="/docs/services/mobileaccess/index.html" alt="{{site.data.keyword.amashort}} documentation link">{{site.data.keyword.amashort}} documentation</a>.</td>
</tr>
<tr>
<td><img src="images/MFPFoundation_icon.png" alt="{{site.data.keyword.mobilefoundation_short}} service icon"><br/> {{site.data.keyword.mobilefoundation_short}}</td>
<td valign="top">Use the {{site.data.keyword.mobilefoundation_long}} service to expedite setting up an {{site.data.keyword.mfp_full}} environment from which you can develop, test, and operate enterprise mobile apps.<br/><br/>
Read more about operating this service in the <a href="/docs/services/mobilefoundation/index.html" alt="{{site.data.keyword.mobilefoundation_short}} documentation link">{{site.data.keyword.mobilefoundation_short}} documentation</a>.</td>
</tr>
<tr>
<td><img src="images/mqa_icon.png" alt="{{site.data.keyword.mqa}} service icon"><br/>{{site.data.keyword.mqa}}</td>
<td valign="top">Use the {{site.data.keyword.mqafull}} service to discover and set up mobile quality services for your apps. You can view high-level quality metrics for your mobile apps to get a quick understanding of the issues for apps that you are working on. These metrics include information for crashes, bugs, user feedback, and user sentiment. By viewing this information for your apps, you can determine whether to investigate specific issues further.<br/><br/>
Read more about operating this service in the <a href="/docs/services/MobileQualityAssurance/index.html" alt="{{site.data.keyword.mqa}} documentation link">{{site.data.keyword.mqa}} documentation</a>.</td>
</tr>
<tr>
<td><img src="images/push_icon.png" alt="{{site.data.keyword.mobilepushshort}} service icon"><br/>{{site.data.keyword.mobilepushshort}}</td>
<td valign="top">The {{site.data.keyword.mobilepushfull}} service provides a unified platform to send and manage mobile and web push notifications that are targeted across platforms.
<br/><br/>
The {{site.data.keyword.mobilepushshort}} manages the mapping of your application users to their devices, device platform, web browsers and handles dispatching push notifications to them. You can send broadcasts, unicasts (based on deviceID and userID), and also tags (or topics) as push notifications to your mobile and web browser application users. You can also use an SDK and REST APIs to further develop your client applications.
<br/><br/>
Read more about operating this service in the <a href="/docs/services/mobilepush/index.html" alt="{{site.data.keyword.mobilepushshort}} documentation link">{{site.data.keyword.mobilepushshort}} documentation</a>.</td>
</table>

## Integrating mobile services
{: #services_integration}
You can integrate your existing {{site.data.keyword.Bluemix_notm}} Mobile services, such as {{site.data.keyword.cloudant}}, into your project.


### Integrating {{site.data.keyword.cloudant}}
{: #cloudant_integration notoc}

To integrate your existing {{site.data.keyword.cloudant}} service, follow these steps:

1. Click your {{site.data.keyword.cloudant}} service instance.
2. Click **LAUNCH**.
3. In the **Databases** view, click your Database name.
4. Click **API** and copy the **API Key** value through your database name.

   **Note**: Do not copy the content past your database name.

5. Click **Permissions** > **Generate API Key** and copy the **Key** and **Password** values.
6. Navigate back to the Mobile dashboard **Projects** view.
7. Click on your project to edit it.
8. Click **Data** > **+ Data Source** > **Cloudant** and provide your data source name and click **Add**.
9. Click **Cloudant Config**.
10. Provide the **API Key** value that you previously copied into **API URL**.
11. Provide the **Key** value that you previously copied into **User**.
12. Provide the **Password** value that you previously copied into **Password**.
13. Click **Ok**.
