---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Using Dynatrace
{: #using_dynatrace}

*Last Updated: 29 April 2016*

Dynatrace is a third-party service that provides monitoring for your app.

For more information about what the Dynatrace service provides, see [Dynatrace Application Monitoring](http://www.dynatrace.com/en/products/application-monitoring.html).

When your Liberty application is configured to use Dynatrace, the default behavior is the
Liberty runtime will acquire a Dynatrace agent jar file from a Dynatrace site and run
that Dynatrace agent with your app.  With that default behavior the minimal necessary
configuration to use Dynatrace is to create a user-provided service that points to
your Dynatrace collector.

## Creating a user-provided service that points to your Dynatrace collector

First, you'll need to set up a Dynatrace collector.  Then you must create a user-provided
service to pass information for the Dynatrace agent to connect with the Dynatrace collector. See [Dynatrace Architecture](https://community.dynatrace.com/community/display/DOCDT63/Architecture) to better understand the relationship between Dynatrace components.

<ol>
<li>Set up a Dynatrace collector.
  <ul>
  <li>See the [Dynatrace community website](https://community.dynatrace.com/community/display/EVAL/Step+3+-+Connect+Agent+to+Dynatrace) for instructions on downloading and setting up the Dynatrace collector.
  </li>
  <li>Ensure that the collector is set up in a location that is accessible to the Dynatrace agent running with your app in Bluemix.
  </li>
  </ul>
</li>
<li>Create a user-provided service that points to the running Dynatrace collector. <b>NOTE</b> The name of the user-provided service must contain <b>dynatrace</b>.  For example, use the command that follows:

  <pre>
  $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring"}'
  </pre>
  {: codeblock}

In this example, my-dynatrace-collector is the name given to the service, DynatraceCollectorIPaddress is the IP address of the Dynatrace collector you have configured, and profile is the optional Dynatrace profile name associated with this monitored app. The default profile value is Monitoring. You can specify optional parameters as in the example that follows.

  <pre>
  $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring",
                                        "options" : {"dynatrace-parameter-1": "value",
                                                     "dynatrace-parameter-2": "value"}}'
  </pre>
  {: codeblock}

See [Agent Setting section of Agent Configuration](https://community.dynatrace.com/community/display/DOCDT62/Agent+Configuration) at the Dynatrace community website for more information about available options. For example, using the exclude option, you can exclude classes from being monitored by Dynatrace. See [DynaTrace Agent Framework](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/framework-dynatrace-agent.md) for more details about configuring the user-provided service.
</li>
<li>After you have pushed your app to Bluemix, bind the user-provided service that you created to the app. For example, use the command

  <pre>
  $ cf bs myApp my-dynatrace-collector
  </pre>  
  {: codeblock}

**Note**: You must restage your application after binding the service.
</li>
</ol>

## Optional Configuration
{: #optional_configuration}

You may choose to acquire and host the Dynatrace agent jar file yourself.  In that case the following
additional configuration steps are needed.
1. Acquire and host the Dynatrace agent jar file so that the Liberty buildpack can download it.
2. Configure your Liberty app so that it can download the Dynatrace agent.

### Hosting the Dynatrace agent
{: #hosting_dynatrace_agent}
The Dynatrace agent must be hosted on a web server, and the Liberty buildpack must be able to download the agent jar from that server. The server must be configured with an index.yml file that specifies details about the agent jar. Complete the steps that follow to set up the Dynatrace agent:
  1. Download the Dynatrace agent jar. See [Dynatrace Server Platform Installers](https://community.dynatrace.com/community/display/EVAL/Step+1+-+Download+and+install+Dynatrace) at the Dynatrace community website for instructions on downloading the Dynatrace agent jar. The appropriate agent jar file for running on Bluemix is the **dynatrace-agent-unix.jar** version **6.+**.
  2. Host the agent jar file in a location from which the Liberty buildpack can download it. You can host it on Bluemix itself using any of the available server facilities, or you can host it on some publicly available location.
     * Ensure that you provide a index.yml file at the hosting location. The index.yml file must contain an entry consisting of the version ID of the agent jar follow by a colon and the complete URL of the location of that agent jar. For example:
```
      ---
      6.3.0: https://my-dynatrace-agent.mybluemix.net/dynatrace-agent-6.3.0-unix.jar
```  
{: codeblock}
     * The **dynatrace-agent-6.3.0-unix.jar** file must be available at the location specified in the index.yml file. The location for both the jar file and the index.yml can be the same directory.

### Configuring the Liberty app
{: #configuring_liberty_app}

The Liberty app you want to monitor must be configured to locate the server hosting the agent jar you previously set up. You can configure the app with the **JBP_CONFIG_DYNATRACEAGENT** environment variable. The **JBP_CONFIG_DYNATRACEAGENT** environment variable tells the buildpack where to download the Dynatrace agent from. To set the environment variable, complete these steps:
<ol>
   <li> Set the variable **JBP_CONFIG_DYNATRACEAGENT** so it has the value
   *"repository_root: URL_of_server_hosting_index.yml"*. For example, after pushing your application issue the following command:
  
  <pre>   
    $ cf se myApp JBP_CONFIG_DYNATRACEAGENT 'repository_root: https://my-dynatrace-agent-host.mybluemix.net'
  </pre>
  {: codeblock}

  In this example, *my-dynatrace-agent-host.mybluemix.net* is the URL of the index.yml file hosted by the server that you previously configured.
  </li>
  <li> After you set the environment variable, restage your app. The staging_task.log for your Liberty app issues a message indicating successful download of the Dynatrace agent from your agent hosting server. For example:

  <pre>
    Downloading dynatrace-agent-6.3.0-unix.jar 6.3.0 from https://my-dynatrace-agent-host.mybluemix.net/dynatrace-agent-6.3.0-unix.jar (17.8s)
  </pre>
  {: codeblock}

</li>
<li>To see the staging_task.log, issue the following command:

  <pre>
    $ cf files myAppName logs/staging_task.log
  </pre>  
  {: codeblock}

</li>
</ol>

# rellinks
## general
* [Liberty runtime](index.html)
* [Liberty Profile Overview](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
