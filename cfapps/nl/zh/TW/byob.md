---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用社群建置套件
*前次更新：2016 年 3 月 15 日*

如果您在 {{site.data.keyword.Bluemix}}「型錄」中，找不到提供您想要之執行時期的入門範本，則可將外部建置套件帶到 {{site.data.keyword.Bluemix_notm}}。利用 cf push 指令部署應用程式時，可指定與 Cloud Foundry 相容的自訂建置套件。
{:shortdesc}

外部建置套件是由 Cloud Foundry 社群提供，可用來作為您自己的建置套件。在將您的應用程式部署至 {{site.data.keyword.Bluemix_notm}} 之前，請確定已安裝 cf 指令行介面。

**附註：**外部建置套件不是由 IBM 提供，因此，您可能需要聯絡 Cloud Foundry 社群，以取得支援。

## 內建社群建置套件

在 {{site.data.keyword.Bluemix_notm}} 中，您可以使用 Cloud Foundry 社群所提供的內建建置套件。若要查看內建的社群建置套件，請執行 cf buildpacks 指令：

```
cf buildpacks
Getting buildpacks...

buildpack      position   enabled   locked   filename
...
java_buildpack     7      true      false    buildpack_java_v2.0.2.zip
ruby_buildpack     8      true      false    buildpack_ruby_v46-245-g2fc4ad8.zip
nodejs_buildpack   9      true      false    buildpack_nodejs_v8-177-g2b0a5cf.zip
```
{:screen}

<ul>

<li>
對於相同的執行時期或架構，IBM 建立的建置套件優先於社群建置套件。如果您想要使用社群建置套件來改寫 IBM 建立的建置套件，則必須使用 -b 選項與 cf push 指令搭配，來指定建置套件。<p>例如，您可以針對 Java™ Web 應用程式使用社群建置套件：</p>
<pre class="pre"><code>cf push app_name -b java_buildpack -p app_path</code></pre>
<p>也可以使用適用於 Node.js 應用程式的社群建置套件：</p>
<pre class="pre"><code>cf push app_name -b nodejs_buildpack -p app_path</code></pre>
</li>

<li>
<p>對於 IBM 建立的建置套件不支援、但內建社群建置套件支援的執行時期或架構，則不需要使用 -b 選項與 cf push 指令搭配。</p><p>例如，對於 Ruby 應用程式，就沒有 IBM 建立的建置套件。您可以輸入下列指令來使用內建社群建置套件：</p>
<pre class="pre"><code>cf push app_name -p app_path</code></pre>
</li>
</ul>

## 外部建置套件

您可以在 {{site.data.keyword.Bluemix_notm}} 中使用外部或自訂建置套件。您必須在 **cf push** 指令上，使用 -b 選項指定建置套件的 URL，並使用 ```-s``` 選項指定堆疊。例如，若要針對靜態檔案使用外部社群建置套件，請執行下列指令：


```
cf push app_name -p app_path -b https://github.com/cloudfoundry-incubator/staticfile-buildpack.git -s cflinuxfs2
```
{:pre}

另一個範例是，如果您不想要將內建社群建置套件用於 Ruby 應用程式，也可以輸入下列指令來使用外部建置套件：

```
cf push app_name -p app_path -b https://github.com/cloudfoundry/heroku-buildpack-ruby -s cflinuxfs2
```
{:pre}

您的應用程式也可以使用自訂建置套件。
例如，若要使用 Cloud Foundry 社群所提供的開放程式碼 PHP 建置套件，請在您將 PHP 應用程式部署至 Bluemix 時，輸入下列指令以指定建置套件的 Git 儲存庫 URL：

```
cf push app_name -p app_path -b https://github.com/dmikusa-pivotal/cf-php-build-pack -s cflinuxfs2
```
{:pre}

## 指定 Java 建置套件版本

<ul>
<li>
使用 <strong>cf set-env</strong> 指令。例如，請輸入下列指令將 Java 版本設為 1.7.0：
<pre class="pre"><code>cf set-env app_name JBP_CONFIG_OPEN_JDK_JRE &#39;{jre: { version: 1.7.0_+ }}&#39;</code></pre>
<p>然後，重新編譯打包應用程式，以讓變更生效：
</p>
<pre class="pre"><code>cf restage app_name</code></pre>
</li>
<li>
使用 <code>manifest.yml</code> 檔案。您可以直接將想要指定的環境變數和值新增至該檔案。
如需詳細資訊，請參閱<a href="https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#env-block">環境變數</a>。</li></ul>
  

