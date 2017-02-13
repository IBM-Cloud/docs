---

copyright:
  years: 2017
  last-updated: "2017-02-13"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Getting started with {{site.data.keyword.uccr_short}} (Experimental)

{: #gettingstartedtemplate}

The {{site.data.keyword.uccr_full}} service on IBM {{site.data.keyword.Bluemix_short}} is a comprehensive release management solution. With IBM Cloud Continuous Release, you can run deployments for all software applications in your development lifecycle.
{:shortdesc}

[After you create an instance](https://console.ng.bluemix.net/catalog/services/continuous-release/){:new_window} ![External link icon](../../icons/launch-glyph.svg "External link icon") of {{site.data.keyword.uccr_short}}, choose how you want to get started.

* Begin with **[creating a deployment plan and running a deployment](#gs_create_plan)** if you want to plunge in and start creating deployment plans.

* Begin with **[installing and configuring DevOps Connect](#gs_install_dc)** if you want to integrate {{site.data.keyword.uccr_short}} with your on-premises IBM UrbanCode&trade; Deploy instance. After you configure an integration, you can use Continuous Release tasks to manage UrbanCode Deploy applications.


## Creating a deployment plan and running a deployment
{: #gs_create_plan}

1. Create a deployment plan.

  * [Create a plan](/docs/services/UCCR/UCCR_deployPlan.html#plan_create) and assign it to one of your teams. Any team member can run the tasks in the deployment plan. You can modify this behavior by assigning tasks to groups or specific team members.

  * [Add tasks to the deployment plan](/docs/services/UCCR/UCCR_tasks.html#tasks_create). Each task is listed on a separate row in the deployment plan. Try adding different types of tasks: manual, UrbanCode Deploy, delay, and note.

  * You can modify the list of tasks in the plan in various ways. You can reposition tasks, copy tasks, and delete them.

4. When your deployment plan is ready, run a deployment by using the deployment plan that you created in the previous step.

  * [You run a deployment by resolving the tasks in a deployment plan](/docs/services/UCCR/UCCR_deployRun.html). Resolve tasks by starting them and then changing their status to `Complete`, `Fail`, or `Skipped`. After all the tasks in a deployment plan are resolved, the deployment has a status of Done.

  * Tasks can be started when they are eligible to start. Eligibility is determined by the plan's execution pattern. By default, a plan's execution pattern is sequential. Initially, the first, or topmost, task is eligible to start. You can modify the execution pattern by grouping tasks together. A task group can have a parallel execution pattern, which means that the group's tasks can be started in any order. A deployment plan can have multiple groups and groups nested within other groups.

  * Some tasks, called auto tasks, start automatically as soon as they are eligible to run. UrbanCode Deploy type tasks, start as soon as they are eligible, without manual intervention. Auto tasks also update their status without manual intervention.  

## Installing and configuring DevOps Connect
{: #gs_install_dc}

IBM Bluemix DevOps Connect coordinates communication between your on-premises IBM UrbanCode Deploy installation and {{site.data.keyword.uccr_short}}. After you install DevOps Connect, you can create integrations that enable you to manage UrbanCode Deploy applications with {{site.data.keyword.uccr_short}} tasks.

**Prerequisites**

* To register DevOps Connect, you must have an IBMid.

* You must have [Java™ Runtime Environment version 7 or later](https://java.com/en/download/){:new_window} ![External link icon](../../icons/launch-glyph.svg "External link icon") on the host system and set the system PATH variable to its location.

* You need an admin authorization token from UrbanCode Deploy.   


1. Install DevOps Connect and use it to integrate {{site.data.keyword.uccr_short}} with UrbanCode Deploy.

  1.  In {{site.data.keyword.uccr_short}}, on the Getting Started page, click **Setup**.

  1.  In the UrbanCode Deploy Integration Setup dialog box, click **Download** to download DevOps Connect. Place the JAR file on a computer that has access to UrbanCode Deploy.

  1.  Using the dialog box, copy the DevOps Connect installation script. The script contains the command to start DevOps Connect and the credentials that are required to identify your {{site.data.keyword.uccr_short}} Bluemix service.

  1.  On the computer where you placed DevOps Connect, open a command shell and paste the copied script into it

  1.  Run the script.  DevOps Connect displays startup messages.

2. Register DevOps Connect.

  1.  Use a web browser to open the DevOps Connect dashboard. The default URL is `https://localhost:8443`. To change the URL and learn about other startup options, see the [DevOps Connect documentation](https://developer.ibm.com/urbancode/plugindoc/urbancode-sync/ibm-urbancode-sync-utility/1-2/){:new_window} ![External link icon](../../icons/launch-glyph.svg "External link icon")

  1.  On the registration page, specify a name for the DevOps Connect installation.

  1.  Click **Register**. The first time that you access DevOps Connect, you are prompted to register it with your IBMid.

  1.  On the **Sign-in to IBM** page, enter your IBMid and password, and then click **Sign In**. You sign in each time you start DevOps Connect.

3. With DevOps Connect, use the IBM UrbanCode Deploy for Cloud Reporting plug-in to create an integration between {{site.data.keyword.uccr_short}} and UrbanCode Deploy.

    1.  From the DevOps Connect dashboard, click **Integrations**, and then click **Add New**.

    1.  In the **Name** field, enter a name for the integration,

    1.  From the **Integration Type** list, select **IBM UrbanCode Deploy for Cloud Reporting**. The IBM UrbanCode Deploy for Cloud Reporting plug-in is included with DevOps Connect.

    1.  In the **Server URI** field, enter the public URL of the UrbanCode Deploy server. For example, `https://my_UCD.example.com:8447`.

    1.  In the **Authentication Token** field, enter or paste the authentication token that was generated by UrbanCode Deploy.

    1.  In the **Admin User Email** field, enter your email address.

    1.  Click **Save**.

4.  Run the integration to confirm that it works.

    1.  On the integration page, click **Run**. DevOps Connect connects to the UrbanCode Deploy instance specified in the **Server URI** field. DevOps Connect is authorized by the token that is pasted in the **Authentication Token** field.

    1.  In {{site.data.keyword.uccr_short}}, confirm that the integration is successful by creating an UrbanCode Deploy type task. If you can select an UrbanCode Deploy application, the integration is successful. The {{site.data.keyword.uccr_short}} instance uses the DevOps Connect login and startup parameters to identify the UrbanCode Deploy applications.  

# Related Links
{: #rellinks}

## Tutorials and Samples
{: #samples}

* [Sample deployment plan. You can import this CSV-type file into a deployment plan.](https://console.ng.bluemix.net/catalog/services/continuous-delivery/sample/SamplePlan.csv){:new_window} ![External link icon](../../icons/launch-glyph.svg "External link icon")

<!--

## SDK
{: #sdk}

## API Reference
{: #api}

## Compatible Runtimes
{: #buildpacks}

-->

## Related Links
{: #general}

* [{{site.data.keyword.uccr_short}} Bluemix service](https://console.ng.bluemix.net/catalog/services/continuous-release/){:new_window} ![External link icon](../../icons/launch-glyph.svg "External link icon")
* [Download DevOps Connect](https://developer.ibm.com/urbancode/plugin/ibm-urbancode-sync-plugin-example/){:new_window} ![External link icon](../../icons/launch-glyph.svg "External link icon")
* [DevOps Connect documentation](https://developer.ibm.com/urbancode/plugindoc/urbancode-sync/ibm-urbancode-sync-utility/1-2/){:new_window} ![External link icon](../../icons/launch-glyph.svg "External link icon")
* [Overview of DevOps Connect architecture](https://developer.ibm.com/urbancode/docs/overview-of-ibm-urbancode-cloud-security/){:new_window} ![External link icon](../../icons/launch-glyph.svg "External link icon")
* [Continuous Delivery Bluemix service](https://console.ng.bluemix.net/catalog/services/continuous-delivery/){:new_window} ![External link icon](../../icons/launch-glyph.svg "External link icon")
* [Continuous Delivery documentation](https://console.stage1.ng.bluemix.net/docs/services/ContinuousDelivery/index.html?pos=2){:new_window} ![External link icon](../../icons/launch-glyph.svg "External link icon")
