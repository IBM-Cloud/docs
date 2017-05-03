---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# node.js 的脱机方式
{: #offline_mode}

将 node.js 应用程序推送到 {{site.data.keyword.Bluemix}} 时，SDK for Node.js buildpack 通常会从外部资源下载工件，
例如从 NPM 下载节点模块。在某些情况下（例如，在 [Bluemix Dedicated](/docs/dedicated/index.html#dedicated)
和 [Bluemix Local](/docs/local/index.html#local) 中），您可能并不想对访问 Bluemix 外部站点有任何依赖，
或者您希望能够对访问这些外部站点有更明确的控制。  
{: shortdesc}

下面是 node.js buildpack 可以访问的外部站点。在 [Bluemix Dedicated](/docs/dedicated/index.html#dedicated)
和 [Bluemix Local](/docs/local/index.html#local) 等 Bluemix 环境中，可能需要将这些站点*列入白名单*。

* http://nodejs.org/，可用于查明可用的节点引擎版本。
* https://s3pository.heroku.com，用于检索该 buildpack 中未包含的节点引擎版本。
*  https://www.npmjs.com/package/npm 和 https://semver.herokuapp.com，用于检索该 buildpack 中未包含的 npm 版本。
* https://iojs.org，用于检索该 buildpack 中未包含且 https://semver.herokuapp.com 上未提供的旧版节点。
* https://registry.npmjs.org，用于检索节点模块，例如 express。

要尽可能缩小列入白名单的站点的集合，请将节点应用程序配置为使用 SDK for Node.js buildpack 中包含的节点引擎版本。有关该 buildpack 中包含的节点引擎版本集，请参阅[最新更新](./updates.html)。如果执行了此操作，那么下载节点模块时只需要有 https://registry.npmjs.org 站点即可。

请注意，安装了新版本的 SDK for Node.js buildpack 后，可用节点引擎版本集通常会升至更新的版本。这可能需要您重新配置节点应用程序，以指定更新的节点引擎版本。


## 脱机应用程序
{: #offline_applications}

为了消除访问 https://registry.npmjs.org 的需要，可以在应用程序中包含应用程序所需的所有节点模块。为此，请对应用程序所需的所有模块运行 **npm install**，并将生成的 *node_modules* 目录包含在推送的应用程序中。

请注意，依赖项中可以包含依赖项，而被包含的依赖项还可以包含依赖项，依此类推，但 package.json 只能包含顶层依赖项。如果某个依赖项使用了 package.json 中的某个范围，且该依赖项的新版本已发布，那么 node_modules 目录中的模块会变为过时。*shrinkwrap* 可帮助您锁定所有依赖项版本，避免发生上述情况。要使用 shrinkwrap，请首先清空或清除 node_modules 目录中的内容，然后在您项目的根目录中运行以下命令：
0. npm install
1. npm dedupe
2. npm shrinkwrap

这可能会更改您的 *package.json*，并将 *npm-shrinkwrap.json* 添加到您的根目录中。
每次对 *package.json* 文件中的依赖项进行更改后，都应重复 *dedupe* 和 *shringwrap* 步骤。

## 使用代理
{: #working_with_proxy}

在某些环境（如 [Bluemix Dedicated](/docs/dedicated/index.html#dedicated)
和 [Bluemix Local](/docs/local/index.html#local)）中，可以配置代理。
有关更多详细信息，请参阅[使用代理](/docs/manageapps/workingWithProxy.html)。
