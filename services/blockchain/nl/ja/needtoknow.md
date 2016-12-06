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
最終更新日: 2016 年 11 月 10 日
{: .last-updated}

**重要:** いずれかの IBM Blockchain on Bluemix プラン (Starter Developer (Beta) または High Security Business Network (GA)) を使用する前に、以下の情報を確認してください。
<br><br>

## IBM サポート・ステートメント

IBM は長い間イノベーションを牽引してきました。それは、最新の IBM Blockchain オファリングにおいても続いています。Blockchain は急速に進化するテクノロジーで、金融から物流まで数多くの業界を混乱に陥れる可能性があります。さまざまな早期導入プログラムによって、IBM のお客様およびビジネス・パートナー様はすでに、ブロックチェーンの将来の方向性に影響を与えています。IBM Blockchain on Bluemix はそのようなプログラムの 1 つです。**新しいテクノロジーと同様に、IBM Blockchain on Bluemix ユーザーも素早くて根本的な変化に対して準備をしておく必要があります**。  
{:shortdesc}

IBM Blockchain の背景にあるアーキテクチャーは Linux Foundation の Hyperledger Project です。Hyperledger Fabric は、現在開発が進められているオープン・ソース・プロジェクトで、現在は*インキュベーション*状況にあります。各オープン・ソース・コミュニティーの貢献によって、Hyperledger Fabric はより堅固になりましたが、導入の課題が残っています。*インキュベーション*・サイクルの間、クライアントは Hyperledger Fabric v0.6 を使用してネットワーク・テストやシミュレーションを行うことができますが、**IBM は、価値ある金融資産を直接 Hyperledger Fabric v0.6 (またはそれ以前の) ブロックチェーン・ネットワーク上で実行しないように警告しています**。  
<br>

## オープン・ソース・ステートメント

IBM Blockchain on Bluemix (Starter Developer プランと High Security Business Network プランの両方) では、Linux Foundation の Hyperledger Fabric v0.6.1 オープン・ソース・コードを使用しています。IBM を含む Hyperledger Project メンバーがコードをファブリックに提供した後、それらのコードはコミュニティーで検討、精査、テストされます。
Hyperledger Fabric v0.6.1 は現時点で*インキュベーション*状態にあります。*インキュベーション*状態や Hyperledger Project のライフサイクル全体について詳しくは、https://github.com/hyperledger/hyperledger/wiki/Project-Lifecycle を参照してください。
<br><br>

## チェーンコード・サポート・ステートメント

IBM Blockchain は、ブロックチェーン・ネットワークでのデータの一貫性や整合性にリスクを及ぼす非決定論的チェーンコードをサポートしていません。新規チェーンコードを IBM Blockchain on Bluemix ネットワークにデプロイする前に、『[非決定論的チェーンコード](nondeterministic.html)』で詳細を確認してください。

[非決定論的チェーンコード](nondeterministic.html)に加えて、以下のコーディング慣例は IBM Blockchain ネットワークではサポートされません。

1. 反復のある結合配列の使用 (Go では順序がランダムになってしまいます)。
2. KVS 表の項目リストの読み込み (順序が保証されません)。
3. スレッド・セーフでないチェーンコードの書き込み (照会と呼び出しが並行して呼び出されます)。
4. チェーンコードの台帳の状態変数の代わりにグローバル・メモリーまたはキャッシュ・ストレージを使用すること。
5. チェーンコードから直接、データベースなどの外部サービスにアクセスすること。
6. 非決定論的になる可能性のあるライブラリーまたはグローバル変数の使用 (「random」や「time」などの使用)。
7. GetRows を使用した反復。  

サポートされているチェーンコードの例については、examples ライブラリーを参照してください。このディレクトリーには Go と Java で作成されたサンプルが含まれています。
<br><br>

## マイグレーションに関する考慮事項

Hyperledger Fabric v0.5-developer-preview で開発したコードを (Hyperledger Fabric v0.6.1 に対して構築された) Bluemix バックエンドで機能させるためには、いくつかのプログラミング変更を実施する必要があります。新しい機能とコード変更の詳細については、Hyperledger Fabric の資料の [Migration considerations](http://hyperledger-fabric.readthedocs.io/en/v0.6/v0.6_migration/) のセクションを参照してください。  

## HSBN の既知の問題

1. Hyperledger Fabric v0.6.1 を使用する High Security Business Network で、約 50 を超えるチェーンコードをデプロイした場合は、開発段階で定期的にネットワークをリセットすることをお勧めします。ネットワークをリセットすると、デプロイされたチェーンコードと収集されたデータが削除されます。これにより、反復型開発の段階で改良されて不要になった古いチェーンコードを削除できます。開発後の段階に入ったら、チェーンコードのデプロイ数をモニターして、最も重要なチェーンコードのために容量を残しておく必要があります。
2. ネットワークとピアの状況の照会を実行すると、散発的に「サービスを利用できません (503 Service Unavailable)」と「ゲートウェイが正しくありません (502 Bad Gateway)」のエラーを受け取ります。
3. VP1 のログに「Server.Serve がセキュリティー・ハンドシェークを完了できませんでした (Server.Serve failed to complete security handshake)」というメッセージが示される可能性があります。これは致命的なエラーではなく、ネットワーク操作に関連するものでもありません。
4. **サービス資格情報**のデータが自動設定ではない場合があります。その場合は、以下のようにして資格情報を生成してください。

 a) サービス・ダッシュボードから、**「サービス資格情報」**タブをクリックします。

  ![HSBN「サービス資格情報」](images/hsbn.png "HSBN「サービス資格情報」")

 **「サービス資格情報」**タブから、**「新しい資格情報 (New Credential)」**のボタンをクリックします。

  ![HSBN「新しい資格情報 (New Credential)」](images/hsbn1.png "HSBN「新しい資格情報 (New Credential)」")

c) **「新しい資格情報の追加 (Add New Credential)」**というタイトルの新しいウィンドウが表示されます。このウィンドウの下部の**「追加」**ボタンをクリックします。

  ![HSBN「新しい資格情報の追加 (Add New Credential)」](images/hsbn2.png "HSBN「新しい資格情報の追加 (Add New Credential)」")

 d) 以下の例のような画面が表示されるはずです。**「資格情報の表示 (View Credentials)」**をクリックすると、HSBN インスタンスのサービス資格情報を含む JSON ペイロードが表示されます。  

  ![HSBN 生成された資格情報 ](images/hsbn3.png "生成された資格情報")



## サポート窓口

IBM Blockchain on Bluemix ネットワークに関するサポートおよびヘルプについては、[サポート窓口](ibmblockchain_support.html)を参照してください。
