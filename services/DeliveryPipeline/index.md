{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

#Getting started with {{site.data.keyword.deliverypipeline}} {: #delivery-pipeline}  

*Last Updated: 21 January 2016*

To automate your builds and deployments to {{site.data.keyword.Bluemix}}, use the IBM Continuous {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}} (the {{site.data.keyword.deliverypipeline}} service).
{: shortdesc} 

As you develop an app in the cloud, you can choose from several build types. You provide the build script, and {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} runs it; you don't need to set up build systems. Then, with one click, you can automatically deploy your app to one or many {{site.data.keyword.Bluemix_notm}} spaces, public Cloud Foundry servers, or Docker containers on IBM Containers for {{site.data.keyword.Bluemix_notm}}.  

Build jobs compile and package your app source code from Git or Jazz source control management (SCM) repositories. The build jobs produce deployable artifacts, such as WAR files or Docker containers for IBM Containers. In addition, you can run unit tests within your build automatically. Each time the source code changes, a build is triggered.  

A deployment job takes output from a build job and deploys it to either IBM Containers or Cloud Foundry servers such as {{site.data.keyword.Bluemix_notm}}.  

You can deploy to one or many regions and services. For example, you can set up your {{site.data.keyword.deliverypipeline}} service so that development artifacts use IBM Containers, are tested in one region, and are deployed to production in multiple regions. For more information, see [Regions](../../overview/index.html#ov_intro__reg).

1. Log in to {{site.data.keyword.Bluemix_notm}} and select an organization and space for your app.
1. On the {{site.data.keyword.Bluemix_notm}} Dashboard, click **CREATE AN APP**.
1. Select a web or mobile app template, select a starter, and click **CONTINUE**. Name your app, and then click **FINISH**.  
1. On the Start Coding page, scroll down and click **VIEW APP OVERVIEW**.  
1. On the {{site.data.keyword.Bluemix_notm}} app Dashboard, create a Git-hosted project for the app by clicking **ADD GIT**. Make sure that the **Populate the repository with the starter app package and enable {{site.data.keyword.deliverypipeline}} (Build & Deploy)** check box is selected and then click **CONTINUE**.   
1. After your Git repository is created, click **CLOSE**. The ADD GIT link is replaced by an EDIT CODE link and your Git URL.  
1. Add the {{site.data.keyword.deliverypipeline}} service to the associated space or spaces. After you add this service, you can create a multi-stage deployment pipeline in your {{site.data.keyword.Bluemix_notm}} spaces by configuring and running stages that contain build, test, and deployment jobs.
    1. On the {{site.data.keyword.Bluemix_notm}} app Dashboard, click **ADD A SERVICE OR API**. For the category, select the **DevOps** check box, and from the catalog, click **Delivery Pipeline**.
    2. Select a plan and click **CREATE**. The {{site.data.keyword.deliverypipeline}} Dashboard opens showing the app that you created earlier.     
  
On the {{site.data.keyword.deliverypipeline}} Dashboard, you can see your 
{{site.data.keyword.jazzhub_short}} projects and the states that they are in. You can check the status of builds, the deployed app, and recent deployments, or see the most recent logs and deployment details.  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks">
<h2 class="topictitle2" id="d68e338">Related links</h2>
<aside>
<div class="linklist" id="general"><h3 class="linklistlabel">Related Links</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="(Opens in a new tab or window)">{{site.data.keyword.Bluemix_notm}} Prerequisites</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">Tutorials and Samples</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="(Opens in a new tab or window)">Clone, edit, and deploy an app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Node.js app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Java app</a></li>
<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/delivery%20pipeline%20service" rel="external" title="(Opens in a new tab or window)">developerWorks: {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.deliverypipeline}} service</a></li>
</ul>
</div>
</aside>
</article>
