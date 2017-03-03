---

copyright:
  years: 2016, 2017
lastupdated: "2017-3-2"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Getting started with {{site.data.keyword.product-insights_short}}
{: #product-insights}

{{site.data.keyword.product-insights_full}} connects to on-premises IBM software products to build a cross-product inventory and provide insights into product usage metrics.

{:shortdesc}

The {{site.data.keyword.product-insights_short}} service runs within IBM Bluemix and receives information from the enabled on-premises IBM software products. This information is then shown within the service instance dashboard. To use the service, you must have a Bluemix account and create the service in an organization and space. The product and usage information for your enabled on-premises products is securely stored and viewed within the scope or context of that unique service. 

Tip: For simplicity, you can initially use a single service instance.

To get started with {{site.data.keyword.product-insights_short}}, complete the following steps:

1.  In the **Manage** tab, click the **Register a product** button to view a list of supported products and the required version level. Instructions for each product type are provided, so that you can connect your on-premise product instances to the {{site.data.keyword.product-insights_short}} service. If required, update your enabled, on-premises IBM software products to the minimum prerequisite level. For a product that requires a minimum supported level, install the fix pack or interim fix to enable the integration with {{site.data.keyword.product-insights_short}}. 
2.  Connect your enabled, on-premises IBM software products to your {{site.data.keyword.product-insights_short}} service. As part of the configuration process for each product, you need the service credentials (that is, the apikey and apihost). You can find the service credentials in the **Service Credentials** tab of your service dashboard. 
3.  After you enable and connect each product instance, you may need to start or restart the products or product instances for them to provide product and usage information to the {{site.data.keyword.product-insights_short}} service. 

For details on the enabling products, the minimum support level required for each product, and how to enable each product to integrate with {{site.data.keyword.product-insights_short}}, join the {{site.data.keyword.product-insights_full}} [Technical Community](https://developer.ibm.com/product-insights/).

You can view your inventory by selecting **Manage** in the service dashboard.  

* In the service dashboard, the names of the products that have been connected are listed in the **Products** pane. 
* To show all product instances, select **View all**. To show product instances for a product, select that product from the **Products** pane and they are displayed in the **Instances** pane.
* To show the details of a single product instance, select the product instance from the **Instances** pane. The **Details** pane is displayed on the right side. The **Details** pane shows details of the product instance and the usage information that has been sent from the instance.
* The **Usage** tab shows product usage information in graphical format. Depending on the product, you can specify the type of information that you want to view and the sampling period.
* The **Details** tab shows product instance information; including product information, environment information, and component information.
* The **Advisor** tab, in its **Services** tab, provides details on additional services that may be of benefit in relation to the current product instance. In its **Updates** tab, it provides information on the product instance version level and its currency.







