---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# IBM {{site.data.keyword.blockchain}} の使用開始にあたって
{: #gettingstartedtemplate}
最終更新日: 2016 年 10 月 13 日
{: .last-updated}

**重要:** Starter Developer プラン (ベータ版) または High Security Business Network プラン (GA) のいずれかを使用する前に、[理解している必要のあること](needtoknow.html)で技術情報およびサポート情報を読む必要があります。
<br><br>

## オファリング・プランの状況

Starter Developer プランはベータ版で、マルチテナント開発環境を提供します。High Security Business Network プランは、2016 年 10 月 20 日に正式版 (GA リリース) になりました。High Security Business Network プランは、[IBM Secure Service Container](etn_ssc.html) を使用したコード分離機能を備えた、高度にセキュアな単一テナントの LinuxONE on z 環境を提供します。
<br><br>

## IBM Blockchain on Bluemix

Bluemix&reg; の {{site.data.keyword.blockchainfull}} サービスでは、1 つのボタンをクリックするだけで、4 ノードの開発およびテスト用のブロックチェーン・ネットワークを配信できます。開発者は、ブロックチェーン・ネットワークを初めから作成しなくても、すぐにアプリケーションを作成して、チェーンコードをデプロイすることができます。IBM Blockchain on Bluemix サービスは、ピアツーピアの許可されたネットワークであり、Linux Foundation Hyperledger Project の [Hyperledger Fabric v0.5](https://github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview) コードの上に作成されています。{:shortdesc}

ブロックチェーン・ネットワークは、デジタル資産をセキュアかつ効率的に交換および追跡し、すべてのトランザクションを共有台帳に永続的に記録するために使用されます。ブロックチェーンについて詳しくは、『[ブロックチェーンについて](ibmblockchain_overview.html)』のトピックを参照してください。
<br><br>

## ネットワーク・プランの選択

2 つの IBM Blockchain on Bluemix プランから選択できます。**Starter Developer Network** または **High Security Business Network** です。下の比較グラフを使用して、自分に適した環境を選択します。

<!-- Commenting our for move to GA status jh 10/07/16
![](images/red_alert.png)  **The High Security Business Network** plan is a limited Beta offering; to select this plan, you must first request preapproval at [IBM Blockchain on IBM Bluemix](http://www-stage.watson.ibm.com/files/blockchain/bluemix.html). -->

| Bluemix プラン:      | Starter Developer Network       | High Security Business Network| ------------------------- |:--------------------------:|:-----:|
| 状況:    | ベータ版     | GA |
| 目的:  |  開発、およびテスト (セキュリティー・レベル、パフォーマンス、可用性) |  エンタープライズ・ネットワークのシミュレート、およびテスト (セキュリティー・レベル、パフォーマンス、可用性) |
| ノード:    | 4 ノード + 認証局     | 4 ノード + 認証局 |
| [ダッシュボード・モニター:](ibmblockchainmonitor.html) | はい | はい |
| 機密トランザクション: | はい | はい |
| [コンセンサス:](etn_pbft.html) | PBFT | PBFT |
| 環境:     | 共有されるマルチテナント | 分離された単一テナント |
| [IBM Secure Service Container:](etn_ssc.html) | いいえ | はい |

<br>
## ネットワーク・プランの起動

以下の手順を使用して、ブロックチェーン・ネットワークのアンバインドされたサービス・インスタンスを作成してデプロイします。ネットワークには、検証ノードとセキュリティー・サービスを備えた開発環境が含まれており、チェーンコードをデプロイし、ログを表示し、アプリケーションを作成することができます。

1. [{{site.data.keyword.blockchain}}「サービス」](https://console.ng.bluemix.net/catalog/services/blockchain/)ページで、右側の**「サービスの追加」**フォームに入力します。
  - **スペース:** **「dev」**を選択します。
  - **アプリ:** **「アンバインドのまま」**を選択するか、サービスを Bluemix.org アプリケーションのいずれかにバインドします。**アプリケーションを選択します**。
  - **サービス名:** 固有の名前または値を入力します。例、**Blockchain Test Net123**。
  - **資格情報名:** デフォルト値のまま。
  - **選択済みプラン:** **Starter Developer** または **High Security** を選択します。
  - **「作成」**ボタンをクリックします。
2.  これで、新規サービスの**「サービス・ダッシュボード」**画面が表示されます。ここで、ネットワークのインスタンスを**管理**します。**「起動」**をクリックしてブロックチェーン・モニターを使用します。
3.  ブロックチェーン・モニターはネットワークの詳細、ライブ・ログ、現在の台帳の状態、API、チェーンコード・テンプレートを表示します。以下のいずれかの機能を実行するためにダッシュボードを使用します。
  - ネットワーク・ピアのディスカバリーや API のルートにアクセスします。
  - 実行中のチェーンコード・コンテナーを表示します。
  - リアルタイム・ログを表示し、チェーンコードをトラブルシューティングします。
  - 台帳のワールド・ステートを表示します。
  - Swagger UI にアクセスし、REST API を介してネットワークと対話します。
  - 3 つのチェーンコード例のいずれかをデプロイします。


# 関連リンク
{: #rellinks}
## チュートリアルとサンプル
{: #samples}
* [IBM Marbles デモ (GitHub)](https://github.com/IBM-Blockchain/marbles)
* [IBM Commercial Paper デモ (GitHub)](https://github.com/IBM-Blockchain/cp-web#readme)
* [IBM Car Lease デモ (Github)](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md)
* [Art Auction デモ (Github)](https://github.com/ITPeople-Blockchain/auction)

## API リファレンス
{: #api}
* [Swagger UI](https://obc-service-broker-staging.stage1.mybluemix.net/swagger)
* [Hyperledger fabric API (GitHub)](https://github.com/hyperledger/fabric/tree/master/docs/API)
* [HFC SDK for Node.js](https://github.com/hyperledger/fabric/tree/master/sdk/node)

## 関連リンク
{: #general}
* [Fabric Code](https://github.com/hyperledger/fabric)
* [ホワイト・ペーパー](https://github.com/hyperledger/hyperledger/wiki/Whitepaper-WG)
* [プロトコル仕様 & 関連資料](https://github.com/hyperledger/fabric/tree/master/docs)
* [StackOverflow](http://stackoverflow.com/questions/tagged/hyperledger)
* [Linux Foundation](https://www.hyperledger.org/)
* [Bluemix サービスの新機能](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}


<!--
[Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/)
[IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs) -->
