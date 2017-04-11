---

copyright:
  years: 2016, 2017
lastupdated: "2016-07-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 使用代理
{: #working_with_proxy}



在某些环境中，例如 [Bluemix Dedicated](/docs/dedicated/index.html#dedicated) 和
[Bluemix Local](/docs/local/index.html#local)，可以对代理进行设置，
以影响应用程序在编译打包和运行时的行为。

您可以使用以下环境变量，对应用程序进行配置，以使用代理：
  * [http_proxy](https://docs.cloudfoundry.org/buildpacks/proxy-usage.html)
  * [https_proxy](https://docs.cloudfoundry.org/buildpacks/proxy-usage.html)
  * [no_proxy](http://www.gnu.org/software/wget/manual/html_node/Proxies.html)

您可以使用 *cf se* 或通过 *manifest.yml* 文件来设置这些环境变量。如果您的应用程序在编译打包期间需要从因特网下载资源，且已设置代理环境变量，那么根据代理环境变量的设置方式，您的资源将通过所配置的代理下载。


例如，假设您具有 nodejs 应用程序且在 *http_proxy* 设置为 *yourProxyURL* 的环境中运行。再假设您想要允许 npm 从因特网下载节点模块。要达成此目的，您可以将 *no_proxy* 设置为 *npmjs.org*。

**注**：可能会出现应用程序在运行时利用代理的情况。这完全依赖于应用程序，且不受 buildpack 和以下三个环境变量中任何一个的影响。


## Java 应用程序
{: #java_apps}

对于 [Liberty for Java](/docs/runtimes/liberty/index.html) 和 [java_buildpack](/docs/runtimes/tomcat/index.html) 应用程序，可以通过 **JAVA_OPTS** 环境变量将代理设置传递给运行时。例如，可以发出以下命令：
```
   $ cf se myApp JAVA_OPTS "-Dhttp.proxyHost=yourProxyURL -Dhttp.proxyPort=yourProxyPort"
```
{: codeblock}

并重新编译打包应用程序。应用程序随后将在运行时使用指定的代理设置。有关 Java 代理选项的更多信息，请参阅 [Java 联网和代理](https://docs.oracle.com/javase/8/docs/technotes/guides/net/proxies.html)。

# rellinks
{: #rellinks notoc}
## general
{: #general}
* [Liberty for Java](/docs/runtimes/liberty/index.html)
* [SDK for Nodejs](/docs/runtimes/nodejs/index.html)
