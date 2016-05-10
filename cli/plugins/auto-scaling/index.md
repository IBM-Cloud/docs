---

 

copyright:

  years: 2016

 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Auto-Scaling CLI
{: #autoscalingcli}

*Last updated: 25 February 2016*

You can configure the {{site.data.keyword.autoscaling}} service by using the {{site.data.keyword.autoscaling}} CLI for {{site.data.keyword.Bluemix_notm}}. The {{site.data.keyword.autoscaling}} CLI supports Linux64, Win64, and OSX, and provides functionality that is similar to the auto-scaling RESTful API provides.
{: shortdesc}

Before you begin, install the {{site.data.keyword.Bluemix_notm}} CLI. See [Download {{site.data.keyword.Bluemix_notm}} CLI](http://plugins.{DomainName}/ui/home.html){: new_window} for instructions.

## Adding the {{site.data.keyword.Bluemix_notm}} CLI plug-in

After the {{site.data.keyword.Bluemix_notm}} CLI is installed, you can add the {{site.data.keyword.autoscaling}} CLI plug-in.

Complete the following steps to add the repository and install the plug-in:
1. To add the {{site.data.keyword.Bluemix_notm}} CLI plugin repository, run the following command:
```
bluemix plugin repo-add bluemix-plugin-repo https://plugins.ng.bluemix.net
```
2. To install the {{site.data.keyword.autoscaling}} CLI plugin, run the following command:
```
bluemix plugin install auto-scaling -r bluemix-plugin-repo
```

## Attaching an auto-scaling policy

You can attach an auto-scaling policy to a specific app. Run the following command:

```bx as policy-attach <APP_NAME> -p <policy_file>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">The name of the app to which you want to attach an auto-scaling policy.</dd>
<dt class="pt dlterm">&lt;policy_file&gt;</dt>
<dd class="pd">The name of the JSON file that describes the auto-scaling policy. See the <a href="https://new-console.{DomainName}/apidocs/48" target="_blank">{{site.data.keyword.autoscaling}} RESTful API doc</a> for more details.</dd>
</dl>


## Generating an auto-scaling policy

You can generate an auto-scaling policy by answering the questions on the command line interface. Depending on your input, a JSON file that contains the definition of the auto-scaling policy is saved with the name that you enter. If you do not enter  the file name, the policy content is printed to the command line directly without saving it to a file. Run the following command:

```bx as policy-create```
{: codeblock}


## Displaying an auto-scaling policy

You can show the auto-scaling policy of an app. The content of the policy is printed to the command line directly. Run the following command:

```bx as policy-show <APP_NAME> [--json]```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">The name of the app for which you want to show the auto-scaling policy. By default, the JSON structure is translated into a series of human readable output.</dd>
</dl>

**Tip:** You can also use the **--json** option to pretty print the original JSON response.


## Detaching an auto-scaling policy

You can remove an auto-scaling policy from an  app. Run the following command:

```bx as policy-detach <APP_NAME>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">The name of the app for which you want to detach the auto-scaling policy.</dd>
</dl>


## Enabling or disabling an auto-scaling policy

You can enable or disable the auto-scaling policy of a specific  app. Run the following command:

```bx as policy-enable|policy-disable <APP_NAME>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">The name of the app for which you want to enable or disable the auto-scaling policy.</dd>
</dl>


## Displaying auto-scaling history of an app

You can show the history of the auto-scaling activity of a specific app. A table of auto-scaling history records is displayed in the command line interface.

```bx as history-show <APP_NAME>  [--start-date=<start_timestamp>]  [--end-date=<end_timestamp>]  [--json]```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">The name of the app for which you want to show the history of the auto-scaling policy.
<dt class="pt dlterm">&lt;start_timestamp&gt;</dt>
<dd class="pd">The time stamp of the beginning of the history range. The supported formats are `yyyy-MM-ddTHH:mm:ss+/-hhmm, yyyy-MM-ddTHH:mm:ssZ`. By default, the time stamp is set to 50 hours ahead of the current time. See the <a href="https://www.w3.org/TR/NOTE-datetime" target="_blank">W3C Date and Time Formats standard</a> for details about the time stamp format. 
<dt class="pt dlterm">&lt;end_timestamp&gt;</dt>
<dd class="pd">The time stamp of the ending of the history range. The supported formats are `yyyy-MM-ddTHH:mm:ss+/-hhmm, yyyy-MM-ddTHH:mm:ssZ`. By default, the time stamp is set to the current time. See the <a href="https://www.w3.org/TR/NOTE-datetime" target="_blank">W3C Date and Time Formats standard</a> for details about the time stamp format. 
</dl>

**Tip:** You can also use the **--json** option to pretty print the original JSON response.

# rellinks
{: #rellinks}
## general
{: #general}
* [{{site.data.keyword.autoscaling}} service](../../../services/Auto-Scaling/index.html)
* [{{site.data.keyword.Bluemix_notm}} CLI](http://plugins.{DomainName}/ui/home.html){: new_window}
* [W3C Date and Time Formats standard](https://www.w3.org/TR/NOTE-datetime){: new_window}


