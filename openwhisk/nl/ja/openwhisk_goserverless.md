---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# OpenWhisk と Serverless Framework の統合
{: #openwhisk_goserverless}

[Serverless Framework](https://serverless.com/) はサーバーレス・アプリケーションを構築するためのオープン・ソース・フレームワークです。シンプルなマニフェスト・ファイルを使用して、開発者はサーバーレス機能を定義し、それらをイベント・ソースに接続して、アプリケーションに必要なクラウド・サービスを宣言することができます。このフレームワークは、こうしたサーバーレス・アプリケーションのクラウド・プロバイダーへのデプロイを処理します。また、開発者による実動サービスのモニター、更新のロールアウト、および問題デバッグの支援も可能にします。また、フレームワークの機能を拡張するサード・パーティー・プラグインの活力あるエコシステムもあります。ここに、OpenWhisk がかかわっています。
{:shortdesc}

OpenWhisk には、[Serverless Framework 向けの固有のプロバイダー・プラグイン](https://github.com/serverless/serverless-openwhisk)があります。Serverless Framework を使用する開発者は、アプリケーションを任意の OpenWhisk プラットフォーム・インスタンス (Bluemix、あるいは他のクラウドまたはプライベートでホスト) にデプロイすることを選択できます。マルチ・プロバイダー・サポートにより、プラットフォーム間でアプリケーションをさらに容易に移動でき、開発者がマルチ・クラウドのサーバーレス・アプリケーションを開発できることになります。

## 開始
{: #openwhisk_goserverless_starting}

Serverless Framework の公式的な [OpenWhisk 向け入門ガイド](https://serverless.com/framework/docs/providers/openwhisk/guide/intro/)があります。これには、インストール、開発ワークフロー、ベスト・プラクティス、動作する OpenWhisk アプリケーションのビルドおよびデプロイの詳細手順ガイドなどが含まれています。

OpenWhisk プロバイダー・プラグインで Serverless Framework を使用する方法について説明した[ビデオ](https://youtu.be/GJY10W98Itc)があります。
## 文書
{: #openwhisk_goserverless_docs}

Serverless Framework で OpenWhisk を使用する方法の最新資料については、[該当サイトを参照してください](https://serverless.com/framework/docs/providers/openwhisk/)。
## サンプル
{: #openwhisk_goserverless_samples}
[Serverless Framework のサンプル GitHub リポジトリー](https://github.com/serverless/examples)では、OpenWhisk による HTTP API、cron ベース・スケジューラー、チェーン機能、その他の作成方法が示されています。
