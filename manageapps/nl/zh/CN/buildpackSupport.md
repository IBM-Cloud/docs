---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Buildpack 支持声明
{: #buildpack_support_statement}


## 内置 IBM buildpack
{: #built-in_ibm_buildpacks}

对于 [Liberty for Java](/docs/runtimes/liberty/index.html)、[SDK for Node.js](/docs/runtimes/nodejs/index.html) 和 [ASP.NET Core](/docs/runtimes/dotnet/index.html)，IBM 将支持两个版本（n 和 n-1），例如 IBM Liberty Buildpack V1.22 和 IBM Liberty Buildpack V1.21。每个 buildpack 将根据需要提供并支持其相应运行时的一个或多个主版本（例如，IBM SDK Java Technology Edition V7.1 和 V8）。通常，每月会使用可用的运行时最新次版本对 buildpack 刷新一次。

对于 [IBM Bluemix Runtime for Swift](/docs/runtimes/swift/index.html)，IBM 将支持与 [Swift.org](http://swift.org) 上提供的最新版本 Swift 匹配的 buildpack。对 buildpack 的更新将与发布的最新可用版本的 Swift 同步。

可以报告 {{site.data.keyword.Bluemix_notm}} 上当前支持的内置 IBM Buildpack 的任何版本的相关问题，但这些问题需要根据最新版本进行验证。如果发现缺陷，IBM 将在运行时的未来级别以及相应的 buildpack 中提供修订。IBM 不会对更低的主版本和次版本（N-1 和 n-1）提供修订。IBM 不会提供对社区运行时的支持，即便这些运行时使用 IBM buildpack（例如，将 Open JDK 与 Liberty buildpack 配合使用）也不例外。这些社区运行时遵循相同的支持政策，如下面的“内置社区 Buildpack”中所述。

## 内置社区 buildpack
{: #built-in_community_buildpacks}

Cloud Foundry 社区提供了以下内置社区 Buildpack：

* [Java](/docs/runtimes/tomcat/index.html)
* [Node.js](https://github.com/cloudfoundry/nodejs-buildpack)
* [PHP](/docs/runtimes/php/index.html)
* [Ruby](/docs/runtimes/ruby/index.html)
* [Python](/docs/runtimes/python/index.html)
* [Go](/docs/runtimes/go/index.html)

{{site.data.keyword.Bluemix_notm}} 升级到新版本的 Cloud Foundry 时，会对这些 buildpack 进行更新。使用 {{site.data.keyword.Bluemix_notm}} 上的这些运行时所遇到的问题可以向 IBM 报告，我们将帮助确定 {{site.data.keyword.Bluemix_notm}} 是否为导致问题的根源。对于与 {{site.data.keyword.Bluemix_notm}} 相关的问题，IBM 将提供修订，但是对于 buildpack 或运行时本身的缺陷，IBM 将帮助向相应的社区进行报告。IBM 不会对这些 buildpack 和运行时提供修订。

## 外部 buildpack
{: #external_buildpacks}


对于外部 buildpack，IBM 不会提供支持。您可能需要联系 Cloud Foundry 社区来获取支持。
