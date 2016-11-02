---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 理解している必要のあること
{: #etn_overview}
最終更新日: 2016 年 10 月 13 日
{: .last-updated}

**重要:** いずれかの IBM Blockchain on Bluemix プラン (Starter Developer (Beta) または High Security Business Network (GA)) を使用する前に、以下の情報を確認してください。
<br><br>

## IBM サポート・ステートメント

IBM は長い間イノベーションを牽引してきました。それは、最新の IBM Blockchain オファリングにおいても続いています。Blockchain は急速に進化するテクノロジーで、金融から物流まで数多くの業界を混乱に陥れる可能性があります。さまざまな早期導入プログラムによって、IBM のお客様およびビジネス・パートナー様はすでに、ブロックチェーンの将来の方向性に影響を与えています。IBM Blockchain on Bluemix はそのようなプログラムの 1 つです。**新しいテクノロジーと同様に、IBM Blockchain on Bluemix ユーザーも素早くて根本的な変化に対して準備をしておく必要があります**。  
{:shortdesc}

IBM Blockchain の背景にあるアーキテクチャーは Linux Foundation の Hyperledger Project です。Hyperledger Fabric は、現在開発が進められているオープン・ソース・プロジェクトで、現在は*インキュベーション*状況にあります。各オープン・ソース・コミュニティーの貢献によって、Hyperledger Fabric はより堅固になりましたが、導入の課題が残っています。*インキュベーション*・サイクルの間、クライアントは Hyperledger Fabric v0.5 を使用してネットワーク・テストやシミュレーションを行うことができますが、**IBM は、価値ある金融資産を直接 Hyperledger Fabric v0.5 ブロックチェーン・ネットワーク上で実行しないよう警告しています**。  
<br>

## オープン・ソース・ステートメント

IBM Blockchain on Bluemix (Starter Developer プランと High Security Business Network プランの両方) は、Linux Foundation の Hyperledger Fabric v0.5 オープン・ソース・コードを使用しています。IBM を含む Hyperledger Project メンバーがコードをファブリックに提供した後、それらのコードはコミュニティーで検討、精査、テストされます。
Hyperledger Fabric v0.5 は現時点で*インキュベーション*状態にあります。*インキュベーション*状態について、および Hyperledger Project のライフサイクル全体について詳しくは、https://github.com/hyperledger/hyperledger/wiki/Project-Lifecycle を参照してください。
<br><br>

## チェーンコード・サポート・ステートメント

IBM Blockchain は、ブロックチェーン・ネットワークでのデータの一貫性や整合性にリスクを及ぼす[非決定論的チェーンコード](ibmblockchain_tutorials.html#ndcc)をサポートしていません。新規チェーンコードを IBM Blockchain on Bluemix ネットワークにデプロイする前に、『[非決定論的チェーンコード](ibmblockchain_tutorials.html#ndcc)』で詳細を確認してください。

[非決定論的チェーンコード](ibmblockchain_tutorials.html#ndcc)に加えて、以下のコーディング慣例は IBM Blockchain ネットワークではサポートされません。

1. 反復のある結合配列の使用 (Go では順序がランダムになってしまいます)。
2. KVS 表の項目リストの読み込み (順序が保証されません)。
3. スレッド・セーフでないチェーンコードの書き込み (照会と呼び出しが並行して呼び出されます)。
4. チェーンコードの台帳の状態変数の代わりにグローバル・メモリーまたはキャッシュ・ストレージを使用すること。
5. チェーンコードから直接、データベースなどの外部サービスにアクセスすること。
6. 非決定論的になる可能性のあるライブラリーまたはグローバル変数の使用 (“random”または "time" などの使用)。
<br><br>

## サポート窓口

IBM Blockchain on Bluemix ネットワークに関するサポートおよびヘルプについては、[サポート窓口](ibmblockchain_support.html)を参照してください。
