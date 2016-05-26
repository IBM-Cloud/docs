---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:prereq: .prereq}
{:download: .download}
{:pre: .pre}
{:app_name: data-hd-keyref="app_name"}
{:app_key: data-hd-keyref="app_key"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:host: data-hd-keyref="host"}
{:org_name: data-hd-keyref="org_name"}
{:route: data-hd-keyref="route"}
{:space_name: data-hd-keyref="space_name"}
{:service_name: data-hd-keyref="service_name"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:user_ID: data-hd-keyref="user_ID"}

# Deploying your app with the command line interface
*Last updated: 24 February 2016*

You can use the command line interface to deploy and modify applications and service instances.
{:shortdesc}

Before you begin, install the Cloud Foundry and {{site.data.keyword.Bluemix}} command line interfaces.

<p>
<a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(Opens in a new tab or window)"><img class="image" src="images/btn_cf_commandline.svg" alt="Download Cloud Foundry command line interface" /> </a>  <a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="(Opens in a new tab or window)"><img class="image" src="images/btn_bx_commandline.svg" alt="Download {{site.data.keyword.Bluemix}} command line interface" /> </a>
</p>

**Restriction:** The command line tools are not supported by Cygwin. Use the tools in a command line window other than the Cygwin command line window.
{:prereq}

After the command line interfaces are installed, you can get started:

  1. {: download} Download your starter code. 
      
    <a class="xref" href="http://bluemix.net" target="_blank" title="(Opens in a new tab or window)"><img class="image" src="images/btn_starter-code.svg" alt="Download starter code" /> </a>
  
  2. Extract the package to a new directory to set up your development environment.
  3. Change to your new directory.
  
  <pre class="pre">cd <var class="keyword varname">your_new_directory</var></pre>
  
   4.  Make changes to your app code as you see fit. We suggest making sure the app runs locally before you deploy it back to {{site.data.keyword.Bluemix}}.<br><br>One file you should take note of is the `manifest.yml` file. When deploying your app back to {{site.data.keyword.Bluemix}}, this file is used to determine your application’s URL, memory allocation, number of instances, and other crucial parameters. You can [read more about the manifest file](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){: new_window} in the Cloud Foundry documentation.
  
  5. Connect to {{site.data.keyword.Bluemix}}.
  
  <pre class="pre">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></pre>
  
  6. Log in to {{site.data.keyword.Bluemix_notm}}.
 
  <pre class="pre">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></pre>
  
  7. Deploy your app to {{site.data.keyword.Bluemix_notm}}. For more information about cf push command, see [Uploading your application](./upload_app.html).
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var></pre>
  
  8. Access your app by entering the following URL into your browser:
  
  <pre class="codeblock"><code><var class="keyword varname" data-hd-keyref="host">host</var>.<span class="keyword" data-hd-keyref="APPDomain">AppDomainName</span></code></pre>
