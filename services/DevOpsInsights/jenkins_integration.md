---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integrating {{site.data.keyword.DRA_short}} with Jenkins
{: #DRA_toolchain_configure_jenkins}

*Last updated: 13 September 2016*
{: .last-updated}

After you define the policies for {{site.data.keyword.DRA_full}} to monitor, the next step is to add {{site.data.keyword.DRA_short}} to a toolchain, and then configure a continuous delivery pipeline.
{:shortdesc}

<!--##Configuring a Jenkins project-->

You can integrate {{site.data.keyword.DRA_short}} into one Jenkins project or across several related Jenkins projects. This allows you set quality gates, as well as receive build quality data on the {{site.data.keyword.DRA_short}} dashboard.

##Prerequisites

* You must have access to a local Jenkins project, or to the server that is running a Jenkins project.

##Installing the {{site.data.keyword.DRA_short}} plugin

To install the {{site.data.keyword.DRA_short}} plugin in your Jenkins project, follow these steps:

  1. [Download the IBM DevOps Insight Plugin installation file (.hpi)](https://github.ibm.com/oneibmcloud/DRA-Jenkins/blob/hpi-release/target/dra.hpi) from the plugin's GitHub repository.
  2. In your Jenkins installation, click **Manage Jenkins**, select **Manage Plugins**, and click the **Advanced** tab.
  3. Click **Choose File** and select the DevOps Insight plugin installation file.
  4. Click **Upload**.
  5. Restart Jenkins and verify that the plugin was installed.

##Integrating {{site.data.keyword.DRA_short}} with Jenkins

After the plugin is installed, but before you integrate {{site.data.keyword.DRA_short}} into your Jenkins installation, go to the [control center](https://control-center.stage1.ng.bluemix.net/) and create at least one policy.

For each of the jobs that you already have, and in which you want to use {{site.data.keyword.DRA_short}}:

1. Add a post-build action with the type **Publish build information to {{site.data.keyword.DRA_short}}**, **Publish deployment information to {{site.data.keyword.DRA_short}}**, or **Publish test result to {{site.data.keyword.DRA_short}}**. The specific type should match the job type (build, deploy, or test). Complete the required fields. 
  * In the Credential field, choose your Bluemix ID and password. If they are not saved in Jenkins, click the **Add** button to add and save them.
  * In the Build Job Name field, specify your build job's name exactly as it is in Jenkins. If the build occurs together with the test job, leave this field empty. If the build job occurs outside of Jenkins, check **Builds are being done outside of Jenkins** and specify the build number and build URL.
  * For the Result File Location field, specify the result file's location. If the test doesn't generate a result file, leave this field empty. The plugin will upload a default result file based on the status of current test job.
3. *Optional*: If you want the DRA policy gates in the test job to control the downstream deploy job, add another post-build action with the type **DevOps Risk Analytics Gate** and complete the required fields. The gate will prevent the downstream job from running if the test job fails to meet the associated policies.
4. Click **Apply**, and then click **Save**.

You can click **Build Now** from the project page to run the project.

After the build runs, go to the [control center](https://control-center.stage1.ng.bluemix.net/) to check your build status in the dashboard. If you configured policy gates, you can also see {{site.data.keyword.DRA_short}} results on the Status page of the current build.
