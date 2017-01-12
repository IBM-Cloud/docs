---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.DRA_short}} と {{site.data.keyword.deliverypipeline}} の統合
{: #toolchain_configure_pipeline}

{{site.data.keyword.DRA_full}} をツールチェーンに追加し、モニターされるポリシーを定義した後に、{{site.data.keyword.DRA_short}} とパイプラインを統合する必要があります。
{:shortdesc}

<!--##Configuring the {{site.data.keyword.deliverypipeline}}

{: #toolchain_integration}
To use {{site.data.keyword.DRA_short}}, add it to any toolchain that uses the {{site.data.keyword.deliverypipeline}}.

1. In {{site.data.keyword.Bluemix_notm}}, on the **Toolchains** tab, open a toolchain.

2. On the toolchain's Overview page, click the add (+) button.

3. In the Tool Integrations section, select **{{site.data.keyword.DRA_short}}**.

4. Click **Create Integration**.

5. In your toolchain, click the {{site.data.keyword.deliverypipeline}} tile. You can configure {{site.data.keyword.DRA_short}} in any number of pipelines.-->

## {{site.data.keyword.DRA_short}} のためのパイプライン・ステージの準備
{: #toolchain_pipeline_props}

ビルド・ジョブまたはデプロイ・ジョブを含む各パイプライン・ステージで、いくつかの環境プロパティーを作成する必要があります。

1. **「ステージ構成 (Stage Configuration)」**をクリックしてから、**「ステージの構成 (Configure stage)」**をクリックします。

2. **「環境プロパティー (ENVIRONMENT PROPERTIES)」**をクリックします。

3. 以下の 3 つのテキスト・プロパティーを追加してから、ステージの変更を保存します。

<table><thead>
<tr>
<th>環境プロパティー</th>
<th>説明</th>
</tr>
</thead><tbody>
<tr>
<td><code>LOGICAL_APP_NAME</code></td>
<td>{{site.data.keyword.DRA_short}} ダッシュボードで表示される、アプリの名前。</td>
</tr>
<tr>
<td><code>LOGICAL_ENV_NAME</code></td>
<td>アプリが実行される環境の名前。このプロパティーを使用して、{{site.data.keyword.DRA_short}} ダッシュボード内のアプリを分類します。</td>
</tr>
<tr>
<td><code>BUILD_PREFIX</code></td>
<td>{{site.data.keyword.DRA_short}} ダッシュボードで表示される、ビルドに追加される接頭部。</td>
</tr>
</tbody></table>


## {{site.data.keyword.DRA_short}} のテスト・ジョブの更新
{: #toolchain_pipeline_upload}

最初に、テスト・ジョブからセットアップ情報を取得します。

1. テスト・ジョブを含むステージで、**「ステージ構成 (Stage Configuration)」**アイコン ![パイプラインのステージ構成アイコン](images/pipeline-stage-configuration-icon.png) をクリックします。**「ステージの構成 (Configure Stage)」**をクリックします。
2. ジョブを作成します。ジョブ・タイプとして**「テスト」**を選択します。
3. 「単純 (Simple)」テスター・タイプを使用するテスト・ジョブを選択し、**「テスト・コマンド (Test Command)」**フィールドと**「作業ディレクトリー (Working Directory)」**フィールドにある情報をエディターにコピーします。この情報は後で必要になります。
4. 同じ「単純 (Simple)」テスト・ジョブから、**「詳細テスター (Advanced Tester)」**を選択してテスター・タイプを変更します。
5. **「テスト・コマンド (Test Command)」**フィールドに、「単純 (Simple)」テスト・ジョブの**「テスト・コマンド (Test Command)」**フィールドからコピーしたコマンドを貼り付けます。
6. **「作業ディレクトリー (Working Directory)」**フィールドに、「単純 (Simple)」テスト・ジョブの**「作業ディレクトリー (Working Directory)」**フィールドからコピーしたパスを貼り付けます。
7. 特定のテスト・タイプのテスト結果をアップロードするための、その他のフィールドに入力します。同じジョブで別のテスト・タイプの結果をアップロードする場合は、*「追加 (Additional)」*と先頭に示されたフィールドにも入力します。

 * メトリックのタイプ (Type of Metric)
 * 形式 (Format)
 * 結果ファイルの場所 (Result File Location)
8. **「保存」**をクリックして、パイプラインに戻ります。

**「メトリックのタイプ (Type of Metric)」**フィールドと**「結果ファイルの場所 (Result File Location)」**フィールドの値は、以下に示す正しい形式と合致していなければなりません。

<table><thead>
<tr>
<th>メトリックのタイプ</th>
<th>サポートされる形式</th>
</tr>
</thead><tbody>
<tr>
<td>機能検証テスト (Functional Verification Test)</td>
<td>Mocha、JUnit</td>
</tr>
<tr>
<td>単体テスト (Unit Test)</td>
<td>Mocha、JUnit、Karma/Mocha</td>
</tr>
<tr>
<td>コード・カバレッジ (Code Coverage)</td>
<td>Istanbul、Blanket.js</td>
</tr>
</tbody></table>

*図 1* で示すテスト・ジョブでは、単体テストを実行し、結果を Mocha 形式でアップロードし、コード・カバレッジ結果を Istanbul 形式でアップロードするように構成されています。

![デプロイメント・リスク分析アップロード・ジョブ](images/DRA_upload_job.png)
*図 1. DevOps Analytics への結果のアップロード*

## パイプラインでの {{site.data.keyword.DRA_short}} ゲートの定義
{: #toolchain_pipeline_gates}

{{site.data.keyword.DRA_short}} ゲートは、定義されたポリシーにテスト結果が準拠しているかどうかを検査します。ポリシーに準拠していない場合、{{site.data.keyword.DRA_short}} ゲートはパスできません。ゲートは通常、パイプラインの各ステージの最後に配置されます。この場所は、ビルドの品質をポリシーに照らして検査して、安全に別の環境にプロモートできることを確認するのに最適です。しかし、ゲートは、特定の基準の検査を必要とする、パイプライン内の任意の場所に配置することが可能です。

1. ステージで**「ステージ構成 (Stage Configuration)」**アイコン ![パイプラインのステージ構成アイコン](images/pipeline-stage-configuration-icon.png) をクリックし、**「ステージの構成 (Configure Stage)」**をクリックします。
2. **「ジョブの追加 (Add Job)」**をクリックします。ジョブ・タイプとして**「テスト」**を選択します。
3. 新規ジョブの名前を入力します (例: *ゲート (単体テスト)*)。
4. テスター・タイプとして**「{{site.data.keyword.DRA_short}} ゲート ({{site.data.keyword.DRA_short}} Gate)」**を選択します。
5. 環境名を指定します。この値が、[環境プロパティー](#toolchain_pipeline_props)で定義したものと一致することを確認してください。
6. このゲートで検査するポリシー名を定義します。

 この名前は、定義したポリシー名のいずれかと完全に一致していなければなりません。ご使用のツールチェーンと同じ {{site.data.keyword.Bluemix_notm}} 組織で定義されたポリシーのみを指定できます。

7. オプション: ゲートを推奨モードで機能させるには、**「このジョブが失敗した場合、このステージの実行を停止する (Stop running this stage if this job fails)」**チェック・ボックスをクリアします。推奨モードでは、{{site.data.keyword.DRA_short}} は同じポリシー分析をゲートで実行し、レポートを生成しますが、失敗となった場合でもパイプラインは停止されません。
8. **「保存」**をクリックして、パイプラインに戻ります。
9. 上記のステップを繰り返して、すべての {{site.data.keyword.DRA_short}} ポリシーについてゲートをセットアップします。

![デプロイメント・リスク分析 Mocha ジョブ](images/DRA_gate_job.png)
*図 2. DevOps Analytics ゲート*

パイプラインを構成した後、{{site.data.keyword.DRA_short}} の使用を開始します。その手順については、[Running the Delivery Pipeline](./pipeline_decision_reports.html#toolchain_reports) を参照してください。
