---

copyright:
  years: 2017
lastupdated: "2017-04-11"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 追加の API Management フィーチャーの利用
{: #upgrade}

API Management によって、呼び出しレート、OAuth、および表示分析を制御できます。{{site.data.keyword.apiconnect_full}} サービスにアップグレードすることによって、より充実した API の管理制御が可能になります。{{site.data.keyword.apiconnect_short}} サービスでは、セキュリティー・ポリシーの選択肢の数が増え、レート制限をさらにきめ細かく制御できます。これに加えて、API をソーシャル化して開発者コミュニティーを運用できるように、完全にカスタマイズ可能な開発者ポータルを構成できます。その他の利点としては、以下のような機能が挙げられます。
* ライフサイクル管理
* 複合 API
* Web サービスの統合
* プロトコル・メディエーション
* スキーマからの API 生成
* マイクロサービス開発

{{site.data.keyword.apiconnect_short}} サービスへのマイグレーションは簡単であり、API Management によって管理しているどの API も再作成する必要はありません。

## {{site.data.keyword.apiconnect_short}} への API のマイグレーション
{: #migrate_api}

{{site.data.keyword.apiconnect_full}} にアップグレードすることを決定した場合、API Management から {{site.data.keyword.apiconnect_short}} サービスへ API をマイグレーションする必要があります。そのためには、各 API に対して以下のステップを実行します。 

1. API Management から API の Swagger 文書をダウンロードします。
    1. アプリを開き、**「API Management」**を選択します。
	2. **「API エクスプローラー (API Explorer)」**タブを選択します。そのプロジェクトに関連する API のリストが表示されます。
    2. API の名前の横にあるアイコンを選択して、API の Swagger 文書をダウンロードします。
2. {{site.data.keyword.apiconnect_short}} インスタンスを作成して準備します。 
    1. {{site.data.keyword.Bluemix_notm}} カタログから {{site.data.keyword.apiconnect_short}} サービスのインスタンスを作成します。
	2. プランを選択します。
	3. **「+追加 (+Add)」**を選択してカタログを作成します。
	4. 表示名とカタログの名前を入力して**「追加」**を選択します。
	5. 作成したカタログを選択します。
3. 以下のステップを実行して、{{site.data.keyword.apiconnect_short}} インスタンスに Swagger 文書をインポートします。
	1. {{site.data.keyword.apiconnect_short}} サービス・ダッシュボードのメニューで**「ナビゲート先... (>>) (Navigate to... (>>))」** > **「ドラフト (Drafts)」**を選択します。
	2. 「API」タブを選択します。
	3. **「+追加 (+Add)」** > **「ファイルまたは URL から API をインポート (Import API from a file or URL)」**を選択します。
	4. API Management からダウンロードした Swagger ファイルを見つけて選択します。**「開く」**を選択します。
	5. **「インポート」**を選択して、API を {{site.data.keyword.apiconnect_short}} サービスにインポートします。
4. API の設定を指定します。
    1. **「製品の作成 (Create product)」**を選択します。
	2. 作成した製品を選択して、その設定を表示します。
	3. API のレート制限を設定します。
	4. API の層を設定します。
5. 必要に応じて、API 用のエンドポイントを追加します。
    1. API を選択します。
	2. 「アセンブリー (Assembly)」タブを選択します。
	3. エンドポイントがまだ指定されていない場合は、エンドポイントを追加します。
	
 API をマイグレーションすると、{{site.data.keyword.apiconnect_short}} サービス・タイルを開くことによって、また {{site.data.keyword.Bluemix_notm}} ダッシュボードを通じて、API Management 機能のすべてにアクセスできるようになります。 

 
