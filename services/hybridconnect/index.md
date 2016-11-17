---

copyright:
  years: 2016
lastupdated: "2016-11-12"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Getting started with {{site.data.keyword.HybridConnect_short}} (Experimental)
{: #hybridconnect}

{{site.data.keyword.HybridConnect_full}} connects to on-premises IBM software products to build a cross-product inventory and provide insights into product usage metrics.

{:shortdesc}

The {{site.data.keyword.HybridConnect_short}} service runs within Bluemix and receives information from the enabled on-premises IBM software products. This information is then shown within the service instance dashboard. To use the service, you must have an an {{site.data.keyword.Bluemix}} account and create the service in an organization and space.  The product and usage information about your enabled on-premises products is securely stored and viewed within the scope or context of that unique service. 

Tip: For an experimental service, you can use a single service instance for simplicity.

To get started with {{site.data.keyword.HybridConnect_short}}, complete the following steps:

1.  Update your enabled, on-premises IBM software products to the minimum prerequisite level, if required. For a product that requires a minimum supported level, install the fix pack or interim fix to enable the integration with {{site.data.keyword.HybridConnect_short}}. 
2.  Connect your enabled, on-premises IBM software products to your {{site.data.keyword.HybridConnect_short}} service. As part of the configuration process for each product, you need the service credentials (i.e. the apikey). You can find the service credentials on the **Service Credentials tab** of your service dashboard. 
3.  After you obtain the enablement changes and install and configure each enabled product, you may need to start or restart the products or product instances for them to provide product and usage information to the {{site.data.keyword.HybridConnect_short}} service. 

For details on the enabling products, the minimum support level required for each product, and how to enable each product to integrate with {{site.data.keyword.HybridConnect_short}}, join the {{site.data.keyword.HybridConnect_full}} [Experimental Customer Program](https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/W04c8ca6d7a05_453c_8e2d_b784cde378be).

You can view your inventory by selecting **Manage** in the service dashboard.  

* In the service dashboard, the names of the products that have provided information are shown under the **All Products** choice in the **Products** pane. 
* To show all product instances, select **All Products** from the **Products** pane.  To show product instances of a single product, select that product from the **Products** pane and they are displayed in the **Product instances** pane.
* To show the details of a single product instance, select the product instance from the **Product instances** pane. The **Details** pane is displayed on the right side. The **Details** pane shows details of the product instance and the usage information that has been sent from the instance.
* The **Details** tab shows product instance information, including product information, and optionally, environment information and component information.
* The **Usage** tab shows product usage information.

