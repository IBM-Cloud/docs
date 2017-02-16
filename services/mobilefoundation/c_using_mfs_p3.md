---

copyright:
  years: 2016, 2017
lastupdated:  "2017-02-17"

---

#	Using the Developer Pro plan
{: #using_mobilefoundation_p3}

{{site.data.keyword.mobilefoundation_short}}: Developer Pro is suitable for team-based development and testing, this plan is not suitable for production.

After you create the {{site.data.keyword.mobilefoundation_short}}: Developer Pro service instance, in a few seconds, you can access the `Overview` page on {{site.data.keyword.Bluemix_notm}}, which provides you tutorials and videos to help you get started with the  {{site.data.keyword.mobilefoundation_short}} service.

## Pre-requisites
{: #prerequisites_p3}

Consider the following before you configure  {{site.data.keyword.mobilefoundation_short}}: Developer Pro service instance.
* {{site.data.keyword.mobilefoundation_short}}: Developer Pro is supported only with {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional (supporting OLTP) {{site.data.keyword.Bluemix_notm}} plans.

* You should have access to the {{site.data.keyword.dashdbshort_notm}} service instance credentials before you can configure the settings of your {{site.data.keyword.mobilefoundation_short}} service instance.

**Note**: The {{site.data.keyword.dashdbshort_notm}} service instance can exist in any `Space` within your {{site.data.keyword.Bluemix_notm}} `Organization` or any other `Organization` that you have access to. Ensure that you have the permissions to access the `Space` where the {{site.data.keyword.dashdbshort_notm}} service instance exists.


## Adding the database connection
{: #configure_dashdb_p3}

###  First steps
{: #firststeps_p3}

After you create the {{site.data.keyword.mobilefoundation_short}}: Developer Pro service instance, follow the procedure below to get started.

### Setting up connection to dashDB service instance
{: #connect_dashdb_p3}

After the {{site.data.keyword.mobilefoundation_short}}: Developer Pro service instance is created you will see the *Overview* page where you will need to specify the connection information for the {{site.data.keyword.dashdbshort_notm}} for Transactions service instance, that the {{site.data.keyword.mobilefoundation_short}} service instance should connect to.

**Note:** If you already have a {{site.data.keyword.dashdbshort_notm}} for Analytics: Enterprise for Transactions service instance, you can configure to use the same to connect to the {{site.data.keyword.mobilefoundation_short}} service instance.

You can also create a new {{site.data.keyword.dashdbshort_notm}} for Transactions service instance, if you do not have one already existing.

Follow the steps below to create a new dashDB for Transactions service instance:

1. In the *Overview* page select **Create New Service** section.

+ Select `Yes` on the **High availability configuration** option, if you want high available {{site.data.keyword.dashdbshort_notm}} for Transactions service instance.

+ Review the plan details and click **Create**.

A new {{site.data.keyword.dashdbshort_notm}} for Transactions: EnterpriseForTransactions2.8.500 service instance is created, which provides a dedicated {{site.data.keyword.dashdbshort_notm}} instance with 8GB RAM and 2 vCPUs, and 500 GB of storage.

Follow the steps below to connect to an existing {{site.data.keyword.dashdbshort_notm}} service instance or to the {{site.data.keyword.dashdbshort_notm}} for Transactions service instance that you just created:

1. Select the {{site.data.keyword.Bluemix_notm}} `Organization` where the {{site.data.keyword.dashdbshort_notm}} service instance exists.

+ Select the {{site.data.keyword.Bluemix_notm}} `Space` where the {{site.data.keyword.dashdbshort_notm}} service instance exists, from the list of spaces available in the selected `Organization`.   
**Note:** If you do not see listed the `Organization` and `Space` where your {{site.data.keyword.dashdbshort_notm}} service instance exists then check if you are a member of that `Organization` and `Space`. You are required to have a *Developer* role access to the organization and space, as the {{site.data.keyword.mobilefoundation_short}} service accesses the credentials from the {{site.data.keyword.dashdbshort_notm}} service.

+ Select the {{site.data.keyword.dashdbshort_notm}} `Service Name` and `Credentials` to connect to the existing  {{site.data.keyword.dashdbshort_notm}} service instance.

+  Test the connection to the specified {{site.data.keyword.dashdbshort_notm}} service instance.

+  Click **Add**. This action creates the required tables in the configured {{site.data.keyword.dashdbshort_notm}} database service instance.

In a few seconds, you can access the `Overview` page that provides you with  tutorials and videos to help you get started with the  {{site.data.keyword.mobilefoundation_short}} service.

**Note**: You cannot change the {{site.data.keyword.dashdbshort_notm}} service instance that is configured to be used by your {{site.data.keyword.mobilefoundation_short}} service instance. However, you can use the same {{site.data.keyword.dashdbshort_notm}} service instance across multiple {{site.data.keyword.mobilefoundation_short}} service instances, as each {{site.data.keyword.mobilefoundation_short}} service instance creates its own schema in the selected {{site.data.keyword.dashdbshort_notm}} service instance.

## Starting the MobileFirst server
{: #start_mobilefoundation_p3}

* To start the {{site.data.keyword.mfserver_short_notm}}, with default settings, click **Start Basic Server**.

* This selection provisions an {{site.data.keyword.mfserver_long_notm}} with the following settings:
    - Single Node with 1 GB of memory. This size is enough for development, moderate testing activities, and small scale production workloads.

    -	The `username` and `password` are automatically generated for you. You have access to them when the server is up and running.

The process of provisioning your server starts. This process takes about 10 minutes, and a message window indicates the progress of this operation. When complete a dashboard is displayed where you can see:

  -	The status of your server that is running (state, size).

  -	The server route is created for you. Use this route in your mobile application to connect to the {{site.data.keyword.mfserver_short_notm}}.

  -	Your personal `username` and `password` to access the {{site.data.keyword.mfp_oc_short_notm}}. The `password` is hidden. Click **Show Password** icon to visualize it.

*	Click **Launch Console** to open the {{site.data.keyword.mfp_oc_short_notm}}.


<!--This console runs inside the container.--> With the console, you can manage your mobile apps, adapters, and mobile devices, use your server as a mobile backend, send push notifications, and do more.

##  Adding Mobile Analytics server
{: #adding_analytics_server_p3}

 You can now monitor your mobile application on {{site.data.keyword.mobilefirst}} server by adding a Mobile Analytics server to the {{site.data.keyword.mobilefoundation_short}} service instance.

 Developer Pro plan creates the Mobile Analytics server in a container group, the user can customize the configuration by selecting the number of container nodes in the container group.

 Users can also attach volumes to the containers to persist data. The volume once selected cannot be changed. 20 GB is the default file share space available to the user. If the user needs additional storage space to persist analytics data, he is required to buy additional file share and create a volume using this file share. He can then select this new volume while deploying the analytics server.

 For more information on adding volumes to {{site.data.keyword.containerlong}}, refer to [Storing persistent data in a volume by using the {{site.data.keyword.Bluemix_notm}} Dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/docs/containers/container_volumes_ui.html){: new_window}.

* Click **Add Analytics** to add the Mobile Analytics server to the {{site.data.keyword.mobilefoundation_short}} service instance.

* You can choose the Mobile Analytics server configuration, a minimum of 1 GB and a maximum of 2 GB memory is supported for the Analytics server configuration. Analytics server is supported only on a single node in this plan.

The process of provisioning starts. This process takes about 10 minutes, and a message window indicates the progress of this operation.  

* Launch the MobileFirst Analytics Console from the {{site.data.keyword.mfp_oc_short_notm}}.

* Single sign-on is enabled between the {{site.data.keyword.mfserver_short_notm}} and the Mobile Analytics server. Mobile Analytics server is configured with the same LTPA keys and user credentials as the {{site.data.keyword.mfserver_short_notm}}. You can use the same `username` and `password` to login to the Mobile Analytics console as used to login to the {{site.data.keyword.mfp_oc_short_notm}}.

For more information on MobileFirst Analytics, you can refer to [MobileFirst Foundation Operational Analytics ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/analytics/){: new_window}.

**Note:** The Mobile Analytics server is removed when you delete the {{site.data.keyword.mobilefoundation_short}} service instance or when you attempt to re-create the {{site.data.keyword.mfserver_short_notm}}.

##  Deleting Mobile Analytics server
{: #deleting_analytics_server_p3}

You can now delete the Mobile Analytics server that was added to the {{site.data.keyword.mobilefoundation_short}} service instance, from the {{site.data.keyword.mobilefoundation_short}} service dashboard.

* Click **Delete Analytics** to delete the  Mobile Analytics server that has been added to the {{site.data.keyword.mobilefoundation_short}} service instance.

 This will delete the analytics container group. The process of deleting analytics containers takes about 10 minutes. You can refresh the screen to view the updated status. Once the analytics containers are deleted, the **Add Analytics** button is re-enabled, you can use this to add the Mobile Analytics server again if you choose to.

## Re-creating the MobileFirst server
{: #recreate_mobilefoundation_p3}

*	Click **Recreate** to re-create the server.

* This action stops your existing server and deletes the data. A new server instance is created with an updated version, if available. This action takes a few minutes to complete.

**Note**: All the data from your previous server instance including information on the apps and adapters is persisted in the configured {{site.data.keyword.dashdbshort_notm}} service instance, this data is used to recreate your server.

##	Setting up advanced configuration
{: #using_mfs_advanced_p3}

Use the **Start Server with Advanced Configuration** from the `Overview` page to create the server with advanced or custom settings. You can also update the server settings to customize your server configuration by clicking the **Configuration** tab. {{site.data.keyword.mobilefoundation_short}} gives you access to some advanced settings.

*	From the **Topology** tab, you can select the server size and memory based on your need. The default server is created with 1 GB of memory.
  - You can change the memory for your server based on your need to a maximum of 2 GB.

  - **Nodes** displays the number of nodes that are created. This field cannot be  edited in {{site.data.keyword.mobilefoundation_short}}: Developer Pro. The number of nodes <!--in your {{site.data.keyword.IBM_notm}} container group--> defaults to **1** in the Developer Pro plan.

See [{{site.data.keyword.mobilefoundation_long}} documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}, for more details.
