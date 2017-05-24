---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 継続的デリバリー・パイプラインとの統合

{{site.data.keyword.DRA_short}} をツールチェーンに追加し、それがモニターするポリシーを定義した後、それを {{site.data.keyword.deliverypipeline}} に統合します。
パイプラインについて詳しくは、[公式のドキュメンテーション](/docs/services/ContinuousDelivery/pipeline_working.html)を参照してください。


## パイプライン・ステージの準備
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
 

## テスト・ジョブの追加
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

## ゲートの定義
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

パイプラインを構成した後、{{site.data.keyword.DRA_short}} の使用を開始します。 
