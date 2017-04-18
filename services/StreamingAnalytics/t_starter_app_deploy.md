---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Deploying the starter applications on {{site.data.keyword.Bluemix_short}}
{: #starterapps_deploy}

You can push and deploy one of the {{site.data.keyword.streaminganalyticsshort}} starter applications to the {{site.data.keyword.Bluemix_short}} cloud.
{:shortdesc}

Before you begin, get {{site.data.keyword.Bluemix_short}} ready to deploy the {{site.data.keyword.streaminganalyticsshort}} starter applications:

* [Install the cf command-line tool](https://github.com/cloudfoundry/cli/releases).
* Create an application in {{site.data.keyword.Bluemix_short}}, add the {{site.data.keyword.streaminganalyticsshort}} service to your application, and restage the application:
	* To deploy the Event Detection starter app, create an application with {{site.data.keyword.sdk4node}} runtime.
	* To deploy the NYC Traffic starter app, create an application with Liberty for Java™ runtime.

Remember the name that you give your application; you will need it later on.

{{site.data.keyword.streaminganalyticsshort}} provides two sample applications to get you started with the service.

The Event Detection starter application analyzes weather-related data in a real-time stream and displays the status and results of the analysis. The application is written in {{site.data.keyword.sdk4node}}. For more details on how to use the Event Detection starter app, see [Detect complex events in a real-time data stream](https://www.ibm.com/developerworks/library/ba-bluemix-detect-complex-events-from-data-stream-trs/index.html).

The NYC Traffic starter application reads and analyzes traffic data from a public website. The application is written in Liberty for Java™. For more details on how to use the NYC Traffic starter app, see [{{site.data.keyword.streaminganalyticsfull}} Starter Application](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-starter-application/).

To download and deploy the starter application to {{site.data.keyword.Bluemix_short}}:

1. Download the [Event Detection](https://hub.jazz.net/project/streamscloud/EventDetection/overview) or the [NYC Traffic](https://hub.jazz.net/project/streamscloud/NYCTraffic/overview) starter application.
2. On the command line, go to the project directory.
  <pre><code>cd myapp</code></pre>
  {:pre}

3. Rename the project directory to match the name you gave your application in {{site.data.keyword.Bluemix_short}}.
4. Connect to {{site.data.keyword.Bluemix_short}}:
  <pre><code>cf api https://api.DomainName</code></pre>
  {:pre}

5. Log in to {{site.data.keyword.Bluemix_short}} and set your target organization when prompted:
  <pre><code>cf login</code></pre>
  {:pre}

6. Deploy your application:
  <pre><code>cf push myapp</code></pre>
  {:pre}

7. Go to your application overview page, accessible from the {{site.data.keyword.Bluemix_short}} dashboard, to verify that your application started successfully.
8. Launch your application to see it in your browser. You can find your application's URL (or "route") on the application overview page.

Now that your app is running, you can go to the service dashboard to see the status of your {{site.data.keyword.streaminganalyticsshort}} instance and to get information for troubleshooting. To access the service dashboard, go to the {{site.data.keyword.Bluemix_short}} dashboard and click the {{site.data.keyword.streaminganalyticsshort}} tile on your application overview page.
