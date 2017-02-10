---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integrating {{site.data.keyword.DRA_short}} with Jenkins
{: #toolchain_configure_jenkins}

After you define the policies for {{site.data.keyword.DRA_full}} to monitor, the next step is to add {{site.data.keyword.DRA_short}} to a toolchain, and then configure a continuous delivery pipeline.
{:shortdesc}

You can integrate {{site.data.keyword.DRA_short}} into one Jenkins project or across several related Jenkins projects by installing a plugin. This allows you to set quality gates, as well as receive analytic data on the {{site.data.keyword.DRA_short}} dashboard.

##Prerequisites    
{: #DI_jenkins_prereqs}

* You must have access to a local Jenkins project, or to the server that is running a Jenkins project.

##Installing and configuring the {{site.data.keyword.DRA_short}} plugin
{: #DI_jenkins_install}

Prior to installation and configuration, download the [the {{site.data.keyword.DRA_short}} plugin installation file (.hpi)](https://github.ibm.com/oneibmcloud/DevOps-Insights-Jenkins-plugin-release/blob/master/dra.hpi). 

For the latest installation and configuration instructions, see [the plugin documentation](https://github.ibm.com/oneibmcloud/DevOps-Insights-Jenkins-plugin-release/blob/master/README.md).

*Note*: If you are not an IBM employee, you must request access before you can download the DevOps Insights plugin. To submit a request for access:

1. Click **Support** at the top of the screen while logged in to Bluemix.
2. Click **Add Ticket**
3. Choose **Something Else** category. 
4. Complete the ticket. In the Subject field, include the words "DevOps Insights Jenkins." 


