---

copyright:
  years: 2016
lastupdated:  "2016-11-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Getting started with {{site.data.keyword.mobilefoundation_short}}
{: #gettingstartedtemplate}

{{site.data.keyword.mobilefoundation_long}} expedites setting up an {{site.data.keyword.mfp_full}} environment from which you can develop, test, and operate enterprise mobile apps. {{site.data.keyword.mobilefoundation_short}} is available under two different service plans: Developer and Professional 1 Application.
{:shortdesc}

<!-- The Professional 1 Application plan allows the {{site.data.keyword.mobilefoundation_short}} server to be deployed on a scalable container group.--> Using the Professional 1 Application plan a single application built on any or all of the supported operating platforms such as Android, iOS, Windows or mobile web, can be managed. The Developer plan <!-- does not support {{site.data.keyword.mobilefoundation_short}} deployment on a container group with more than 1 node. This plan --> is best suited for development and test.

## Getting started with {{site.data.keyword.mobilefoundation_short}}: Developer plan

After you create an instance of the {{site.data.keyword.mobilefoundation_short}}: Developer, you can start building your mobile channel with just a few clicks.

*	To create a {{site.data.keyword.mobilefirst_notm}} server instance with the default configuration, click **Start Basic Server**.

  `The basic server instance includes a single node, 1 GB of memory.`

* To create a {{site.data.keyword.mobilefirst_notm}} server instance with advanced configuration for topology, security, and other server configuration, click **Start Server with Advanced Configuration**. See [Setting up advanced configuration](c_using_mfs_p1.html#using_mfs_advanced_p1), for more information.

## Getting started with {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application plan

After you create an instance of the {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application service, you can start building your mobile channel by completing the following steps.

1.  Connect to an existing {{site.data.keyword.dashdbshort}}: Enterprise Transactional service on {{site.data.keyword.Bluemix_notm}}.

    1.  Select the {{site.data.keyword.Bluemix_notm}} `Organization` where the {{site.data.keyword.dashdbshort_notm}} service instance exists.

    + Select the {{site.data.keyword.Bluemix_notm}} `Space` where the {{site.data.keyword.dashdbshort_notm}} service instance exists, from the list of spaces available in the selected `Organization`.

    + Select the {{site.data.keyword.dashdbshort_notm}} `Service Name` and `Credentials` to connect to the existing  {{site.data.keyword.dashdbshort_notm}} service instance.

    + Test the connection to the selected {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional service instance by clicking **Test Connection**.

    + Click **Add**, followed by **Continue** on the pop up window asking for confirmation on the selected {{site.data.keyword.dashdbshort_notm}} service. This action creates the required tables in the configured {{site.data.keyword.dashdbshort_notm}} database service instance.

    **Note:** After you add a {{site.data.keyword.dashdbshort_notm}} connection to the {{site.data.keyword.mobilefoundation_short}} instance you will not be able to change it.

2.  Create and start the server.

    * To create a {{site.data.keyword.mobilefirst_notm}} server instance with the default configuration, click **Start Basic Server**.

      `The basic server instance includes a single node, 1 GB of memory.`

    * To create a {{site.data.keyword.mobilefirst_notm}} server instance with advanced configuration for topology, security, and other server configuration, click **Start Server with Advanced Configuration**. See [Setting up advanced configuration](c_using_mfs_p2.html#using_mfs_advanced_p2), for more information.

Go to [Using the Mobile Foundation service to set up MobileFirst Server<!-- on IBM Containers-->](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/bluemix/using-mobile-foundation/) to learn more about how to get started with {{site.data.keyword.mobilefoundation_short}}.

##  Known limitations

* The {{site.data.keyword.mobilefoundation_short}} service UI does not use the user selected locale-specific pattern to display numbers.


# Related Links
{: #rellinks}

## Related Links
{: #general}

*	[IBM MobileFirst Platform Foundation V8.0.0 product documentation](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}
*	[IBM MobileFirst Platform Developer Center](https://mobilefirstplatform.ibmcloud.com){: new_window}
