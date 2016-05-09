---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


#创建“部署到 {{site.data.keyword.Bluemix_notm}}”按钮 {: #deploy-button} 

*上次更新时间：2016 年 3 月 2 日* 

使用“部署到 {{site.data.keyword.Bluemix}}”按钮，可以高效地将自己的公共 Git 源应用程序共享给其他人员，以便其他人员可以试验代码并将其部署到 IBM {{site.data.keyword.Bluemix_notm}}。此按钮不但需要的配置最少，而且可插入到支持标记的任何位置。无论是谁，只要单击该按钮，即可在新的 Git 存储库中创建代码的克隆副本，而您的原始应用程序将不受影响。
{: shortdesc} 

**提示：**如果公司标记很重要，那么可以在您的内容中[嵌入“部署到 {{site.data.keyword.Bluemix_notm}}”iFrame 流](../develop/deploy_button_embed.html)，而不是插入按钮。当其他人员对您的公共 Git 源应用程序创建克隆副本时，他们会停留在您的内容中，而不会被重定向到 bluemix.net Web 站点。 

当有人单击您的按钮时，会发生这些操作： 

1. 如果该人员没有活动 {{site.data.keyword.Bluemix}} 帐户，那么必须创建一个试用帐户。 

2. 该人员可以选择区域、组织、空间和应用程序名称。可以从先前的应用程序名称、人员的用户名和时间构建建议的应用程序名称。 

3. 会将原始公共 Git 存储库的主分支克隆到带有新 Git 存储库的专用 {{site.data.keyword.jazzhub_title}} 项目。 

4. 如果应用程序需要一个构建文件，那么会自动检测到该构建文件，并且会构建该应用程序。 

5. 如果管道配置用于构建和部署过程，那么将使用 `pipeline.yml` 文件来部署应用程序。

6. 如果应用程序需要容器，那么 `pipeline.yml`（定义 **IBM Container** 服务）和 Dockerfile（定义映像）用于在 {{site.data.keyword.Bluemix_notm}} 容器中部署应用程序。 

7. 应用程序将部署到该人员的 {{site.data.keyword.Bluemix_notm}} 组织。 

##按钮示例 {: #button-examples} 

请参阅公共 {{site.data.keyword.jazzhub_short}} 存储库的应用程序按钮示例：

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://hub.jazz.net/git/idsorg/sample-java-cloudant" target="_blank" title="（在新选项卡或窗口中打开）"><img class="image" src="images/deploy_buttonx2.png" alt="部署到 Bluemix" /></a></p> 

请参阅公共 GitHub 存储库的应用程序按钮示例： 

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://github.com/ibmjstart/bluemix-node-mysql-uploader" target="_blank" title="（在新选项卡或窗口中打开）"><img class="image" src="images/deploy_buttonx2.png" alt="部署到 Bluemix" /></a></p> 

请参阅 {{site.data.keyword.Bluemix_notm}} 容器中部署的应用程序的按钮示例： 

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://github.com/Puquios/hello-containers" target="_blank" title="（在新选项卡或窗口中打开）"><img class="image" src="images/deploy_buttonx2.png" alt="部署到 Bluemix" /></a></p> 

##创建按钮 {: #create-button}

要创建“部署到 {{site.data.keyword.Bluemix_notm}}”按钮，请执行以下操作： 

<ol>
<li> 复制并修改以下某个片段模板，并在其中加入公共 Git 存储库。<p></p>
<p>
<strong>提示</strong>：如果想要为 DevOps Services 项目指定构建输入，请向 Git URL 添加分支参数。添加分支参数后，系统会将原始公共 Git 存储库（包括其所有分支）克隆到带有新 Git 存储库的新专用 DevOps Services 项目中。系统会将指定的 Git 分支设置为构建作业的输入。如果未指定分支，那么缺省情况下，会将构建作业的输入设置为主分支。</p>
<ul>
<li>HTML：<p>
缺省主分支：</p>
<pre class="codeblock">
&lt;a href="https://bluemix.net/deploy?repository=&lt;git_repository_URL>" # [必需]&gt;&lt;img src="https://bluemix.net/deploy/button.png" alt="部署到 Bluemix"&gt;&lt;/a&gt;
</pre>
<p>
指定的 Git 分支：
</p>
<pre class="codeblock">
&lt;a href="https://bluemix.net/deploy?repository=&lt;git_repository_URL&gt;&branch=&lt;git_branch>" # [必需]&gt;&lt;img src="https://bluemix.net/deploy/button.png" alt="部署到 Bluemix"&gt;&lt;/a&gt;
</pre>
</li>
<li>Markdown：<p>
缺省主分支：</p>
<pre class="codeblock">
[&#33;[部署到 Bluemix]&#40;https://bluemix.net/deploy/button.png&#41;]&#40;https://bluemix.net/deploy?repository=&lt;git_repository_URL> # [必需]&#41;
</pre>
<p>指定的 Git 分支：
</p>
<pre class="codeblock">
[&#33;[部署到 Bluemix]&#40;https://bluemix.net/deploy/button.png&#41;]&#40;https://bluemix.net/deploy?repository=&lt;git_repository_URL> &branch=&lt;git_branch&gt; # [必需]&#41;
</pre>
</li>
</ul>
</li>
<li>将该片段插入博客、文章、Wiki、自述文件或您希望推广您应用程序的任何位置。</li>
</ol>

##按钮片段的注意事项 {: #button-snippet}

如果您要定制“部署到 Bluemix”按钮片段，请查看以下注意事项。 

* 这两个模板均使用外部按钮图像的缺省路径，图像采用 PNG 格式，文本使用英语。 

    * 如果您倾向于使用按钮的 SVG 图像而不是 PNG 图像，那么也有可用的 SVG 版本。您可以将片段中使用的外部按钮图像的路径更改为 `https://bluemix.net/deploy/button.svg`。
	
	* 如果您希望使用较大的按钮图像，我们还提供了比原始大小大两倍的图像。您可以将片段中使用的外部按钮图像的路径更改为 `https://bluemix.net/deploy/button_x2.png`。 
	
	* 如果您偏向于将图像存储在本地，那么可下载图像并将其存储在 Git 存储库中。调整路径以使用图像的相对位置。 
	
	* 如果您希望使用此按钮的翻译版本，那么可远程进行引用或从 [ftp://public.dhe.ibm.com/cloud/bluemix/deploy_button](ftp://public.dhe.ibm.com/cloud/bluemix/deploy_button) 进行下载。 
	
##按钮的存储库注意事项 {: #button-repo} 

对于要在“部署到 Bluemix”按钮中使用的项目存储库，请查看以下注意事项。 

<ul>
<li>存储库中不是必须要有 <code>manifest.yml</code>。但如果应用程序需要其他服务运行，那么必须提供声明这些服务的清单文件。  

您可以使用此清单文件指定以下内容： 
    <ul>
    <li>唯一应用程序名称。</li>  
    <li>声明的服务：清单扩展，它可以创建或查找期望在部署应用程序之前先设置好的必需或可选服务，如数据高速缓存服务。您可以查找合格的 {{site.data.keyword.Bluemix_notm}} 服务、标签和计划的列表，方法是使用 <a href="https://github.com/cloudfoundry/cli/releases">CF 命令行界面</a>来运行 <code>cf marketplace</code> 命令，也可以浏览 <a href="https://console.ng.bluemix.net/?ssoLogout=true&cm_mmc=developerWorks-*-dWdevcenter-*-devops-services-_-lp#/store">{{site.data.keyword.Bluemix_notm}} 目录</a>。
    
    <strong>注：</strong>声明的服务是标准 Cloud Foundry 清单格式的 IBM 扩展。随着该功能部件的演化和改进，在未来发行版中，可能会对此扩展进行修改。<a href="http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#minimal-manifest" target="_blank">了解如何创建 <code>manifest.yml</code> 文件。</a>  
<pre class="codeblock">
	---
    #manifest.yml 模板

  declared-services:

    &lt;`arbitrary_service_instance_name`&gt;:  # [必需]
      label: &lt;`actual_service_name`&gt; # [必需] 市场上的实际服务名称
      plan: Shared # [可选] 如果提供，用于访存声明的服务。否则，缺省值为“Free”或“free”。
applications:

  - 服务
    - &lt;`arbitrary_service_instance_name`&gt;
    name: &lt;`appname`&gt;
    host: &lt;`apphostname`&gt;
</pre>

<pre class="codeblock">
	---
    #manifest.yml 示例

  declared-services:
 
      sample-java-cloudant-cloudantNoSQLDB:
        label: cloudantNoSQLDB
        plan: Shared
  applications:
  - 服务
    - sample-java-cloudant-cloudantNoSQLDB
    name: My app
    host: myapp
</pre>
   </li>
   </ul>
	<li> 如果必须在部署应用程序之前构建存储库，那么会先触发存储库中代码的自动构建，再进行部署。在存储库的根目录中检测到构建脚本文件时，会执行自动构建。	受支持的构建器： 
	    <ul>
		<li> <a href="http://ant.apache.org/manual/using.html" target="_blank">Ant:</a> /<code>build.xml</code>，它会将输出构建到 <code>./output/</code> 文件夹中</li>
		<li> <a href="http://docs.cloudfoundry.org/buildpacks/java/build-tool-int.html#gradle" target="_blank">Gradle:</a> <code>/build.gradle</code>，它会将输出构建到 <code>.</code> 文件夹中</i><li> <a href="http://gruntjs.com/getting-started#the-gruntfile" target="_blank">Grunt:</a> <code>/Gruntfile.js</code>，它会将输出构建到 <code>.</code> 文件夹中</li>
		<li> <a href="http://docs.cloudfoundry.org/buildpacks/java/build-tool-int.html#maven" target="_blank">Maven:</a> <code>/pom.xml</code>，它会将输出构建到 <code>./target/</code> 文件夹中</li>
	   </ul>
	</li>	
	<li>要为项目配置管道，请将 <code>pipeline.yml</code> 文件放入 <code>.bluemix</code> 目录中。您可以手动创建 <code>pipeline.yml</code> 文件，也可以根据现有 DevOps Services 项目来生成 pipeline.yml 文件。要根据 {{site.data.keyword.jazzhub_short}} 项目创建 pipeline.yml 文件，并将其添加到您的存储库中，请完成以下步骤。
<ol>
<li>在浏览器中打开您的 DevOps Services 项目，然后单击<b>构建和部署</b>。</li>
<li>使用构建和部署作业来配置管道。</li>
<li>在浏览器中，将 <code>/yaml</code> 添加到项目管道 URL 中，然后按 Enter 键。<br>示例：<code>https://hub.jazz.net/pipeline/<owner>/<project_name>/yaml</code></li>
<li>保存生成的 <code>pipeline.yml</code> 文件。</li>
<li>在项目的根目录中，创建 <code>.bluemix</code> 目录。</li>
<li>将 <code>pipeline.yml</code> 文件上传到 <code>.bluemix</code> 存储库。</li>
</ol> </li>
	<li>如果您要使用 <stong>IBM Containers</strong> 在容器中部署应用程序，那么必须将 Dockerfile 放入存储库的根目录中，并将 <code>pipeline.yml</code> 文件放入 <code>.bluemix</code> 目录中。<ul>
	    <li> 要了解有关创建 Dockerfile 的更多信息，请参阅 <a href="https://docs.docker.com/reference/builder/" target="_blank">Docker 文档</a>。</li>
	    <li>您可以手动创建 <code>pipeline.yml</code> 文件，也可以根据现有 DevOps Services 项目来生成 pipeline.yml 文件。要手动创建专用于容器的 <code>pipeline.yml</code>，请参阅 <a href="https://github.com/Puquios/" target="_blank">GitHub</a> 中的示例。</li>
        </ul>

 </li>
 </ul>
</ul>

有关故障诊断帮助，请参阅[“部署到 Bluemix”按钮不部署应用程序](../troubleshoot/index.html#deploytobluemixbuttondoesntdeployanapp){:new_window}。	
