---

copyright:
  years: 2016
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Liberty のオフライン・モード
{: #offline_mode}

Liberty アプリケーションが {{site.data.keyword.Bluemix}} にプッシュされると、Liberty ビルドパックは Bluemix の外部のサイトにアクセスして、アプリケーションに必要な成果物を取得できます。Liberty ビルドパックによるアクセスが可能な外部サイトを以下に示します。[Bluemix Dedicated](/docs/dedicated/index.html#dedicated) および [Bluemix Local](/docs/local/index.html#local) の環境では、これらのサイトは*ホワイトリスト*に登録されていることが必要な場合があります。

* https://download.run.pivotal.io および https://java-buildpack.cloudfoundry.org を使用して、以下を対象とするコンポーネントにアクセスします。
  * [AppDynamics エージェント](https://www.appdynamics.com/)
  * [MariaDB JDBC ドライバー](https://mariadb.com/)
  * [New Relic エージェント](newRelic.html)
  * [OpenJDK](customizingJRE.html#OpenJDK)
  * [PostgreSQL JDBC ドライバー](https://www.postgresql.org)
* https://dl.zeroturnaround.com/jrebel/ を使用して、[JRebel](https://zeroturnaround.com/software/jrebel/) のコンポーネントにアクセスします。
* https://download.ruxit.com/agent/paas/cloudfoundry/java を使用して、[Dynatrace Ruxit エージェント](dynatrace.html)のコンポーネントにアクセスします。
* http://downloads.dynatracesaas.com/cloudfoundry/buildpack/java/ を使用して、[Dynatrace エージェント](dynatrace.html)のコンポーネントにアクセスします。

## プロキシーの処理
{: #working_with_proxy}

[Bluemix Dedicated](/docs/dedicated/index.html#dedicated) および [Bluemix Local](/docs/local/index.html#local) などの一部の環境では、プロキシーの構成が可能です。詳しくは、[『プロキシーの処理』](/docs/manageapps/workingWithProxy.html)を参照してください。

# 関連リンク
{: #rellinks}
## 一般
{: #general}
* [Liberty ランタイム](index.html)
* [Liberty プロファイル概要](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
