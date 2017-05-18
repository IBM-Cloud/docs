---

copyright:
  years: 2016, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 結果の表示

## Deployment Risk の評価

パイプラインが実行された後、{{site.data.keyword.DRA_short}} はそのパイプラインでのテスト結果の収集と分析を開始して、基準を確立します。その後の実行のたびに、そのデータが収集され、前の結果と比較されます。決定ゲートでは、このデータを利用して、デプロイメントを停止する時を決定します。 

Deployment Risk ダッシュボードから、デプロイメントとゲートの評価データを確認することができます。
ダッシュボードを開くには、{{site.data.keyword.DRA_short}} を開き、サイド・メニューから**「Deployment Risk」**をクリックします。


{{site.data.keyword.contdelivery_short}} パイプラインを使用している場合、パイプライン自体から個々のゲート実行レポートを表示できます。
パイプラインからゲートの決定レポートを表示するには、次のようにします。


1. 確認するゲートを含むステージで、**「ログおよび履歴の表示 (View logs and history)」**をクリックします。

2. そのゲートを含むジョブから、そのゲートの名前をクリックします。


3. ログ・ビューで「`ここから {{site.data.keyword.DRA_short}} レポートを確認します (Check {{site.data.keyword.DRA_short}} report here)`」というメッセージを見つけ、リンクをクリックしてレポートを開きます。


## Developer Insights と Team Dynamics のレポート

初期データ・マイニング期間が終わると、チームとコードについてのダッシュボードを表示できるようになります。
サービス・ナビゲーション・メニューで、**「Developer Insights」**または**「Team Dynamics」**をクリックした後、この情報を表示するデータ・カテゴリーを選択します。

