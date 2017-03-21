---

copyright:
  years: 2016, 2017
lastupdated: "2016-07-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 使用 Proxy
{: #working_with_proxy}



在部分環境（例如 [Bluemix 專用](/docs/dedicated/index.html#dedicated)及
[Bluemix 本端](/docs/local/index.html#local)）中，配置的 Proxy 可能會影響應用程式在編譯打包期間及執行時的行為。

您可以配置應用程式使用下列環境變數來使用 Proxy：
  * [http_proxy](https://docs.cloudfoundry.org/buildpacks/proxy-usage.html)
  * [https_proxy](https://docs.cloudfoundry.org/buildpacks/proxy-usage.html)
  * [no_proxy](http://www.gnu.org/software/wget/manual/html_node/Proxies.html)

您可以使用 *cf se* 或透過 *manifest.yml* 檔案來設定這些環境變數。如果您的應用程式需要在編譯打包期間從網際網路下載資源，並且已設定 Proxy 環境變數，則會根據 Proxy 環境變數的配置方式，透過所配置的 Proxy 來下載資源。

例如，假設您有 nodejs 應用程式，並且在 *http_proxy* 設為 *yourProxyURL* 的環境中執行。此外，假設您要容許 npm 從網際網路下載 node 模組。作法是將 *no_proxy* 設為 *npmjs.org*。

**附註**：在執行時，您的應用程式可能會運用 Proxy。這完全與應用程式相依，且不受建置套件及這三個環境變數中的任何一個所影響。

## Java 應用程式
{: #java_apps}

若為 [Liberty for Java](/docs/runtimes/liberty/index.html) 及 [java_buildpack](/docs/runtimes/tomcat/index.html) 應用程式，可以透過 **JAVA_OPTS** 環境變數將 Proxy 設定傳遞給運行環境。例如，您可以發出指令：
```
   $ cf se myApp JAVA_OPTS "-Dhttp.proxyHost=yourProxyURL -Dhttp.proxyPort=yourProxyPort"
```
{: codeblock}

並且重新編譯打包應用程式。然後，您的應用程式就會在執行時使用指定的 Proxy 設定。如需 Java Proxy 選項的相關資訊，請參閱 [Java 網路及 Proxy](https://docs.oracle.com/javase/8/docs/technotes/guides/net/proxies.html)。

# rellinks
{: #rellinks notoc}
## general
{: #general}
* [Liberty for Java](/docs/runtimes/liberty/index.html)
* [SDK for Nodejs](/docs/runtimes/nodejs/index.html)
