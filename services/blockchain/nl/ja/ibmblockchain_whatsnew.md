---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 新機能
{: #whatsnew}

**HSBN vNext Beta** プランは、[Hyperledger Fabric v1.0](https://www.hyperledger.org/){:new_window} オープン・ソース・コードベースの継続的なコミットを基礎としています。Hyperledger Fabric v1.0 は、エンタープライズ・ブロックチェーン・ネットワークを構築するための回復力のあるセキュアでカスタマイズ可能なプラットフォームを提供するモジュラー・アーキテクチャーを実装します。  
{: shortdesc}

**HSBN vNext Beta** サービスは、単一のサンドボックス環境を超えて、リソース・グループがさまざまな Bluemix 組織にまたがっている分散ブロックチェーン・ネットワークを提供します。ネットワーク・アーキテクチャーについて詳しくは、『[概要](v10_netoverview.html)』のトピックを参照してください。

## v1.0 の新規アーキテクチャー
{:why}

Hyperledger Fabric アーキテクチャーは、セキュリティー、スケーラビリティー、機密性、およびパフォーマンスに重点を置いたエンタープライズ・グレードのネットワークを駆動するように、v1.0 で大きく進化しました。ピアは、**endorsing** および **committing** という 2 つの異なるランタイムに分割され、トランザクションの順序付けの責任は、別個のコンポーネントに抽出されています。プライバシーと機密保持の懸案事項は、チャネル (データ分離を提供する) を通じて対処されます。台帳はチャネルごとに存在するため、二者間トランザクション、多者間トランザクション、または公開トランザクションの異なる組み合わせをサポートするようにネットワークをカスタマイズすることができます。

ネットワーク・トポロジーおよび対話について詳しくは、[Hyperledger アーキテクチャーの詳細](http://hyperledgerdocs.readthedocs.io/en/latest/arch-deep-dive.html){: new_window}のセクションを参照してください。

## その他の変更点

HSBN vNext Beta プランには、以下の変更点も含まれています。
* [新規ダッシュボード](v10_dashboard.html)で、サブスクライバーは、ブロックチェーン・ネットワークの作成、メンバーの招待、別のネットワークへの参加、およびリソースと資産の管理を実行できます。
* [v1.0の新しい Marbles サンプル・チェーンコード・アプリケーション](https://github.com/hyperledger/fabric/blob/master/examples/chaincode/go/marbles02/marbles_chaincode.go){: new_window}により、最新のコードベースを試してみることができます。
* Hyperledger Fabric v1.0 の新しい[トランザクション・フロー](http://hyperledger-fabric.readthedocs.io/en/latest/txflow.html)を使用すると、トランザクション・プロセス全体で複数のチェックポイントを実装することで、データの一貫性と保全性が保証されます。
