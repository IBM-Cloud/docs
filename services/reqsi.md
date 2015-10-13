#Services
*Last Updated: 8/25/2015*

You can find available services in the **Catalog** under **Services** in the {{site.data.keyword.Bluemix}} user interface.

Predefined services are available in {{site.data.keyword.Bluemix_notm}} for mobile applications. {{site.data.keyword.Bluemix_notm}} makes it easy for you to implement, host, and scale these mobile services for your mobile apps. You can focus on your application logic and application design.

{{site.data.keyword.Bluemix_notm}} hosts and manages middleware services for web applications. Application developers can specify the middleware services that they require. {{site.data.keyword.Bluemix_notm}} then automatically provisions new instances of the specified middleware services and binds the service instances to the application.

{{site.data.keyword.Bluemix_notm}} displays services in two ways: by service category and by service support type.

**Category**

{{site.data.keyword.Bluemix_notm}} services are organized in different categories. In each service category, the IBM created services are listed first, followed by third-party services, and then community services.

**Support**

Multiple levels of support are provided for {{site.data.keyword.Bluemix_notm}} services. The following table describes the general support information for {{site.data.keyword.Bluemix_notm}} services:

*Table 1. {{site.data.keyword.Bluemix_notm}} services support information*

|Type	|Description	|Support details|
|:------|:--------------|:--------------|
|IBM	|A service that is provided by IBM and is generally available.	|Problems that are determined to be a defect in an IBM-provided service that is generally available are supported. Support is provided based on the severity that you set. For more information about ticket severity, see [Contacting {{site.data.keyword.Bluemix_notm}} support](https://www.ng.bluemix.net/docs/troubleshoot/getting_customer_support.html#bluemix_support).|
|Third Party	|A service that is provided by a company other than IBM.	|Support for third-party services is provided by the service provider. If a problem is investigated by IBM and the problem is determined to be a defect in a third-party service, IBM is not obligated to provide a fix. IBM will share analysis with the third-party service provider if needed.|
|Community	|A service that is provided by an open source community.	|Support for community services is provided by the {{site.data.keyword.Bluemix_notm}} Developers [Community](https://developer.ibm.com/bluemix/), through the {{site.data.keyword.Bluemix_notm}} Developers Community [Forum](https://developer.ibm.com/answers/smartspace/bluemix/). If a problem is investigated by IBM and the problem is determined to be a defect in a community service, IBM is not obligated to provide a fix.|
|Beta	|A service that is not production-ready and is in a trial stage of development. A Beta service can help the development and marketing teams assess the value of the services before they make the service generally available.	|Problems that are determined to be a defect in an IBM-provided beta service are supported, but IBM is not obligated to provide a fix. In addition, the problem ticket will be assigned a severity 3 or 4 where applicable. For information about ticket severity, see [Contacting {{site.data.keyword.Bluemix_notm}} support](https://www.ng.bluemix.net/docs/troubleshoot/getting_customer_support.html#bluemix_support).|

{{site.data.keyword.Bluemix_notm}} also has experimental services that you can try out. To view all available experimental services, boilerplates, and runtimes, log in to {{site.data.keyword.Bluemix_notm}}, scroll to the bottom of the Catalog, and then click **{{site.data.keyword.Bluemix_notm}} Lab Catalog**.

Experimental services might not be stable and can change in ways that are not compatible with earlier versions. These services are not recommended for use in production environments. Support for experimental services is provided through the {{site.data.keyword.Bluemix_notm}} Developers Community [Forum](https://developer.ibm.com/answers/smartspace/bluemix/). If a problem is investigated by IBM and the problem is determined to be a defect in an experimental service, IBM is not obligated to provide a fix.

To use a service in the {{site.data.keyword.Bluemix_notm}} user interface, cf command line interface, IBM {{site.data.keyword.Bluemix_notm}} DevOps Services, or any supported tools, take the following steps:

1. Create an instance of the service. In most cases, the service instance can be created when you create the application.

2. Identify the application that uses the new service instance. For web applications, you can specify more than one application to use the same service instance, typically for data sharing.

3. Write your own code in your application to interact with the service.

##Services by region

Not all services are available in every {{site.data.keyword.Bluemix_notm}} region. The following table shows the services that are provided by IBM.

*Table 2. Service availability*

|Service	|Available in US South region	|Available in Europe United Kingdom region|
|:----------|:------------------------------|:------------------|
|App Sec Manager	|Yes	|No|
|AppScan® Dynamic Analyzer	|Yes	|No|
|AppScan Mobile Analyzer	|Yes	|No|
|Advanced Mobile Access	|Yes	|Yes|
|Analytics for Apache Hadoop	|Yes	|No|
|API Management	|Yes	|Yes|
|Auto-Scaling	|Yes	|Yes|
|BigInsights®	|Yes	|No|
|Business Rules	|Yes	|Yes|
|Cloud Integration	|Yes	|Yes|
|Cloudant® NoSQL DB	|Yes	|Yes|
|Concept Expansion	|Yes	|Yes|
|dashDB™	|Yes	|Yes|
|Data Cache	|Yes	|Yes|
|Delivery Pipeline	|Yes	|Yes|
|Embeddable Reporting	|Yes	|No|
|Gamification	|Yes	|Yes|
|Geospatial Analytics	|Yes	|Yes|
|Globalization	|Yes	|No|
|IBM DataWorks	|Yes	|Yes|
|Insights for Twitter	|Yes	|Yes|
|Integration Testing	|Yes	|Yes|
|Internet of Things Foundation	|Yes	|No|
|Message Hub	|Yes	|No|
|Message Resonance	|Yes	|Yes|
|Mobile Analyzer for iOS	|Yes	|No|
|Mobile Application Security	|Yes	|Yes|
|Mobile Data	|Yes	|Yes|
|Monitoring and Analytics	|Yes	|Yes|
|Mobile Quality Assurance	|Yes	|Yes|
|MQ Light	|Yes	|Yes|
|Object Storage	|Yes	|No|
|Push	|Yes	|Yes|
|Push for iOS 8	|Yes	|Yes|
|Question and Answer	|Yes	|Yes|
|Rapid Apps	|Yes	|Yes|
|Relationship Extraction	|Yes	|Yes|
|Secure Gateway	|Yes	|Yes|
|Session Cache	|Yes	|Yes|
|Single Sign On	|Yes	|No|
|SQL Database	|Yes	|Yes|
|Static Analyzer	|Yes	|Yes|
|Streaming Analytics	|Yes	|No|
|Time Series Database	|Yes	|Yes|
|Track & Plan	|Yes	|Yes|
|Visualization Rendering	|Yes	|Yes|
|Workflow	|Yes	|Yes|
|Workload Scheduler	|Yes	|Yes|
|XPages NoSQL Database	|Yes	|Yes|


##Adding a service to your application
*Last Updated: 8/25/2015*

{{site.data.keyword.Bluemix}} has a list of services and manages them on behalf of the developers. To add a service for your application to use, you must request an instance of this service and configure the application to interact with the service.

You can see all the services that are available in {{site.data.keyword.Bluemix_notm}} in the following ways:

* From the {{site.data.keyword.Bluemix_notm}} user interface. View the {{site.data.keyword.Bluemix_notm}} Catalog.
* From the cf command line interface. Use the **cf marketplace** command.
* From your own application. Use the [GET /v2/services Services API](http://apidocs.cloudfoundry.org/197/services/list_all_services.html).

You can select the service that you need when you develop applications. Upon your selection, {{site.data.keyword.Bluemix_notm}} interacts with the service and takes necessary steps to provision resources of the service. The provisioning process might be different for different types of services. For example, a database service creates a database, and a push notification service for mobile applications generates configuration information.

{{site.data.keyword.Bluemix_notm}} provides the resources of a service to your application by using a service instance. A service instance can be shared across web applications.

You can also use services that are hosted in other regions if those services are available in those regions. These services must be accessible from the internet and have API endpoints. You must manually code your application to use these services in the same way that you code external applications or third-party tools to use {{site.data.keyword.Bluemix_notm}} services. For more information, see [Enabling external applications and third-party tools to use {{site.data.keyword.Bluemix_notm}} services](https://www.ng.bluemix.net/docs/services/reqnsi.html#accser_external).

If you want to add a service to the {{site.data.keyword.Bluemix_notm}} service catalog for {{site.data.keyword.Bluemix_notm}} applications to use, you can build your own service and integrate it with {{site.data.keyword.Bluemix_notm}}. For more information, see [Integrating a service with {{site.data.keyword.Bluemix_notm}}](https://www.stage1.ng.bluemix.net/docs/services/v2api.html).

###Requesting a new service instance

To request a new service instance, you must use the {{site.data.keyword.Bluemix_notm}} user interface or the cf command line interface.

**Note:** When you specify the service name, avoid using characters other than alphabetic or numeric characters, because results might be unpredictable.

If you use the {{site.data.keyword.Bluemix_notm}} user interface to request a service instance, complete the following steps:

1. In the {{site.data.keyword.Bluemix_notm}} **Catalog**, click the tile for the service that you want to add. The service details page opens.

2. In the Add Service pane, select an application that you want to bind this service instance to from the **App** list.

3. Type a name in the **Service name** field. A default service name is provided. You can change the name in the field, or leave it unchanged.

4. Complete additional fields or selections, and then click **CREATE**.

If you use the cf command line interface to request a service instance, complete the following steps:

1. Use the **cf marketplace** command to find the name and the plan of the service that you require.

2. Use the following command to create a service instance, where service_name is the name of the service, service_plan is the plan of the service, and service_instance is the name that you want to use for this service instance.

    ```
    cf create-service service_name service_plan service_instance
    ```

3. Use the following command to bind the service instance to an application, where appname is the name of the application, and service_instance is the name of the service instance.

    ```
    cf bind-service appname service_instance
    ```

**Note:** A service instance is specific to a space where the service instance is created. You cannot move a service instance to another space or organization. Instead, you must request a new service instance for each space in which you want to use it.

### <a id='config'></a> Configuring your application to interact with a service ###

After you bind a service instance to your application, you must configure your application to interact with the service.

Each service might require a different mechanism for communicating with applications. These mechanisms are documented as part of the service definition for your information when you develop applications. For consistency, the mechanisms are required for your application to interact with the service.

* To interact with database services, use the information that {{site.data.keyword.Bluemix_notm}} provides such as the user ID, password, and the access URI for the application.
* To interact with mobile back-end services, use the information that {{site.data.keyword.Bluemix_notm}} provides such as the application identity (app ID), security information that is specific to the client, and the access URI for the application. The mobile services typically work in context with each other so that context information, such as the name of the application developer and the user that uses the application, can be shared across the set of services.
* To interact with web applications or server-side cloud code for mobile applications, use the information that {{site.data.keyword.Bluemix_notm}} provides such as the runtime credentials in the *VCAP_SERVICES* environment variable of the application. The value of the *VCAP_SERVICES* environment variable is the serialization of a JSON object. The variable contains the runtime data that is required to interact with the services that the application is bound to. The format of the data is different for different services. You might need to read the service documentation about what to expect and how to interpret each piece of information.

If a service that you bind to an application crashes, the application might stop running or have errors. {{site.data.keyword.Bluemix_notm}} does not automatically restart the application to recover from these problems. Consider coding your application to identify and recover from outages, exceptions, and connection failures. See the [Apps won't be automatically restarted](https://www.ng.bluemix.net/docs/troubleshoot/managingapps.html#tr_appnotautorestarted) troubleshooting topic for more information.

###Enabling external apps to use {{site.data.keyword.Bluemix_notm}} services

You might have applications that were created and run outside of {{site.data.keyword.Bluemix_notm}}, or you might use third-party tools. If {{site.data.keyword.Bluemix_notm}} services provide endpoints that are accessible from the internet, you can use those services with your local apps or third-party tools.

To enable an external app or third-party tool to use a {{site.data.keyword.Bluemix_notm}} service, complete the following steps:

1. Request an instance of the service.
    1. On the Dashboard in the {{site.data.keyword.Bluemix_notm}} user interface, click **Use Services or APIs**. The Catalog displays.
    2. From the Catalog, select the service that you want by clicking the service tile. The service details page opens.
    3. In the Add Service window, keep the **App**: list selection as **Leave unbound**. This selection means that the service will not be connected to a {{site.data.keyword.Bluemix_notm}} app.
    4. Make any other selections as needed. Then, click **CREATE**. A service instance is created, and the service Dashboard displays.
2. In the left navigation pane of the service Dashboard, you can select **Service Credentials** to view or add credentials in JSON format. Use the API key that is displayed as the credentials to connect to the service instance.

Your application that runs outside of {{site.data.keyword.Bluemix_notm}} can now access the {{site.data.keyword.Bluemix_notm}} service.

**Note:** If you want to delete service instances or check the billing information, you must go back to your Dashboard in the user interface to manage the service instances.

###Creating a user-provided service instance

You might have resources that are managed outside of {{site.data.keyword.Bluemix_notm}}. If you have credentials to access those external resources from the internet, you can create {{site.data.keyword.Bluemix_notm}} user-provided service instances to represent and communicate with your external resources.

To create a user-provided service instance and bind it to an application, complete the following steps:

1. Create a user-provided service instance by using either the **cf create-user-provided-service** or the **cf cups** command:
    * To create a general user-provided service instance, use the **-p** option, and separate the parameter names with commas. The cf command line interface then prompts you for each parameter in turn. For example:
        ```
        cf cups testups1 -p "host, port, dbname, username, password"
        host> pubsub01.example.com
        port> 1234
        dbname> sampledb01
        username> pubsubuser
        password> p@$$w0rd
        Creating user provided service testups1 in org my-org / space dev as user@sample.com...
        OK
        ```

    * To create a service instance that drains information to a third-party log management software, use the **-l** option, and specify the destination that the third-party log management software provides. For example:

        ```
        cf cups testups2 -l syslog://example.com
        Creating user provided service testups2 in org my-org / space dev as user@sample.com...
        OK
        ```

    If you want to update one or more parameters of the user-provided service instance, use either the **cf update-user-provided-service** or the **cf uups** command.

    * To update a general user-provided service instance, use the **-p** option, and specify the parameter keys and values in a json object. For example:

        ```
        cf uups testups1 -p "{\"username\":\"pubsubuser2\",\"password\":\"p@$$w0rd2\"}"
        Updating user provided service testups1 in org my-org / space dev as user@sample.com...
        OK
        ```

    * To create a service instance that drains information to a third-party log management software, use the -l option. For example:

        ```
        cf uups testups2 -l syslog://example2.com
        Updating user provided service testups2 in org my-org / space dev as user@sample.com...
        OK
        ```

2. Bind the service instance to your application by using the cf bind-service command. For example:

	```
	cf bind-service myapp testups1
	Binding service testups1 to app myapp in org my-org / space dev as user@sample.com...
	OK
	```

You can now configure your application to use the external resources. For information on how to configure your application to interact with a service, see [Configuring your application to interact with a service](#config).

###Using services in another region

If you have a service instance that is created and bound to apps in one region, you can use this service instance in another region by creating a user-provided service.

Assume that you are starting in the region where you want to use the service instance. To use a service instance that exists in another region, complete the following steps:

1. Switch to the region where the service instance exists. In the {{site.data.keyword.Bluemix_notm}} top menu bar, expand **Region** or click the **Region** icon, and then select the region where the service instance exists.

2. Retrieve the credentials and the connection parameters from the VCAP_SERVICES environment variable of the service instance in the region where the service exists. Complete the following steps:

	1. In the {{site.data.keyword.Bluemix_notm}} Dashboard, click your application tile. The Overview page is displayed.
	2. In the left navigation pane, click **Environment Variables**. The *VCAP_SERVICES* environment variable details are displayed on the right pane. Record the JSON content for the service instance.

3. Switch to the region where you want to use the service instance. In the {{site.data.keyword.Bluemix_notm}} top menu bar, expand **Region** or click the **Region** icon, and then select the region where you want to use the service instance.

4. Create a user-provided service instance by using the credentials and connection parameters that you recorded from the *VCAP_SERVICES* environment variable. For information about how to create a user-provided service instance, see [Creating a user-provided service instance](creating-a-user-provided-service-instance).

5. Bind the user-provided service instance to your app by using the following command:

	```
	cf bind-service myapp user-provided_service_instance
	```

# rellinks
## general 
* [Binding a service by using {{site.data.keyword.Bluemix_notm}} user interface](https://www.ng.bluemix.net/docs/starters/ee.html#ee_bindui)
* [Retrieving VCAP_SERVICES](https://www.ng.bluemix.net/docs/cli/retrieving.html)


