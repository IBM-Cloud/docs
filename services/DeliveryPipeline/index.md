---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-10"

---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# Getting started with {{site.data.keyword.deliverypipeline}} Classic {: #delivery-pipeline}  

To automate your builds and deployments to {{site.data.keyword.Bluemix}}, use the IBM {{site.data.keyword.deliverypipeline}} Classic service for {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

With the {{site.data.keyword.deliverypipeline}} Classic service, you can choose from several build types. You provide the build script, and {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} runs it; you don't need to set up build systems. Then, with one click, you can automatically deploy your app to one or many {{site.data.keyword.Bluemix_notm}} spaces, public Cloud Foundry servers, or Docker containers on IBM Containers for {{site.data.keyword.Bluemix_notm}}.  

Build jobs compile and package your app source code from Git or Jazz source control management (SCM) repositories. The build jobs produce deployable artifacts, such as WAR files or Docker containers for IBM Containers. In addition, you can run unit tests within your build automatically. Each time the source code changes, a build is triggered.

A deployment job takes output from a build job and deploys it to either IBM Containers or Cloud Foundry servers such as {{site.data.keyword.Bluemix_notm}}.  

You can deploy to one or many regions and services. For example, you can set up your {{site.data.keyword.deliverypipeline}} Classic service so that development artifacts use IBM Containers, are tested in one region, and are deployed to production in multiple regions. For more information, see [Regions](/docs/overview/whatisbluemix.html#ov_intro_reg).

There are several ways to create a pipeline, including adding a pipeline to an existing application and creating a pipeline without an existing application. If you do not already have a {{site.data.keyword.deliverypipeline}} Classic service in your organization, you can go to the catalog, click {{site.data.keyword.deliverypipeline}} Classic, and click Create.

Complete these steps to set up a {{site.data.keyword.deliverypipeline}} Classic service for an existing application:    

1. On the {{site.data.keyword.Bluemix_notm}} app Dashboard, on the Overview tab, under **Continuous Delivery Classic**, create a Git-hosted project for the app by clicking **Add Git Repo And Pipeline** or **Add Git**, depending on the context.
1. Make sure that the **Populate the repo with the starter app package and enable the Build & Deploy pipeline** check box is selected and then click **CONTINUE**. You may need to verify your e-mail address to proceed.  
1. After your Git repository is created, click **CLOSE**. The Add Git button is replaced by an Edit Code button and your Git URL.  
1. To open the pipeline, click **Edit Code**, and then click **Build & Deploy**. To run the pipeline for the first time, push a change to the Git repository.

After you add this service, you can create a multi-stage deployment pipeline in your {{site.data.keyword.Bluemix_notm}} spaces by configuring and running stages that contain build, test, and deployment jobs. On the {{site.data.keyword.deliverypipeline}} Classic Dashboard, you can see your {{site.data.keyword.jazzhub_short}} projects and the states that they are in. You can check the status of builds, the deployed app, and recent deployments, or see the most recent logs and deployment details.  

1. After your Git repository is created, click **CLOSE**. The Add Git button is replaced by an Edit Code button and your Git URL.  
1. To open the pipeline, click **Edit Code**, and then click **Build & Deploy**. To run the pipeline for the first time, push a change to the Git repository.

After you add this service, you can create a multi-stage deployment pipeline in your {{site.data.keyword.Bluemix_notm}} spaces by configuring and running stages that contain build, test, and deployment jobs. On the {{site.data.keyword.deliverypipeline}} Dashboard, you can see your {{site.data.keyword.jazzhub_short}} projects and the states that they are in. You can check the status of builds, the deployed app, and recent deployments, or see the most recent logs and deployment details.  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks" role="article">
<h2 class="topictitle2" id="d68e338">Related links</h2>
<aside role="complementary" aria-labelledby="related_links">
<div class="linklist" id="general"><h3 class="linklistlabel" id="related_links">Related Links</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="(Opens in a new tab or window)">{{site.data.keyword.Bluemix_notm}} Prerequisites</a></li>
<li><img src="./sout.gif" alt=""><a href="https://www.ibm.com/devops/method/content/deliver/practice_delivery_pipeline/" rel="external" title="(Opens in a new tab or window)">IBM Bluemix Garage Method: Delivery pipeline</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">Tutorials and Samples</h3>
<ul>

<!--
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="(Opens in a new tab or window)">Clone, edit, and deploy an app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Node.js app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Java app</a></li>
-->

<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/delivery%20pipeline%20service" rel="external" title="(Opens in a new tab or window)">developerWorks: {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.deliverypipeline}} service</a></li>
</ul>
</div>
</aside>
</article>
