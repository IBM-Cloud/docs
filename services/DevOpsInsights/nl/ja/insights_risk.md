---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Deployment Risk (ベータ)
{: #gettingstarted}

{{site.data.keyword.DRA_short}} は、デプロイメント、特にリスクについての豊富な情報を提供します。
この情報を使用し、ポリシーやゲートを利用することにより、デリバリー・パイプラインの中で品質保護を自動化することができます。
{:shortdesc}

ツールチェーンから {{site.data.keyword.DRA_short}} を開いた後、**「Deployment Risk」**をクリックします。
そこから、ステージング環境や実稼働環境でのアプリケーションの概要を得ることができ、ドリルダウンしてコード・カバレッジ、テスト・パフォーマンス、セキュリティー・レポートを確認できます。
ダッシュボードには、パイプラインの {{site.data.keyword.DRA_short}} テストからの最新情報が自動的に取り込まれます。


## Deployment Risk について
{: #about}

Deployment Risk を使用することにより、ポリシーやゲートを通じてツールチェーンの中で品質基準を適用することができます。
ポリシーは一連のルールで構成されます。ゲートはポリシーを適用するためのものです。
例えば、ビルドが単体テストやテスト・カバレッジの基準に適合することを求める「単体テストとテスト・カバレッジ」ポリシーを作成することができます。
そして、そのポリシーを参照するゲートを、継続的デリバリーのプロセスに追加します。
そのポリシーを満たさないビルドは、そのゲートで制止されます。
 

Deployment Risk は、{{site.data.keyword.contdelivery_full}} の一部である {{site.data.keyword.deliverypipeline}}、および Jenkins プロジェクトと連携します。
それらの使用手順は、概略で類似しています。
  

{{site.data.keyword.deliverypipeline}} を使用している場合は、以下の手順に従います。


1. {{site.data.keyword.DRA_short}} が管理する[ポリシーとルールを作成する](#policies_and_rules)。
2. {{site.data.keyword.DRA_short}} との統合のための[パイプラインのステージを準備する](#integrate_pipeline)。

3. パイプラインの中に、結果を {{site.data.keyword.DRA_short}} にアップロードする[テスト・ジョブを作成または編集する](#configure_pipeline_jobs)。
4. それらの結果やポリシーに基づいてプロモーション決定を下す[ゲートをパイプラインに追加する](#configure_pipeline_gates)。
5. パイプラインを実行し、[結果を表示する](#view_results)。

Jenkins を使用している場合、以下の手順に従います。


1. {{site.data.keyword.DRA_short}} が管理する[ポリシーとルールを作成する](#policies_and_rules)。
2. [Jenkins プラグインをインストールし、構成する](#integrate_jenkins)。
3. [プラグインの指示に従ってテスト・ジョブとゲートを作成する](#integrate_jenkins)。
テスト結果が {{site.data.keyword.DRA_short}} にアップロードされて分析され、ゲートがそれらの結果を使用してプロモーション決定を下す。

4. プロジェクトを実行し、[結果を表示する](#view_results)。 

コードをどんな方法でビルドしデプロイするかに関係なく、結果は同じです。
基準を満たすビルドは Deployment Risk ゲートを通過し、基準を満たさないビルドは制止されます。
 

## 前提条件
{: #prerequisites}

Deployment Risk では、[「{{site.data.keyword.DRA_short}} の概説」](/docs/services/DevOpsInsights/index.html)の説明にはない構成が必要になります。


Deployment Risk を使用するには、以下の 2 つが必要です。


* {{site.data.keyword.deliverypipeline}} または Jenkins プロジェクトのインスタンス
* プロジェクトを評価するために使用するテスト

## ポリシーとルールの作成
{: #policies_and_rules}

ポリシーは、デリバリー・パイプラインの中のゲートを制御するルールの集まりです。
特定のゲートにおいて制定されているポリシーをコードが満たしていない、または超えていない場合、リスクのある変更版がリリースされることがないよう、デプロイメントが制止されます。


ポリシーは {{site.data.keyword.DRA_short}} で定義します。
ポリシーは、{{site.data.keyword.DRA_short}} が含まれている {{site.data.keyword.Bluemix_notm}} 組織 (org) 内に作成されます。
同じ org 内のすべてアプリケーションが、そのポリシーを使用できます。
 

### ポリシーの作成
{: #create_policies}

ポリシーを作成するには、


1. 左側のナビゲーションから、**「設定」**をクリックします。


2. **「ポリシー」**をクリックします。


3. **「ポリシーの作成 (Create Policy)」**をクリックしてから、新しいポリシーの名前と説明を入力します。


4. **「次へ」**をクリックします。

4. 以下のようにして、1 つ以上のルールをポリシーに追加します。
  1. **「ルールをポリシーに追加する (Add Rule to Policy)」**をクリックします。
  2. ルールのタイプを選択します。
  3. ルールの詳細情報と条件を入力します。
  4. **「保存」**をクリックします。

5. ルールをポリシーに追加し終えたら、**「完了」**をクリックします。

### ルールの作成
{: #creating_rules}

ルールは、ポリシーで成功か失敗かを判断するために使用する基準を定義します。
例えば、80% の単体テスト成功を求める単体テスト・ルールと、100% コード・カバレッジを求めるテスト・カバレッジ・ルールを含む「単体テストとテスト・カバレッジ」ポリシーを作成するとします。
パイプラインの中にこのルールを参照するゲートを追加すると、これらのルールの両方を満たさないビルドは、このゲートより先には進めなくなります。 

テストに重大のマークを付けることにより、どんな場合であろうと成功を必須とすることができます。
ルールを作成するには、ポリシーを選択して**「ルールをポリシーに追加する (Add Rule to Policy)」**をクリックします。
 

#### 機能検証テストのルールの作成
{: #criteria_fvt}

1. 説明を入力して形式を選択します。

2. 成功と宣言するのに必要なテスト・ケースの合格パーセンテージを指定します。

3. クリティカルなテスト・ケースを定義します。

4. テスト・ケースの回帰をモニターするには、**「テスト・ケースの回帰のモニター (Monitor for test case regression)」**チェック・ボックスを選択します。

5. **「保存」**をクリックします。


#### 単体テストのルールの作成
{: #criteria_ut}

1. 説明を入力して形式を選択します。

2. 成功と宣言するのに必要なテスト・ケースの合格パーセンテージを指定します。

3. クリティカルなテスト・ケースを定義します。

4. テスト・ケースの回帰をモニターするには、**「テスト・ケースの回帰のモニター (Monitor for test case regression)」**チェック・ボックスを選択します。

5. **「保存」**をクリックします。


#### コード・カバレッジのルールの作成
{: #criteria_codecoverage}

1. 説明を入力して形式を選択します。

2. 成功と宣言するのに必要なコード・カバレッジのパーセンテージを指定します。

3. コード・カバレッジの回帰をモニターするには、**「テスト・ケースの回帰のモニター (Monitor for test case regression)」**チェック・ボックスを選択します。

4. **「保存」**をクリックします。

#### 静的セキュリティー・スキャン・ルールの作成
{: #criteria_static}

{{site.data.keyword.DRA_short}} を IBM Application Security on Cloud に統合して、静的コードと動的アプリのスキャンを実行することができます。
Application Security on Cloud について詳しくは、[公式のドキュメンテーション](/docs/services/ApplicationSecurityonCloud/index.html)を参照してください。


1. 説明を入力します。


2. ルールによって許容される高、中、低の重大度の問題の最大数を指定します。
 

3. **「保存」**をクリックします。

#### 動的セキュリティー・スキャン・ルールの作成
{: #criteria_dynamic}

{{site.data.keyword.DRA_short}} を {{site.data.keyword.appseccloudfull}} に統合して、動的アプリ・スキャンを実行することができます。
Application Security on Cloud について詳しくは、[公式のドキュメンテーション](/docs/services/ApplicationSecurityonCloud/index.html)を参照してください。


1. 説明を入力します。


2. ルールによって許容される高、中、低の重大度の問題の最大数を指定します。
 

3. **「保存」**をクリックします。

## {{site.data.keyword.deliverypipeline}} の構成 
{: #configuration}

{{site.data.keyword.DRA_short}} をツールチェーンに追加し、それがモニターするポリシーを定義した後、それを {{site.data.keyword.deliverypipeline}} に統合します。
パイプラインについて詳しくは、[公式のドキュメンテーション](/docs/services/ContinuousDelivery/pipeline_working.html)を参照してください。


### パイプライン・ステージの準備
{: #integrate_pipeline}

Deployment Risk でプロジェクトを分析するには、パイプラインの中にステージングと実動のステージを定義する必要があります。
ステージを定義するには、各種のテキスト環境プロパティーを使用します。
これらは、各ステージの構成メニュー ![パイプライン・ステージ構成アイコン](images/pipeline-stage-configuration-icon.png) の中の**「環境プロパティー」**の下にあります。


1. ステージング・ステージの場合は、`LOGICAL_ENV_NAME` プロパティーを `STAGING` に設定します。
 

2. 実動ステージの場合は、`LOGICAL_ENV_NAME` プロパティーを `PRODUCTION` に設定します。
 

アプリをビルドまたはデプロイするステージに以下のプロパティーを追加することもできます。


* `LOGICAL_APP_NAME`。ダッシュボード上のアプリの名前を定義します。

* `BUILD_PREFIX`。ステージのビルドの前に付加するテキストを定義します。
このテキストは、ダッシュボードにも表示されます。
 

### テスト・ジョブの追加
{: #configure_pipeline_jobs}

{{site.data.keyword.DRA_short}} をパイプラインに統合するには、2 種類のテスト・ジョブ (結果を分析のために {{site.data.keyword.DRA_short}} にアップロードするものと、その分析に基づいて処理を実行するゲート) を使用します。  

まず、テストを実行し、結果をアップロードするための詳細テスター・ジョブをパイプラインに追加します。
 

**注:** 結果を {{site.data.keyword.DRA_short}} にアップロードしてテスト・ジョブをアップデートする場合、先に進む前にその構成をどこか便利な場所に保存しておいてください。
その後、そのジョブ構成メニューを開いて、ステップ 3 に進みます。
 

1. 結果をアップロードするジョブを追加するステージで、**「ステージ構成」**アイコン ![パイプライン・ステージ構成アイコン](images/pipeline-stage-configuration-icon.png) をクリックします。
**「ステージの構成 (Configure Stage)」**をクリックします。
2. テスト・ジョブを作成し、その名前を入力します。
 
3. ジョブ・タイプとして、**「詳細テスター (Advanced Tester)」**を選択します。

4. 通常のパイプライン・テスト・ジョブの場合と同じようにして、**「テスト・コマンド」**と**「作業ディレクトリー」**のフィールドに情報を入力します。
 
5. 特定のテスト・タイプのテスト結果をアップロードするための、その他のフィールドに入力します。
 

 1. 使用する {{site.data.keyword.DRA_short}} ポリシーの中で定義したものと合致するメトリック・タイプを選択します。

 2. 結果ファイルの場所を入力します。
この場所は作業ディレクトリーを基準とする相対位置です。
 

6. 同じジョブで別のテスト・タイプの結果をアップロードする場合は、*「追加 (Additional)」*と先頭に示されたフィールドに入力します。

7. **「保存」**をクリックして、パイプラインに戻ります。

**「メトリックのタイプ (Type of Metric)」**フィールドと**「結果ファイルの場所 (Result File Location)」**フィールドの値は、以下に示す正しい形式と合致していなければなりません。

<table><thead>
<tr>
<th>メトリックのタイプ</th>
<th>サポートされる形式</th>
</tr>
</thead><tbody>
<tr>
<td>機能検証テスト (Functional Verification Test)</td>
<td>Mocha、xUnit</td>
</tr>
<tr>
<td>単体テスト (Unit Test)</td>
<td>Mocha、xUnit、Karma/Mocha</td>
</tr>
<tr>
<td>コード・カバレッジ (Code Coverage)</td>
<td>Istanbul、Blanket.js</td>
</tr>
</tbody></table>

図 1 に示すテスト・ジョブは、単体テストを実行し、結果を Mocha 形式でアップロードし、コード・カバレッジ結果を Istanbul 形式でアップロードするように構成されています。


![DevOps Insights アップロード・ジョブ](images/insights_upload_job.png)
*図 1. 結果を DevOps Insights にアップロードする*

### ゲートの定義
{: #configure_pipeline_gates}

{{site.data.keyword.DRA_short}} ゲートは、定義されたポリシーにテスト結果が準拠しているかどうかを検査します。
ポリシーに準拠していない場合、デフォルトで {{site.data.keyword.DRA_short}} ゲートは失敗します。
また、失敗の後もパイプラインを先へ進むことを許可するアドバイザリー・ロールで機能するゲートを構成することもできます。


Deployment Risk ダッシュボードは、ステージング・デプロイメント・ジョブの後にゲートが存在することに依存しています。
ダッシュボードを使用する場合は、ステージング環境へのデプロイの後、実稼働環境へのデプロイの前にゲートを配置してください。


通常、ゲートは、パイプラインの中でビルド・プロモーションの前に配置されます。
この場所は、ビルドの品質をポリシーに照らして検査して、それが別の環境に安全にプロモートできるものであることを確認するのに理想的な場所です。しかし、ゲートは、特定の基準の検査を必要とする、パイプライン内の任意の場所に配置することが可能です。ステージング環境へのデプロイの前に配置されるゲートでも、ポリシーが適用されますが、それらは Deployment Risk ダッシュボードに表示されません。


1. ステージで**「ステージ構成 (Stage Configuration)」**アイコン ![パイプラインのステージ構成アイコン](images/pipeline-stage-configuration-icon.png) をクリックし、**「ステージの構成 (Configure Stage)」**をクリックします。
2. **「ジョブの追加 (Add Job)」**をクリックします。ジョブ・タイプとして**「テスト」**を選択します。
3. テスター・タイプとして**「{{site.data.keyword.DRA_short}} ゲート ({{site.data.keyword.DRA_short}} Gate)」**を選択します。
4. 環境名を指定します。この値が、[環境プロパティー](#toolchain_pipeline_props)で定義したものと一致することを確認してください。
5. このゲートにおいてチェックするポリシー名を入力します。


 この名前は、定義したポリシー名のいずれかと完全に一致していなければなりません。ご使用のツールチェーンと同じ {{site.data.keyword.Bluemix_notm}} 組織で定義されたポリシーのみを指定できます。

6. オプション: ゲートを推奨モードで機能させるには、**「このジョブが失敗した場合、このステージの実行を停止する (Stop running this stage if this job fails)」**チェック・ボックスをクリアします。推奨モードでは、{{site.data.keyword.DRA_short}} は同じポリシー分析をゲートで実行し、レポートを生成しますが、失敗となった場合でもパイプラインは停止されません。
7. **「保存」**をクリックして、パイプラインに戻ります。
8. 上記のステップを繰り返して、すべての {{site.data.keyword.DRA_short}} ポリシーについてゲートをセットアップします。

![Deployment Risk の Mocha ジョブ](images/insights_gate_job.png)
*図 2. DevOps Insights ゲート*

パイプラインを構成した後、{{site.data.keyword.DRA_short}} の使用を開始します。その手順については、[Running the Delivery Pipeline](/docs/services/DevOpsInsights/pipeline_decision_reports.html#toolchain_reports) を参照してください。

## Jenkins プロジェクトの構成
{: #integrate_jenkins}

{{site.data.keyword.DRA_full}} をオープン・ツールチェーンに追加し、それがモニターするポリシーを定義した後、それを Jenkins プロジェクトに統合することができます。
 

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

### 前提条件
{: #jenkins_prerequisites}

Jenkins プロジェクトを実行しているサーバーに対するアクセス権がなければなりません。


### ツールチェーンの作成
{: #jenkins_create}

{{site.data.keyword.DRA_short}} と Jenkins プロジェクトを統合するには、その前にツールチェーンを作成する必要があります。
 

1. ツールチェーンを作成するには、[「ツールチェーンの作成 (Create a Toolchain)」ページ](https://console.ng.bluemix.net/devops/create)に移動し、そのページに示されている手順を実行します。
 

2. ツールチェーンの作成後、それに {{site.data.keyword.DRA_short}} を追加します。
その手順については、[{{site.data.keyword.DRA_short}} のドキュメンテーション](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html)を参照してください。
 

### プラグインのインストール
{: #jenkins_install}

まず、{{site.data.keyword.DRA_short}} からプラグインをダウンロードします。
  

1. ツールチェーンの概要ページから、**DevOps Insights** をクリックします。

2. **「設定」**、**「Jenkins プラグインのセットアップ (Jenkins Plugin Setup)」** の順にクリックします。

3. ページの指示に従い、プラグインをダウンロードします。


次に、Jenkins サーバーでプラグインをインストールします。


1. **「Jenkins の管理 (Manage Jenkins)」&gt;「プラグインの管理」**をクリックした後、**「詳細」**タブをクリックします。

2. **「ファイルの選択」**をクリックし、IBM Cloud DevOps プラグインのインストール・ファイルを選択します。
 
3. **「アップロード」**をクリックします。
4. Jenkins を再始動して、プラグインがインストールされたことを確認します。

### Deployment Risk ダッシュボードのための Jenkins ジョブの構成
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

    
### 通知の構成
{: #jenkins_notifications}

[Bluemix の資料](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins)にある手順を実行することにより、Slack や PagerDuty などのツールに通知を送信するよう、Jenkins ジョブを構成することができます。


次のサンプルには、ジョブ構成のための `ICD_WEBHOOK_URL` の構成方法が示されています。 ![ICD_WEBHOOK_URL パラメーターの設定](images/Set-Parameterized-Webhook.png "パラメーター化 WebHook の設定")


次のサンプルには、ジョブ通知のためのビルド後アクションの構成方法が示されています。![WebHook 通知のためのビルド後アクション](images/PostBuild-WebHookNotification.png "ビルド後アクションでの WebHook 通知の構成")


## 結果の表示
{: #view_results}

パイプラインが実行された後、{{site.data.keyword.DRA_short}} はそのパイプラインでのテスト結果の収集と分析を開始して、基準を確立します。その後の実行のたびに、そのデータが収集され、前の結果と比較されます。決定ゲートでは、このデータを利用して、デプロイメントを停止する時を決定します。 

Deployment Risk ダッシュボードから、デプロイメントとゲートの評価データを確認することができます。
ダッシュボードを開くには、{{site.data.keyword.DRA_short}} を開き、サイド・メニューから**「Deployment Risk」**をクリックします。


{{site.data.keyword.contdelivery_short}} パイプラインを使用している場合、パイプライン自体から個々のゲート実行レポートを表示できます。
パイプラインからゲートの決定レポートを表示するには、次のようにします。


1. 確認するゲートを含むステージで、**「ログおよび履歴の表示 (View logs and history)」**をクリックします。

2. そのゲートを含むジョブから、そのゲートの名前をクリックします。


3. ログ・ビューで「`ここから {{site.data.keyword.DRA_short}} レポートを確認します (Check {{site.data.keyword.DRA_short}} report here)`」というメッセージを見つけ、リンクをクリックしてレポートを開きます。







