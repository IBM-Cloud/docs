---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Buildpack 支持声明
{: #buildpack_support_statement}

上次更新时间：2016 年 9 月 8 日
{: .last-updated}

## 内置 IBM buildpack
{: #built-in_ibm_buildpacks}

* [Liberty for Java](../runtimes/liberty/index.html)
* [SDK for Node.js](../runtimes/nodejs/index.html)
* [ASP.NET 核心](../runtimes/dotnet/index.html)

IBM 在 Bluemix 上支持每个运行时 buildpack 的两个版本（n 和 n-1），例如 IBM Liberty Buildpack V1.22 和 IBM Liberty Buildpack V1.21）。每个 buildpack 将根据需要提供并支持其相应运行时的一个或多个主版本（例如，IBM SDK Java Technology Edition V7.1 和 V8）。Buildpack 通常将每两周使用可用的最新次版本运行时进行刷新。上述策略将确保任何部署的运行时版本在部署后至少会得到 1 个月的支持。

可以报告与 Bluemix 上当前支持的内置 IBM Buildpack 的任何版本的相关问题，但这些问题需要根据最新版本进行验证。如果发现缺陷，IBM 将在运行时的未来级别以及相应的 buildpack 中提供修订。IBM 不会对更低的主版本和次版本（N-1 和 n-1）提供修订。IBM 不会提供对社区运行时的支持，即便这些运行时使用 IBM buildpack（例如，将 Open JDK 与 Liberty buildpack 配合使用）也不例外。这些社区运行时遵循相同的支持政策，如下面的“内置社区 Buildpack”中所述。

## 内置社区 buildpack
{: #built-in_community_buildpacks}

Cloud Foundry 社区提供了以下内置社区 Buildpack：

* [Java](../runtimes/tomcat/index.html)
* [Node.js](https://github.com/cloudfoundry/nodejs-buildpack)
* [PHP](../runtimes/php/index.html)
* [Ruby](../runtimes/ruby/index.html)
* [Python](../runtimes/python/index.html)
* [Go](../runtimes/go/index.html)

Bluemix 升级到新版本的 Cloud Foundry 时，会对这些 buildpack 进行更新。使用 Bluemix 上的这些运行时时遇到的问题可以向 IBM 进行报告，我们将帮助确定是否 Bluemix 是导致问题的根源。对于与 Bluemix 相关的问题，IBM 将提供修订，但是对于 buildpack 或运行时本身的缺陷，IBM 将帮助向相应的社区进行报告。IBM 不会对这些 buildpack 和运行时提供修订。

## 外部 buildpack
{: #external_buildpacks}


对于外部 buildpack，IBM 不会提供支持。您可能需要联系 Cloud Foundry 社区来获取支持。 


