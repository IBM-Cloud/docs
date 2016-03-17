---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Uploading your application
*Last updated: 17 February 2016*

After you are logged in to {{site.data.keyword.Bluemix}}, you can upload your application with the cf push command.
{:shortdesc}

Before you begin, you must:
  1. Install the {{site.data.keyword.Bluemix}} and Cloud Foundry command line interfaces.

  <a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="(Opens in a new tab or window)"><img class="image" src="images/btn_bx_commandline.svg" alt="Download {{site.data.keyword.Bluemix}} command line interface" /> </a>  <a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(Opens in a new tab or window)"><img class="image" src="images/btn_cf_commandline.svg" alt="Download Cloud Foundry command line interface" /> </a> 

  2. Connect to {{site.data.keyword.Bluemix}}.

  <pre class="pre">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></pre>
  
  3. Log in to {{site.data.keyword.Bluemix_notm}}.

  <pre class="pre">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></pre>

When a **cf push** command is issued, the **cf** command line interface provides the working directory to the {{site.data.keyword.Bluemix_notm}} environment that uses a buildpack to build and run the application.

  1. From your application directory, enter the **cf push** command with the application name. The app name must be unique in the {{site.data.keyword.Bluemix_notm}} environment.
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -m 512m</pre>
  
  {{site.data.keyword.Bluemix_notm}} includes built-in buildpacks. In some cases, even for the built-in buildpacks, you must also supply a -c option to specify the command that is used to start your application. For example, you need to use the -c option to push your Node.js application:
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -c start_command</pre>
  
  In addition, the Node.js application must contain a valid package.json file.

  All other external buildpacks must be pushed by using the -b option. For example:

  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -b buildpack_URL</pre>
  
  **Tip:** When you use the **cf push** command, the **cf** command line interface copies all of the files and directories from your current directory to Bluemix. Ensure that you have only the required files in your application directory.

  The cf push command uploads and deploys your application to {{site.data.keyword.Bluemix_notm}}. See [cf commands](../cli/reference/cfcommands/index.html) for more information about cf push. See [Using community buildpacks](../cfapps/byob.html) for information about buildpacks.

  2. If you change your application, you can upload those changes by entering the cf push command again. The cf command line interface uses your previous options and your responses to the prompts to update any running instances of your application with the new bits of code.

**Tip:** You can also upload or deploy an application from DevOps Services. See [Developing a {{site.data.keyword.Bluemix_notm}} application in Node.js with the Web IDE](https://hub.jazz.net/tutorials/devopsweb/){: new_window}.
