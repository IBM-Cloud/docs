{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Getting started with the {{site.data.keyword.trackplan}} service {: #track-plan}  

*Last Updated: 21 January 2016*

To view, edit, and plan tasks, use {{site.data.keyword.trackplanlong}} (the {{site.data.keyword.trackplan}} service). You can track your work and your team's work, create defects, see what's incoming, maintain your backlog, and plan work for future sprints.
{: shortdesc}

The {{site.data.keyword.trackplan}} service links plans and code so that plans stay in sync with the development team's progress. With the service, you can create stories, tasks, and defects to describe and track project work. You can also plan and manage the product backlog, releases, and sprints.

1. Log in to 
{{site.data.keyword.Bluemix_notm}} and select an organization and space for your app.
1. On the {{site.data.keyword.Bluemix_notm}} Dashboard, click **CREATE AN APP**.
1. Select a web or mobile app template, select a starter, and click **CONTINUE**. Name your app, and then click **FINISH**.
1. On the Start Coding page, scroll down and click **VIEW APP OVERVIEW**.
1. On the {{site.data.keyword.Bluemix_notm}} app Dashboard, create a Git-hosted project for the app by clicking **ADD GIT**. Make sure that the **Populate the repository with the starter app package and enable Delivery Pipeline (Build & Deploy)** check box is selected and then click **CONTINUE**. After your Git repository is created, click **CLOSE**. The ADD GIT link is replaced by an EDIT CODE link and your Git URL.
1. Add the {{site.data.keyword.trackplan}} service to the space so that you can manage your team's work.
    1. On the {{site.data.keyword.Bluemix_notm}} app Dashboard, click **ADD A SERVICE OR API**. For the category, select **DevOps**, and from the catalog, click **Track & Plan**.
    2. On the {{site.data.keyword.trackplan}} page, select a plan and click **CREATE**.    
1. In the list of apps, in the State column, change the state for the {{site.data.keyword.trackplan}} service by clicking the current state, which in this case is **OFF**. The Project Settings page opens in {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}}.
    1. Select the option to enable the {{site.data.keyword.trackplan}} service. If necessary, update your region, organization, or space
    2. Click **SAVE**.  
1. Return to the {{site.data.keyword.Bluemix_notm}} Dashboard and click the {{site.data.keyword.trackplan}} service tile. The state for the {{site.data.keyword.trackplan}} service is changed to **ON** for your app.
1. In the list of apps, in the Work Item column, click **CREATE** to begin using the {{site.data.keyword.trackplan}} service.  

On the {{site.data.keyword.Bluemix_notm}} Dashboard, you can see your {{site.data.keyword.jazzhub_short}} projects and their member counts, visibility, and whether they have the {{site.data.keyword.trackplan}} service enabled. You can create work items for any of your {{site.data.keyword.jazzhub_short}} projects or go to your planning tools.  

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
<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/track%20and%20plan%20service" rel="external" title="(Opens in a new tab or window)">developerWorks: {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.trackplan}} service</a></li>
</ul>
</div>
</aside>
</article>
