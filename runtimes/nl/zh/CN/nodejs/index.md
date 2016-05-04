---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# SDK for Nodejs
{: #nodejs_runtime}
*上次更新时间：2016 年 3 月 16 日*

{{site.data.keyword.Bluemix}} 上的 Node.js 运行时采用 sdk-for-nodejs buildpack 技术。
sdk-for-nodejs buildpack 为 Node.js 应用程序提供完整的运行时环境。
{: shortdesc}

应用程序在根目录中包含 **package.json** 文件时，会使用 sdk-for-nodejs buildpack。

## 入门模板应用程序
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供 Node.js 入门模板应用程序。Node.js 入门模板应用程序是简单的 Node.js 应用程序，提供可用于您应用程序的模板。您可以体验该入门模板应用程序，对其进行更改并将更改推送到 Bluemix 环境。请参阅[使用入门模板应用程序](../../cfapps/starter_app_usage.html)，以获取有关使用入门模板应用程序的帮助。

## 启动命令
{: #starup_commmand}

建议您使用以下方式为 Bluemix Node.js 应用程序指定启动命令：使用 **Procfile** 或 **package.json** 文件。

在 **Procfile** 中以下面的格式指定启动命令。此处，app.js 是应用程序的启动 js 脚本。```
web: node app.js```
{: codeblock}

将 **Procfile** 保存在应用程序的根目录中。

如果未提供 **Procfile**，那么 IBM Bluemix Node.js buildpack 会检查 **package.json** 文件中是否有 scripts.start 条目。同样，在下面的示例中，app.js 是应用程序的启动 js 脚本。```
{
    ...   
"scripts": {
"start": "node app.js"
}
}
```
{: codeblock}

如果 **package.json** 中提供了启动脚本条目，那么将自动生成 **Procfile**。自动生成的 **Procfile** 的内容如下所示：
```
    web: npm start```
{: codeblock}

有关 **Procfile** 和 **package.json** 文件的更多信息，请参阅 [Tips for Node.js Applications](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html)。

## 用于本地运行 Node.js 应用程序的提示
{: #hints}

使用此信息有助于在本地和在 Bluemix 上运行 Node.js 应用程序。

以下示例显示 **js** 文件的部分源代码：
```
var port = (process.env.VCAP_APP_PORT || 3000);
var host = (process.env.VCAP_APP_HOST || 'localhost');
```
{: codeblock}

使用此代码，当应用程序在 Bluemix 上运行时，VCAP_APP_HOST 和 VCAP_APP_PORT 环境变量包含 Bluemix 内部的主机和端口值，并且应用程序在其上侦听入局连接。当应用程序在本地运行时，VCAP_APP_HOST 和 VCAP_APP_PORT 未定义，所以 **localhost** 用作主机，而 **3000** 用作端口号。通过这种方式编写源代码，您可以在本地运行应用程序以用于测试，以及在 Bluemix 上运行应用程序，而无需进一步更改。

## 应用程序管理
{{site.data.keyword.Bluemix}} 提供若干用于管理和调试 Node.js 应用程序的实用程序。请参阅[应用程序管理](../../manageapps/app_mng.html)，以获取完整详细信息。

## 可用版本
{: #available_versions}

{{site.data.keyword.Bluemix}} 提供所有[目前可用的 Node.js 运行时](http://nodejs.org/dist/)。其中，IBM 提供的版本包含增强功能和错误修订。请参阅 [Node.js Buildpack 的最新更新](../../runtimes/nodejs/updates.html)，以获取更多信息。

IBM Node.js buildpack 高速缓存所有 IBM 运行时版本。因此，如果在应用程序中使用 IBM SDK for Node.js 运行时，那么在将应用程序推送到 Bluemix 时可提高应用程序性能。

使用 **package.json** 文件的 **engines** 部分中的 **node** 参数，可指定要运行的 Node.js 运行时版本。

如果需要指定除了与 Node.js 捆绑的 npm 版本之外的其他版本，请使用 **package.json** 文件的 **engines** 部分中的 **npm** 参数。  

请参阅以下示例：

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "2.11.3"
  }
}
```
{: codeblock}

应该始终在 **package.json** 文件中指定节点版本。如果未指定，那么将使用最新的节点版本。

## 配置选项
{: #configuration_options}

### NPM 脚本
{: #npm_scripts}
NPM 提供了脚本编制功能，允许您运行脚本，其中包括分别适用于 node_modules 安装前后的 **preinstall** 和 **postinstall** 脚本。请参阅 [npm-scripts](https://docs.npmjs.com/misc/scripts)，以获取完整详细信息。

### 高速缓存行为
{: #cache_behavior}
{{site.data.keyword.Bluemix}} 为每个节点应用程序保留一个高速缓存目录，并且将在构建之间持久存储该目录。高速缓存会存储解析的依赖项，这样每次部署应用程序时就不需要再下载和安装这些依赖项。例如，假设 myapp 依赖于 **express**。那么第一次部署 myapp 时会下载 **expess** 模块。在后续部署 myapp 时，会使用高速缓存的 **express** 实例。缺省行为是对 NPM 安装的所有 node_modules 以及 bower 安装的 bower_components 进行高速缓存。

使用 NODE_MODULES_CACHE 变量来确定 Node buildpack 是使用还是忽略先前构建的高速缓存。缺省值为 true。要禁用高速缓存，请将 NODE_MODULES_CACHE 设置为 false，例如，通过 cf 命令行：
```
    $ cf set-env myapp NODE_MODULES_CACHE false
```
{: codeblock}

请注意，不会高速缓存应用程序中包含的 node_modules。

可使用顶层 **package.json** 中的 **cacheDirectories** 数组，以精确控制将哪些模块高速缓存。当 **cacheDirectories** 元素显示在 **package.json** 中时，仅高速缓存位于 **cacheDirectories** 数组中的那些模块。在以下示例中，仅高速缓存 node_modules 和 bower_components。
```
{
  "cacheDirectories": ["node_modules","bower_components"],
  ...
}
```
{: codeblock}

### FIPS 方式
{: #fips_mode}

Nodejs buildpack V3.2-20160315-1257 及更高版本支持 [FIPS](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards)。要启用 FIPS，请将环境变量 FIPS_MODE 设置为 true。
例如：

```
    $ cf set-env myapp FIPS_MODE true
```
{: codeblock}

了解以下情况很重要：FIPS_MODE 为 true 时，**使用 [MD5](https://en.wikipedia.org/wiki/MD5) 的节点模块会失败**。例如，[Express](http://expressjs.com/) 模块会失败。在 Expess 应用程序中将 [etag](http://expressjs.com/en/api.html) 设置为 false 可能会帮助解决此问题。例如，您可以在代码中执行以下操作：
```
    app.set('etag', false);
```
{: codeblock}
请参阅这篇 [stackoverflow 帖子](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js)以获取更多信息。

要验证应用程序中的 FIPS_MODE 是否为 true，请检查 **process.versions.openssl** 的值。例如：```
    console.log('ssl version is [' +process.versions.openssl +']');
```
{: codeblockd}

如果 SSL 版本包含“fips”，那么应用程序会以 FIPS 方式运行。    


## Node.js buildpack

Bluemix 提供多个版本的 Node.js buildpack。
* IBM 创建的 **sdk-for-nodejs** buildpack 是 Bluemix 中用于 Node.js 应用程序的缺省 buildpack。
* **nodejs_buildpack** 是 Cloud Foundry 社区提供的外部 buildpack。

在 Bluemix 中，**sdk-for-nodejs** buildpack 优先于 **nodejs_buildpack**。如果想要将 **nodejs_buildpack**（而不是 **sdk-for-nodejs** buildpack）用于应用程序，那么必须指定 buildpack，例如，使用 -b 选项以及 **cf push** 命令。

通常会提供 **sdk-for-nodejs** buildpack 的当前版本和低版本。要查看所有可用的 buildpack，请使用 **cf buildpacks** 命令。例如：
<pre>
      cf buildpacks
Getting buildpacks...

      buildpack                      position          enabled          locked          filename	
   

      sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip

</pre>
{: codeblock}

# 相关链接
## 常规
* [Node.js buildpack 的最新更新](../../runtimes/nodejs/updates.html)
* [应用程序管理](../../manageapps/app_mng.html)
* [Node.js](https://nodejs.org)
* [StrongLoop](https://strongloop.com)
