---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty for Java
{: #liberty_runtime}

{{site.data.keyword.Bluemix}} の Java アプリケーション用 Liberty には liberty-for-java ビルドパックが採用されています。liberty-for-java ビルドパックは、Liberty プロファイルに加えて、Java EE 7 アプリケーションおよび OSGi アプリケーションを実行するための完全なランタイム環境を提供します。また、Spring のような一般的なフレームワークをサポートし、IBM JRE を含んでいます。WebSphere Liberty は素早いアプリケーション開発を可能にし、これはクラウドによく適しています。
{: shortdesc}

## 検出
{: #detection}
Liberty ビルドパックは、以下のような種類のアプリケーションがデプロイされた場合に使用されます。
* [WAR ファイル](optionsForPushing.html#stand_alone_apps)
* [EAR ファイル](optionsForPushing.html#stand_alone_apps)
* [Liberty サーバー・ディレクトリー](optionsForPushing.html#server_directory)
* [パッケージされた Liberty サーバー](optionsForPushing.html#packaged_server)
* Java メイン
* [Distzip](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/container-distZip.md)

## スターター・アプリケーション
{: #starter_application}
{{site.data.keyword.Bluemix}} には、いくつかの Liberty スターター・アプリケーションが用意されています。Liberty スターター・アプリケーションは、使用可能なテンプレートを提供する、シンプルな Liberty アプリケーションです。スターター・アプリケーションを試し、Bluemix 環境に対して変更を行い、プッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](/docs/cfapps/starter_app_usage.html)を参照してください。

# 関連リンク
{: #rellinks notoc}
## 一般
{: #general notoc}
* [Liberty プロファイル概要](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
* [Liberty アプリケーションの管理](/docs/manageapps/app_mng.html#Utilities)
* [IBM Eclipse Tools for Bluemix を使用したアプリのデプロイ](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools)
* [IBM Monitoring and Analytics for Bluemix サービス概説](/docs/services/monana/index.html#monana_oview)

