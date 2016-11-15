---



copyright:

  years: 2015, 2016



---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# Working with {{site.data.keyword.deliverypipeline}}s {: #pipeline-working}  

Last Updated: 15 November 2016
{: .last-updated}

To automate your builds and deployments to {{site.data.keyword.Bluemix}}, use {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

With {{site.data.keyword.deliverypipeline}}, you can choose from several build types. You provide the build script, and {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} runs it; you don't need to set up build systems. Then, with one click, you can automatically deploy your app to one or many {{site.data.keyword.Bluemix_notm}} spaces, public Cloud Foundry servers, or Docker containers on IBM Containers for {{site.data.keyword.Bluemix_notm}}.  

Build jobs compile and package your app source code from Git or Jazz source control management (SCM) repositories. The build jobs produce deployable artifacts, such as WAR files or Docker containers for IBM Containers. In addition, you can run unit tests within your build automatically. Each time the source code changes, a build is triggered.

A deployment job takes output from a build job and deploys it to either IBM Containers or Cloud Foundry servers such as {{site.data.keyword.Bluemix_notm}}.  

You can deploy to one or many regions and services. For example, you can set up your {{site.data.keyword.deliverypipeline}} service so that development artifacts use IBM Containers, are tested in one region, and are deployed to production in multiple regions. For more information, see [Regions](/docs/overview/whatisbluemix.html#ov_intro_reg).

There are several ways to create a pipeline, including adding a pipeline to an existing application and creating a pipeline without an existing application. If you do not already have a {{site.data.keyword.deliverypipeline}} service in your organization, you can go to the catalog, click {{site.data.keyword.deliverypipeline}}, and click Create.

Complete these steps to set up a {{site.data.keyword.deliverypipeline}} for an existing application:    

1. On the {{site.data.keyword.Bluemix_notm}} app Dashboard, click your app.
1. From the hamburger menu, click **Services**, and then click **DevOps**.
1. Click **Pipelines**, and then click **Create a Pipeline**.

If you want to create a pipeline that is configured to deploy a Cloud Foundry application:    

1. Select **Cloud Foundry**.  
1. The pipeline's name identifies it in {{site.data.keyword.Bluemix_notm}}. If you want to use a different name, change the pipeline's default name.
1. The app's name identifies it in Bluemix. If you want to use a different name, change the app's default name.
1. If you don't have any existing toolchains, we'll create a toolchain for you. The toolchain will allow you to extend the capabilities of your pipeline by integrating with other tools and services. A default toolchain name is provided. If you want to use a different name, change the toolchain's name.
1. If you already have toolchains, select the toolchain that you want to use, or enter a name for the new toolchain that you want to create.
1. Provide the location of your GitHub repo:

  a. If you already have a GitHub repo and want to use it, for the repository type, select **Link**. Search for the location of the repo or select the repo from the list of available repos.
 
  b. If you want to create an empty GitHub repo, for the repository type, select **New**. Type a name for the repo.
 
  c. If you want to create a copy of a GitHub repo, for the repository type, select **Copy**. Search for the location of the repo or select the repo from the list of available repos.
 
  d. If you want to fork a GitHub repo so that you can contribute changes through pull requests, select **Fork**. Search for the location of the repo or select the repo from the list of available repos.
 
1. Click **Create**. The pipeline is created, configured, and represented as a tile on the Toolchain's Overview page. 
 ![Pipeline tile](images/cd_pipeline.png)

If you want to create an empty pipeline without any pre-configured stages:

 1. Select **Custom**.
 1. The pipeline's name identifies it in {{site.data.keyword.Bluemix_notm}}. If you want to use a different name, change the pipeline's default name.
 1. If you don't have any existing toolchains, we'll create a toolchain for you. The toolchain will allow you to extend the capabilities of your pipeline by integrating with other tools and services. A default toolchain name is provided. If you want to use a different name, change the toolchain's name.
 1. If you already have toolchains, select the toolchain that you want to use, or enter a name for the new toolchain that you want to create.
 1. Click **Create**. An empty pipeline is created and represented as a tile on the Toolchain's Overview page. 

From your {{site.data.keyword.deliverypipeline}} tile, change your configuration; check the status of builds, the deployed app, and recent deployments; see the most recent logs and deployment details; or delete your pipeline.  

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
