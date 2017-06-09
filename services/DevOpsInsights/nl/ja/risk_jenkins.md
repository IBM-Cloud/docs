---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# フリー・フォーム Jenkins プロジェクトとの統合

{{site.data.keyword.DRA_full}} をオープン・ツールチェーンに追加し、それがモニターするポリシーを定義した後、それをフリー・フォーム Jenkins プロジェクトに統合することができます。
フリー・フォーム Jenkins プロジェクトは、Jenkins Web インターフェースから構成され、管理されます。
 

Jenkins 用 IBM Cloud DevOps プラグインは、Jenkins プロジェクトをツールチェーンに統合します。
*ツールチェーン*は、開発、デプロイメント、運用の作業をサポートするツール統合のセットです。
ツールチェーンの集合体としての能力は、それに含まれる個々のツール統合の総和よりも優れています。
オープン・ツールチェーンは、{{site.data.keyword.contdelivery_full}} サービスの一部です。
{{site.data.keyword.contdelivery_short}} サービスについて詳しくは、[そのドキュメンテーション](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html)を参照してください。


IBM Cloud DevOps プラグインをインストールした後は、テスト結果を {{site.data.keyword.DRA_short}} に公開し、自動の品質ゲートを追加して、デプロイメント・リスクを追跡することができます。
また、ジョブ通知を、Slack や PagerDuty など、ツールチェーン内の他のツールに送信することもできます。
デプロイメントの追跡のために、Git コミットやそれに関連した Git または JIRA の問題に対して、ツールチェーンからデプロイメント・メッセージを追加することができます。
また、デプロイメントを「ツールチェーン接続」ページに表示することもできます。
 

このプラグインは、統合をサポートするためのビルド後アクションや CLI を提供します。
{{site.data.keyword.DRA_short}} は、単体テスト、機能テスト、コード・カバレッジ・ツール、静的セキュリティー・コード・スキャン、動的セキュリティー・コード・スキャンからの結果を集約し、分析することによって、デプロイメント・プロセス内のゲートにおいて、コードが事前定義されたポリシーを満たしているかどうかを判別します。
コードがポリシーを満たしていないか、ポリシーを超えていない場合、リスクのある変更版がリリースされないように、デプロイメントが停止されます。{{site.data.keyword.DRA_short}} は、継続的デリバリー環境のセーフティー・ネット、品質規格を実装して時間の経過とともに向上させるための方法、およびプロジェクトの正常性を把握するのに役立つデータ可視化ツールとして使用できます。

## 前提条件
{: #jenkins_prerequisites}

Jenkins プロジェクトを実行しているサーバーに対するアクセス権がなければなりません。


## ツールチェーンの作成
{: #jenkins_create}

{{site.data.keyword.DRA_short}} と Jenkins プロジェクトを統合するには、その前にツールチェーンを作成する必要があります。
 

1. ツールチェーンを作成するには、[「ツールチェーンの作成 (Create a Toolchain)」ページ](https://console.ng.bluemix.net/devops/create)に移動し、そのページに示されている手順を実行します。
 

2. ツールチェーンの作成後、それに {{site.data.keyword.DRA_short}} を追加します。
その手順については、[{{site.data.keyword.DRA_short}} のドキュメンテーション](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html)を参照してください。
 

## プラグインのインストール
{: #jenkins_install}

まず、Jenkins サーバーにプラグインをインストールします。サーバー・インターフェースを開き、次のようにします。

1. **「Jenkins の管理」**をクリックします。
2. **「プラグインの管理」**をクリックします。 
3. **「利用可能」**タブをクリックします。
4. `「IBM Cloud DevOps」`でフィルタリングします。 
5. 「IBM Cloud DevOps」を選択します。
6. **「ダウンロードして再起動後にインストール」**をクリックします。 

プラグインは、サーバーの再起動後に使用できます。  

## Deployment Risk ダッシュボードのための Jenkins ジョブの構成
{: #jenkins_configure}

プラグインをインストールし終えたら、{{site.data.keyword.DRA_short}} を Jenkins プロジェクトに統合することができます。
 

プロジェクトで Deployment Risk のゲートとダッシュボードを使用するには、以下の手順を実行します。


1. 使用するジョブ (ビルド、テスト、またはデプロイメントなど) の構成を開きます。


2. 該当するタイプのビルド後アクションを追加します。


   * ビルド・ジョブについては、**IBM Cloud DevOps へのビルド情報の公開**を参照してください。

   
   * テスト・ジョブについては、**IBM Cloud DevOps へのテスト結果の公開**を参照してください。

   
   * デプロイメント・ジョブについては、**IBM Cloud DevOps へのデプロイメント情報の公開**を参照してください。

   
3. 必須フィールドに入力します。それらは、ジョブ・タイプに応じて異なります。
 

   * **「資格情報」**リストから、使用する {{site.data.keyword.Bluemix_notm}} ID とパスワードを選択します。
Jenkins で保存されていない場合は、**「追加」**をクリックして追加し、保存します。
{{site.data.keyword.Bluemix_notm}} で**「接続のテスト」**をクリックして接続をテストします。

   
   * **「ビルド・ジョブ名 (Build Job Name)」**フィールドに、ビルド・ジョブの名前を Jenkins での名前と正確に一致するように指定します。
ビルドがテスト・ジョブに出現する場合、このフィールドは空のままにします。
ビルド・ジョブが Jenkins 外に出現する場合は、**「Jenkins 以外でビルドを実行する (Builds are being done outside of Jenkins)」**チェック・ボックスにチェック・マークを付け、ビルド番号とビルド URL を指定します。

   
   * 環境については、ビルド・ステージでテストを実行している場合は、ビルド環境のみ選択します。
デプロイメント・ステージでテストを実行している場合は、デプロイ環境を選択し、環境名を指定します。
`STAGING` と `PRODUCTION` の 2 つの値がサポートされています。

   
   * **「結果ファイルの場所 (Result File Location)」**フィールドには、結果ファイルの場所を指定します。
テストで結果ファイルを生成しない場合は、このフィールドを空のままにします。プラグインにより、現在のテスト・ジョブの状況に基づくデフォルト結果ファイルがアップロードされます。


   これらの画像には、サンプル構成が示されています。

   
   ![ビルド情報のアップロード](images/Upload-Build-Info.png "ビルド情報を DRA に公開")
   *ビルド情報の公開*
   
   ![テスト結果のアップロード](images/Upload-Test-Result.png "テスト結果を DRA に公開")
   *テスト結果の公開*
   
   ![デプロイメント情報のアップロード](images/Upload-Deployment-Info.png "デプロイメント情報を DRA に公開")
   *デプロイメント情報の公開*

4. {{site.data.keyword.DRA_short}} ポリシー・ゲートを使用してダウンストリーム・デプロイメント・ジョブを制御する場合、ビルド後アクション**「IBM Cloud DevOps ゲート (IBM Cloud DevOps Gate)」**を追加します。
ポリシーを選択し、テスト結果のスコープを指定します。
ポリシー・ゲートでダウンストリーム・デプロイメントを阻止できるようにするには、**「ポリシー・ルールに基づいてビルドを阻止 (Fail the build based on the policy rules)」**チェック・ボックスにチェック・マークを付けます。
次の図は、サンプルの構成を示しています。


    ![DevOps Insights ゲート](images/DRA-Gate.png "DevOps Insights ゲート")

5. Jenkins ビルド・ジョブを実行します。


6. [IBM Bluemix DevOps](https://console.ng.bluemix.net/devops) に移動し、ツールチェーンを選択し、**DevOps Insights** をクリックすることにより、Deployment Risk ダッシュボードを表示します。


Deployment Risk ダッシュボードは、ステージング・デプロイメント・ジョブの後にゲートが存在することに依存しています。
ダッシュボードを使用する場合は、ステージング環境へのデプロイの後、実稼働環境へのデプロイの前にゲートを配置してください。

    
## 通知の構成
{: #jenkins_notifications}

[Bluemix の資料](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins)にある手順を実行することにより、Slack や PagerDuty などのツールに通知を送信するよう、Jenkins ジョブを構成することができます。

