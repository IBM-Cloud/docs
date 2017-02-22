---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-31"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# About IBM {{site.data.keyword.HybridConnect_short}}
{: #about_hybridconnect}

{{site.data.keyword.HybridConnect_full}} is a Bluemix service, which is part of IBM Connect to Cloud. It connects your on-premises IBM software products to your {{site.data.keyword.HybridConnect_short}} service and provides insights into your running inventory and runtime usage metrics.

{:shortdesc}

The {{site.data.keyword.HybridConnect_short}} service is an entry point and more functions may be added in the future.

{{site.data.keyword.HybridConnect_short}} provides the following features:

* Registration of your on-premises IBM software products with IBM, specifically with a Bluemix service.
* Data collection for enabled and configured on-premise products and associated usage data.
* Through a dashboard, you can view runtime usage data to provide real insights into your product usage and workload.


To use the IBM Hybrid Connect capabilities, complete the following steps:

1. Create at least one service within Bluemix for {{site.data.keyword.HybridConnect_short}}.
1. Upgrade your on-premises IBM software products to the required release levels, and add the enablement code for each product installation. 
1. Configure the software installation with the Bluemix credentials for your {{site.data.keyword.HybridConnect_short}} service instance. All of your data is securely stored with these credentials. The data is available only to the individuals with proper permissions to the service.



## How it works
{: #hybridconnect_howitworks}
The {{site.data.keyword.HybridConnect_full}} service integrates with your on-premises IBM software products to gather and display runtime product information and usage metrics. Initially, a subset of IBM software products is enabled to integrate with this service. When enabled and configured, on-premise software products periodically send startup and usage information. The information is stored in relation to this service instance through the configured credentials. You can use the service instance dashboard to view the information within Bluemix.

The {{site.data.keyword.HybridConnect_short}} solution includes multiple components, as shown in the following graphic:

![{{site.data.keyword.HybridConnect_full}} architecture](images/architecture_hybridconnect.png "{{site.data.keyword.HybridConnect_full}} architecture").  


## Organizations and spaces
{: #hybridconnect_orgs}
Your {{site.data.keyword.HybridConnect_full}} service is associated with a single organization and space and has unique credentials. You must set up at least one organization and space. If you want to separate the data, for example, to limit access to specific individuals, you can create multiple spaces within an organization with one service instance in each space. Each service instance has unique credentials that you need to provide for your IBM software products.

Information for the products that are configured with a set of credentials is only visible within the service with those credentials. Multiple services can be created to separate the data if needed, each with unique credentials.


## Service dashboard
{: #service_dashboard}
After you create your service instance, you are directed to the service dashboard. You can always return to the service dashboard by clicking the service icon in your organization dashboard. From the service dashboard, you can access the following items:

* The Getting started documentation
* The service credentials that you need to configure your on-premises products
* The inventory of enabled products and the runtime instances that are registered to the {{site.data.keyword.HybridConnect_short}} service instance
* Product and environment information for the runtime instances
* Usage information for the runtime instances

If there are no registered products, a message is shown.
![Service dashboard with no registered products](images/NoRegisteredProducts.jpg "Service dashboard with no registered products")  

## Product inventory
{: #hybridconnect_products}
After you configure your products to send data to {{site.data.keyword.HybridConnect_short}}, you can view your inventory by selecting **Manage** in the service dashboard.

![Service dashboard](images/products.png "Service dashboard") 

For {{site.data.keyword.HybridConnect_short}}, a product is different from a product instance. A product has a product name, like IBM MQ or WebSphere Application Server Liberty Network Deployment. A product instance is used to represent a product after the product is installed and running. Some products have multiple instances that are run from within the same installation of the product. For example, WebSphere Application Server Liberty Network Deployment can run multiple applications servers that are created from a single installation of the product.

In the service dashboard, the names of the registered products are shown under the *All Products* choice in the **Products** pane. To the right of the Products pane is the **Product instances** pane. This pane contains instances of the products that are selected in the Products pane. In the following example, all of the product instances are shown because the *All Products* choice is selected in the Products pane. This example shows two products: IBM Product ABC and IBM Product XYZ. The product instances are shown to the right of the list of products.


![Service dashboard with products and product instances](images/productinstances.png "Service dashboard with products and product instances") 

To show product instances of a single product, select that product from the **Products** pane.

In the example, the list of product instances is filtered to show only the instances of IBM Product ABC. You can see your selection at the top of the window.


## Product instance information
{: #hybridconnect_productinstances}
When a product instance is selected, the *Details* pane is displayed on the right side. The Details pane shows details of the product instance and the usage information for that instance.

The **Details** tab shows product instance information, which might include the following items:

* The product name and version
* The location where the product is installed, including the host name and directory
* The last time when the instance sent information on startup
* The instance identifier if the product can have multiple instances within a single directory

![Product instance details](images/instancedetail.png "Product instance details") 

The product instance also provides the following optional information:

* A list of APARs that are installed. 
* The operating system and its version, which is shown in the **Environment** tab.
* Components or installed features, which are shown in the **Components** tab. The example does not show the  **Components** tab because the instance of IBM Product XYZ does not provide any additional component information. 
* The unique identifier for the product instance, which is a combination of the host name, directory, and instance identifier.

![Product instance details - Environment tab](images/instancedetails-env.png "Product instance details - Environment tab") 

![Product instance details - Component tab](images/instancedetails-comps.png "Product instance details - Component tab") 

## Usage information
{: #hybridconnect_usage}
The usage information is shown on the **Usage** tab. Use the two drop-down lists to select the metric to display (if the product instance sends more than one metric) and the time period to be displayed.

If the product instance sends more than one metric, use the first drop-down to select which metric to display. Select the time period to display from the second drop-down. The selections impact the sections below the drop-downs. The options for the time period for the sections are Last 24 hours, 1 week, 1 month, 6 months, 1 year.

The first section shows the average maximum, average, average minimum, and total of the metric values over the selected time period. The second section shows a graph of the values within the time period with the x-axis period, which changes based on the selected time period. For example, Last 24 hours shows graph points for each hour, while the 1-week display shows graph points for each day within that week). The final section shows the maximum, average, and minimum for the selected graph point. To see the values for another point on the graph, drag the blue time bar left and right.

A message is shown if there is no data for that time period. For example, a stopped instance would not provide data and no data will be shown for the time period when it was stopped. Other time periods can have usage to display. Change the time period in the drop-down to see other time periods.


## Searching 
{: #hybridconnect_search}
The **Product instance** pane provides a basic search capability to filter the product list. In the search field, type in the string that you want to use for the search. The search can be done only for product instance data (that is, the information in the **Details** tab). In the following example, from all product instances, the display is filtered to show only product instances that have product instance data that contains 1.4. Only one instance in the list contains 1.4, IBM Product XYZ within the version attribute. The attribute that the search string is found in and the value of the search string are highlighted.



<!-- If your service doc doesn't have a troubleshooting topic or section, you can add the following to your About: -->
<!-- Add a heading and content for how to get help and support. Use this template for beta and GA services:  -->
## Getting help for {{site.data.keyword.HybridConnect_short}}
{: #gettinghelp}

Detailed information about creating a service, getting the updates to the enabled IBM software products, and installation and configuration steps are found in the [{{site.data.keyword.HybridConnect_full}} Customer Community](https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/W04c8ca6d7a05_453c_8e2d_b784cde378be). If you have problems or questions when you are using {{site.data.keyword.HybridConnect_short}}, view or post questions in the forums section of the Community. These questions are handled by the development and customer programs team.

You can also use Stack Overflow and IBM DeveloperWorks dw Answers forums to view or post questions. For questions about the service and getting start instructions, use IBM developerWorks dW Answers. When you post a question on either of those two forums, apply the following tagging rules so that the Bluemix development teams can easily see your question.

* If you post on [Stack Overflow](http://stackoverflow.com/search?q=hybrid-connect+ibm-bluemix){:new_window}, tag your question with "ibm-bluemix" and "hybrid-connect".
* If you post on [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/hybrid-connect/?smartspace=bluemix){:new_window}, tag your questions with "hybrid-connect" and "bluemix".

For more information about using the forums, see the [Getting help](https://www.{DomainName}/docs/support/index.html#getting-help) topic.
