---

copyright:
  years: 2016

---

#	Using the Developer plan
{: #using_mobilefoundation_p1}

*Last updated: 15 June 2016*
{: .last-updated}

After you create the {{site.data.keyword.mobilefoundation_short}}: Developer service instance, agree on the license terms for {{site.data.keyword.mfp_full_notm}} V8.0, to get started.
After a few seconds, you can access the `Overview` page on {{site.data.keyword.Bluemix_notm}}, which provides you tutorials and videos to help you get started with the  {{site.data.keyword.mobilefoundation_short}} service.

## Starting the {{site.data.keyword.mobilefirst}} server
{: #start_mobilefoundation_p1}
* To start the {{site.data.keyword.mfserver_short_notm}} with default settings, click **Start Basic Server**.

This selection provisions an {{site.data.keyword.mfserver_long_notm}} with the following settings:
*	1 GB of memory and 64 GB of storage. This size is enough for development and light testing activities.

*	The `username` and `password` is automatically generated for you. You have access to them when the server is up and running.

The process of provisioning starts. This process takes about 10 minutes, and a message window indicates the progress of this operation. When complete a dashboard is displayed where you can see:
*	The status of your server that is running (state, size, storage).

*	The server route created for you. Use this route to reach your mobile server from the public internet. Your mobile applications use that route to access the server.

*	Your personal `username` and `password` to access the {{site.data.keyword.mfp_oc_short_notm}}. The `password` is hidden. Click **Show Password** to visualize it.

*	Click **Launch Console** to launch the {{site.data.keyword.mfp_oc_short_notm}}.


This console runs inside the container. With the console you can manage your mobile apps and mobile devices, use your server as a mobile backend, send push notifications, and do more.

## Re-creating the {{site.data.keyword.mobilefirst}} server
{: #recreate_mobilefoundation_p1}

*	Click **Recreate** to re-create the server.

* This action stops your existing server and deletes it. All the data in your mobile server is lost. A new server instance is created. This action takes a few minutes to complete.

##	Setting up advanced configuration
{: #using_mfs_advanced_p1}

Use the **Start Server with Advanced Configuration** from the `Overview` page to create the server with advanced or custom settings. You can also update the server settings to customize your server configuration by clicking the **Configuration** tab. {{site.data.keyword.mobilefoundation_short}} gives you access to some advanced settings.

*	From the **Topology** tab, you can select the size of your container. The default 1 GB server is enough for development and moderate testing.

  - Select the correct size for your server based on your need.


* **Nodes** displays the number of nodes that are created. This field is not editable in {{site.data.keyword.mobilefoundation_short}}: Developer. The number of nodes in your {{site.data.keyword.IBM_notm}} container group is defaulted to **1** in the Developer plan.

Refer to the [{{site.data.keyword.mobilefoundation_long}} documentation](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window} for more details.
