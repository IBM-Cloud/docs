---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-24"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Getting started with IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}
{: #getting_started}

{{site.data.keyword.IBM}} WebSphere Application Server in {{site.data.keyword.Bluemix}} is a service that facilitates quick setup on a pre-configured WebSphere Application Server Liberty, Traditional Network Deployment, or Traditional WebSphere Java EE instance in a hosted cloud environment on {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

## Overview of WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}
{: #overview}

WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} provides consumers with pre-configured Traditional WebSphere and Liberty Profile servers. It is hosted on virtual machine guests with root access to the guest operating system. When you are creating your service, choose between _Liberty_, _Traditional ND_, or _Traditional WebSphere_.

**Note:** Consumers are now able to choose between V8.5 and V9.0 when you create a new _Traditional ND_ or _Traditional WebSphere_ instance.

You are given a familiar WebSphere administration experience and have full access to the underlying operating system. You can reuse your existing scripts and make the little system tweaks that you need to make to work with your own, or third party, frameworks. The Admin Center and Admin Consoles are provided to administer your WebSphere Application Server Liberty, ND or Traditional service, just like your on-premises WebSphere configurations.

The WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} Network Deployment Plan consists of a WebSphere Application Server Network Deployment cell environment with two or more virtual machines. The first virtual machine contains the Deployment Manager and IBM HTTP Server and the remaining virtual machines contain custom nodes (node agents) federated to the Deployment Manager. Use your existing wsadmin scripts to create your WebSphere configuration or use the WebSphere Admin Console to manually configure the environment. These new capabilities allow users to set up a clustered environment, which is a critical aspect of any middleware enterprise application. Clients can now elect to cluster a topology to load balance requests across two or more Instances.

The WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} Liberty Core Plan includes the use of a Liberty Collective. The Liberty Collective is an administrative domain for a group of Liberty profiles (servers) and consists of two or more virtual machines. The first virtual machine contains the Collective Controller liberty server, which is a control point for the Liberty Collective. In addition to the liberty collective, this virtual machine also contains the IBM HTTP Server, which allows access to your applications from a web browser. The remaining virtual machines are the collective hosts where the collective members reside (liberty profile servers). The Liberty Admin Center feature is also enabled on the liberty controller server.

The following figure shows the architecture of the WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} Network Deployment Cell and Liberty Collective environments.

Figure 1. Network deployment cell and Liberty collective architecture

![Figure1. Architecture of Network deployment cell and Liberty collective](images/CellCollectiveDiagram.gif)

**Note**: In _Figure 1_ above, the pattern that depicts collocation of the Deployment Manager or the Collective controller with the IBM HTTP Server is intended for development and testing purposes. WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} also gives you the freedom to reconfigure the preinstalled software to meet your production application and operational needs; just as you would on-premises. Further, for the strictest production requirements, contact your IBM Sales representative who can speak to our single-tenant IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} offering, which offers isolated networking and compute resources.


## Operational Environment
{: #operational_environment}

IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} is a service that returns guests (virtual machines) in a shared environment for consumers to deploy applications. A VPN protects the public service from generic port scans and other unsolicited network-based attacks. However, it is important to note that the service VPN you use to access your service instance might be shared between multiple {{site.data.keyword.Bluemix_notm}} organizations and users. The virtual machines provide compute, memory, and I/O resources, which come from a shared pool of IaaS resources.

As specific compute, memory, and I/O resources are run by virtual machines in a shared environment, service configurations might vary. Configurations for each specific service instance can be viewed through the IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} service dashboards and portals.

IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} provides virtual machine instances. With these instances, clients use a simple portal to create and manage enterprise WebSphere Application Server deployments in a consistent, repeatable manner with significant flexibility to tune their applications. Users can get up and running on pre-configured WebSphere Application Server Liberty, ND, or Traditional virtual machines in a hosted cloud environment. Users can migrate existing WebSphere Application Server applications to {{site.data.keyword.Bluemix_notm}} and take full control of the underlying OS and middleware.

## Pricing Strategy
{: #pricing_strategy}

IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} provides T-Shirt sized instances for clients with memory-intensive applications to "right-size" their environment with larger virtual machines. Clients can select the specific resource size of a provisioned WebSphere Application Server component or single system up to 32 GB RAM virtual machines.

The following tables represent IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} plan prices as of April 1, 2016 and are represented in US dollars (USD).

*Table 1. Liberty Core Plan*

| **T-Shirt** | **vCPU** | **RAM (GB)** | **HD (GB)** | **Price/Hr** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | $0.21 |
| M | 2 | 4 | 25 | $0.42 |
| L | 4 | 8 | 50 | $0.84 |
| XL | 8 | 16 | 100 | $1.68 |
| XXL | 16 | 32 | 200 | $3.36 |

*Table 2. WebSphere Application Server Base Plan*

| **T-Shirt** | **vCPU** | **RAM (GB)** | **HD (GB)** | **Price/Hr** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | $0.30 |
| M | 2 | 4 | 25 | $0.60 |
| L | 4 | 8 | 50 | $1.20 |
| XL | 8 | 16 | 100 | $2.40 |
| XXL | 16 | 32 | 200 | $4.80 |

*Table 3. WebSphere Application Server ND Plan*

| **T-Shirt** | **vCPU** | **RAM (GB)** | **HD (GB)** | **Price/Hr** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | $0.70 |
| M | 2 | 4 | 25 | $1.40 |
| L | 4 | 8 | 50 | $2.80 |
| XL | 8 | 16 | 100 | $5.60 |
| XXL | 16 | 32 | 200 | $11.20 |

<p></p>

IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} is offered in accordance with the following charge metric:

*  *Instance-Hour*: An Instance is defined as access to a specific configuration of the IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} Service. Clients are charged for each full or partial hour for each Instance of the Service that is deployed during the billing period. Each Instance Hour is billed monthly and if an instance is only used part of the month, the usage rate is prorated.

For example, if you use the ND Plan, one Instance equates to 1vCPU with 2 GB RAM and 12 GB HD. So if you chose to configure your Cell with one Control node and eight Custom nodes, you would be charged for nine nodes (instances).

**Note**: Minimum billing is set at 0.25 instance hour per Custom node or Liberty host. In the example above, one Control node and one Custom node that is configured for at least 15 minutes would equate to a minimum charge of (.25 * # of Instances).

**Note**: Due to a specific amount of compute, memory, and I/O resources, clients are charged for accumulated instances in the STOPPED state at a reduced rate of 5%. Clients are managed to a fixed number of STOPPED instances with no more than 10 IP addresses or 64 GB of memory.

# rellinks
{: #rellinks}
## general
{: #general}
* [WASdev](https://developer.ibm.com/wasdev/){: new_window}
* [WebSphere Application Server V9 Documentation](http://www.ibm.com/support/knowledgecenter/SSEQTP_9.0.0/as_ditamaps/was900_welcome_base.html){: new_window}
