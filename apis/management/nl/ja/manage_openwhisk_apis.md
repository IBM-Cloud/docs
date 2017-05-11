---

copyright:
  years: 2017
lastupdated: "2017-04-12"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} アクションからの API の作成
{: #manage_openwhisk_apis}

OpenWhisk アクションを API Management によって管理することでメリットがあります。

API Management を使用すると、{{site.data.keyword.openwhisk_short}} アクションを API として公開できます。API を定義した後に、セキュリティー・ポリシーおよびレート制限ポリシーを適用したり、API 使用量および応答ログを表示したり、API 共有ポリシーを定義したりすることができます。  

{{site.data.keyword.openwhisk_short}} API を作成するには、以下のステップを実行します。

1. {{site.data.keyword.openwhisk_short}} ダッシュボードで**「API」**タブをクリックします。既に {{site.data.keyword.openwhisk_short}} API を作成済みの場合は、{{site.data.keyword.openwhisk_short}} API のリストが表示されます。{{site.data.keyword.openwhisk_short}} API がない場合は、「開始」画面が表示されます。 
2. **「{{site.data.keyword.openwhisk_short}} API の作成 (Create an OpenWhisk API)」**をクリックします。「{{site.data.keyword.openwhisk_short}} 用の API の作成 (Create API for OpenWhisk)」ウィンドウが表示されます。 
3. 「API 情報 (API Info)」セクションのフィールドに入力し、次に**「操作の作成 (Create Operation)」**をクリックします。「操作の作成 (Create Operation)」ウィンドウが表示されます。API 用のエンドポイント、https パス、およびメソッドを定義する操作を作成します。
4. 「操作の作成 (Create Operation)」ウィンドウで、必須フィールドに入力し、**「作成」**を選択します。その操作が、{{site.data.keyword.openwhisk_short}} アクション・テーブルを呼び出す操作に追加されます。
5. 入力したい残りの情報を入力します。後で API を管理するときに、残りの情報を追加したり更新したりすることもできます。
6. **「保存」**をクリックします。API の API 管理概要ページが開き、定義したすべての情報が表示されます。
7. [「API の管理 (Manage APIs)」](manage_apis.html)で API の管理を続行します。
