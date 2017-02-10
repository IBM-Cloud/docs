---

copyright:
  years: 2016, 2017
lastupdated: "2017-2-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integrating {{site.data.keyword.DRA_short}} with Jenkins
{: #toolchain_configure_jenkins}

After you define the policies for {{site.data.keyword.DRA_full}} to monitor, you can add {{site.data.keyword.DRA_short}} to a toolchain and configure a continuous delivery pipeline.
{:shortdesc}

You can integrate {{site.data.keyword.DRA_short}} into one Jenkins project or across several related Jenkins projects by installing a plugin. After you install the plugin, you can set quality gates and receive analytic data on the {{site.data.keyword.DRA_short}} dashboard.

##Prerequisites    
{: #DI_jenkins_prereqs}

* You must have access to a local Jenkins project or to the server that is running a Jenkins project.

##Installing and configuring the {{site.data.keyword.DRA_short}} plugin
{: #DI_jenkins_install}

Before you begin, download the [the {{site.data.keyword.DRA_short}} plugin installation file (.hpi)](https://github.ibm.com/oneibmcloud/DevOps-Insights-Jenkins-plugin-release/blob/master/dra.hpi). 

For the latest installation and configuration instructions, see [the plugin documentation](https://github.ibm.com/oneibmcloud/DevOps-Insights-Jenkins-plugin-release/blob/master/README.md).

**Note:** If you are not an IBM employee, you must request access before you can download the {{site.data.keyword.DRA_short}} plugin. To submit a request for access, follow these steps:

1. While you are logged in to {{site.data.keyword.Bluemix_notm}}, in the header, click **Support**.
2. Click **Add Ticket**
3. Click **Something Else**. 
4. Complete the ticket. In the **Subject** field, include the words *DevOps Insights Jenkins*. 
