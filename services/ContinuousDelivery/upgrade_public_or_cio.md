---

copyright:
  years: 2015, 2017
lastupdated: "2017-5-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Toolchains on {{site.data.keyword.Bluemix_notm}} Public compared to toolchains on {{site.data.keyword.Bluemix_notm}} CIO Dedicated 
{: #upgrade_public_or_cio}

{{site.data.keyword.jazzhub}} is evolving into IBM Bluemix {{site.data.keyword.contdelivery_short}}. As part of that change, projects will be upgraded to toolchains.

When your project is ready to be upgraded, a message is displayed on its Overview page. You can then upgrade the project to a toolchain on {{site.data.keyword.Bluemix_notm}} Public or on {{site.data.keyword.Bluemix_notm}} CIO Dedicated.
{: shortdesc}

To decide which environment to create your toolchain on, see the following table.

|Decision factors |{{site.data.keyword.Bluemix_notm}} Public |{{site.data.keyword.Bluemix_notm}} CIO Dedicated	|
|:----------|:------------------------------|:------------------------------|
|Upgrades		|Frequent		|Controlled and less frequent	|
|Services		|All services |Limited services |
|Support  |Standard {{site.data.keyword.Bluemix_notm}} support with industry-standard service level agreement  |Best-effort basis  |
|Access |General public  |IBMers only  |
{: caption="Table 1. Toolchains on {{site.data.keyword.Bluemix_notm}} Public compared to toolchains on {{site.data.keyword.Bluemix_notm}} CIO Dedicated" caption-side="top"} 

No matter which environment you create your toolchain on, if your project uses a Git repository (repo) that is hosted on JazzHub, during the upgrade a new repo is created on Whitewater {{site.data.keyword.ghe_short}}. After the upgrade, the person who started the upgrade must add team members to the {{site.data.keyword.ghe_short}} repo and ensure that they have the correct privileges before they can access the new repo.
