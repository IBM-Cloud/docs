---

copyright:
  years: 2016

---

#	Using the Professional 1 Application plan
{: #using_mobilefoundation_p2}

*Last updated: 15 June 2016*
{: .last-updated}

After you create the {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application service instance, read the following procedure to get started with the service.

## Pre-requisites
{: #prerequisites_p2}

Consider the following before you configure  {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application service instance.
* {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application is supported only with {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional (supporting OLTP) {{site.data.keyword.Bluemix_notm}} plans.

* {{site.data.keyword.dashdbshort_notm}} service instance and its credentials should be available before you can configure the settings of your {{site.data.keyword.mobilefoundation_short}} service instance.

**Note**: The {{site.data.keyword.dashdbshort_notm}} service instance can exist in any `Space` within your {{site.data.keyword.Bluemix_notm}} `Organization`. If you choose to deploy the {{site.data.keyword.mobilefoundation_short}} service to a {{site.data.keyword.Bluemix_notm}} `Space` other than the one on which the {{site.data.keyword.dashdbshort_notm}} service exists,  then you must ensure that you have the permissions to access the {{site.data.keyword.dashdbshort_notm}} service.


## Adding the database connection
{: #configure_dashdb_p2}

###  First steps
{: #firststeps_p2}

After you create the {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application service instance, agree on the license terms for {{site.data.keyword.mfp_full_notm}} V8.0, to get started.

### Setting up connection to {{site.data.keyword.dashdbshort_notm}} service instance
{: #connect_dashdb_p2}

After the {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application service instance is created you will see the *Overview* page where you will need to specify the connection information for the {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional service instance.

1.  Select the {{site.data.keyword.Bluemix_notm}} `Space` where the {{site.data.keyword.dashdbshort_notm}} service instance exists, from the list of spaces available in the current `Organization`.

+ Select the {{site.data.keyword.dashdbshort_notm}} `Service Name` and `Credentials` to connect to the existing  {{site.data.keyword.dashdbshort_notm}} service instance.

+  Test the connection to the specified {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional service instance.

+  Click **Continue**. This action creates the required tables in the configured {{site.data.keyword.dashdbshort_notm}} database service instance.

**Note**: You cannot change the {{site.data.keyword.dashdbshort_notm}} service instance that is configured to be used by your {{site.data.keyword.mobilefoundation_short}} service instance. However, you can use the same {{site.data.keyword.dashdbshort_notm}} service instance across multiple {{site.data.keyword.mobilefoundation_short}} service instances, as each {{site.data.keyword.mobilefoundation_short}} service instance creates its own schema in the selected {{site.data.keyword.dashdbshort_notm}} service instance.

* In a few seconds, you can access the `Overview` page that provides you with  tutorials and videos to help you get started with the  {{site.data.keyword.mobilefoundation_short}} service.

## Starting the {{site.data.keyword.mobilefirst}} server
{: #start_mobilefoundation_p2}

* To start the {{site.data.keyword.mfserver_short_notm}}, with default settings, click **Start Basic Server**.

* This selection provisions an {{site.data.keyword.mfserver_long_notm}} with the following settings:
    -  1 GB of memory and 64 GB of storage. This size is enough for development and moderate testing activities.

    -	The `username` and `password` is automatically generated for you. You have access to them when the server is up and running.

The process of provisioning your server starts. This process takes about 10 minutes, and a message window indicates the progress of this operation. When complete a dashboard is displayed where you can see:

  -	The status of your server that is running (state, size, storage).

  -	The server route created for you. Use this route to reach your mobile server from the public internet. Your mobile applications use that route to access the server.

  -	Your personal `username` and `password` to access the {{site.data.keyword.mfp_oc_short_notm}}. The `password` is hidden. Click **Show Password** to visualize it.

*	Click **Launch Console** to open the {{site.data.keyword.mfp_oc_short_notm}}.


This console runs inside the container. With the console you can manage your mobile apps and mobile devices, use your server as a mobile backend, send push notifications, and do more.

## Re-creating the {{site.data.keyword.mobilefirst}} server
{: #recreate_mobilefoundation_p2}

*	Click **Recreate** to re-create the server.

* This action stops your existing server and deletes it. A new server instance is created. This action takes a few minutes to complete.

**Note**: All the data from your previous server instance including information on the apps and adapters is persisted in the configured {{site.data.keyword.dashdbshort_notm}} service instance, this data is available for use after the server is re-created.

##	Setting up advanced configuration
{: #using_mfs_advanced_p2}

Use the **Start Server with Advanced Configuration** from the `Overview` page to create the server with advanced or custom settings. You can also update the server settings to customize your server configuration by clicking the **Configuration** tab. {{site.data.keyword.mobilefoundation_short}} gives you access to some advanced settings.

*	From the **Topology** tab, you can select the size of your container. The default 1 GB server is enough for development and light testing.
  - Select the correct size for your server based on your need.

  - **Nodes** displays the number of nodes that are created.
      - You can configure the number of minimum and maximum nodes you require in your {{site.data.keyword.IBM_notm}} container group. Container groups provide high availability and scalability.

      - {{site.data.keyword.mobilefirst}} server farm can be created by configuring the number of nodes here.

See [{{site.data.keyword.mobilefoundation_long}} documentation](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}, for more details.
