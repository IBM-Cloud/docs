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

#Modifying the starter application to {{site.data.keyword.Bluemix_short}}
{: #modifying_starter_app}

You can modify the starter application and then redeploy it to {{site.data.keyword.Bluemix_short}} to see the results.
{:shortdesc}


A simple modification is to raise or remove the event limit in the starter application so that it runs longer.

1. Open app.js in a text editor or development environment.
2. Change the eventTarget variable, or delete this line to remove the event limit entirely.
	 <pre><code>var eventTarget = 100;</code></pre>
3. If you would like to remove the event limit, you also need to delete the following if statement:
	 <pre><code>  
	if (eventCount >= eventTarget) {
		    status_step[3] = "Completed";
		    console.log("\nTarget event count has been reached.  Geospatial Analytics service will be stopped.\n");
		    callback(null, null);
		    }
	</code></pre>
4. Redeploy your modified application to {{site.data.keyword.Bluemix_short}} with the cf push command.
	 <pre><code>  
	cf push myapp
	</code></pre>
5. Enter your application's URL or "route" into your browser or launch it from the {{site.data.keyword.Bluemix_short}} dashboard.
