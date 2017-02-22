---

copyright:
  years: 2016, 2017
lastupdated:  "2017-02-17"

---

#	Using the Developer plan
{: #using_mobilefoundation_p1}

After you create the {{site.data.keyword.mobilefoundation_short}}: Developer service instance, in a few seconds, you can access the `Overview` page on {{site.data.keyword.Bluemix_notm}}, which provides you tutorials and videos to help you get started with the  {{site.data.keyword.mobilefoundation_short}} service.

## Starting the MobileFirst server
{: #start_mobilefoundation_p1}
* To start the {{site.data.keyword.mfserver_short_notm}} with default settings, click **Start Basic Server**.

This selection provisions an {{site.data.keyword.mfserver_long_notm}} with the following settings:
*	1 GB of memory. This size is enough for development, light testing activities and small scale production workloads.

*	The `username` and `password` is automatically generated for you. You have access to them when the server is up and running.

The process of provisioning starts. This process takes about 10 minutes, and a message window indicates the progress of this operation. When complete a dashboard is displayed where you can see:
*	The status of your server that is running (state, size).

*	The server route created for you. Use this route in your mobile application to connect to the {{site.data.keyword.mfserver_short_notm}}.

*	Your personal `username` and `password` to access the {{site.data.keyword.mfp_oc_short_notm}}. The `password` is hidden. Click **Show Password** icon to visualize it.

*	Click **Launch Console** to launch the {{site.data.keyword.mfp_oc_short_notm}}.


<!--This console runs inside the container.--> With the console you can manage your mobile apps and mobile devices, use your server as a mobile backend, send push notifications, and do more.

##  Adding Mobile Analytics server
{: #adding_analytics_server_dev}

 You can now monitor your mobile application on {{site.data.keyword.mobilefirst}} server by adding a Mobile Analytics server to the {{site.data.keyword.mobilefoundation_short}} service instance. Developer plan creates the Mobile Analytics server in a container group with a single node having 1 GB memory.

* Click **Add Analytics** to add the Mobile Analytics server to the {{site.data.keyword.mobilefoundation_short}} service instance.

The process of provisioning starts. This process takes about 10 minutes, and a message window indicates the progress of this operation.  

* Launch the MobileFirst Analytics Console from the {{site.data.keyword.mfp_oc_short_notm}}.

* Single sign-on is enabled between the {{site.data.keyword.mfserver_short_notm}} and the Mobile Analytics server. Mobile Analytics server is configured with the same LTPA keys and user credentials as the {{site.data.keyword.mfserver_short_notm}}. You can use the same `username` and `password` to log in to the Mobile Analytics console as used to log in to the {{site.data.keyword.mfp_oc_short_notm}}.

For more information on MobileFirst Analytics you can refer to [MobileFirst Foundation Operational Analytics ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/analytics/){: new_window}.

**Note:** The Mobile Analytics server is removed when you delete the {{site.data.keyword.mobilefoundation_short}} service instance or when you attempt to re-create the {{site.data.keyword.mfserver_short_notm}}.

##  Deleting Mobile Analytics server
{: #deleting_analytics_server_dev}

You can now delete the Mobile Analytics server that was added to the {{site.data.keyword.mobilefoundation_short}} service instance, from the {{site.data.keyword.mobilefoundation_short}} service dashboard.

* Click **Delete Analytics** to delete the  Mobile Analytics server that was added to the {{site.data.keyword.mobilefoundation_short}} service instance.

 This will delete the analytics container group. The process of deleting analytics containers takes about 10 minutes. You can refresh the screen to view the updated status. Once the analytics containers are deleted, the **Add Analytics** button is re-enabled, you can use this to add the Mobile Analytics server again if you choose to.


## Re-creating the MobileFirst server
{: #recreate_mobilefoundation_p1}

*	Click **Recreate** to re-create the server.

* This action stops your existing server and deletes the data. All the data in your mobile server is lost. A new server instance is created with an updated version, if available. This action takes a few minutes to complete.

##	Setting up advanced configuration
{: #using_mfs_advanced_p1}

Use the **Start Server with Advanced Configuration** from the `Overview` page to create the server with advanced or custom settings. You can also update the server settings to customize your server configuration by clicking the **Configuration** tab. {{site.data.keyword.mobilefoundation_short}} gives you access to some advanced settings.

*	From the **Topology** tab, you can select the server size and the number of instances you need. The default 1 GB server is enough for development and moderate testing.

  - Select the correct size for your server based on your need.

* **Nodes** displays the number of nodes that are created. This field is not editable in {{site.data.keyword.mobilefoundation_short}}: Developer. The number of nodes <!--in your {{site.data.keyword.IBM_notm}} container group--> is defaulted to **1** in the Developer plan.

Refer to the [{{site.data.keyword.mobilefoundation_long}} documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window} for more details.
