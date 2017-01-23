---

copyright:
  years: 2017
  last-updated: "2017-01-23"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Getting started with IBM Cloud Continuous Release (Experimental)

{: #gettingstartedtemplate}

The {{site.data.keyword.UCCR_full}} service on Bluemix is a comprehensive release management solution. With IBM Cloud Continuous Release, you can run deployments for all software applications in your development lifecycle.
{:shortdesc}

After you create an instance of IBM Cloud Continuous Release, choose how you want to get started.

* Begin with **[Creating a deployment plan and running a deployment](#gs_create_plan)** if you want to plunge in and start creating deployment plans.

* Begin with **[Installing and configuring DevOps Connect](#gs_install_dc)** if you want to integrate Continuous Release with your on-prem IBM UrbanCode Deploy instance. After you configure an integration, you can use Continuous Release tasks to manage UrbanCode Deploy applications.







## Creating a deployment plan and running a deployment
{: #gs_create_plan}

1. Create a deployment plan.

  * [Create a plan](/docs/UCCR/UCCR_deployPlan.html) and assign it to one of your teams. Any team member can run the tasks in the deployment plan. You can modify this behavior by assigning tasks to groups or specific team members.

  * [Add tasks to the deployment plan](/docs/UCCR/UCCR_tasks.html). Each task is listed on a separate row in the deployment plan. Try adding different types of tasks: manual, UrbanCode Deploy, delay, and note.

  * You can modify the list of tasks in the plan in various ways. You can reposition tasks, copy, and delete them.

4. When your deployment plan is ready, run a deployment by using the deployment plan that you created in the previous step.

  * [You run a deployment by resolving the tasks in a deployment plan](/docs/UCCR/UCCR_deployRun.html). Resolve tasks by starting them and then changing their status to Complete, Failed, or Skipped. After all the tasks in a deployment plan are resolved, the deployment has a status of Done.

  * Tasks can be started when they are eligible to start. Eligibility is determined by the plan's execution pattern. By default, a plan's execution pattern is sequential. Initially, the first, or topmost, task is eligible to start. You can modify the execution pattern by grouping tasks together. A task group can have a parallel execution pattern, which means that the group's tasks can be started in any order. A deployment plan can have multiple groups and groups nested within other groups.

  * Some tasks start automatically as soon as they are eligible to run. Automated tasks, such as UrbanCode Deploy type tasks, start as soon as they are eligible without manual intervention. Automated tasks also update their status without manual intervention.  

## Installing and configuring DevOps Connect
{: #gs_install_dc}

IBM® Bluemix® DevOps Connect coordinates communication between your on-prem IBM UrbanCode Deploy installation and DevOps Connect. After you install DevOps Connect, you can create integrations that enable you to manage IBM UrbanCode Deploy applications with Continuous Release tasks.

**Prerequisites**

* To register IBM Bluemix DevOps Connect, you must have an IBMid.

* You must have a Java™ Runtime Environment version 7 or later on the host system and set the system PATH variable to its location.

* You need an authorization token from IBM UrbanCode Deploy.   


1. Install IBM Bluemix DevOps Connect and use it to integrate Continuous Release with IBM UrbanCode Deploy. After you configure an integration, you can manage IBM UrbanCode Deploy applications with Continuous Release tasks.

  1.  In Continuous Release, copy the DevOps Connect installation script. The script contains the command to start DevOps Connect and the credentials that are required to identify Continuous Release.

  1.  Download IBM Bluemix DevOps Connect and place the JAR file on a computer that has access to IBM UrbanCode Deploy.

  1.  On the computer where you placed DevOps Connect, open a command window and paste the copied script into it

  1.  Run the script.  DevOps Connect displays startup messages.

2. With the DevOps Connect dashboard, register DevOps Connect.

  1.  Use a web browser to open the DevOps Connect dashboard. The default URL is `https://localhost:8443`. To change the URL and learn about other startup options, see the DevOps Connect documentation.

  1.  On the registration page, specify a name for the DevOps Connect installation.

  1.  Click **Register**. The first time that you access DevOps Connect, you are prompted to register it with your IBMid.

  1.  On the **Sign-in to IBM** page, enter your IBMid and password, and then click **Sign In**. You sign in each time you start DevOps Connect.

3. With DevOps Connect, use the IBM UrbanCode Deploy for Cloud Reporting plug-in to create an integration between Continuous Release and IBM UrbanCode Deploy.

    1.  From the DevOps Connect dashboard, click **Integrations**, and then click **Add New**.

    1.  In the **Name** field, enter a name for the integration,

    1.  From the **Integration Type** list, select **IBM UrbanCode Deploy for Cloud Reporting**. The IBM UrbanCode Deploy for Cloud Reporting plug-in is included with DevOps Connect.

    1.  In the **Server URI** field, enter the public URL of the IBM UrbanCode Deploy server. For example, `https://my_UCD.example.com:8447`.

    1.  In the **Authentication Token** field, enter or paste the authentication token that was generated by IBM UrbanCode Deploy.

    1.  In the **Admin User Email** field, enter your email addess.

    1.  Click **Save**.

4.  Run the integration to confirm that it works.

    1.  On the integration page, click **Run**. DevOps Connect connects to the IBM UrbanCode Deploy instance specified in the **Server URI** field. DevOps Connect is authorized by the token pasted in the **Authentication Token** field.

    1.  In Continuous Release, confirm that the integration is successful by creating an UrbanCode Deploy type task. If you can select an IBM UrbanCode Deploy application, the integration is successful. The Continuous Release instance uses the DevOps Connect login and startup parameters to identify the UrbanCode Deploy applications.  

<!-- Related links section: REQUIRED.
Related links display in the upper right of the getting started page.
Ensure that you retain the lowercase anchor IDs (eg. {: #rellinks}) as shown in this template. These are used as IDs during transform and the doc framework keys off the IDs for display.
The headings coded here are not actually used. The doc framework provides the correct headings.
Also ensure that the related links stay in position at the end of this file or the doc framework will not display them properly.
Use {:new_window} for external links to open a new window.-->
<!-- Please delete all comments within the related links section to avoid breaking the build. Thanks. -->

# Related Links
{: #rellinks}

## Tutorials and Samples
{: #samples}
<!-- Recommended external links to your top three devWorks articles and sample applications. 	Link text should be: <sample_name> sample or developerworks: <article_name>. To confirm the available articles for your service, go to http://www.ibm.com/developerworks/views/global/libraryview.jsp?show_abstract=falsecontentarea_by=All+Zonesproduct_by=-1topic_by=BlueMixindustry_by=-1type_by=All+Typesibm-search=Search and select your service from the product drop-down menu -->
* [link text](URL){:new_window}

## SDK
{: #sdk}
<!-- Links to SDK download and SDK Developer Guide -->
* [link text](URL){:new_window}

## API Reference
{: #api}
<!-- External links to the landing page of each generated doc for the APIs that are supported by your service. Use only the type of API as the link text (Java, JavaScript, REST, Objective-C) -->
* [link text](URL){:new_window}

## Compatible Runtimes
{: #buildpacks}
<!-- MAY BE REMOVING THIS: Peer links to the Getting Started page of each runtime that is supported by your service. Use only the name of the runtime as the link text (Node.js, Liberty for Java, Ruby on Rails, Ruby Sinatra) -->
* [link text](URL)

## Related Links
{: #general}
<!-- Include a link to your full product documentation, pricing sheet, IBM Bluemix prerequisites -->
<!-- NOTE: Remove these comments when using this template. Otherwise the comment will break the build! Thanks. -->
* [link text](URL){:new_window}
* [link text](URL)
* [link text](URL)
