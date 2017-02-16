---

copyright:
  years: 2016, 2017
lastupdated: "2016-07-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# プロキシーの操作
{: #working_with_proxy}



[Bluemix Dedicated](/docs/dedicated/index.html#dedicated) や
[Bluemix Local](/docs/local/index.html#local) などの一部の環境では、ステージングおよび実行時のアプリケーションの動作に影響するプロキシーを構成できます。

プロキシーで動作するようにアプリケーションを構成するには、以下の環境変数を使用できます。
  * [http_proxy](https://docs.cloudfoundry.org/buildpacks/proxy-usage.html)
  * [https_proxy](https://docs.cloudfoundry.org/buildpacks/proxy-usage.html)
  * [no_proxy](http://www.gnu.org/software/wget/manual/html_node/Proxies.html)

これらの環境変数は、*cf se* を使用して、または *manifest.yml* ファイルで設定できます。ステージングでインターネットからリソースをダウンロードすることがアプリケーションで要求されていて、
プロキシー環境変数が設定されている場合、プロキシー環境変数の構成方法に応じて、構成されたプロキシーでリソースはダウンロードされます。

例えば、nodejs アプリケーションがあって、*http_proxy* を *yourProxyURL* に設定した環境で稼働しているとします。さらに、npm がインターネットからノード・モジュールをダウンロードできるようにしたいとします。これを行うには、
*no_proxy* を *npmjs.org* に設定します。

**注**: アプリケーションが実行時にプロキシーを利用することがあります。これは完全にアプリケーションに依存し、
ビルドパックやこれらの 3 つの環境変数の影響は受けません。

## Java アプリケーション
{: #java_apps}

[Liberty for Java](/docs/runtimes/liberty/index.html) および [java_buildpack](/docs/runtimes/tomcat/index.html) アプリケーションでは、**JAVA_OPTS** 環境変数でプロキシー設定をランタイムに渡すことができます。例えば、以下のコマンドを実行します。
```
   $ cf se myApp JAVA_OPTS "-Dhttp.proxyHost=yourProxyURL -Dhttp.proxyPort=yourProxyPort"
```
{: codeblock}

その後、アプリケーションを再ステージングします。これにより、アプリケーションは、指定されたプロキシー設定を実行時に使用します。Java プロキシー・オプションについて詳しくは、[「Java Networking and Proxies」](https://docs.oracle.com/javase/8/docs/technotes/guides/net/proxies.html)を参照してください。

# 関連リンク
{: #rellinks}
## 一般
{: #general}
* [Liberty for Java](/docs/runtimes/liberty/index.html)
* [SDK for Nodejs](/docs/runtimes/nodejs/index.html)
