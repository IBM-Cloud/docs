---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# ビルドパックのサポートに関する記述
{: #buildpack_support_statement}

最終更新日: 2016 年 9 月 8 日
{: .last-updated}

## 組み込みの IBM ビルドパック
{: #built-in_ibm_buildpacks}

* [Liberty for Java](../runtimes/liberty/index.html)
* [SDK for Node.js](../runtimes/nodejs/index.html)
* [ASP.NET Core](../runtimes/dotnet/index.html)

IBM は、IBM が Bluemix 上で提供するランタイム・ビルドパックのそれぞれについて、2 つのバージョン (n & n - 1) をサポートします (例: IBM Liberty ビルドパック v1.22 & IBM Liberty ビルドパック v1.21)。各ビルドパックは、必要に応じて、対応するランタイムの 1 つ以上のメジャー・バージョンを提供し、サポートします (例: IBM SDK、Java Technology Edition バージョン 7 リリース 1 とバージョン 8)。通常、ビルドパックは、使用可能なランタイムの最新のマイナー・バージョンで 2 週間ごとにリフレッシュされます。上記のポリシーによって、デプロイされたすべてのランタイム・バージョンは、デプロイされてから少なくとも 1 カ月間サポートされることが保証されます。

Bluemix 上で現在サポートされているバージョンの組み込み IBM ビルドパックについて問題が報告される可能性がありますが、それらの問題は最新バージョンに対して検証される必要があります。欠陥が検出された場合、IBM は将来レベルのランタイムでのフィックスと、対応するビルドパックを提供します。IBM は、前のメジャー・バージョンおよびマイナー・バージョン (N-1、n-1) 用のフィックスは提供しません。IBM は、IBM ビルドパックを使用している場合でも (例えば、Liberty ビルドパックと共に Open JDK を使用している場合など)、コミュニティー・ランタイムをサポートすることはありません。これらのコミュニティー・ランタイムは、下記の『組み込みのコミュニティー・ビルドパック』に記述されているのと同じサポート・ポリシーに従います。

## 組み込みのコミュニティー・ビルドパック
{: #built-in_community_buildpacks}

以下の組み込みコミュニティー・ビルドパックが Cloud Foundry コミュニティーによって提供されています。

* [Java](../runtimes/tomcat/index.html)
* [Node.js](https://github.com/cloudfoundry/nodejs-buildpack)
* [PHP](../runtimes/php/index.html)
* [Ruby](../runtimes/ruby/index.html)
* [Python](../runtimes/python/index.html)
* [Go](../runtimes/go/index.html)

これらのビルドパックに対する更新は、Bluemix が Cloud Foundry の新バージョンにアップグレードされたときに行われます。Bluemix 上のこれらのランタイムでの問題を IBM に報告して、Bluemix がその問題の原因かどうかを判別するための支援を受けることができます。Bluemix に関連する問題であれば IBM はフィックスを提供しますが、ビルドパックまたはランタイム自体の欠陥の場合、IBM は問題を該当のコミュニティーに報告することを支援します。それらのビルドパックおよびランタイム用のフィックスを IBM が提供することはありません。

## 外部ビルドパック
{: #external_buildpacks}


IBM は外部ビルドパックのサポートを提供しません。サポートについては Cloud Foundry コミュニティーに問い合わせる必要があります。 


