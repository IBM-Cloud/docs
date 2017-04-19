---



copyright:

  years: 2015, 2017

lastupdated: "2017-04-19"



---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Uploading your application

After you are logged in to {{site.data.keyword.Bluemix}}, you can upload your application with the `bluemix app push` command.
{:shortdesc}

Before you begin, you must:
  1. Install the {{site.data.keyword.Bluemix}} command line interface.

  <a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="(Opens in a new tab or window)"><img class="image" src="images/btn_bx_commandline.svg" alt="Download {{site.data.keyword.Bluemix}} command line interface" /> </a> 

  2. Connect to {{site.data.keyword.Bluemix}}.

  <pre class="pre"><code class="hljs">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></code></pre>

  3. Log in to {{site.data.keyword.Bluemix_notm}}.

  <pre class="pre"><code class="hljs">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></code></pre>

When a **bluemix app push** command is issued, the command line interface provides the working directory to the {{site.data.keyword.Bluemix_notm}} environment that uses a buildpack to build and run the application.

  1. From your application directory, enter the **bluemix app push** command with the application name. The app name must be unique in the {{site.data.keyword.Bluemix_notm}} environment.

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -m 512m</code></pre>

  {{site.data.keyword.Bluemix_notm}} includes built-in buildpacks. In some cases, even for the built-in buildpacks, you must also supply a -c option to specify the command that is used to start your application. For example, you need to use the -c option to push your Node.js application:

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -c start_command</code></pre>

  In addition, the Node.js application must contain a valid package.json file.

  All other external buildpacks must be pushed by using the -b option. For example:

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -b buildpack_URL</code></pre>

  **Tip:** When you use the **bluemix app push** command, the command copies all of the files and directories from your current directory to Bluemix. Ensure that you have only the required files in your application directory.

  
  2. If you change your application, you can upload those changes by entering the `bluemix app push` command again. The command uses your previous options and your responses to the prompts to update any running instances of your application with the new bits of code.

{{site.data.keyword.Bluemix}} CLI bundled a cf cli in its installation. `bluemix app push` command acutually invokes `cf push` to upload and deploy your application to {{site.data.keyword.Bluemix_notm}}. See [cf commands](/docs/cli/reference/cfcommands/index.html) for more information about cf push. See [Using community buildpacks](/docs/cfapps/byob.html) for information about buildpacks.


**Tip:** You can also upload or deploy an application from DevOps Services. See [Developing a {{site.data.keyword.Bluemix_notm}} application in Node.js with the Web IDE](https://hub.jazz.net/tutorials/devopsweb/){: new_window}.
