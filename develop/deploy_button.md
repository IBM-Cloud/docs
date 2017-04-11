---

copyright:
  years: 2015, 2017
lastupdated: "2017-2-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


#Creating a Deploy to {{site.data.keyword.Bluemix_notm}} button {: #deploy-button} 

The Deploy to {{site.data.keyword.Bluemix}} button is an efficient way to share your public Git-sourced app so that other people can experiment with the code and deploy it to IBM {{site.data.keyword.Bluemix_notm}}. The button requires minimal configuration and you can insert it anywhere that supports markup. Anyone who clicks the button creates a cloned copy of the code in a new Git repository so that your original app remains unaffected. 
{: shortdesc} 

**Tip:** If company branding is important, you can [embed a Deploy to {{site.data.keyword.Bluemix_notm}} iFrame flow](/docs/develop/deploy_button_embed.html) in your content instead of inserting a button. When people create a cloned copy of your public Git-sourced app, they stay in your content instead of being redirected to the bluemix.net website. 

**Note**: The toolchains feature is now available. Anyone who clicks the Deploy to {{site.data.keyword.Bluemix_notm}} button can click the link in the banner to try deploying their application by using a toolchain.

When someone clicks your button, these actions occur: 

1. If the person does not have an active {{site.data.keyword.Bluemix_notm}} account, a trial account must be created. 

2. The person can select a region, organization, space, and app name. The suggested app name is constructed from the previous app name, the person's user name, and the time. 

3. The master branch of the original public Git repository is cloned into a new, private {{site.data.keyword.jazzhub_title}} project with a new Git repository. 

4. If the app requires a build file, the build file is detected automatically and the app is built. 

5. If a pipeline is configured for the build and deployment process,  a `pipeline.yml` file is used to deploy the app.

6. If the app requires a container, a `pipeline.yml` that defines the **IBM Containers** service and a Dockerfile that defines an image are used to deploy the app in a {{site.data.keyword.Bluemix_notm}} container. 

7. The app is deployed to the person's {{site.data.keyword.Bluemix_notm}} organization. 

##Examples of the button {: #button-examples} 

See an app button example for a public {{site.data.keyword.jazzhub_short}} repository:

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://hub.jazz.net/git/idsorg/sample-java-cloudant" target="_blank" title="(Opens in a new tab or window)"><img class="image" src="images/deploy_buttonx2.png" alt="Deploy to Bluemix" /></a>
</p> 

See an app button example for a public GitHub repository: 

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://github.com/ibmjstart/bluemix-node-mysql-uploader" target="_blank" title="(Opens in a new tab or window)"><img class="image" src="images/deploy_buttonx2.png" alt="Deploy to Bluemix" /></a>
</p> 

See a button example for an app that is deployed in a {{site.data.keyword.Bluemix_notm}} container: 

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://github.com/Puquios/hello-containers" target="_blank" title="(Opens in a new tab or window)"><img class="image" src="images/deploy_buttonx2.png" alt="Deploy to Bluemix" /></a>
</p> 

##Creating a button {: #create-button}

To create a Deploy to {{site.data.keyword.Bluemix_notm}} button: 

<ol>
<li> Copy and modify one of the following snippet templates and include a public Git repository.
<p></p>
<p>
<strong>Tip</strong>: If you want to specify the build input for a DevOps Services project, add a branch parameter to the Git URL. When you add a branch parameter, the original public Git repository, including all of its branches, is cloned into a new, private DevOps Services project with a new Git repository. The specified Git branch is set as the input for the build job. If you don't specify a branch, the input for the build job is set to the master branch by default.
</p>
<ul>
<li>HTML:
<p>
Default master branch:
</p>
<pre class="codeblock">
&lt;a href="https://bluemix.net/deploy?repository=&lt;git_repository_URL>" # [required]&gt;&lt;img src="https://bluemix.net/deploy/button.png" alt="Deploy to Bluemix"&gt;&lt;/a&gt;
</pre>
<p>
Specified Git branch:
</p>
<pre class="codeblock">
&lt;a href="https://bluemix.net/deploy?repository=&lt;git_repository_URL&gt;&branch=&lt;git_branch>" # [required]&gt;&lt;img src="https://bluemix.net/deploy/button.png" alt="Deploy to Bluemix"&gt;&lt;/a&gt;
</pre>
</li>
<li>Markdown:
<p>
Default master branch:
</p>
<pre class="codeblock">
[&excl;[Deploy to Bluemix]&lpar;https://bluemix.net/deploy/button.png&rpar;]&lpar;https://bluemix.net/deploy?repository=&lt;git_repository_URL> # [required]&rpar;
</pre>
<p>Specified Git branch:
</p>
<pre class="codeblock">
[&excl;[Deploy to Bluemix]&lpar;https://bluemix.net/deploy/button.png&rpar;]&lpar;https://bluemix.net/deploy?repository=&lt;git_repository_URL> &branch=&lt;git_branch&gt; # [required]&rpar;
</pre>
</li>
</ul>
</li>
<li>Insert the snippet into blogs, articles, wikis, readme files, or anywhere you want to promote your app. 
</li>
</ol>

##Snippet considerations for the button {: #button-snippet}

Review these considerations when you are customizing the snippet for your Deploy to Bluemix button. 

* Both of the templates use a default path to an external button image in PNG format and in English. 

    * If you prefer to use an SVG image for the button instead of a PNG, there is an SVG version available. You can change the path to the external button image that is used in the snippet to `https://bluemix.net/deploy/button.svg`.
	
	* If you prefer to use a larger image for the button, there is a PNG image available that is twice the size of the original. You can change the path of the external button image that is used in the snippet to `https://bluemix.net/deploy/button_x2.png`. 
	
	* If you prefer to store the image locally, you can download the image and store it in your Git repository. Adjust the path to use the relative location of the image. 
	
	* If you want to use a translated version of the button, you can reference it remotely or download it from [ftp://public.dhe.ibm.com/cloud/bluemix/deploy_button![External link icon](../icons/launch-glyph.svg "External link icon")](ftp://public.dhe.ibm.com/cloud/bluemix/deploy_button){:new_window}. 
	
##Repository considerations for the button {: #button-repo} 

Review these considerations for the project repository that you will use in your Deploy to Bluemix button. 

<ul>
<li>A <code>manifest.yml</code> is not required to be in your repository. However, if your app requires other services to run, you must provide a manifest file that declares those services.  

With the manifest file, you can specify: 
    <ul>
    <li>A unique app name.</li>  
    <li>Declared services: A manifest extension, which creates or looks for the required or optional services that are expected to be     set up before the app is deployed, such as a data cache service. You can find a list of the eligible     {{site.data.keyword.Bluemix_notm}} services, labels, and plans by using the <a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(Opens in a new tab or window)">CF Command Line Interface<img class="image" src="../icons/launch-glyph.svg" alt="External link icon"/></a> to run the <code>cf marketplace</code> command or by browsing the <a class="xref" href="https://console.ng.bluemix.net/?ssoLogout=true&cm_mmc=developerWorks-_-dWdevcenter-_-devops-services-_-lp#/store" target="_blank" title="(Opens in a new tab or window)"> {{site.data.keyword.Bluemix_notm}} catalog<img class="image" src="../icons/launch-glyph.svg" alt="External link icon"/></a>. 
    
        
    <strong>Note:</strong> Declared services is an IBM extension of the standard Cloud Foundry manifest format. This extension might be revised in a future release as the feature evolves and improves.
	
	<a class="xref" href="http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#minimal-manifest" target="_blank" title="(Opens in a new tab or window)">Learn how to create a <code>manifest.yml</code> file<img class="image" src="../icons/launch-glyph.svg" alt="External link icon"/></a>.  
<pre class="codeblock">
	---
    #Template manifest.yml

  declared-services:
    &lt;`arbitrary_service_instance_name`&gt;:  # [required] 
      label: &lt;`actual_service_name`&gt; # [required] The actual service name from market place 
      plan: Shared # [optional] If provided, used to fetch the declared service. Otherwise, defaults to 'Free' or 'free'.
  applications:
  - services
    - &lt;`arbitrary_service_instance_name`&gt;
    name: &lt;`appname`&gt;
    host: &lt;`apphostname`&gt;
</pre>

<pre class="codeblock">
	---
    #Example manifest.yml

  declared-services: 
      sample-java-cloudant-cloudantNoSQLDB: 
        label: cloudantNoSQLDB 
        plan: Shared 
  applications:
  - services
    - sample-java-cloudant-cloudantNoSQLDB
    name: My app
    host: myapp
</pre>
   </li>
   </ul>
	<li> If the app must be built before it can be deployed, you must include a build file in your repository. If a build script file is detected in the root directory of the repository, an automated build of the code is triggered before deployment. 
	
	Supported builders: 
	    <ul>
		<li> <a class="xref" href="http://ant.apache.org/manual/using.html" target="_blank" title="(Opens in a new tab or window)">Ant:<img class="image" src="../icons/launch-glyph.svg" alt="External link icon"/></a> /<code>build.xml</code>, which builds output to the <code>./output/</code> folder </li>
		<li> <a class="xref" href="http://docs.cloudfoundry.org/buildpacks/java/build-tool-int.html#gradle" target="_blank" title="(Opens in a new tab or window)">Gradle:<img class="image" src="../icons/launch-glyph.svg" alt="External link icon"/></a> <code>/build.gradle</code>, which builds output to the <code>. </code> folder </li>
		<li> <a class="xref" href="http://gruntjs.com/getting-started#the-gruntfile" target="_blank" title="(Opens in a new tab or window)">Grunt:<img class="image" src="../icons/launch-glyph.svg" alt="External link icon"/></a> <code>/Gruntfile.js</code>, which builds output to the <code>. </code> folder </li>
		<li> <a class="xref" href="http://docs.cloudfoundry.org/buildpacks/java/build-tool-int.html#maven" target="_blank" title="(Opens in a new tab or window)">Maven:<img class="image" src="../icons/launch-glyph.svg" alt="External link icon"/></a> <code>/pom.xml</code>, which builds output to the <code>./target/</code> folder</li>
	   </ul>
	</li>	
	<li>To configure pipeline for the project, in a <code>.bluemix</code> directory, include a <code>pipeline.yml</code> file. You can create a <code>pipeline.yml</code> file manually or you can generate one from an existing DevOps Services project. To create a pipeline.yml file from a {{site.data.keyword.jazzhub_short}} project and add it to your repository, complete these steps. 
<ol>
<li>Open your DevOps Services project in a browser and click <b>Build and Deploy</b>.</li>
<li>Configure your pipeline with build and deployment jobs.</li>
<li>In your browser, add <code>/yaml</code> to the project pipeline URL and press Enter. 
<br>Example: <code>https://hub.jazz.net/pipeline/<owner>/<project_name>/yaml</code></li>
<li>Save the resulting <code>pipeline.yml</code> file.</li>
<li>In the root directory of your project, create a <code>.bluemix</code> directory.</li>
<li>Upload the <code>pipeline.yml</code> file to the <code>.bluemix</code> repository.</li>
</ol> </li>
	<li>To deploy an app in a container by using <strong>IBM Containers</strong>, you must include Dockerfile in the root directory of the repository and, in a <code>.bluemix</code> directory, include a <code>pipeline.yml</code> file. 
	<ul>
	    <li>The Dockerfile acts as a kind of build script for the app. If a Dockerfile is detected in the repository, the app is automatically built into an image before it is deployed in a container. If the app itself must be built before the app is built into an image, include a build script for the app as well as a Dockerfile, as previously described.</li>
	    <li> To learn more about creating Dockerfiles, <a class="xref" href="https://docs.docker.com/reference/builder/" target="_blank" title="(Opens in a new tab or window)">see the Docker documentation<img class="image" src="../icons/launch-glyph.svg" alt="External link icon"/></a>. </li>
	    <li>You can create a <code>pipeline.yml</code> file manually or you can generate one from an existing DevOps Services project. To create a <code>pipeline.yml</code> manually that is specifically for containers, <a class="xref" href="https://github.com/Puquios/" target="_blank" title="(Opens in a new tab or window)">see the examples in GitHub<img class="image" src="../icons/launch-glyph.svg" alt="External link icon"/></a>. </li>
        </ul>

 </li>
 </ul>
</ul>

For troubleshooting help, see [Deploy to Bluemix button doesn't deploy an app](/docs/troubleshoot/index.html#deploytobluemixbuttondoesntdeployanapp){:new_window}.	
