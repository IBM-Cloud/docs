---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# SDK for Nodejs buildpack 的最新更新
{: #latest_updates}

sdk-for-nodejs buildpack 中最新更新的列表。

## 2017 年 3 月 10 日：更新了 Node.js buildpack V3.11
此 buildpack 发行版支持以下 IBM SDK for Node.js 运行时版本：0.10.47、0.10.48、0.12.17、0.12.18、4.7.3、4.8.0、6.9.5 和 6.10.0。现在的缺省版本为 4.8.0。

除了新运行时，此发行版还包含一个修订，用于解决使用 devconsole UI 启用 shell 应用程序管理处理程序时遇到的错误。此 buildpack 还更改了 Monitoring and Analytics 服务的自动配置工作方式。使用免费套餐的应用程序不再向其应用程序添加日志功能，此功能将替换为 logmet。

## 2017 年 1 月 20 日：更新了 Node.js buildpack V3.10
此 buildpack 发行版支持以下 IBM SDK for Node.js 运行时版本：0.10.47、0.10.48、0.12.17、0.12.18、4.7.0、4.7.2、6.9.2 和 6.9.4。现在的缺省版本为 4.7.2。

此发行版包含一个修订，用于解决不能每次都调用“npm start”来启动应用程序的错误。

## 2016 年 11 月 17 日：更新了 Node.js buildpack V3.9
此 buildpack 发行版支持以下 IBM SDK for Node.js 运行时版本：0.10.47、0.10.48、0.12.16、0.12.17、4.6.1、4.6.2、6.7.0 和 6.9.1。现在的缺省版本为 4.6.2。

请注意，2016 年 10 月 18 日 Node.js V6 已升级到 LTS 状态，不久将成为此 buildpack 的缺省运行时。Node.js V0.10 已于 2016 年 10 月 31 日到期，很快就不会再包含在此 buildpack 中。有关更多详细信息，请参阅 [Node.js version long-term support and the SDK for Node.js buildpack](https://www.ibm.com/blogs/bluemix/2016/11/node-version-support-and-sdk-buildpack/)。

在此发行版中解决了与 Node.js V6 一起使用时，影响跟踪和检验器“应用程序管理”处理程序的错误。有关 Node.js V6 集成了检验器功能后检验器处理程序有何变化的更多信息，请参阅[管理 Liberty 和 Node.js 应用程序](/docs/manageapps/app_mng.html#inspector)。

## 2016 年 10 月 7 日：更新了 Node.js buildpack V3.8-20161006-1211
此 buildpack 发行版支持以下 IBM SDK for Node.js 运行时版本：0.10.46、0.10.47、0.12.15、0.12.16、4.5.0、4.6.0、6.6.0 和 6.7.0。现在的缺省值为 4.6.0。

除了新运行时，此发行版还包含 buildpack 错误修订。使用 Node.js 6.x 和 V3.7-20160826-1101 发行版更新中提到的开发方式时已知问题的修订如下所示。此发行版还与 [Cloud Foundry Node.js buildpack V1.5.20](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.20) 同步。

## 2016 年 8 月 26 日：更新了 Node.js buildpack V3.7-20160826-1101
此 buildpack 发行版支持以下 IBM SDK for Node.js 运行时版本：0.10.45、0.10.46、0.12.14、0.12.15、4.4.7、4.5.0、6.2.2 和 6.4.0。现在的缺省值为 4.5.0。

此发行版包含错误修订，包括 [Cloud Foundry Node.js buildpack 1.5.18](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.18) 中的那些错误修订。

该发行版不再支持 strongpm 应用程序管理处理程序，如 [Bluemix Node.js Buildpack v3.3 – FIPS mode and more](https://developer.ibm.com/bluemix/2016/05/05/node-buildpack-update-fips-mode/) 中所声明。

请注意，使用 Node.js 6.x 和[开发方式](/docs/manageapps/app_mng.html#devmode)时存在一个已知问题。要解决该问题，您将需要在启用“开发方式”之后重新编译打包应用程序，然后才能开始使用。

## 2016 年 7 月 22 日：更新了 Node.js buildpack V3.6-20160715-0749
此 buildpack 发行版添加了以下 IBM SDK for Node.js 运行时版本：0.10.45、0.10.46、0.12.14、0.12.15、4.4.6、4.4.7、6.2.1 和 6.2.2。现在的缺省版本为 4.4.7。

此发行版包含更新的“应用程序管理”代理，该代理支持联合登录。

其中包含对以下安全漏洞的修订：
* [CVE-2016-1669](http://www-01.ibm.com/support/docview.wss?uid=swg21986383)

## 2016 年 6 月 22 日：更新了 Node.js buildpack V3.5-20160609-1608

此 buildpack 发行版添加了 IBM SDK for Node.js 运行时 V4.4.5 和 6.2.0。缺省版本变为 4.4.5。

该发行版不再支持如 [Bluemix Node.js Buildpack v3.3 – FIPS mode and more](https://developer.ibm.com/bluemix/2016/05/05/node-buildpack-update-fips-mode/) 中所声明的较旧版本的运行时。该 buildpack 现在支持 0.10.44、0.10.45、0.12.13、0.12.14、4.4.4、4.4.5、6.1.0 和 6.2.0。

此发行版包含 [Cloud Foundry’s Node.js buildpack 1.5.14](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.14) 中的错误修订。

## 2016 年 5 月 20 日：更新了 Node.js buildpack V3.4-20160518-1653

此 buildpack 发行版添加了 IBM SDK for Node.js 运行时 V0.10.45、0.12.14、4.4.4、6.0.0 和 6.1.0。现在的缺省值为 4.4.4。

其中包含对以下安全漏洞的修订：
* [CVE-2015-8855](http://www-01.ibm.com/support/docview.wss?uid=swg21982852)
* [CVE-2016-2108 CVE-2016-2107 CVE-2016-2105 CVE-2016-2106 CVE-2016-2109 CVE-2016-2176 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.openssl.org/news/secadv/20160503.txt)

请注意，npm V3 和“应用程序管理”检验器实用程序存在一个已知问题。npm 3.8.6 是 6.0.0 和 6.1.0 运行时的缺省值。如果想要使用其中任一 6.x 运行时与检验器实用程序，那么变通的方法是在 package.json 中指定 2.x npm 版本。

## 2016 年 4 月 29 日：更新了 Node.js buildpack V3.3-20160428-1409

此 buildpack 发行版添加了 IBM SDK for Node.js 运行时 V0.10.44、0.12.13、4.4.0、4.4.1、4.4.2 和 4.4.3。现在的缺省值为 4.4.3。
对于 4.3.1 及更高版本，现在可以通过为应用程序设置 `FIPS_MODE=true` 环境变量来使用已启用 FIPS 的运行时版本。

更新的 buildpack 和新的运行时版本还包含对以下安全漏洞的修订：
* [CVE-2016-2515](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-2537](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-3956](http://www-01.ibm.com/support/docview.wss?uid=swg21980827)

更新的 buildpack 还包含对以下错误的修订：
* 现在，只要 IBM SDK for Node.js 构建符合所请求的范围，将始终使用该构建。以前这只适用于 4.x 运行时版本。
* 现在“应用程序管理”检验器实用程序将与 4.x 运行时版本搭配使用。
* 修订了 strongpm“应用程序管理”实用程序中的回归。

## 2016 年 3 月 18 日：更新了 Node.js buildpack V3.2-20160315-1257

此 buildpack 发行版将缺省 IBM SDK for Node.js 运行时从 V4.3.0 移至 V4.3.2。此外，还包含 IBM SDK for Node.js V0.10.43、V0.12.12 和 V4.3.1。请使用这些最新的 Node.js 版本以获取针对几种安全漏洞的修订。

## 2016 年 3 月 4 日：更新了 Node.js buildpack V3.1-20160222-1123

此 buildpack 发行版将缺省 IBM SDK for Node.js 运行时从 V4.2.4 移至 V4.3.0。此外，还包含 IBM SDK for Node.js V0.10.42、V0.12.10 和 V4.2.6。请使用这些最新的 Node.js 版本以获取针对几种安全漏洞的修订。

## 2016 年 2 月 4 日：更新了 Node.js buildpack V3.0-20160125-1224

此发行版已与 [Cloud Foundry 社区 Node.js](https://github.com/cloudfoundry/nodejs-buildpack) buildpack 全面同步。除了社区更改外，还对某些缺省值进行了更改，为缩短编译打包时间而进行了优化，以及对“应用程序管理”功能进行了更新。

* Buildpack 更新

  * Node.js V4.2.4 (IBM SDK for Node.js V4) 现在替代 V0.12.9 成为 Bluemix 上的缺省运行时。如果没有为应用程序指定特定版本，那么此更改可能会导致应用程序行为不同。要了解如何为 Bluemix 应用程序指定 Node.js 版本，请参阅 [Node.js 运行时](index.html)文档。

  * 现在，缺省情况下，NODE_ENV 设置为 *production*。此更改将造成某些节点依赖项的行为不同。例如，对于发生故障的端点，Express 框架不会再在 Web 浏览器中返回堆栈跟踪，而是改为显示*内部服务器错误*。当 NPM_CONFIG_PRODUCTION 设置为 *true* 时，只有在 npm 安装阶段，NPM 会将子 shell 脚本的 NODE_ENV 设置为 *production*。此功能使用户可以将应用程序运行时的 NODE_ENV 设置为其他值，例如 *development*。为了清晰明确，npm 脚本将看到消息 **NODE_ENV=production**。

  * 包含了对 Monitoring and Analytics 服务的错误修订。

* 高速缓存更新：

  * 如果禁用了高速缓存 (NODE_MODULES_CACHE=false)，那么 buildpack 不会尝试对任何模块/组件进行高速缓存。先前此设置是这样的：高速缓存不会弹出，但仍会对已安装的模块进行高速缓存以用于未来部署。而现在，高速缓存既不会弹出，也不会尝试存储任何高速缓存。

  * 缺省情况下，除了 node_modules 以外，还会对 bower_components 进行高速缓存。

* 其他更新：

  * 针对缺少依赖项（例如，gulp、bower 和 angular）的情况添加了有用的警告。

  * 检测脚本已使用 buildpack 版本信息进行更新。

  * 除去了社区初始引入的集群建议 (WEB_CONCURRENCY)，因为在 Bluemix 上无法准确地确定内存。


## 2015 年 12 月 16 日：更新了 Node.js buildpack V2.8-20151209-1403 和 V3.0beta-20151211-2041

本发行版的 Node.js buildpack 提供了 2 个版本：V2.8 和 V3.0beta。这两个版本都包含以下更改：

针对 Monitoring and Analytics 服务的错误修订
包含 IBM SDK for Node.js V4.2.3.0、V4.2.2.0、V1.2.0.8 和 V1.2.0.7（分别基于社区 Node.js V4.2.3、V4.2.2、V0.12.9 和 V0.12.8）的高速缓存运行时。此外，在 V3.0beta 中，缺省 Node.js 运行时更改为 V4.2.3。

现在，IBM Node.js buildpack V3.0beta 在 Bluemix 上作为非缺省 buildpack 发布，而 Node.js V4.2.3 作为缺省运行时。要确保应用程序和服务继续在 Bluemix 上工作，请使用 beta 版本的 buildpack 推送应用程序。30 天或更长时间后，V3 将成为缺省 buildpack。

要使用 V3.0beta 推送应用程序：

* 使用“cf push”命令中的“-b”选项：


```
cf push -b sdk-for-nodejs-v3beta
```
{: codeblock}

* 或者在 manifest.yml 文件中使用“buildpack”选项：

```
buildpack: sdk-for-nodejs-v3beta
```
{: codeblock}

如果已在应用程序的 package.json 中配置特定版本的 Node.js，那么对缺省运行时进行此更改不会影响您的应用程序。

**注：**您可以始终指定要运行应用程序的 Node.js 版本，方法是如[可用版本](index.html#available_versions)中所述使用 package.json 中的 engines.node 条目。

## 2015 年 11 月 23 日：更新了 Node.js buildpack V2.7-20151118-1003

在 2.7 中包含了 IBM SDK for Node.js V4.2.1.0（基于 Node V4.2.1 LTS）。它还不是缺省值，但可以指定供使用。**注：**此版本将替换先前可用的开放式源代码构建版本。我们还对服务扩展框架进行了一些小的错误修订。

## 2015 年 10 月 19 日：更新了 Node.js buildpack V2.6.1-20151015-1326

Node.js V2.6.1 引入了对 [StrongPM 应用程序管理处理程序](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/)的错误修订，以及一致性更好的 NPM 版本。

## 2015 年 10 月 15 日：更新了 Node.js buildpack V2.6-20151006-1309

此发行版的 Node.js buildpack 的特点是将 [StrongLoop Process Manager ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://strong-pm.io) 集成到“应用程序管理”功能部件中。有关更多信息，请参阅博客帖子 [StrongLoop DevOps for Node.js Applications on Bluemix](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/)。

## 2015 年 6 月 15 日：更新了 Node.js buildpack V2.0-20150608-1503

在此发行版中，我们已将 Node.js buildpack 与最新的 [CF 社区 Node.js buildpack](https://github.com/cloudfoundry/nodejs-buildpack) 同步，这带来大量来自该社区的新功能。
此外，我们改进了 Node.js buildpack 中的“应用程序管理”功能，该功能启用 shell、node-inspector、Bluemix Live Sync 等实用程序。请参阅[应用程序管理](/docs/manageapps/app_mng.html)，以获取详细信息。

## 2015 年 5 月 5 日：更新了 Node.js buildpack V1.17-20150429-1033

* 该 Node.js buildpack 现在随 [IBM SDK for Node.js V0.12.1](https://developer.ibm.com/node/sdk/) 一起提供。
* 如果应用程序未在其 package.json 文件中指定运行时，那么现在应用程序将使用 V0.12.1 启动，而不使用 V0.10.x。如果需要使用先前的版本，请在 package.json 中指定 V0.10.x，如下所示。

```
"engines": {
"node": "0.10.x"
}
```
{: codeblock}

* V0.12.1 的已知问题：
   * 使用 Bluemix Live Sync 提供的“调试工具”功能时，“暂挂”功能会中断。
   * V0.12.x 上不支持用于 MQ Light 服务的 mqlight 模块

* 解决了各种安全漏洞：
  * 已修复 OpenSSL 中影响 IBM SDK for Node.js 的漏洞。更多详细信息在 [Security Bulletin](http://www-01.ibm.com/support/docview.wss?uid=swg21701494) 中提供。
  * 已修复 RC4 流密码中影响 IBM SDK for Node.js 的漏洞。更多详细信息在 [Security Bulletin](http://www-01.ibm.com/support/docview.wss?uid=swg21882778) 中提供。

##  2015 年 4 月 2 日：更新了 Node.js buildpack V1.15-20150331-2231

* 该 Node.js buildpack 现在包含三个新功能，可帮助您在 Bluemix 上快速进行开发，就像在桌面上操作一样，而无需重新部署
  * 桌面同步：将任何 (Windows) 桌面树同步到基于云的项目工作空间
  * 实时编辑：使您可以对在 Bluemix 中运行的 Node.js 应用程序执行更改，并立即在浏览器中对更改进行测试。
  * 调试：在环境中执行 Shell 并进行调试！您可以使用 Node Inspector 调试器来动态编辑代码、插入断点、单步执行代码、重新启动运行时等
  * 请参阅[应用程序管理](/docs/manageapps/app_mng.html#Utilities)，以获取更多信息。
* 我们已从 [Cloud Foundry 的 Node.js buildpack](https://github.com/cloudfoundry/nodejs-buildpack) 中拉入最新的更改。此更改带来该社区进行的大量错误修订和改进。
* 该 Node.js buildpack 现在随 [IBM SDK for Node.js V1.1.0.13](https://developer.ibm.com/node/sdk/) 一起提供。

## 2015 年 1 月 5 日：更新了 Node.js buildpack V1.9.1-20141208-1221

* 该 Node.js buildpack 现在包含动态日志设置支持。通过此支持，如果开发者的应用程序是使用 log4js、bunyan 或 ibmbluemix 模块进行日志记录，那么开发者可以动态更改其应用程序的日志级别。
* 该 Node.js buildpack 现在随 [IBM SDK for Node.js V0.10.33](https://developer.ibm.com/node/sdk/) 一起提供。此更新包含对 POODLE 问题的修订。

## 2014 年 10 月 23 日：更新了 Node.js buildpack V1.6-20141013-1736

* 该 Node.js buildpack 现在随 [IBM SDK for Node.js V1.1.0.8](https://developer.ibm.com/node/sdk/) 一起提供。此更新意味着在为应用程序指定最新稳定的 Node.js 运行时 V0.10.32 时，您将获取完全受支持的 IBM Node.js 运行时。此最新 SDK 随附一个修订，其解决了嵌入式 qs 模块导致拒绝服务的问题。还包含更新版本的 npm 模块以及对 http 和 url 模块的其他改进。有关更多详细信息，请参阅 [V0.10.32 更改日志](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog)。
* 该 buildpack 还包含一个修订，其解决了部署期间在客户的应用程序中添加不正确的 index.html 文件的错误。

## 2014 年 9 月 30 日：更新了 Node.js buildpack V1.4-20140908-1746

* 该 Node.js buildpack 现在随 [IBM SDK for Node.js V1.1.0.7](https://developer.ibm.com/node/sdk/) 一起提供。此更新意味着在为应用程序指定最新稳定的 Node.js 运行时 V0.10.31 时，您将获取完全受支持的 IBM Node.js 运行时。使用完全受支持的 Node.js 运行时，客户将获取一致的支持体验。
* 该 buildpack 包含改进的服务框架。具体而言，改进的服务框架在绑定 Monitoring and Analytics 服务时能更好地运行，并在服务发生故障时提供更多诊断信息。

## 2014 年 8 月 28 日：更新了 Node.js buildpack V1.3-20140821-1143

* 最新的 Node.js buildpack 现在随 IBM SDK for Node.js V1.1.0.6 一起提供。此更新意味着在为应用程序指定最新稳定的 Node.js 运行时 V0.10.30 时，您将获取完全受支持的 IBM Node.js 运行时。此运行时修订了 [V8 Memory Corruption 漏洞 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow)。
* 该 buildpack 还包含 Monitoring and Analytics 服务扩展的增强功能和错误修订，使您能够通过该服务诊断性能和错误状况。

## 2014 年 7 月 29 日：更新了 Node.js buildpack V1.1-20140717-1447

该 Node.js buildpack 现在随 IBM SDK for Node.js V1.1.0.5 一起提供。此更新意味着在为应用程序指定最新稳定的 Node.js 运行时 V0.10.29 时，您将获取完全受支持的 IBM Node.js 运行时。请参阅有关 [IBM Node.js SDK](https://developer.ibm.com/node/sdk/) 的更多信息。

# 相关链接
{: #rellinks notoc}
## 常规
{: #general notoc}
* [node.js 运行时](index.html)
