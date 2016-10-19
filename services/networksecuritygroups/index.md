---

copyright:

  years: 2016

lastupdated: "2016-10-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:note: .deprecated}

# Getting started with {{site.data.keyword.networksecuritygroups_short}}
{: #nsgintro}  

The {{site.data.keyword.networksecuritygroups_full}} service in Bluemix&reg; focuses on network security. Use the IBM Network Security Groups service to configure and manage network policies that control inbound and outbound traffic between virtual servers.  
{: shortdesc}

**This service is deprecated:** Existing service instances can be used until 23 December 2016. 
{: deprecated}

Before you begin, create a Network Security Groups service instance from the [Bluemix catalog](https://console.{DomainName}/catalog/services/network-security-groups/). The service UI is displayed after you create the service instance. You can also access the service UI by selecting the service instance tile from the Bluemix dashboard.

You can use the Bluemix UI or the [command line interface](https://new-console.{DomainName}/docs/cli/plugins/networksecuritygroups/index.html) to configure the Network Security Groups service. The following instructions are for using the Bluemix UI.

**Note:** Use only Google Chrome 47.0.2526 or Mozilla Firefox 38.5.2 browser to create and configure IBM Network Security Groups.

To get started:

1. Select **CREATE SECURITY GROUP +** on the service dashboard.
2. Provide the following information:  
	* **Security Group Name**: Enter a name for the security group.
	* **Instance Type**: Select the instance type for which you want to create the security group. Value: Virtual Servers.  
	* **Description**: Enter a description of the security group.
3. Select **CREATE**. The security group is created.  

Next, you can add one or more rules to the security group. See [Configuring rules](https://new-console.{DomainName}/docs/services/networksecuritygroups/networksecuritygroups_rules.html#nsgrules).

# rellinks
## general  
{: #general}  
* [IBM Network Security Groups command line interface](../../cli/plugins/networksecuritygroups/index.html)
* [IBM Bluemix Pricing Sheet](https://console.{DomainName}/pricing/){: new_window}
* [IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs)
