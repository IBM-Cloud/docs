---

copyright:
  years: 2017
lastupdated: "2017-03-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# HSBN の既知の問題
{: #etn_overview}



HSBN プランについて以下の問題が報告されています。

1. Hyperledger Fabric v0.6.1 を使用する High Security Business Network で、約 50 を超えるチェーンコードをデプロイした場合は、開発段階で定期的にネットワークをリセットすることをお勧めします。ネットワークをリセットすると、デプロイされたチェーンコードと収集されたデータが削除されます。これにより、反復型開発の段階で改良されて不要になった古いチェーンコードを削除できます。開発後の段階に入ったら、チェーンコードのデプロイ数をモニターして、最も重要なチェーンコードのために容量を残しておく必要があります。
2. ネットワークとピアの状況の照会を実行すると、散発的に「サービスを利用できません (503 Service Unavailable)」と「ゲートウェイが正しくありません (502 Bad Gateway)」のエラーを受け取ります。
3. VP1 のログに「Server.Serve がセキュリティー・ハンドシェークを完了できませんでした (Server.Serve failed to complete security handshake)」というメッセージが示される可能性があります。これは致命的なエラーではなく、ネットワーク操作に関連するものでもありません。
4. **サービス資格情報**のデータが自動設定ではない場合があります。その場合は、以下のようにして資格情報を生成してください。

 a) サービス・ダッシュボードから、**「サービス資格情報」**タブをクリックします。

  ![HSBN「サービス資格情報」](images/hsbn.png "HSBN「サービス資格情報」")

 b) **「サービス資格情報」**タブから、**「新しい資格情報 (New Credential)」**のボタンをクリックします。

  ![HSBN「新しい資格情報 (New Credential)」](images/hsbn1.png "HSBN「新しい資格情報 (New Credential)」")

c) **「新しい資格情報の追加 (Add New Credential)」**というタイトルの新しいウィンドウが表示されます。このウィンドウの下部の**「追加」**ボタンをクリックします。

  ![HSBN「新しい資格情報の追加 (Add New Credential)」](images/hsbn2.png "HSBN「新しい資格情報の追加 (Add New Credential)」")

 d) 以下の例のような画面が表示されるはずです。**「資格情報の表示 (View Credentials)」**をクリックすると、HSBN インスタンスのサービス資格情報を含む JSON ペイロードが表示されます。  

  ![HSBN 生成された資格情報 ](images/hsbn3.png "生成された資格情報")


## サポート窓口

IBM Blockchain on Bluemix ネットワークに関するサポートおよびヘルプについては、[サポート窓口](ibmblockchain_support.html)を参照してください。
