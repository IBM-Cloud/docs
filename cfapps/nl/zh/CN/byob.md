---

 

copyright:

  years: 2015，2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用社区 buildpack
*上次更新时间：2016 年 3 月 15 日*

如果在 {{site.data.keyword.Bluemix}}“目录”中找不到提供所需运行时的入门模板，那么可以将外部 buildpack 添加到 {{site.data.keyword.Bluemix_notm}} 中。使用 cf push 命令部署应用程序时，可以指定 Cloud Foundry 兼容的定制 buildpack。
{:shortdesc}

外部 buildpack 由 Cloud Foundry 社区提供，可用作您自己的 buildpack。将应用程序部署到 {{site.data.keyword.Bluemix_notm}} 之前，请确保安装了 cf 命令行界面。

**注：**IBM 不提供外部 buildpack；因此，您可能需要联系 Cloud Foundry 社区来获取支持。

## 内置社区 buildpack

在 {{site.data.keyword.Bluemix_notm}} 中，您可以使用 Cloud Foundry 社区提供的内置 buildpack。要查看内置社区 buildpack，请运行 cf buildpacks 命令：

```
cf buildpacks
正在获取 buildpack...

buildpack          位置   已启用    已锁定   文件名
...
java_buildpack     7      true      false    buildpack_java_v2.0.2.zip
ruby_buildpack     8      true      false    buildpack_ruby_v46-245-g2fc4ad8.zip
nodejs_buildpack   9      true      false    buildpack_nodejs_v8-177-g2b0a5cf.zip
```
{:screen}

<ul>

<li>
对于同一运行时或框架，IBM 创建的 buildpack 优先于社区 buildpack。如果想要使用社区 buildpack 覆盖 IBM 创建的 buildpack，必须使用带 -b 选项的 cf push 命令来指定该 buildpack。
<p>例如，可以将社区 buildpack 用于 Java™ Web 应用程序：</p>
<pre class="pre"><code>cf push app_name -b java_buildpack -p app_path</code></pre>
<p>还可以将社区 buildpack 用于 Node.js 应用程序：</p>
<pre class="pre"><code>cf push app_name -b nodejs_buildpack -p app_path</code></pre>
</li>

<li>
<p>对于 IBM 创建的 buildpack 不支持但内置社区 buildpack 支持的运行时或框架，不必使用带 -b 选项的 cf push 命令。</p><p>例如，对于 Ruby 应用程序，没有 IBM 创建的 buildpack。可以通过输入以下命令使用内置社区 buildpack：</p>
<pre class="pre"><code>cf push app_name -p app_path</code></pre>
</li>
</ul>

## 外部 buildpack

您可以在 {{site.data.keyword.Bluemix_notm}} 中使用外部或定制 buildpack。在 **cf push** 命令中，必须使用 -b 选项来指定 buildpack 的 URL，并使用 `-s` 选项来指定堆栈。例如，要对静态文件使用外部社区 buildpack，请运行以下命令：

```
cf push app_name -p app_path -b https://github.com/cloudfoundry-incubator/staticfile-buildpack.git -s cflinuxfs2
```
{:pre}

另一个示例是，如果不想将内置社区 buildpack 用于 Ruby 应用程序，那么可以通过输入以下命令使用外部 buildpack：

```
cf push app_name -p app_path -b https://github.com/cloudfoundry/heroku-buildpack-ruby -s cflinuxfs2
```
{:pre}

您还可以将定制 buildpack 用于自己的应用程序。例如，要使用 Cloud Foundry 社区提供的开放式源代码 PHP buildpack，请在将 PHP 应用程序部署到 Bluemix 时，输入以下命令来指定 buildpack 的 Git 存储库 URL：

```
cf push app_name -p app_path -b https://github.com/dmikusa-pivotal/cf-php-build-pack -s cflinuxfs2
```
{:pre}

## 指定 Java buildpack 版本

<ul>
<li>
使用 <strong>cf set-env</strong> 命令。例如，输入以下命令，将 Java 版本设置为 1.7.0：
<pre class="pre"><code>cf set-env app_name JBP_CONFIG_OPEN_JDK_JRE &#39;{jre: { version: 1.7.0_+ }}&#39;</code></pre>
<p>然后，重新编译打包应用程序以使更改生效：</p>
<pre class="pre"><code>cf restage app_name</code></pre>
</li>
<li>
使用 <code>manifest.yml</code> 文件。您可以添加想要直接对文件指定的环境变量和值。有关详细信息，请参阅<a href="https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#env-block">环境变量</a>。</li></ul>
  

