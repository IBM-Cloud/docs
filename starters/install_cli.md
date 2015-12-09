{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
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

# Deploying your app with the Cloud Foundry command line interface
*Last updated: 11 November 2015*

You can use the Cloud Foundry command line interface to deploy and modify applications and service instances.
{:shortdesc}

Before you begin, install the cf command line interface.

<p>
<a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(Opens in a new tab or window)"><img class="image" src="images/btn_cf_commandline.svg" alt="Download Cloud Foundry command line interface" /> </a> 
</p>

**Restriction:** The Cloud Foundry command line interface is not supported by Cygwin. Use the Cloud Foundry command line interface in a command line window other than the Cygwin command line window.

After the cf command line interface is installed, you can get started:

  1. Download your starter code.
  
    <p>
    <a class="xref" href="http://bluemix.net" target="_blank" title="(Opens in a new tab or window)"><img class="image" src="images/btn_starter-code.svg" alt="Download Starter Code" /> </a> 
    </p>
  
  {:download}
  2. Extract the package to a new directory to set up your development environment.
  3. Change to your new directory.
  
  <pre class="pre">cd <var class="keyword varname">your_new_directory</var></pre>
  
  4. Connect to {{site.data.keyword.Bluemix}}.
  
  <pre class="pre">cf api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></pre>
  
  5. Log in to {{site.data.keyword.Bluemix_notm}}.
 
  <pre class="pre">cf login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></pre>
  
  6. Deploy your app to {{site.data.keyword.Bluemix_notm}}. For more information about cf push command, see [Uploading your application](upload_app.html#upload_app__push).
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var></pre>
  
  7. Access your app by entering the following URL into your browser:
  
  <pre class="codeblock"><code><var class="keyword varname" data-hd-keyref="host">host</var>.<span class="keyword" data-hd-keyref="APPDomain">AppDomainName</span></code></pre>
