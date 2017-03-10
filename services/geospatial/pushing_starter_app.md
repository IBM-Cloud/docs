---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-09"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Pushing the starter application to {{site.data.keyword.Bluemix_short}}
{: #pushing_starter_app}



Deploy the starter application and quickly learn how to use the {{site.data.keyword.geospatialshort_Geospatial}} service:
{:shortdesc}

1. If you haven't already, [install the cf command-line tool](docs/starters/install_cli.html).
2. [Get the code](https://hub.jazz.net/project/streamscloud/geo-starter/overview) of the {{site.data.keyword.geospatialshort_Geospatial}} starter app.
3. Rename the directory that contains the application files to match the name you gave your application in {{site.data.keyword.Bluemix_short}}. For example, if your application is named myapp, rename the directory to myapp.
4. On the command line, change to the renamed directory.
<pre><code>cd myapp</code></pre>
5. Connect to {{site.data.keyword.Bluemix_short}}:
<pre><code>cf api https://api.DomainName</code></pre>
6. Log in to {{site.data.keyword.Bluemix_short}} and set your target organization when prompted and deploy your application.
<pre><code>
cf login
cf push myapp
</code></pre>

##What to do next
{: #next notoc}

* Go to your application overview page, accessible from the {{site.data.keyword.Bluemix_short}} dashboard, to verify that your application started successfully.
* Launch your application to see it in your browser. You can find your application's URL (or "route") on the application overview page. The web page for the sample application displays information about the status of the REST API calls in the application code and the events {{site.data.keyword.geospatialshort_Geospatial}} detects.
