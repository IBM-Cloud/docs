---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 建置套件支援陳述式
{: #buildpack_support_statement}

前次更新：2016 年 9 月 8 日
{: .last-updated}

## 內建 IBM 建置套件
{: #built-in_ibm_buildpacks}

* [Liberty for Java](../runtimes/liberty/index.html)
* [SDK for Node.js](../runtimes/nodejs/index.html)
* [ASP.NET Core](../runtimes/dotnet/index.html)

IBM 將支援它在 Bluemix 上提供之每一個運行環境建置套件的兩個版本（n 及 n - 1）（例如 IBM Liberty 建置套件 1.22 版及 IBM Liberty 建置套件 1.21 版）。每一個建置套件都會視情況提供及支援其對應運行環境的一個以上主要版本（例如 IBM SDK、Java Technology Edition 7.1 版及第 8 版）。一般會每隔兩週使用可用運行環境的最新次要版本來重新整理建置套件。上述原則確保任何已部署的運行環境版本從部署時開始算起至少支援 1 個月。

可以報告 Bluemix 上目前所支援之任何內建「IBM 建置套件」版本的問題，不過，需要針對最新版本來驗證它們。如果發現問題，IBM 將提供運行環境及對應建置套件之未來層次的修正程式。IBM 不會提供較舊的主要版本及次要版本（N-1、n-1）的修正程式。IBM 將不支援社群運行環境，即使使用 IBM 建置套件時也是一樣（例如，搭配使用 Open JDK 與 Liberty 建置套件）。這些社群運行環境所遵循的支援原則與下面的「內建社群建置套件」相同。

## 內建社群建置套件
{: #built-in_community_buildpacks}

「Cloud Foundry 社群」提供下列內建「社群建置套件」：

* [Java](../runtimes/tomcat/index.html)
* [Node.js](https://github.com/cloudfoundry/nodejs-buildpack)
* [PHP](../runtimes/php/index.html)
* [Ruby](../runtimes/ruby/index.html)
* [Python](../runtimes/python/index.html)
* [Go](../runtimes/go/index.html)

將 Bluemix 升級至新版本的 Cloud Foundry 時，將不會更新這些建置套件。Bluemix 上這些運行環境的問題可以報告給 IBM，而我們將協助判定 Bluemix 是否為問題來源。若為 Bluemix 相關問題，IBM 將提供修正程式，不過，若為建置套件或運行環境本身的問題，IBM 會協助將它們報告給適當的社群。IBM 不會提供這些建置套件及運行環境的修正程式。

## 外部建置套件
{: #external_buildpacks}


對於外部建置套件，IBM 不提供支援。您可能需要聯絡「Cloud Foundry 社群」以獲得支援。 


