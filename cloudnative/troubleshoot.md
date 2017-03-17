---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Troubleshooting
{: #ts}

Some known issues with the {{site.data.keyword.dev_cli_notm}} are documented, along with their workarounds.
{:shortdesc}

<!-- Add a headings and paragraphs about troubleshooting for your service, or a list of known issues and workarounds. -->

## Known issues
{: #knownissues}

The following sections describe known issues and possible resolutions.


### Service broker error while adding {{site.data.keyword.objectstorageshort}} capability
{: #os}

You might see the following error if you use the {{site.data.keyword.dev_cli_short}} to create two projects with the {{site.data.keyword.objectstorageshort}} capability:

```
FAILED
Service broker error: {"description"=>"You can not create this Object Storage instance. Each organization using the Object Storage service is limited to one instance of the Free plan."}
```
{: codeblock}


#### Cause
{: #os-cause}
   
This error is due to the {{site.data.keyword.objectstorageshort}} service allowing only one instance of the Free {{site.data.keyword.objectstorageshort}} plan.


#### Resolution
{: #os-resolution}

You will be prompted to choose a different plan to avoid this error.


### Failure getting the code during project creation
{: #code}

You might see the following error if you use the {{site.data.keyword.dev_cli_short}} to create a project:
	
```
FAILED                            
Project created, but could not get code
https://console.ng.bluemix.net/developer/projects/b22165f3-cbc6-4f73-876f-e33cbec199d4/code
```
{: codeblock}
	

#### Cause
{: #code-cause}

This error is due to an internal timeout.
	

#### Resolution
{: #code-resolution}

You can get the code either of the following ways:

* Run the following command using the CLI:

	```
	bx dev code <your-project-name>
	```
	{: codeblock}
	
	`<your-project-name>` should be replaced with the project name that you used during project creation.

* Use the {{site.data.keyword.dev_console}}.

	1. Select your [project ![External link icon](../icons/launch-glyph.svg "External link icon")](../../developer/projects) in the {{site.data.keyword.dev_console}} and click **Get the Code**.

	2. Click **Generate Code**.

	3. After the code is generated, click **Download Code**.


### Error running `bx dev run` for Node.js projects
{: #node}

You might see the following error if you are running `bx dev run` with the {{site.data.keyword.dev_cli_short}} for Node.js Web or BFF projects:

```
module.js:597
  return process.dlopen(module, path._makeLong(filename));
                 ^

Error: /app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/appmetrics.node: invalid ELF header
    at Error (native)
    at Object.Module._extensions..node (module.js:597:18)
    at Module.load (module.js:487:32)
    at tryModuleLoad (module.js:446:12)

    at Function.Module._load (module.js:438:3)
    at Module.require (module.js:497:17)
    at require (internal/module.js:20:19)
    at Object.<anonymous> (/app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/index.js:25:13)
    at Module._compile (module.js:570:32)
    at Object.Module._extensions..js (module.js:579:10)
```
{: codeblock}


#### Cause
{: #node-cause}
   
This error is due to the `appmetrics` module being installed in a different architecture. Native npm modules installed on one architecture will not work on another. The included Docker images are based on the Linux kernel.


#### Resolution
{: #node-resolution}

Delete `node_modules` folder and run `bx dev run` again.


<!--
## Troubleshooting techniques
{: #tstechniques}
-->

<!-- Add a heading and content for how to get help and support. Use this template for beta and GA services:  -->


## Getting help and support
{: #gettinghelp}

If you have problems or questions when using the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} or the {{site.data.keyword.dev_cli_notm}}, you can get help by searching for information or by asking questions through a forum. You can also open a support ticket.

When using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.Bluemix_notm}} development teams.

<!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->

If you have technical questions about developing or deploying an app with the {{site.data.keyword.dev_console}} or the {{site.data.keyword.dev_cli_notm}}:

* Post your question on [Stack Overflow ![External link icon](../icons/launch-glyph.svg "External link icon")](http://stackoverflow.com/search?q=bluemix-dev-services+ibm-bluemix) and tag your question with `bluemix-dev-services` and `ibm-bluemix`.
* Post your question on [Slack ![External link icon](../icons/launch-glyph.svg "External link icon")](http://dwopen.slack.com/) in the `bluemix-dev-services` channel.


<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
<!--
* For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers ![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/topics/bluemix-dev-services/?smartspace=bluemix) forum. Include the  "bluemix-dev-services" and "bluemix" tags.
* -->

See [Getting help ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/support/index.html#getting-help) for more details about using the forums.

For information about opening an {{site.data.keyword.IBM}} support ticket, or about support levels and ticket severities, see [Contacting support ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/support/index.html#contacting-support).

<!--Add a heading and content for how to get help. (Support not available for experimental.) Use this template for experimental services:  -->

