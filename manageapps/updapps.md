---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Updating apps
{: #updatingapps}

*Last updated: 9 May 2016*


You can use the cf push command or {{site.data.keyword.Bluemix}} DevOps Services to update the applications in {{site.data.keyword.Bluemix_notm}}. In many cases, even for the built-in buildpacks such as Node.js, you must also supply a -c parameter to specify which command is used to start your application.
{:shortdesc}

##Creating and using a custom domain
{: #domain}

You can use a custom domain in the URL of your application instead of the default {{site.data.keyword.Bluemix_notm}} system domain that is mybluemix.net.

Domains provide the URL route that is allocated to your organization in {{site.data.keyword.Bluemix_notm}}. To use a custom domain, you must register the custom domain on a public DNS server, configure the custom domain in {{site.data.keyword.Bluemix_notm}}, and then map the custom domain to the {{site.data.keyword.Bluemix_notm}} system domain on the public DNS server. After your custom domain is mapped to the {{site.data.keyword.Bluemix_notm}} system domain, requests for your custom domain are routed to your application in {{site.data.keyword.Bluemix_notm}}.

You can create and use a custom domain in {{site.data.keyword.Bluemix_notm}} by using either the {{site.data.keyword.Bluemix_notm}} user interface, or the cf command line interface.

* Use the {{site.data.keyword.Bluemix_notm}} user interface:

  1. Create a custom domain for your organization.
    
	1. On the menu bar of the {{site.data.keyword.Bluemix_notm}} **DASHBOARD**, click **MANAGE ORGANIZATIONS**.
	
	2. On the **DOMAINS** tab, click **ADD DOMAIN**, enter your custom domain name, and click **SAVE**.
    	
  2. Add the route with the custom domain to an application.
  
    1. On the menu bar of the {{site.data.keyword.Bluemix_notm}} **DASHBOARD**, click the tile of the application that you want to add the route to. The **Overview** page is displayed.
	
	2. From the application menu on the **Overview** page, click **Edit Routes and App Access**.
	
	3. Click **Add route** and specify the route that you want to use for the application.
	
* Use the cf command line interface:
  
  1. Create a custom domain for your organization by typing the following command:
    
    ```
    cf create-domain <your org name> mydomain
    ```
    
    *organization_name*
  
        The name of your organization.
	  
    *mydomain*
    
        The custom domain name that you want to use.
	  
  2. Add the route with the custom domain to an application by typing the following command:
    
    ```
    cf map-route myapp mydomain -n host_name
    ```
    
    *myapp*
      
    	The name of your application.
  	
    *mydomain*
      
    	The name of your custom domain.
	
    *host_name*
    
        The host name in the route that you want to use for your application.
	
After you configure the custom domain in {{site.data.keyword.Bluemix_notm}}, you must map the custom domain to the {{site.data.keyword.Bluemix_notm}} system domain on your registered DNS server:

  1. Set up a 'CNAME' record for the custom domain name on your DNS server.
  2. Map the custom domain name to the secure endpoint for the {{site.data.keyword.Bluemix_notm}} region where your application is running. Use the following region endpoints to provide the URL route that is allocated to your organization in {{site.data.keyword.Bluemix_notm}}:
  
    * US-SOUTH: `secure.us-south.bluemix.net`
    * EU-GB: `secure.eu-gb.bluemix.net`
    * AU-SYD: `secure.au-syd.bluemix.net`
  
In a browser or command line interface, enter the following URL to access the myapp application:

```
http://host_name.mydomain
```

**Note:** To remove an orphaned route, use the following command:

```
cf delete-route domain -n hostname -f
```

*domain* is the name of your domain, and *hostname* is the host name of the route for your application. For more information about the **cf delete-route** command, type `cf delete-route -h`.

##Blue-green deployments
{: #blue_green}

{{site.data.keyword.Bluemix_notm}} supports the blue-green deployment technique to enable continuous delivery and minimize downtime events.

*Blue-green deployment* is a zero-downtime deployment technique that consists of two nearly identical production environments, called Blue and Green. They differ by the artifacts that the developer has intentionally changed, typically by the version of the application. At any given time, at least one of the environments is active. Using the blue-green deployment technique, you can realize the following benefits:

* Take software quickly from the final stage of testing to live production.
* Deploy a new version of an application without disrupting traffic to the application.
* Rollback rapidly. If there is something wrong with one of your environments, you can quickly switch to the other environment.

If you have already deployed an application to {{site.data.keyword.Bluemix_notm}} and you want to update the application to a new version, you can use either of the following two approaches to assure blue-green deployment.

###Example: Using the cf rename command

In this example, the name of the application is Blue. The example demonstrates how to update the version of *Blue* using the **cf rename** command without disrupting traffic to the application. Optionally the now old version of *Blue* can be deleted when the updated version is in place.

1. Push the *Blue* app to {{site.data.keyword.Bluemix_notm}}.
  
  ```
  cf push Blue
  ```
  
  **Result:** The *Blue* app is running and is responding to URL `Blue.mybluemix.net`.
  
2. Use the **cf rename** command to rename the *Blue* app to *Green*:
  
  ```
  cf rename Blue Green
  ```
  
  List the applications in the current space by using the **cf apps** command:
  
  ```
  ...
  name             requested state   instances   memory   disk   urls
  Green            started           1/1         1G       1G	 Blue.mybluemix.net
  ...
  ```
  
  **Result:** The *Green* app is running and is responding to URL `Blue.mybluemix.net`.

3. Make the necessary changes and get the updated *Blue* version ready. Push the updated *Blue* app to {{site.data.keyword.Bluemix_notm}}:
  
  ```
  cf push Blue
  ```
  
  List the applications in the current space by using the **cf apps** command:
  
  ```
  ...
  name             requested state   instances   memory   disk   urls
  Green            started           1/1         1G       1G	 Blue.mybluemix.net
  Blue             started           1/1         1G       1G	 Blue.mybluemix.net
  ...
  ```
  
  **Results:**
    * Two instances of the application are deployed, the *Blue* and the *Green*.
	* The *Green* app is running and is responding to URL `Blue.mybluemix.net`.
	
4. Optional: If you want to delete the old version (*Green*) of the app, use the **cf delete** command.
  
  ```
  cf delete Green -f
  ```
  
  List the routes in your space by using the **cf route** command:
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue
  ...
  ```
  
  **Result:** The *Blue* app is responding to URL `Blue.mybluemix.net`.
  
###Example: Using the cf map-route command

In this example, *Blue* is the previously deployed application and *Green* is the updated version. This example demonstrates how to update the version of *Blue* using the **cf map-route** command without disrupting traffic to the application. Optionally the now old version of *Blue* can be deleted when the updated version is in place.

1. Push the *Blue* app to {{site.data.keyword.Bluemix_notm}}.
  
  ```
  cf push Blue
  ```
  
  **Result:** The *Blue* app is running and is responding to URL `Blue.mybluemix.net`.
  
2. Make the necessary changes and get the *Green* version ready. Push the *Green* app to {{site.data.keyword.Bluemix_notm}}:
  
  ```
  cf push Green
  ```
  
  List the applications in the current space by using the **cf route** command:
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue
  Green            mybluemix.net    Green
  ...
  ```
  
  **Results:**
  
    * Two instances of the app are deployed, the *Blue* and the *Green*.
	* The *Blue* app is responding to URL `Blue.mybluemix.net`. And the *Green* app is responding to URL `Green.mybluemix.net`.
	
3. Map the *Blue* app to the *Green* app so that all traffic to `Blue.mybluemix.net` is routed to both the *Blue* app and the *Green* app.
  
  ```
  cf map-route Green mybluemix.net -n Blue
  ```
  
  List the routes in your space by using the cf routes command:
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue, Green
  Green            mybluemix.net    Green
  ...
  ```
  
  **Result:**

    * The CF Router now sends traffic for Blue.mybluemix.net to both the Blue app and the Green app.
	* The CF Router continues to send traffic for Green.mybluemix.net to the Green app.
	
4. When you verify *Green* is running as expected, remove the `Blue.mybluemix.net` route from the *Blue* app:
  
  ```
  cf unmap-route Blue mybluemix.net -n Blue
  ```
  
  List the routes in your space by using the cf routes command:
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Green
  Green            mybluemix.net    Green
  ...
  ```
  
  **Result:** The CF Router stops sending traffic to the *Blue* app. The *Green* app is responding to both the URLs: `Green.mybluemix.net` and `Blue.mybluemix.net`.
  
5. Remove the `Green.mybluemix.net` route to the *Green* app.
  
  ```
  cf unmap-route Green mybluemix.net -n Green
  ```
  
  **Result:** The CF Router stops sending traffic to the *Blue* app. The *Green* app is responding to the URL `Blue.mybluemix.net`.
  
6. Optional: If you want to delete the old version (*Blue*) of the application, use the `cf delete` command.
  
  ```
  cf delete Blue -f
  ```
  
  List the routes in your space by using the cf route command:
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Green
  ...
  ```
  
  **Result:** The *Green* app is responding to the URL `Blue.mybluemix.net`.


# Related Links
{: #rellinks}

## Related Links
{: #general}

* [Blue-green deployments](http://martinfowler.com/bliki/BlueGreenDeployment.html){:new_window}
* [IBM {{site.data.keyword.Bluemix_notm}} DevOps Services](https://hub.jazz.net/){:new_window}
