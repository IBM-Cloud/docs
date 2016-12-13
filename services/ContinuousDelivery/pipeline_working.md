---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-18"

---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# Working with {{site.data.keyword.deliverypipeline}} {: #pipeline-working}  

To automate your builds and deployments to {{site.data.keyword.Bluemix}}, use {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

With {{site.data.keyword.deliverypipeline}}, you can choose from several build types. You provide the build script, and {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} runs it; you don't need to set up build systems. Then, with one click, you can automatically deploy your app to one or many {{site.data.keyword.Bluemix_notm}} spaces, public Cloud Foundry servers, or Docker containers on IBM Containers for {{site.data.keyword.Bluemix_notm}}.  

Build jobs compile and package your app source code from Git repositories. The build jobs produce deployable artifacts, such as WAR files or Docker containers for IBM Containers. In addition, you can run unit tests within your build automatically. You can set up your build jobs so that each time a commit is pushed, a build is triggered.

A deployment job takes output from a build job and deploys it to either IBM Containers or Cloud Foundry servers such as {{site.data.keyword.Bluemix_notm}}.  

You can deploy to one or many regions and services. For example, you can set up your {{site.data.keyword.deliverypipeline}} to use one or more services, test in one region, and deploy to production in multiple regions. For more information, see [Regions](/docs/overview/whatisbluemix.html#ov_intro_reg){: new_window} ![New window icon](images/launch--glyph.svg).

There are several ways to create a pipeline, including adding a pipeline to an existing application and creating a pipeline without an existing application. If you do not already have a {{site.data.keyword.deliverypipeline}} service in your organization, you can go to the catalog, click {{site.data.keyword.deliverypipeline}}, and click Create.

Complete these steps to set up a {{site.data.keyword.deliverypipeline}} for an existing application:    

1. On the {{site.data.keyword.Bluemix_notm}} app Dashboard, click your app.
1. From the hamburger menu on the {{site.data.keyword.Bluemix_notm}} menu bar, click **Services**, and then click **DevOps**.
1. Click **Pipelines**, and then click **Create a Pipeline**.

To [create a pipeline](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} ![New window icon](images/launch--glyph.svg) that is configured to deploy a Cloud Foundry application, follow these steps:    

1. Click **Cloud Foundry**.  
1. If you want to use a different name for the pipeline, change its default name. 
1. If you want to use a different name for the application, change its default name. This name is the application that the pipeline deploys to. 
1. If you don't have a toolchain, a toolchain with a default name is created for you. If you want to use a different name for the toolchain, change its name. With the toolchain, you can extend the capabilities of your pipeline by integrating with other tools and services.

 **Tip**: Pipelines and toolchains belong to organizations (orgs). If you belong to an org that has toolchains, you can use those toolchains even if you didn't create them.
 
1. Either select the toolchain that you want to use or type a name for the new toolchain that you want to create.
1. Provide the location of your GitHub repo.

 **Tip**: If you have not authorized {{site.data.keyword.Bluemix_notm}} to access GitHub, you are prompted to click **Authorize** to go to the GitHub website. If you don't have an active GitHub session, you are prompted to log in. Click **Authorize Application** to allow {{site.data.keyword.Bluemix_notm}} to access your GitHub account. If you have an active GitHub session but you haven't entered your password recently, you might be prompted to enter your GitHub password to confirm.

   * If you have a GitHub repo and want to use it, for the repository type, select **Link**. Search for the location of the repo or select the repo from the list of available repos.
   
   * If you want to create an empty GitHub repo, for the repository type, select **New**. Type a name for the repo.
   
   * If you want to create a clone of a GitHub repo, for the repository type, select **Copy**. Search for the location of the repo or select the repo from the list of available repos.
   
   * If you want to fork a GitHub repo so that you can contribute changes through pull requests, select **Fork**. Search for the location of the repo or select the repo from the list of available repos.
 
1. Click **Create**. The pipeline is created, configured, and displayed on the toolchain's Overview page. 
 ![Pipeline card](images/cd_pipeline.png)

To create an [empty pipeline](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} ![New window icon](images/launch--glyph.svg) without any preconfigured stages:

1. Click **Custom**.
1. If you want to use a different name for the pipeline, change its default name. 
1. If you don't have a toolchain, a toolchain with a default name is created for you. If you want to use a different name for the toolchain, change its name. With the toolchain, you can extend the capabilities of your pipeline by integrating with other tools and services.
1. Either select the toolchain that you want to use or type a name for the new toolchain that you want to create.
1. Click **Create**. An empty pipeline is created and represented as a card on the toolchain's Overview page.

From your {{site.data.keyword.deliverypipeline}}, change your configuration; check the status of builds, the deployed app, and recent deployments; see the most recent logs and deployment details; or delete your pipeline.  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks" role="article">
<h2 class="topictitle2" id="d68e338">Related links</h2>
<aside role="complementary" aria-labelledby="related_links">
<div class="linklist" id="general"><h3 class="linklistlabel" id="related_links">Related Links</h3>
<ul>
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
