---

copyright:
  years: 2017
lastupdated: "2017-04-13"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# マイ API
{: #manage_api}

**「管理対象 API の表示 (View Managed APIs)」**タブを使用して、管理している API および以前に管理していたが現在は公開していない API の全体の状況を表示します。**「共有された API (Shared APIs)」**タブに、API Management または {{site.data.keyword.apiconnect_short}} サービスを通じて {{site.data.keyword.Bluemix_notm}} 組織と共有されたすべての API が表示されます。

API ダッシュボードを使用して、API Management によって一緒に管理しているすべての API を表示できます。 

## 管理対象 API の表示
{: #view_api}

{{site.data.keyword.openwhisk_short}} アクションおよびその他の外部ソース用に作成された API をここで表示できます。

1. {{site.data.keyword.Bluemix_notm}} ダッシュボードから、**「メニュー」**アイコン > **「サービス」** > **「API」**を選択します。
2. ソースを選択するには、**「API の管理 (Manage APIs)」**をクリックします。現在管理されている API のリストが表示されます。API のタイプには、以下のものがあります。
    * ユーザー定義エンドポイント - これは、{{site.data.keyword.Bluemix_notm}} 環境の外部にあり、URL エンドポイントによって追跡される API です。 
    * {{site.data.keyword.openwhisk_short}} アプリ - これは、API 内部にラップされている {{site.data.keyword.openwhisk_short}} アクションです。

API の名前を選択すると、その API の詳細が表示されます。

## 管理対象 API の作成
{: #create_mgd_api}

**「管理対象 API の作成 (Create Managed API)」**を選択することにより、管理対象 API のリストの外に出なくても、リストに API を追加できます。

{{site.data.keyword.openwhisk_short}} と API プロキシー (外部) API のどちらを作成するかを選択してから、新規 API の情報を入力します。  

これは、API プロキシー (外部 API) を追加できる唯一の場所です。外部 API は、{{site.data.keyword.Bluemix_notm}} 組織スペース内で作成されず、保管もされていない API です。外部 API は、その外部エンドポイントの URL を指定することによって管理できます。ニーズを満たすかどうかを確認するために API Management を試している場合、または既存の URL を使用して実行中の API が既にあり、それを中断したくない場合に、これが役立ちます。 

API を作成するために必要な設定に関する追加情報については、『[API の管理](manage_apis.html)』を参照してください。

## 共有 API の処理
{: #share_api}

**「共有 API の探索 (Explore Shared APIs)」**タブで、他のユーザーが作成して自分と共有している API を表示できます。{{site.data.keyword.openwhisk_short}} アクションおよび {{site.data.keyword.appconserviceshort}} サービスに関連付けられた API 用の API キーを作成することもできます。

1. {{site.data.keyword.Bluemix_notm}} ダッシュボードから、**「メニュー」**アイコン > **「サービス」** > **「API」**をクリックします。
2. ナビゲーションで**「共有 API の探索 (Explore Shared APIs)」**を選択します。取り込むことができるすべての API がここに表示されます。
3. API を取り込むには、その API を選択して開発者ポータルを開きます。開発者ポータルで、API を使用するためのプランに登録することができます。 
4. 管理する API を選択した後で、以下のタスクを実行する方法について詳しくは、『[API の管理](manage_apis.html)』を参照してください。 
    * API 使用量の表示
    * API キーの作成
    * API エクスプローラー を使用した資料の表示および API のテスト
