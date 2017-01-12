---

copyright:
  years: 2016
lastupdated: "2016-10-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 빌드팩 지원 구문
{: #buildpack_support_statement}


## 기본 제공 IBM 빌드팩
{: #built-in_ibm_buildpacks}

[Liberty for Java](/docs/runtimes/liberty/index.html), [SDK for Node.js](/docs/runtimes/nodejs/index.html) 및 [ASP.NET Core](/docs/runtimes/dotnet/index.html)의 경우, IBM은 두 버전(n 및 n - 1)을 지원합니다(예: IBM Liberty Buildpack v1.22 및 IBM Liberty Buildpack v1.21).
각 빌드팩은 그에 해당하는 런타임의 주 버전을 필요에 따라 하나 이상 제공하고 지원합니다(예: IBM SDK, Java Technology Edition 버전 7 릴리스 1 및 버전 8). 빌드팩은 일반적으로 한 달에 한 번 사용 가능한 런타임의 최신 부 버전으로 새로 고쳐집니다.  

[IBM Bluemix Runtime for Swift](/docs/runtimes/swift/index.html)의 경우 IBM은 [Swift.org](http://swift.org)에서 사용 가능한 Swift의 최신 버전과 일치하는 빌드팩에 대한 지원을 제공합니다. 빌드팩에 대한 업데이트는 사용 가능한 최신 Swift 릴리스 버전과 일치합니다. 

{{site.data.keyword.Bluemix_notm}}에서 현재 지원되는 기본 제공 IBM 빌드팩의 어느 버전에 대해서든 문제점을 보고할 수 있지만, 최신 버전에 대해 해당 문제점을 확인해야 합니다. 결함이 발견되면 IBM은 이후 레벨의 런타임 및 해당 빌드팩에서 수정사항을 제공합니다. IBM은 이전 주 버전 및 부 버전(N-1, n-1)에 대해서는 수정사항을 제공하지 않습니다. IBM은 IBM 빌드팩을 사용하는 경우에도(예를 들어, Liberty 빌드팩이 있는 Open JDK를 사용하는 경우) 커뮤니티 런타임에 대한 지원은 제공하지 않습니다. 이러한 커뮤니티 런타임은 아래의 "기본 제공 커뮤니티 빌드팩"과 동일한 지원 정책을 따릅니다. 

## 기본 제공 커뮤니티 빌드팩
{: #built-in_community_buildpacks}

Cloud Foundry 커뮤니티에서는 다음 기본 제공 커뮤니티 빌드팩을 제공합니다. 

* [Java](/docs/runtimes/tomcat/index.html)
* [Node.js](https://github.com/cloudfoundry/nodejs-buildpack)
* [PHP](/docs/runtimes/php/index.html)
* [Ruby](/docs/runtimes/ruby/index.html)
* [Python](/docs/runtimes/python/index.html)
* [Go](/docs/runtimes/go/index.html)

{{site.data.keyword.Bluemix_notm}}를 새 버전의 Cloud Foundry로 업그레이드하면 이러한 빌드팩이 업데이트됩니다. {{site.data.keyword.Bluemix_notm}}에서 발생하는 이러한 런타임 관련 문제점을 IBM에 보고할 수 있으며 IBM에서는 {{site.data.keyword.Bluemix_notm}}가 문제점의 원인인지 판별하는 데 도움을 줍니다. {{site.data.keyword.Bluemix_notm}} 관련 문제점인 경우 IBM은 수정사항을 제공하지만, 빌드팩 또는 런타임 자체의 결함인 경우 IBM은 적절한 커뮤니티에 결함을 보고하는 데 도움을 줍니다. IBM은 이러한 빌드팩 및 런타임에 대한 수정사항은 제공하지 않습니다. 

## 외부 빌드팩
{: #external_buildpacks}


외부 빌드팩에 대해서는 IBM에서 지원을 제공하지 않습니다. 지원을 원하는 경우 Cloud Foundry 커뮤니티에 문의해야 합니다. 
