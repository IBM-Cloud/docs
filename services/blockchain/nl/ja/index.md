---

copyright:
  years: 2017
lastupdated: "2017-04-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 概説
{: #gettingstartedtemplate}

**重要:** IBM Blockchain on Bluemix プランのいずれかを使用する前に、[特記事項](needtoknow.html)の技術情報およびサポート情報を読んでおく必要があります。
{:shortdesc}

## IBM Blockchain on Bluemix

{{site.data.keyword.blockchainfull}} on Bluemix&reg; サービスは、3 つのブロックチェーン・ネットワーク・プランからなります。最新のプランである **High Security Business Network (HSBN) vNext Beta** は、Hyperledger Fabric v1.0 コード・ベースを基礎としており、モジュラー・アーキテクチャーを利用して新機能を提供します。IBM Blockchain on Bluemix のプランを使用すると、開発者は、プライベートなブロックチェーン・ネットワークを設計および構成しなくても、即時にチェーンコード・アプリケーションを作成してテストすることができます。チェーンコードは、Fabric ブロックチェーン・ネットワーク上で安全かつ効率的に資産交換を行い、台帳にそれらのトランザクションを永続的に記録するためのエンジンです。

## オファリング・プラン

IBM Blockchain on Bluemix の新規サブスクライバーは、**HSBN vNext Beta** プランに登録できるようになりました。この最新のオファリングは、次世代のセキュリティー、保全性、スケーラビリティー、およびパフォーマンスを提供する Hyperledger Fabric v1.0 を基礎としています。表 1 で、Bluemix のプランを説明します。

表 1: IBM Blockchain on Bluemix のプラン  

| Bluemix プラン      | 状況       | 新規サブスクライバーが使用可能  | Hyperledger Fabric バージョン
| ------------------------- |:--------------------------:|:-----:|:-----:|
| **HSBN vNext Beta** (1)   | ベータ版     | はい |  v1.0 |
| HSBN (2) |  GA |  はい |  v0.6 |
| Starter Developer (3)    | ベータ版     | はい | v0.6 |

(1) **High Security Business Network (HSBN) vNext Beta** プランは、Bluemix 組織に参加し、分散ブロックチェーン・ネットワークを構築するための簡単なメカニズムを提供します。  
(2) **High Security Business Network (HSBN) GA** プランは、[IBM Secure Service Container](etn_ssc.html) を使用したコード分離機能を備えた、高度にセキュアな単一テナントの LinuxONE on z Systems 環境を提供します。  
(3) Starter Developer Beta プランは、マルチテナント開発のみの環境を提供します。  

## オファリング・プランの詳細

表 2 では、各 IBM Blockchain on Bluemix の各プランを詳細に比較しています。IBM Blockchain on Bluemix の新規サブスクライバーは、**HSBN vNext Beta** プランを選択する必要があります。HSBN プランおよび Starter Developer プランを新規サブスクライバーが利用することはできませんが、IBM によるそれらのプランのサポートは継続します。

表 2: IBM Blockchain on Bluemix のプランの詳細  

| Bluemix プラン:      | Starter Developer Network       | High Security Business Network       | High Security Business Network (HSBN) vNext Beta
| ------------------------- |:--------------------------:|:-----:|:-----:|
| 状況:    | ベータ版     | GA | ベータ版 |
| 目的:  |  開発、およびテスト (セキュリティー・レベル、パフォーマンス、可用性) |  エンタープライズ・ネットワークのシミュレート、およびテスト (セキュリティー・レベル、パフォーマンス、可用性) |  実動レベルのセキュリティー、パフォーマンス、および可用性を持つエンタープライズ・ビジネス・ネットワークをセットアップする |
| ノード:    | 4 ピア + 認証局     | 4 ピア + 認証局 | ネットワーク・コンポーネントの動的管理 |
| ダッシュボード・モニター: | [はい](ibmblockchainmonitor.html) | [はい](ibmblockchainmonitor.html) | [はい](v10_dashboard.html) |
| 環境:     | 共有されるマルチテナント | 分離された単一テナント | 複数の分離レベル |

# 関連リンク
{: #rellinks}
## チュートリアルとサンプル
{: #samples}
* [IBM Marbles デモ (GitHub)](https://github.com/IBM-Blockchain/marbles) - v0.6 & v1.0
* [IBM Commercial Paper デモ (GitHub)](https://github.com/IBM-Blockchain/cp-web#readme) - v0.6
* [IBM Car Lease デモ (Github)](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md) - v0.6
* [Art Auction デモ (Github)](https://github.com/ITPeople-Blockchain/auction) v0.6 - v1.0 (ローカルで実行)

## API リファレンス
{: #api}
* [Hyperledger Fabric API (GitHub)](https://github.com/hyperledger/fabric/tree/v0.6/docs/API)
* [HFC SDK for Node.js](https://github.com/hyperledger/fabric/tree/v0.6/sdk/node)

## 関連リンク
{: #general}
* [Fabric Code](https://github.com/hyperledger/fabric)
* [Fabric Composer](https://fabric-composer.github.io/)
* [Fabric v1.0 資料](http://hyperledger-fabric.readthedocs.io/en/latest/)
* [Fabric v0.6 資料](https://github.com/hyperledger/fabric/tree/v0.6/docs)
* [StackOverflow](http://stackoverflow.com/questions/tagged/hyperledger)
* [Bluemix サービスの新機能](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}


<!--
[Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/)
[IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs) -->
