---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integrating {{site.data.keyword.DRA_short}} with Jenkins (Experimental)
{: #toolchain_configure_jenkins}

After you define the policies for {{site.data.keyword.DRA_full}} to monitor, you can add it to a toolchain and configure a continuous delivery pipeline.
{:shortdesc}

You can integrate {{site.data.keyword.DRA_short}} into one Jenkins project or across several related Jenkins projects by installing a plugin. After you install the plugin, you can set quality gates and view analytic data in {{site.data.keyword.DRA_short}}.

##Prerequisites    
{: #DI_jenkins_prereqs}

* You must have access to a local Jenkins project or to the server that is running a Jenkins project.

##Installing and configuring the plugin
{: #DI_jenkins_install}

Before you begin, download the [the {{site.data.keyword.DRA_short}} plugin installation file (.hpi)](https://github.ibm.com/oneibmcloud/Jenkins-IBM-Bluemix-Toolchains/tree/release/target/dra.hpi). 

For the latest installation and configuration instructions, see [the plugin documentation](https://github.com/imvijay2007/Jenkins-IBM-Bluemix-Toolchains).

**Note:** If you are not an IBM employee, you must request access before you can download the {{site.data.keyword.DRA_short}} plugin. To submit a request for access, send an email to aggarwav@us.ibm.com and jichen@us.ibm.com. In the email subject, include the phrase *Need Jenkins plugin*.
