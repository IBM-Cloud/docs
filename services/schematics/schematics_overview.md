---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# About
{: #about}

{{site.data.keyword.bplong}} can be used to create infrastructure building blocks. You can put together {{site.data.keyword.IBM_notm}} Cloud services to create infrastructure that is deployable and reusable.
{:shortdesc}

{{site.data.keyword.bpshort}} uses Terraform to simplify infrastructure management. For example, if you want to spin up multiple copies of your service that uses a cluster of app servers, a load balancer, and a database server, you might write a bash script to run commands to spin up these components. But, it's easier, faster, and more orderly to have a configuration with a runner that takes the configuration and turns it into real resources. With Terraform, you can spin up numerous resources at the same time, as a collective group, with dependencies mapped within. 

## Reasons to use {{site.data.keyword.bpshort}}
{: #reasons}

You might want to use codified infrastructure in the following scenarios:
{:shortdesc}

| Scenario     | Reasons    |
| :------------- | :------------- |
| You want to re-create and reuse your infrastructure. | You can use {{site.data.keyword.bpshort}} for infrastructure management. With {{site.data.keyword.bpshort}}, you can provision, modify, and destroy your resources programmatically. When you codify and configure resources, you can build up a library of resources that can be reused again and again to net the same results.|
| You want transparency as to how your environments are set up. | {{site.data.keyword.bpshort}} works with configurations in source control, which enables collaboration, review, and gives you an audit trail to see how and when changes were made. You can also view your changes if you need to roll back to a previous configuration. |
| You want to simplify the execution of environmental changes. | {{site.data.keyword.bpshort}} follows the declarative model that provides a single source of truth. When you plan a change to your environment, you state the outcome you want. |
| You already use a configuration management (CM) tool, but you want a more automated way to set up your environments. | {{site.data.keyword.bpshort}} can work along with CM tools. Environments that are deployed with {{site.data.keyword.bpshort}} are high-level abstractions that can create infrastructure resources. You can then use CM tools to install and configure software on the resources that {{site.data.keyword.bpshort}} provisioned.  
  
## How it works
{: #how}

You can deploy resources to your environments by using {{site.data.keyword.bpshort}}. 
{:shortdesc}

{{site.data.keyword.bpshort}} uses Terraform as the underlying tool to enable infrastructure as code so that you can define {{site.data.keyword.IBM}} Cloud resources as code. Cloud resources can be different components of your infrastructure, such as bare metal servers, virtual servers, load balancers, software-defined networking components. 

### Configurations to define resources
{: #how-define}

A configuration, or Terraform configuration, is a file that defines which resources make up your infrastructure. Configurations are deployable architectures that can be applied to one or more environments. The following diagram shows what makes up a configuration and how the pieces work together to create a deployable environment in {{site.data.keyword.bpshort}}.


![{{site.data.keyword.bpshort}} architecture diagram](/images/anatomy_of_a_schematic.png)

Figure 1. {{site.data.keyword.bpshort}} architecture diagram

### Source control to enable collaboration
{: #how-collaborate}

Configurations are stored in GitHub so that teams can review code and collaborate. With GitHub, you have a built-in audit trail and can view a full commit history of changes that are made to your configurations. You can save usage information in readme files to make the configuration shareable and usable by multiple teams.

### {{site.data.keyword.bpshort}} environments to provision resources
{: #how-provision}

You can use {{site.data.keyword.bpshort}} to scan your code in GitHub and deploy resources to an environment. Environments can share common configurations. For example, you can spin up a temporary QA environment that looks like production and tear it down when you're done with testing. You can build a library of common environment configurations that can be tagged and searched by all users in your {{site.data.keyword.Bluemix_notm}} account.
