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

# DevOps Insights の概説 (ベータ)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} は、開発者、チーム、デプロイメントの分析を、最も忙しい DevOps プロジェクトに適用します。
それを使用することにより、チームが DevOps と開発者のプラクティスにどの程度準拠しているかを調べたり、コードベースのリスクを管理したり、継続的デリバリー・プロジェクトで品質基準を自動的に適用したりすることができます。
{:shortdesc}

{{site.data.keyword.DRA_short}} は、いくつかの機能グループで構成されています。


   * Developer Insights には、プロジェクトの開発成熟度を検討するための包括的な方法が用意されています。
エラーが発生しやすいファイルを識別したり、開発者プラクティスに対するプロジェクトの適合性を表示したりできます。


   * Team Dynamics ではソーシャル・コーディング分析が使用され、これはチームのコラボレーション度を調べたり、改善点を検討したりするのに役立ちます。


   * Deployment Risk は、継続的デリバリーの安全ネットのようなものです。
デプロイメント・プロセス内の指定されたゲートで、単体テスト、機能テスト、アプリケーション・スキャン、コード・カバレッジ・ツールからの結果を分析し、リスクのある変更がリリースされないようにします。


   * Delivery Insights は、IBM UrbanCode Deploy インストールに関するデプロイメントの統計やメトリックなどの情報を表示します。
例えば、デプロイメントの期間、成功、失敗のグラフを、論理的に分類した環境別にすべてソートした状態で表示することができます。
[「DevOps Insights と IBM UrbanCode Deploy の統合」](/docs/services/DevOpsInsights/uc_insights_overview.html)を参照してください。


{{site.data.keyword.DRA_short}} は、Bluemix オープン・ツールチェーン・カタログ内の統合の 1 つです。
ツールチェーンについて詳しくは、[ツールチェーンを使用した作業](/docs/services/ContinuousDelivery/toolchains_working.html)を参照してください。

{{site.data.keyword.DRA_short}} を使用するには、それをツールチェーンに追加する必要があります。
多くのツールチェーン・テンプレートには、{{site.data.keyword.DRA_short}} が既に含まれています。
さらに、[それを {{site.data.keyword.Bluemix_notm}} org にサービスとして追加する](/docs/services/reqnsi.html)ことにより、{{site.data.keyword.DRA_short}} に関する情報を表示したり、それを含むツールチェーン・テンプレートのいくつかに {{site.data.keyword.Bluemix_notm}} ダッシュボードからアクセスしたりできるようにしてください。
  

## DevOps Insights をツールチェーンに追加する
{: #catalog}

{{site.data.keyword.DRA_short}} は {{site.data.keyword.contdelivery_short}} の一部です。
ツール統合カタログから選択することにより、任意のツールチェーンに {{site.data.keyword.DRA_short}} を追加することができます。


{{site.data.keyword.DRA_short}} は、多くのツールチェーン・テンプレートの一部ともなっています。
{{site.data.keyword.DRA_short}} を含むテンプレートからツールチェーンを作成する場合、{{site.data.keyword.DRA_short}} が**「詳細」**に設定されていることを確認してください。
その上で、ツールチェーンを作成し、[「Insights の使用」](/docs/services/DevOpsInsights/index.html#using)に進んでください。


{{site.data.keyword.DRA_short}} をツールチェーンに追加するには、次のようにします。


1. **「ツールの追加 (Add a Tool)」**をクリックします。

2. **「{{site.data.keyword.DRA_short}}」** をクリックします。

3. **「統合の作成 (Create Integration)」**をクリックします。

{{site.data.keyword.DRA_short}} は、ツールチェーンの概要ページから利用できるようになりました。
データを検索するために、リポジトリーと問題追跡システムが自動的にスキャンされます。 

## DevOps Insights の使用
{: #using}

ツールチェーンに GitHub、GitLab、JIRA が含まれている場合、{{site.data.keyword.DRA_short}} は、いくらかの初期データ収集と分析の後に、コードベースについての情報を自動的に提供します。
ツールチェーンにそれらの統合のどれも含まれていない場合は、それらのうちのいずれか 1 つを追加してから、以下の手順を実行します。


1. ツールチェーンの概要ページから、**「{{site.data.keyword.DRA_short}}」**をクリックします。


2. **「Team Dynamics」**または**「Developer Insights」**をクリックしてから、データのカテゴリーを選択します。 

3. そのデータ・カテゴリーの中のダッシュボードを表示することにより、プロジェクトのデータを調べます。
グラフについて、またその情報の処理方法については、**「情報」**または**「ガイダンス」**をクリックしてください。


Team Dynamics や Developer Insights について調べた後、[Deployment Risk の構成](/docs/services/DevOpsInsights/insights_risk.html)を行って、コード品質を維持強制することができます。
Deployment Risk は、{{site.data.keyword.contdelivery_short}} パイプラインと Jenkins の両方と互換性があります。
   
