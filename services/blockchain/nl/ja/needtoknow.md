---

copyright:
  years: 2017
lastupdated: "2017-03-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 特記事項
{: #etn_overview}

**重要:** どの IBM Blockchain on Bluemix プランでも、そのプランを使用する前に以下の情報を検討する必要があります。

## IBM サポート・ステートメント

IBM は長い間イノベーションを牽引してきました。それは、IBM Blockchain on Bluemix オファリング・プランにおいても続いています。ブロックチェーンは急速に進化するテクノロジーであり、これにより金融からサプライ・チェーンや物流までといった数多くの業界の既存のモデルが崩壊するのではないかと考えられています。さまざまな早期導入プログラムによって、IBM のお客様およびビジネス・パートナー様は、産業用ソリューションとしてブロックチェーンを積極的に推進してきました。IBM Blockchain on Bluemix はそのようなプログラムの 1 つです。**他の新しいテクノロジーと同様に、IBM Blockchain on Bluemix ユーザーも急速な根本的変化の可能性を認識しておく必要があります**。  
{:shortdesc}

IBM Blockchain の背景にあるアーキテクチャーは Linux Foundation の Hyperledger Fabric プロジェクトです。Fabric は現在、*アクティブ* 状況であり、開発が継続されています。各オープン・ソース・コミュニティーのコントリビューションによって、Hyperledger Fabric は改良されましたが、導入の課題が残っています。*アクティブ* なプロジェクト・サイクル中に、クライアントは Hyperledger Fabric v1.0 を使用してネットワークのテストおよびシミュレーションを実行できます。**IBM では、直接 Hyperledger Fabric ブロックチェーン・ネットワークで金融資産などの価値ある資産を定義または交換することは避けるように注意を促しています**。  

## オープン・ソース・ステートメント

**High Security Business Network (HSBN) vNext Beta** プランは、 Linux Foundation の Hyperledger Fabric v1.0 オープン・ソース・コード上に構築されています。Starter Developer プランおよび High Security Business Network (HSBN) プランは、Hyperledger Fabric v0.6 コード上に構築されています。IBM を含む Hyperledger Project メンバーは継続してソース・コードにコントリビューションを提供します。その後、それらのコードはコミュニティーで検討、精査、テストされます。Hyperledger Fabric v1.0 は現時点で*アクティブ* です。the*アクティブ* 状況や Hyperledger Project のライフサイクルについて詳しくは、https://wiki.hyperledger.org/community/project-lifecycle を参照してください。  

## チェーンコード・サポート・ステートメント

以下のコーディング慣例は IBM Blockchain ネットワークではサポートされません。

1. 反復のある結合配列の使用 (Go では順序がランダムになってしまいます)。
2. KVS 表の項目リストの読み込み (順序が保証されません)。
3. スレッド・セーフでないチェーンコードの書き込み (照会と呼び出しが並行して呼び出されます)。
4. チェーンコードの台帳の状態変数の代わりにグローバル・メモリーまたはキャッシュ・ストレージを使用すること。
5. チェーンコードから直接、データベースなどの外部サービスにアクセスすること。
6. 非決定論的になる可能性のあるライブラリーまたはグローバル変数の使用 (「random」や「time」などの使用)。
7. GetRows を使用した反復。  

また、HSBN プランおよび Starter プラン (Hyperledger Fabric v0.6) は、データの一貫性や保全性にリスクを及ぼす非決定論的チェーンコードをサポートしていません。詳細については、『[非決定論的チェーンコード](nondeterministic.html)』を参照してください。
