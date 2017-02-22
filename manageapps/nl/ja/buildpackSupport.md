---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# ビルドパックのサポートに関する記述
{: #buildpack_support_statement}


## 組み込みの IBM ビルドパック
{: #built-in_ibm_buildpacks}

[Liberty for Java](/docs/runtimes/liberty/index.html)、[SDK for Node.js](/docs/runtimes/nodejs/index.html)、および [ASP.NET Core](/docs/runtimes/dotnet/index.html) については、IBM は 2 つのバージョン (n & n - 1) (例えば、IBM Liberty Buildpack v1.22 & IBM Liberty Buildpack v1.21) をサポートします。
各ビルドパックは、必要に応じて、対応するランタイムの 1 つ以上のメジャ
ー・バージョンを提供し、サポートします (例えば IBM SDK, Java Technology Edition バージョン 7 リリース 1 とバージョン 8)。ビルドパックは通常、使用可能なランタイムの最新のマイナー・バージョンを使用して、1 カ月に 1 回更新されます。

[IBM Bluemix Runtime for Swift](/docs/runtimes/swift/index.html) については、IBM は、[Swift.org](http://swift.org) で使用可能な Swift の最新バージョンに適合したビルドパックのサポートを提供します。ビルドパックに対する更新は、Swift の使用可能な最新リリース・バージョンに合わせて行われます。

{{site.data.keyword.Bluemix_notm}} 上で現在サポートされているバージョンの組み込み IBM ビルドパックについて問題が報告される可能性がありますが、それらの問題は最新バージョンに対して検証される必要があります。欠陥が検出された場合、IBM は将来レベルのランタイムでのフィックスと、対応するビルドパックを提供します。IBM は、前のメジャー・バージョンおよびマイナー・バージョン (N-1、n-1) 用のフィックスは提供しません。IBM は、IBM ビルドパックを使用している場合でも (例えば、Liberty ビルドパックと共に Open JDK を使用している場合など)、コミュニティー・ランタイムをサポートすることはありません。これらのコミュニティー・ランタイムは、下記の『組み込みのコミュニティー・ビルドパック』に記述されているのと同じサポート・ポリシーに従います。

## 組み込みのコミュニティー・ビルドパック
{: #built-in_community_buildpacks}

以下の組み込みコミュニティー・ビルドパックが Cloud Foundry コミュニティーによって提供されています。

* [Java](/docs/runtimes/tomcat/index.html)
* [Node.js](https://github.com/cloudfoundry/nodejs-buildpack)
* [PHP](/docs/runtimes/php/index.html)
* [Ruby](/docs/runtimes/ruby/index.html)
* [Python](/docs/runtimes/python/index.html)
* [Go](/docs/runtimes/go/index.html)

これらのビルドパックに対する更新は、{{site.data.keyword.Bluemix_notm}} が Cloud Foundry の新バージョンにアップグレードされたときに行われます。{{site.data.keyword.Bluemix_notm}} 上のこれらのランタイムでの問題を IBM に報告して、{{site.data.keyword.Bluemix_notm}} がその問題の原因かどうかを判別するための支援を受けることができます。{{site.data.keyword.Bluemix_notm}} に関連する問題であれば IBM はフィックスを提供しますが、ビルドパックまたはランタイム自体の欠陥の場合、IBM は問題を該当のコミュニティーに報告することを支援します。それらのビルドパックおよびランタイム用のフィックスを IBM が提供することはありません。

## 外部ビルドパック
{: #external_buildpacks}


IBM は外部ビルドパックのサポートを提供しません。サポートについては Cloud Foundry コミュニティーに問い合わせる必要があります。
