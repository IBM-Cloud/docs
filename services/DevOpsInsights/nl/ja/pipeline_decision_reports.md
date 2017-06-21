---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# ダッシュボードとレポートの表示
{: #DRA_toolchain_reports}

{{site.data.keyword.DRA_short}} は、お客様のプロジェクトに関する実用的な情報を豊富に提供します。
{:shortdesc}

## {{site.data.keyword.DRA_short}} ダッシュボード    
{: #DI_toolchain_dashboards}

{{site.data.keyword.DRA_short}} は、Bluemix 組織全体のパフォーマンスに関する情報を表示するダッシュボードを備えています。ダッシュボードを表示するには、{{site.data.keyword.DRA_short}} を開いてから、**「ビルドの検証 (Build Verification)」**または**「デプロイの検証 (Deploy Verification)」**をクリックします。

ダッシュボードには、ご使用のパイプラインの {{site.data.keyword.DRA_short}} テスト・ジョブからの最新情報が自動的に取り込まれます。ダッシュボード内の各構成要素をクリックすると、それに関する詳細情報を参照できます。

### ビルドの重要パフォーマンス指標    
{: #DI_key_performance_indicators}

**「ビルドの検証 (Build Verification)」**ページに表示される以下の 3 つのグラフには、選択した開発ブランチの正常性に関する情報が示されます。

<table>
<thead>
<tr>
<th>グラフ</th>
<th>説明</th>
</tr>
</thead>

<tbody>
<tr>
<td>最新のビルド (Latest Builds)</td>
<td>最近のビルドの総数に対する、完了した最近のビルドの数。</td>
</tr>
<tr>
<td>テスト (Tests)</td>
<td>テスト総数に対する、合格したテストの数。</td>
</tr>
<tr>
<td>コード・カバレッジ (Code Coverage)</td>
<td>テストで呼び出される、コードのステートメントと関数のパーセンテージ。</td>
</tr>
</tbody></table>

## 決定レポートの表示    
{: #DI_decision_reports}

パイプラインが実行された後、{{site.data.keyword.DRA_short}} はそのパイプラインでのテスト結果の収集と分析を開始して、基準を確立します。その後の実行のたびに、そのデータが収集され、前の結果と比較されます。決定ゲートでは、このデータを利用して、デプロイメントを停止する時を決定します。 

パイプラインからのゲートの決定レポートを表示するには、以下の手順を実行します。

   1. 確認するゲートを含むステージで、**「ログおよび履歴の表示 (View logs and history)」**をクリックします。

   2. ステージのジョブ・ウィンドウで、ゲートの名前をクリックします。

   3. ログ・ビューで「ここから {{site.data.keyword.DRA_short}} レポートを確認します (Check {{site.data.keyword.DRA_short}} report here)」というメッセージを見つけ、用意されているリンクをクリックしてレポートを開きます。
