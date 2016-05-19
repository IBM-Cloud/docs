---

copyright:

  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Getting started with {{site.data.keyword.cdn_short}} (Beta)
{: #cdn}  
*Last updated: 03 May 2016*  

Use {{site.data.keyword.cdn_full}} (CDN) to reduce content load time, enhance user experience, and lower bandwidth usage in your Bluemix&reg; or virtual server applications. The service supports only HTTP applications. HTTPS applications are not supported. 
{:shortdesc}

Before you begin, create a Bluemix application from the Bluemix user interface. Then, get started by adding a custom domain name for your Bluemix application and configuring the IBM CDN service for your app.

## Adding a custom domain name 

You'll need to add a custom domain name for your Bluemix application. The custom domain name must be externally visible. For example: www.myapp.com. 

Complete the following tasks to add a custom domain name.

1. Use the following command to verify the availability of the custom domain name that you want to use:  
  ```
  dig www.myapp.com
  ```  
2. Add the custom domain name as shown in the following steps.  
	1. Select your application tile from the Bluemix Dashboard.  
	2. Select the **Edit routes and App Access** ![](images/icon.png) icon.  
	3. Select **Add Custom Domain**. The **Manage Organizations** page is displayed.
	4. Select **DOMAINS** > **ADD DOMAIN**, enter the custom domain name, and select **SAVE**.  
	5. Select the **Edit routes and App Access** icon from the dashboard.  
	6. Select the custom domain name from the domain names drop-down, enter **www** in the host field, and select **SAVE**.  
	The custom domain name along with your application route is displayed.  

## Adding the service to an application

Bind the IBM CDN service to your application as given in the following steps.

1. Select the **DOMAINS** tab. The **Domain and URL Management** page is displayed.  
2. Select **ADD APP URL**.  
3. Enter your application URL. This URL is your externally visible domain name.  
4. Enter the origin route. This route is the Bluemix application route or IP address.  
**Note:** For a virtual server application, specify the origin server's IP address.  
5. Select **ADD**. The CDN service is provisioned in the backend. A CNAME for your application is displayed.  
6. Replace the CNAME target for your domain in your DNS provider record with the CNAME displayed.  

	**Important:** If you do not update the CNAME target in your DNS provider record, your application will not be accessible. The IBM CDN service will continue to report an error until the CNAME target is updated.

	**Note:** Keep a record of the original CNAME target. You will need it if you stop the IBM CDN service.

Requests to your domain will now be routed by using the IBM CDN infrastructure.

# rellinks
## general 
* [Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/){: new_window}
* [IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
